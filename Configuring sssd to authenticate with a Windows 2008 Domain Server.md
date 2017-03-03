<div class="wiki-toc">

1.  1.  [Synopsis](#Synopsis)
    2.  [Windows 2008 Server Setup](#Windows2008ServerSetup)
        1.  [Operating System
            Installation](#OperatingSystemInstallation)
        2.  [Domain Configuration](#DomainConfiguration)
        3.  [Enabling LDAP Searches](#EnablingLDAPSearches)
            1.  [Using SASL/GSSAPI Binds for LDAP
                Searches](#UsingSASLGSSAPIBindsforLDAPSearches)
                1.  [Creating Service Keytab with
                    Samba](#CreatingServiceKeytabwithSamba)
                2.  [/etc/samba/smb.conf](#etcsambasmb.conf)
                3.  [Creating Service Keytab on
                    AD](#CreatingServiceKeytabonAD)
            2.  [Using DN/Password Binds for LDAP
                Searches](#UsingDNPasswordBindsforLDAPSearches)
        4.  [Adding a Group](#AddingaGroup)
        5.  [Adding a User](#AddingaUser)
    3.  [Linux Client Setup](#LinuxClientSetup)
        1.  [/etc/krb5.conf](#etckrb5.conf)
        2.  [/etc/sssd/sssd.conf](#etcsssdsssd.conf)
        3.  [NSS/PAM Configuration](#NSSPAMConfiguration)
            1.  [Fedora/RHEL](#FedoraRHEL)
            2.  [Debian/Ubuntu?](#DebianUbuntu)
            3.  [Configure NSS/PAM manually](#ConfigureNSSPAMmanually)
                1.  [/etc/nsswitch.conf](#etcnsswitch.conf)
                2.  [/etc/pam.d/common-auth](#etcpam.dcommon-auth)
                3.  [/etc/pam.d/common-account](#etcpam.dcommon-account)
                4.  [/etc/pam.d/common-password](#etcpam.dcommon-password)
                5.  [/etc/pam.d/common-session](#etcpam.dcommon-session)
    4.  [Understanding Kerberos & Active
        Directory](#UnderstandingKerberosActiveDirectory)
        1.  [Optional Final Test](#OptionalFinalTest)
        2.  [Further reading](#Furtherreading)

</div>

Synopsis {#Synopsis}
--------

This describes how to configure SSSD to authenticate with a Windows 2008
Domain Server. This guide is a work in progress.

Windows 2008 Server Setup {#Windows2008ServerSetup}
-------------------------

The domain to be configured is *ad.example.com* using realm
*AD.EXAMPLE.COM*, the Windows server is *server.ad.example.com*, and the
client host where SSSD is running is *client.ad.example.com*. Reboot
Windows during installation and setup when prompted and complete the
needed steps as Administrator.

### Operating System Installation {#OperatingSystemInstallation}

-   Boot from the Windows 2008 Server DVD
-   Install Windows 2008 Server using the hostname
    *server.ad.example.com*
-   Make sure *server.ad.example.com* is in DNS

### Domain Configuration {#DomainConfiguration}

-   In *Server Manager* add the *Active Directory Domain Services* role
-   Create a new domain named *ad.example.com*
-   Required: in *Server Manager* add the *Identity Management for UNIX*
    Role Service for *Active Directory Domain Services*, use the domain
    name for the NIS domain name
    -   Currently SSSD won't work with AD in a meaningful fashion
        without this (this might change if
        [\#995](https://fedorahosted.org/sssd/ticket/995 "enhancement: RFE: Enhance Handling of primaryGroupID from Active Directory (closed: wontfix)"){.closed
        .ticket} and
        [\#996](https://fedorahosted.org/sssd/ticket/996 "enhancement: RFE: Allow Constructing uid from Active Directory objectSid (closed: fixed)"){.closed
        .ticket} are solved)

### Enabling LDAP Searches {#EnablingLDAPSearches}

In order to allow SSSD to do LDAP searches for user information in AD
SSSD must be configured to bind with SASL/GSSAPI or DN/password. GSSAPI
is recommended.

#### Using SASL/GSSAPI Binds for LDAP Searches {#UsingSASLGSSAPIBindsforLDAPSearches}

Create the service keytab for the host running SSSD on AD. Either do
this with Samba, or using Windows. Samba is recommended.

##### Creating Service Keytab with Samba {#CreatingServiceKeytabwithSamba}

On the Linux client with properly configured */etc/krb5.conf* (see
below) and suitable */etc/samba/smb.conf*:

##### /etc/samba/smb.conf

``` {.wiki}
[global]
   workgroup = EXAMPLE
   client signing = yes
   client use spnego = yes
   kerberos method = secrets and keytab
   log file = /var/log/samba/%m.log
   password server = AD.EXAMPLE.COM
   realm = EXAMPLE.COM
   security = ads
```

-   *net ads join -U Administrator*
    -   Or do *kinit Administrator* first and use *-k* instead of *-U
        Administrator*
-   Additional principals can be created later with *net ads keytab add*
    if needed.

You don't need a Domain Administrator account to do this, you just need
an account with sufficient rights to join a machine to the domain. This
is a notable advantage of this approach over generating the keytab
directly on the AD controller. If you're using NFS you may want to
specify a different createupn argument here. This does not cause any
problems for sssd. This would be done using:

*net ads join createupn="nfs/client.ad.example.com@``AD.EXAMPLE.COM" -U
Administrator*

##### Creating Service Keytab on AD {#CreatingServiceKeytabonAD}

Do not do this step if you've already created a keytab using Samba.

On the Windows server:

-   Open *Users & Computers* snap-in
-   Create a new *Computer* object named *client* (i.e., the name of the
    host running SSSD)
-   On the command prompt:
    -   *setspn -A host/client.ad.example.com@``AD.EXAMPLE.COM client*
    -   *setspn -L client*
    -   *ktpass /princ host/client.ad.example.com@``AD.EXAMPLE.COM /out
        client-host.keytab /crypto all /ptype KRB5\_NT\_PRINCIPAL
        -desonly /mapuser AD\\client\$ /pass \**
        -   This sets the machine account password and UPN for the
            principal
        -   If you create additional keytabs for the host add *-setpass
            -setupn* for the above command to prevent resetting the
            machine password (thus changing kvno) and to prevent
            overwriting the UPN
-   Transfer the keytab created in a secure manner to the client as
    */etc/krb5.keytab* and make sure its permissions are correct:
    -   *chown root:root /etc/krb5.keytab*
    -   *chmod 0600 /etc/krb5.keytab*
    -   *restorecon /etc/krb5.keytab*

See the *Linux Client Setup* section for verifying the keytab file and
the example sssd.conf below for the needed SSSD configuration.

#### Using DN/Password Binds for LDAP Searches {#UsingDNPasswordBindsforLDAPSearches}

Not generally recommended but see the example sssd.conf below.

### Adding a Group {#AddingaGroup}

-   Open *Administrative Tools* -&gt; *Active Directory Users and
    Computers*
-   Browse to *ad.example.com*, then to *Users*
-   Right click on *Users* and *Create a New Group* named *unixusers*
-   Double click on the *unixusers* group then switch to the *UNIX
    Attributes* tab
-   Select the NIS Domain created earlier
-   Set the *GID* as appropriate

### Adding a User {#AddingaUser}

-   Open *Administrative Tools* -&gt; *Active Directory Users and
    Computers*
-   Browse to *ad.example.com*, then to *Users*
-   Right click on *Users* and *Create a New User* named *aduser*
-   Make sure *User must change password at next logon* and *Account is
    disabled* are unchecked
-   Double click on the *aduser* group then switch to the *UNIX
    Attributes* tab
-   Select the NIS Domain created earlier
-   Set the *UID* as appropriate
-   Set the *Login Shell* to */bin/bash*
-   Set the *Home Directory* to */home/aduser*
-   Set *Primary Group Name/GID* to *unixusers*

Linux Client Setup {#LinuxClientSetup}
------------------

-   Install *sssd* package on the Linux client machine
-   Make configuration changes to the files below
-   Start the *sssd* service

### /etc/krb5.conf

``` {.wiki}
[logging]
 default = FILE:/var/log/krb5libs.log

[libdefaults]
 default_realm = AD.EXAMPLE.COM
 dns_lookup_realm = true
 dns_lookup_kdc = true
 ticket_lifetime = 24h
 renew_lifetime = 7d
 rdns = false
 forwardable = yes

# You may also want either of:
# allow_weak_crypto = true
# default_tkt_enctypes = arcfour-hmac

[realms]
# Define only if DNS lookups are not working
# AD.EXAMPLE.COM = {
#  kdc = server.ad.example.com
#  admin_server = server.ad.example.com
# }

[domain_realm]
# Define only if DNS lookups are not working
# .ad.example.com = AD.EXAMPLE.COM
# ad.example.com = AD.EXAMPLE.COM
```

Make sure *kinit aduser@``AD.EXAMPLE.COM* works properly. Add the
Windows server IP/hostname to */etc/hosts* only if needed.

If using SASL/GSSAPI to bind to AD also test that the keytab is working
properly:

*klist -ke*

*kinit -k CLIENT\$@``AD.EXAMPLE.COM*

If you generated your keytab with a different createupn argument, it's
possible this won't work and the following works instead. This is
absolutely fine as far as sssd is concerned, and you can instead
generate a ticket for the upn you have created:

*kinit -k -t /etc/krb5.keytab
'nfs/client.ad.example.com@``AD.EXAMPLE.COM'*

Now using this credential you've just created try fetching data from the
server with *ldapsearch* (in case of issues make sure
*/etc/openldap/ldap.conf* does not contain any unwanted settings):

*/usr/bin/ldapsearch -H ldap://server.ad.example.com/ -Y GSSAPI -N -b
"dc=ad,dc=example,dc=com"
"(&(objectClass=user)(sAMAccountName=aduser))"*

By using the credential from the keytab, you've verified that this
credential has sufficient rights to retrieve user information.

After both *kinit* and *ldapsearch* work properly proceed to actual SSSD
configuration.

### /etc/sssd/sssd.conf

Example *sssd.conf* configuration, additional options can be added as
needed.

``` {.wiki}
[sssd]
config_file_version = 2
domains = ad.example.com
services = nss, pam
debug_level = 0

[nss]

[pam]

[domain/ad.example.com]
# Unless you know you need referrals, turn them off
ldap_referrals = false
# Uncomment if you need offline logins
# cache_credentials = true
enumerate = false

id_provider = ldap
auth_provider = krb5
chpass_provider = krb5
access_provider = ldap

# Uncomment if service discovery is not working
#ldap_uri = ldap://server.ad.example.com/

# Comment out if not using SASL/GSSAPI to bind
ldap_sasl_mech = GSSAPI
# Uncomment and adjust if the default principal host/fqdn@REALM is not available
#ldap_sasl_authid = nfs/client.ad.example.com@AD.EXAMPLE.COM

# Define these only if anonymous binds are not allowed and no keytab is available
# Enabling use_start_tls is very important, otherwise the bind password is transmitted
# over the network in the clear
#ldap_id_use_start_tls = True
#ldap_default_bind_dn = CN=binduser,OU=user accounts,DC=ad,DC=example,DC=com
#ldap_default_authtok_type = password
#ldap_default_authtok = bindpass

ldap_schema = rfc2307bis

ldap_user_search_base = ou=user accounts,dc=ad,dc=example,dc=com
ldap_user_object_class = user

ldap_user_home_directory = unixHomeDirectory
ldap_user_principal = userPrincipalName

ldap_group_search_base = ou=groups,dc=ad,dc=example,dc=com
ldap_group_object_class = group

ldap_access_order = expire
ldap_account_expire_policy = ad
ldap_force_upper_case_realm = true

# Uncomment if dns discovery of your AD servers isn't working.
#krb5_server = server.ad.example.com
krb5_realm = AD.EXAMPLE.COM

# Probably required with sssd 1.8.x and newer
krb5_canonicalize = false

# Perhaps you need to redirect to certain attributes?
# ldap_user_object_class = user
# ldap_user_name = sAMAccountName
# ldap_user_uid_number = msSFU30UidNumber
# ldap_user_gid_number = msSFU30GidNumber
# ldap_user_gecos = displayName
# ldap_user_home_directory = msSFU30HomeDirectory
# ldap_user_shell = msSFU30LoginShell
# ldap_user_principal = userPrincipalName
# ldap_group_object_class = group
# ldap_group_name = cn
# ldap_group_gid_number = msSFU30GidNumber
```

### NSS/PAM Configuration {#NSSPAMConfiguration}

Depending on your distribution you have different options how to enable
SSSD.

#### Fedora/RHEL {#FedoraRHEL}

Use *authconfig* to enable SSSD, install *oddjob-mkhomedir* to make sure
home directory creation works with SELinux:

*authconfig --enablesssd --enablesssdauth --enablemkhomedir --update*

#### [Debian/Ubuntu?](https://docs.pagure.org/sssd-test2/Debian/Ubuntu.html){.missing .wiki} {#DebianUbuntu}

Install *libnss-sss* and *libpam-sss* to have SSSD added as NSS/PAM
provider in */etc/nsswitch.conf* and */etc/pam.d/common-\**
configuration files. Add *pam\_mkhomedir.so* to PAM session
configuration manually. Restart SSSD after these changes.

#### Configure NSS/PAM manually {#ConfigureNSSPAMmanually}

Manual configuration can be done with the following changes. The PAM
example file paths are from
[Debian/Ubuntu?](https://docs.pagure.org/sssd-test2/Debian/Ubuntu.html){.missing
.wiki}, in Fedora/RHEL corresponding manual configuration should be done
in */etc/pam.d/system-auth* and */etc/pam.d/password-auth*.

##### /etc/nsswitch.conf

More maps will be available later (see at least tickets
[\#359](https://fedorahosted.org/sssd/ticket/359 "enhancement: SSSD NSS should support host map (new)"){.new
.ticket},
[\#360](https://fedorahosted.org/sssd/ticket/360 "enhancement: SSSD NSS should support automount map (closed: duplicate)"){.closed
.ticket},
[\#900](https://fedorahosted.org/sssd/ticket/900 "enhancement: Implement automount map intgration with SSSD (closed: fixed)"){.closed
.ticket},
[\#901](https://fedorahosted.org/sssd/ticket/901 "enhancement: [Feature] Implement support for the LDAP served maps (new)"){.new
.ticket},
[\#929](https://fedorahosted.org/sssd/ticket/929 "enhancement: Add support for the services map (closed: fixed)"){.closed
.ticket}).

``` {.wiki}
#
# /etc/nsswitch.conf
#

passwd:         files sss
shadow:         files sss
group:          files sss

hosts:          files dns

bootparams:     files

ethers:         files
netmasks:       files
networks:       files
protocols:      files
rpc:            files
services:       files

netgroup:       files sss

publickey:      files

automount:      files
aliases:        files
```

##### /etc/pam.d/common-auth

Right after the *pam\_unix.so* line, add

``` {.wiki}
auth         sufficient    pam_sss.so use_first_pass
```

##### /etc/pam.d/common-account

Right after the *pam\_unix.so* line, add

``` {.wiki}
account      [default=bad success=ok user_unknown=ignore] pam_sss.so
```

##### /etc/pam.d/common-password

Right after the *pam\_unix.so* line, add

``` {.wiki}
password     sufficient    pam_sss.so use_authtok
```

##### /etc/pam.d/common-session

Just before the *pam\_unix.so* line, add

``` {.wiki}
session      optional      pam_mkhomedir.so
```

Right after the *pam\_unix.so* line, add

``` {.wiki}
session      optional      pam_sss.so
```

Understanding Kerberos & Active Directory {#UnderstandingKerberosActiveDirectory}
-----------------------------------------

It is important to understand that (unlike Linux MIT based KDC) Active
Directory based KDC divides Kerberos principals into two groups:

-   *User Principals* - usually equals to the sAMAccountname attribute
    of the object in AD. In short, User Principal is entitled to obtain
    TGT (ticket granting ticket). User Principals could be hence used to
    generate a TGT via `kinit -k <principalname>`
-   *Service Principals* - represents which Kerberized service can be
    used on the computer in question. Service principals **CANNOT** be
    used to obtain a TGT -&gt; cannot be used to grant an access to
    Active Directory controller for example.

Each user object in Active Directory (understand that a computer object
in AD is de-facto user object as well) can have:

-   maximum of 2 User Principal Names (UPN). One is pre-defined by its
    *sAMAccountName* LDAP attribute (mentioned above, for computer
    objects it has a form of "&lt;hostname&gt;\$") and second by its
    *[UserPrincipalName?](https://docs.pagure.org/sssd-test2/UserPrincipalName.html){.missing
    .wiki}* string attribute
-   many Service Principal Names (typically one for each Kerberized
    service we want to enable on the computer) defined by the
    *[ServicePrincipalName?](https://docs.pagure.org/sssd-test2/ServicePrincipalName.html){.missing
    .wiki}* (SPN) list attribute. The attributes can be seen/set using
    the ADSIedit snap-in for example.

### Optional Final Test {#OptionalFinalTest}

You may have made iterative changes to your setup while learning about
SSSD. To make sure that your setup actually works, and you're not
relying on cached credentials, or cached LDAP information, you may want
to clear out the local cache. Obviously this will erase local
credentials, and all cached user information, so you should only do this
for testing, and while on the network with network access to the AD
servers.

*service sssd stop; rm -f /var/lib/sss/db/\*; service sssd start*

If all looks well on your system after this, you know that sssd is able
to use the kerberos and ldap services you've configured.

### Further reading {#Furtherreading}

Please see the following article on Technet site
([[​]{.icon}http://technet.microsoft.com/en-us/library/cc772815%28WS.10%29.aspx](http://technet.microsoft.com/en-us/library/cc772815%28WS.10%29.aspx){.ext-link})
for more in-depth Kerberos understanding