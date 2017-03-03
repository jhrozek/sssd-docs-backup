<div class="wiki-toc">

1.  1.  [Synopsis](#Synopsis)
    2.  [Daemon options](#Daemonoptions)
    3.  [PAM responder options](#PAMresponderoptions)
    4.  [PAC responder options](#PACresponderoptions)
    5.  [IFP responder options](#IFPresponderoptions)
    6.  [General domain options](#Generaldomainoptions)
    7.  [LDAP provider options](#LDAPprovideroptions)
    8.  [Kerberos provider options](#Kerberosprovideroptions)
    9.  [Simple access provider options](#Simpleaccessprovideroptions)
    10. [IPA and AD provider options](#IPAandADprovideroptions)

</div>

Synopsis {#Synopsis}
--------

This page describes SSSD options that have a security implication. It
was last updated with SSSD 1.13.1 in mind. The option description are
often pasted from the man pages along with a short sentence explaining
why the option has a security implication. Please see the sssd man pages
for a more detailed description and the default values.

As a general note, the SSSD should already include secure-by-default
options, so normally no hardening is needed after the SSSD is
configured. A notable exception is the `user` option. Additionally, SSSD
tends to honor settings its libraries use and only allows means to
override the library settings with SSSD specific This is especially true
for libkrb5 and openldap-libs.

Daemon options {#Daemonoptions}
--------------

Options in this page section control the daemon behaviour and should be
placed in the `[sssd]` section.

services
:   Comma separated list of services that are started when sssd itself
    starts. It is advisable to disable services that are not required.
    The same applies for domains.

user
:   The user to drop the privileges to where appropriate to avoid
    running as the root user. At the time of writing, the default is
    still root, although SSSD in RHEL and Fedora is also configured with
    the `sssd` user in mind. Adding `user = sssd` to the `[sssd]`
    section will cause the SSSD worker processes to run as the `sssd`
    user.

certificate\_verification
:   If this option is set to no\_ocsp, then Online Certificate Status
    Protocol checks are completely disabled.

PAM responder options {#PAMresponderoptions}
---------------------

Options in this section configure the PAM responder and belong to the
`[pam]` section.

offline\_credentials\_expiration
:   If the authentication provider is offline, how long should we allow
    cached logins (in days since the last successful online login).

<!-- -->

offline\_failed\_login\_attempts
:   If the authentication provider is offline, how many failed login
    attempts are allowed. Can prevent brute-force attacks when offline.

<!-- -->

offline\_failed\_login\_delay
:   The time in minutes which has to pass after
    offline\_failed\_login\_attempts has been reached before a new login
    attempt is possible. Can prevent brute-force attacks.

<!-- -->

pam\_verbosity
:   Controls what kind of messages are shown to the user during
    authentication. The default is 0 to make sure no info is leaked
    through a side channel.

<!-- -->

pam\_trusted\_users
:   Specifies the comma-separated list of UID values or user names that
    are allowed to access the PAM responder as trusted users. Can be
    used to restrict access to the PAM responder. Users not included in
    this list can only access `pam_public_domains`.

<!-- -->

pam\_public\_domains
:   Specifies the comma-separated list of domain names that are
    accessible even to untrusted users.

PAC responder options {#PACresponderoptions}
---------------------

Options in this section configure the PAC responder and belong to the
`[pac]` section.

allowed\_uids
:   Specifies the comma-separated list of UID values or user names that
    are allowed to access the PAC responder. By default, only root can,
    so additional values for this option should be justified.

IFP responder options {#IFPresponderoptions}
---------------------

Options in this section configure the InfoPipe responder and belong to
the `[ifp]` section.

allowed\_uids
:   Specifies the comma-separated list of UID values or user names that
    are allowed to access the IFP responder. By default, only root can,
    so additional values for this option should be justified.

General domain options {#Generaldomainoptions}
----------------------

Options in this page section are not related to any particular back end
type or responder and apply to the `[domain]` section.

access\_provider
:   contrary to other providers, the default for `access_provider` is
    permit all. Setting `access_provider` to another access control
    provider may increase security, on the other hand, if there is no
    explicit `access_provider` value, then all authenticated users are
    allowed access.

<!-- -->

cache\_credentials
:   Determines if user credentials are also cached in the local LDB
    cache. User credentials are stored in a SHA512 hash, not in
    plaintext. Setting to true would store hash of password after
    authentication.

<!-- -->

cache\_credentials\_minimal\_first\_factor\_length
:   If 2-Factor-Authentication (2FA) is used and credentials should be
    saved this value determines the minimal length the first
    authentication factor (long term password) must have to be saved as
    hash in the cache. This should avoid that the short PINs of a PIN
    based 2FA scheme are saved in the cache which would make them easy
    targets for brute-force attacks.

<!-- -->

account\_cache\_expiration
:   Number of days entries are left in cache after last successful login
    before being removed during a cleanup of the cache.
    Security-paranoid environments might want to set this option
    especially if `cache_credentials` is set as well.

LDAP provider options {#LDAPprovideroptions}
---------------------

Options in this section only apply for configurations that set any of
the providers to `ldap`.

ldap\_tls\_reqcert
:   Specifies what checks to perform on server certificates in a TLS
    session, if any. Setting anything but `hard` or `demand` lowers
    security.

<!-- -->

ldap\_tls\_cipher\_suite
:   Specifies acceptable cipher suites, uses OpenLDAP defaults normally.
    In theory, the admin could set insecure ciphers here.

<!-- -->

ldap\_id\_use\_start\_tls
:   Specifies that the id\_provider connection must also use tls to
    protect the channel. Normally identity lookups happen in the clear,
    unlike authentication that must always be encrypted. Similar effect
    can be achieved with `ldap_sasl_mech=gssapi`

Kerberos provider options {#Kerberosprovideroptions}
-------------------------

Options in this section only apply for configurations that set any of
the providers to `krb5`.

krb5\_validate
:   Verify with the help of krb5\_keytab that the TGT obtained has not
    been spoofed. Setting this option to True helps mitigate MITM
    attacks.

<!-- -->

krb5\_store\_password\_if\_offline
:   Store the password of the user if the provider is offline in the
    kernel keyring and use it to request a TGT when the provider comes
    online again.

<!-- -->

krb5\_use\_fast
:   Enables flexible authentication secure tunneling (FAST) for Kerberos
    pre-authentication.

<!-- -->

krb5\_ccname\_template
:   Using certain credential cache types such as keyrings can increase
    security as the credential cache would only be accessible to the
    owner and root.

Simple access provider options {#Simpleaccessprovideroptions}
------------------------------

The simple access provider provides ACLs that contain list of user or
group names that are permitted or allowed access. It's more secure to
whitelist users that should be allowed access (`simple_allow_*`) rather
then blacklist those that should be denied access (`simple_deny_*`)

IPA and AD provider options {#IPAandADprovideroptions}
---------------------------

None of the options that are specific to either IPA or AD provider have
a security consequence. But since both IPA and AD providers are more or
less wrappers around `id_provider=ldap` and `auth_provider=krb5`, any
LDAP or Kerberos options can be used in IPA or AD domains as well. That
said, both providers already use GSSAPI for identity lookups.
Additionally, both enable `krb5_validate` by default and the IPA
provider also sets the `krb5_use_fast` option to `try`.

Please note that the IPA and AD clients are typically configured using
tools such as `realmd` or `ipa-client-install` that may set additional
options differently than SSSD defaults. A typical example is
`cache_credentials` being enabled by default by `ipa-client-install`. In
a similar manner, these installers tend to enable a sensible set of
services (responders) that might not be required for security-sensitive
setups.
