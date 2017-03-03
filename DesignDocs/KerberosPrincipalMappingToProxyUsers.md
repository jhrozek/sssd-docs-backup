Mapping ID provider names to Kerberos principals {#MappingIDprovidernamestoKerberosprincipals}
================================================

Related ticket(s):

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2509](https://fedorahosted.org/sssd/ticket/2509){.ext-link}

### Problem statement {#Problemstatement}

Some users are migrating to SSSD from a legacy configuration that
consisted of a traditional UNIX user stored in `/etc/passwd` and
managing their Kerberos tickets either with the use of some GUI tool or
just command-line `kinit`. While these users can use SSSD by configuring
the `id_provider` proxy, very often the name of their UNIX user is
different from the name of their company-wide Kerberos credentials.

This feature helps the above use-case by mapping their UNIX user name to
the Kerberos principal name.

### Use cases {#Usecases}

Joe User has a company laptop where his UNIX user has been traditionally
named `joe`. At the same time, his company Kerberos principal is called
`juser@EXAMPLE.COM`. Joe would like to start using SSSD to leverage
features like offline kinit without having to rename his UNIX user and
chown all his local files to the corporate user ID.

While most of this design page describes setup using the proxy provider,
which would be the typical case, this option can be used along with any
`id_provider`.

### Overview of the solution {#Overviewofthesolution}

The Kerberos provider will acquire a new option that describes how are
the user names from the ID provider mapped onto the user part of the
Kerberos principal. The user would then add the appropriate mapping to
the `domain` section of `sssd.conf`.

### Implementation details {#Implementationdetails}

A new option `krb5_map_user` would be added to the Kerberos auth code.
This option would have form similar to how we map the LDAP extra
attributes, that is `local_name:krb5_name`. When mapping exists for the
user who is authenticating, the krb5\_auth module would use that user
name for calls like `find_or_guess_upn` instead of `pd->name`. We should
consider whether to keep using `pd->name` or introduce another attribute
to the `krb5_child_req` structure.

### Configuration changes {#Configurationchanges}

A new configuration option tentatively called `krb5_map_user` would be
added. This option is unset by default, which means whatever user name
the ID provider stores will be used.

### How To Test {#HowToTest}

1.  Prepare a Kerberos KDC, add a user principal (`juser@EXAMPLE.COM`)
2.  Add a local user using `useradd` with name that differs from
    Kerberos principal in the name portion. (`joe`)
3.  Configure SSSD with `id_provider=proxy` with `proxy_lib_name=files`
    and `auth_provider=krb5` pointing to our test KDC
4.  Attempt to authenticate using a PAM service. The authentication
    should fail and the logs would show authentication as
    `joe@EXAMPLE.COM`
5.  Set `krb5_map_user` to `joe:juser` and restart SSSD.
6.  Authenticate again. This time, authentication should succeed and the
    user's klist output should list `juser@EXAMPLE.COM`. The `id(1)`
    output should still list `joe`, though.
7.  Test that Kerberos ticket renewals still work
8.  Test that delayed kinit still works.

### Authors {#Authors}

-   Jakub Hrozek
    &lt;[[​]{.icon}jhrozek@redhat.com](mailto:jhrozek@redhat.com){.mail-link}&gt;
