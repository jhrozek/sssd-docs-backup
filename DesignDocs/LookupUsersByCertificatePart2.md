Lookup Users by Certificate - Active Directory {#LookupUsersbyCertificate-ActiveDirectory}
==============================================

Related ticket(s):

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2897](https://fedorahosted.org/sssd/ticket/2897){.ext-link}

### Problem statement {#Problemstatement}

So far the main focus of the SSSD certificate and Smartcard
authentication support in SSSD was on FreeIPA. Although it is possible
to use it with the AD provider as well (see
[[​]{.icon}SmartcardAuthenticationTestingWithAD](https://docs.pagure.org/sssd-test2/DesignDocs/SmartcardAuthenticationTestingWithAD.html){.ext-link}
for details) it requires some manual configuration.

On this page we describe the enhanced support for certificates in AD and
in override data for the direct (AD provider) and indirect (IPA with
trust to AD) integration.

### Use cases {#Usecases}

#### Apache {#Apache}

Apache is using *mod\_lookup\_identity* to look up a user who used
certificate based authentication with the help of the certificate.
Currently, without additional configuration, only IPA users were
supported. Now users from AD which have the certificate stored in the
user entry as supported as well for both direct and indirect
integration. Additionally certificates can be stored in local overrides
for the direct integration and in IPA server-side overrides for the
indirect integration.

#### Smartcard authentication {#Smartcardauthentication}

If the certificate of the user is stored in the user's entry in AD or in
a IPA or local override the user can authenticate with a Smartcard which
holds the certificate and the matching private key.

Since both use-case rely in the same common code only the user lookup is
discussed later on because it is easier to test and validate.

### Overview of the solution {#Overviewofthesolution}

#### General {#General}

The common override lookup code must be enhanced to allow lookups by
certificates as well.

#### AD provider (direct integration) {#ADproviderdirectintegration}

To support the direct integration

-   the attribute containing the certificate must be read by default
-   sss\_override must be enhanced to store certificates in local
    overrides as well

#### IPA provider (indirect integration) {#IPAproviderindirectintegration}

To support the indirect integration

-   the IPA override lookup code must be enhanced to read certificate
    overrides from the server and store them in the cache
-   the IPA client code to look up AD users via the extdom plugin must
    be enhanced to allow lookups by certificates

#### Support for the IPA extdom plugin {#SupportfortheIPAextdomplugin}

Currently it is only possible to look up users by certificate with the
[InfoPipe?](https://docs.pagure.org/sssd-test2/InfoPipe.html){.missing
.wiki} which uses DBus. To avoid to add a DBus requirement to the extdom
plugin and the directory server a call similar to
sss\_nss\_getnamebysid() should be added to allow easy lookups by
certificate via the NSS responder.

### Implementation details {#Implementationdetails}

Most of the changes are related to adding the new attribute to the
various lookup requests.

### Configuration changes {#Configurationchanges}

For the AD provider the currently unset option *ldap\_user\_certificate*
will be set to *userCertificate;binary*. This means that is a
certificate is available in the user entry it will be downloaded and
written to the cache by default. To avoid this *ldap\_user\_certificate*
must be set to a non-existing attribute name like e.g.

``` {.wiki}
ldap_user_certificate = nonExistingAttributeName
```

The *sss\_override user-add* utility has a new option *--certificate*
(*-x*) which expects the base64-endode certificate as an argument.

### How To Test {#HowToTest}

Testing can be done with *dbus-send* as described in
[LookupUsersByCertificate?](https://docs.pagure.org/sssd-test2/LookupUsersByCertificate.html){.missing
.wiki}. Instead of storing the certificate in the user object of an IPA
user it should be now stored in the user object of an AD user as e.g.
described in
[[​]{.icon}WritingthecertificatetoAD](https://docs.pagure.org/sssd-test2/DesignDocs/SmartcardAuthenticationTestingWithAD.html#WritingthecertificatetoAD){.ext-link}.
Additionally certificates overrides can be written with the
*sss\_override* utility for the direct integration or the *ipa
idoverrideuser\_add\_cert* command for the indirect integration.

If multiple certificate are added it should be noted that a user my have
multiple different certificates but a single certificate should be only
assigned to a single user. If a certificate is assigned to multiple
users no matter if in the user object or in the override the lookup will
fail sooner or later.

For the indirect integration the different lookups should be tested
independently on the IPA master and an IPA client because different code
paths are used since SSSD is running in the ipa-server-mode on the
master.

### How To Debug {#HowToDebug}

Explain how to debug this feature if something goes wrong. This section
might include examples of additional commands the user might run (such
as keytab or certificate sanity checks) or explain what message to look
for.

### Authors {#Authors}

-   Sumit Bose
    &lt;[[​]{.icon}sbose@redhat.com](mailto:sbose@redhat.com){.mail-link}&gt;
