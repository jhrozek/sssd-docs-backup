Allow Kerberos Principals in getpwnam() calls {#AllowKerberosPrincipalsingetpwnamcalls}
=============================================

Related ticket(s):

-   [[​]{.icon}RFE Implement localauth plugin for MIT krb5
    1.12](https://fedorahosted.org/sssd/ticket/1835){.ext-link}
-   [[​]{.icon}RFE Allow email-address in
    ldap\_user\_principal](https://fedorahosted.org/sssd/ticket/1749){.ext-link}
-   [[​]{.icon}RFE: Add a configuration option to specify where a
    snippet with sssd\_krb5\_localauth\_plugin.so is
    generated](https://fedorahosted.org/sssd/ticket/2473){.ext-link}

Problem Statement {#ProblemStatement}
-----------------

When using Kerberos/GSSAPI authentication for a service running on a
Linux host strictly speaking not a POSIX user of the Linux system is
authenticated but a Kerberos principal. I.e. authentication is
successful for every Kerberos principal with a valid ticket for the
service running on the Linux host. This is done intentional to keep
Kerberos independent of the operating system of the host. But it creates
the problem of mapping Kerberos principals to POSIX users.

Basic mappings are integrated in the MIT Kerberos library. By default
the realm part of the Kerberos principal is stripped off and what
remains is considered as a POSIX user name. The administrator can
enhance this by adding some minimal regular-expression operations in
/etc/krb5.conf. Addionally the user can create a .k5login file in his
home directory and add all Kerberos principals which should be allowed
to log in with his identity. All those methods do not scale in
environments with multiple realm and cross-realm trust.

To allow more advance mapping schemes a plugin interface was introduced
in MIT Kerberos version 1.12.

If the Kerberos principal is available SSSD will store it in its cache
in the related user object. The Kerberos principal can be retrieved by
looking it up in the central IdM system (LDAP/IPA/AD). If the Kerberos
principal is not available but Kerberos authentication is configured
SSSD will guess it by adding the configured realm or domain name to the
POSIX user name. If authentication is successful with this principal it
is stored in the cache as well.

A plugin which looks up the Kerberos principal in SSSD and gets the
POSIX user entry back would provide a reliable mapping and scale across
multiple realms and trusts because SSSD supports it.

Use case {#Usecase}
--------

In Windows environments, the user typically logs in using his UPN.
Implementing this feature would reach parity with how Windows users are
used to log in.

Implementing the localauth plugin will not only help the feature of
looking up UPNs but will make it easier for administrator to configure
client machines in a trust scenario as mapping will be done inside sssd
instead of the `auth_to_local` rule in `krb5.conf` or a `.k5login` file.

Overview of the Solution {#OverviewoftheSolution}
========================

Implementation details {#Implementationdetails}
----------------------

Currently the NSS responder expects that the argument of the getpwnam()
call is a user name, either fully qualified or the short version without
a domain name. The name is evaluated with the help of regular expression
and split into a user and a domain component. By default the '@'
character is one of the characters to separate the user and the domain
component in a fully qualified user name. This collides with the usage
of the '@' character in Kerberos principals, because here it is used to
separate the user and the realm component.

One way to solve this is to introduce a special prefix tag, e.g.
':princ:' to indicate that the remainder of the string should be
considered as a Kerberos principal and not be split as fully qualified
user names. While this would work for the localauth plugin use-case
there are other potential use-cases where this would not be possible.
E.g if SSSD should allow AD user to use their UPN (see
[[​]{.icon}http://technet.microsoft.com/en-us/library/cc739093(v=WS.10).aspx](http://technet.microsoft.com/en-us/library/cc739093(v=WS.10).aspx){.ext-link}
for details). This UPN is build by joining the user logon name and a UPN
suffix with an '@' character. I think it cannot be expected from the AD
users to add a prefix to this name and pam\_sss cannot do it either
because it does not know it is a fully qualified name or a UPN.

Especially with the second use-case, we should process the argument of
getpwnam() like a fully qualified user name first. If no matching user
was found during this pass SSSD can take the orginal input, check if it
contains an '@' character and search the configured backends for a
matching Kerberos principal or UPN. It has to be noted that in theory
there might be a user with the fully qualified name `abc@domain.name`
and the Kerberos principal `def@domain.com` and a user with the fully
qualified name `def@domain.name` and the Kerberos principal
`abc@domain.name`. In this case getpwnam("`abc@domain.name`") will
always return the entry for the user with the fully qualified name
`abc@domain.name` even if the input was meant as Kerberos principal.
This is even possible with Active Directory, i.e. the pre-Windows 2000
name and the user logon name of different users can be the same. I would
say that those cases are rare and can be considered as broken
configuration.

If the NSS responder decides that the given argument should be
considered as a Kerberos principal and was not able to find a matching
principal in the cache it can iterate over the configured backends and
send a GETACCOUNTINFO request for a user with a new filter type, e.g.
BE\_FILTER\_PRINCIPAL. The LDAP based ID backend which wants to support
this new filter type can process it like a any user request but have to
use an appropriate search filter.

The localauth plugin will be implemented according to [[​]{.icon}the
Kerberos
documentation](http://k5wiki.kerberos.org/wiki/Projects/Plugin_support_improvements){.ext-link}.
The plugin can be enabled manually by the admin, but it's more
user-friendly to enable the plugin automatically. To this end, SSSD will
gain a new option, tentatively called `krb5_localauth_snippet_path`.
When this option is enabled, a configuration snippet similar to the
following is generated into a `/var/lib/sss/pubconf/krb5.include.d`
directory that is already sourced by krb5.conf:

``` {.wiki}
[plugins]
 localauth = {
  module = sssd:/usr/lib/sssd/modules/sssd_krb5_localauth_plugin.so
  enable_only = sssd
 }   
```

Additional notes {#Additionalnotes}
----------------

The SSSD cache knows two attributes for principals "userPrincipalName"
and "canonicalUserPrincipalName". The first is used to save the data
read from the LDAP server. The second is used if the TGT contains a
different principal than the one used to request the TGT, i.e. if the
original principal was an alias. While searching principals in the cache
both should be respected. Currently "userPrincipalName" is already
declared CASE\_INSENSITIVE for searched in the cache.
"canonicalUserPrincipalName" should be declared the same way to make
searches consistent.

Configuration Changes {#ConfigurationChanges}
---------------------

A new option, tentatively called `krb5_localauth_snippet_path` will be
added to sssd's Kerberos provider. When this option is set (mostly via
SSSD default values, not administrator's change), then SSSD will
generate a file that will be automatically included in krb5.conf and the
localauth plugin will be enabled.

How to test {#Howtotest}
-----------

To make sure that a `getent passwd user@domain.name` search for the
Kerberos principal `user@domain.name` and not for a fully qualified name
the domain name in sssd.conf should differ from the realm name in the
principal. Probably the easiest configuration is to use the ldap ID
provider and make sure the targeted LDAP server has a Kerberos principal
attribute set for the users and the ldap\_user\_principal option points
to the corresponding attribute name.

``` {.wiki}
...
[domain/default]
id_provider = ldap
ldap_user_principal = krbPrincipalName
...
```

Now the fully qualified names end with '@default' while the Kerberos
principal are defined by the LDAP entries. E.g. if there is a user
'testabc' with the principal `testabc@MY.REALM` the command
`getent passwd testabc@default` will return the POSIX user entry
searched with the fully qualified name. `getent passwd testabc@MY.REALM`
will return the same entry but now search with the Kerberos principal.

Additionaly, logging in as a Windows user using GSSAPI should succeed
without requiring password with stock krb5.conf on an IPA client when
IPA-AD trust is established, as the following sequence illustrates:

``` {.wiki}
    kinit aduser@AD.DOMAIN.COM
    ssh `hostname` -l aduser@AD.DOMAIN.COM
```

Previously, this required either a `.k5login` file or an elaborate
`auth_to_local` rule.

### Author(s) {#Authors}

Sumit Bose
&lt;[[​]{.icon}sbose@redhat.com](mailto:sbose@redhat.com){.mail-link}&gt;
