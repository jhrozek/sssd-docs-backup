Do not always override home directory with subdomain\_homedir value in server mode {#Donotalwaysoverridehomedirectorywithsubdomain_homedirvalueinservermode}
==================================================================================

Related ticket(s):

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2583](https://fedorahosted.org/sssd/ticket/2583){.ext-link}

### Problem statement {#Problemstatement}

Prior to sssd 1.12, we didn't have the ability to read home directory
values from AD in AD-IPA trust setups at all. Instead, we always used
the `subdomain_homedir` value. We can read custom LDAP values now, but
in order to stay backwards-compatible, we kept using the
`subdomain_homedir` value.

### Use cases {#Usecases}

Users from AD with POSIX attributes want to use individually set value
for home directory.

### Overview of the solution {#Overviewofthesolution}

`subdomain_homedir` for SSSD in server mode should support '%o' template
expansion (The original home directory retrieved from the identity
provider). In case when `subdomain_homedir` would be expanded to an
empty string ('subdomain\_homedir=%o' and AD user without POSIX
attributes) SSSD should not error out but `fallback_homedir` should be
utilized instead.

### Implementation details {#Implementationdetails}

-   Extend set of attributes returned by `get_object_from_cache()` by
    SYSDB\_HOMEDIR attribute.
-   Update `apply_subdomain_homedir()`
    -   to parse AD home dirrctory from ldb\_msg
    -   do not call `store_homedir_of_user()` if value of expanded home
        directory is an empty string.
-   Extend interface of `get_subdomain_homedir_of_user()` to accept AD
    home directory as parameter.

### Configuration changes {#Configurationchanges}

No configuration changes are proposed.

### How To Test {#HowToTest}

1.  On SSSD in server mode
    -   For AD user with posix attributes set home directory attribute
        -   in sssd.conf set `subdomain_homedir` option to '%o'
        -   invalidate cache (sss\_cache) and restart SSSD
        -   call `getent passwd user` and check that home directory
            reflects value from AD
    -   For AD user `without` posix attributes
        -   in sssd.conf set `subdomain_homedir` option to %o and
            `fallback_homedir` to /home/%u
        -   invalidate cache (sss\_cache) and restart SSSD
        -   call `getent passwd user` and check that home directory
            reflects `fallback_homedir`
2.  On SSSD acting as IPA client
    -   Check that results are the same as on SSSD in server mode and
        that local `fallback_homedir` is ignored

### Authors {#Authors}

[[​]{.icon}preichl@redhat.com](mailto:preichl@redhat.com){.mail-link}