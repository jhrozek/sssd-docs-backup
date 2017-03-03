Global Catalog Lookups in SSSD {#GlobalCatalogLookupsinSSSD}
------------------------------

Related tickets:

-   [[​]{.icon}RFE Use the Global Catalog in SSSD for the AD
    provider](https://fedorahosted.org/sssd/ticket/1557){.ext-link}
-   [[​]{.icon}RFE sssd should support DNS
    sites](https://fedorahosted.org/sssd/ticket/1032){.ext-link}

### Problem Statement {#ProblemStatement}

Currently SSSD uses the standard LDAP interface of Active Directory to
lookup users and groups when joined to an Active Directory domain. But
the LDAP interface only offers information for users and groups of the
local domain and not from the whole forest. This information is
available in the Global Catalog of an Active Directory domain.

To make lookups of users and groups from the whole forest easier SSSD
should use the Global Catalog instead of the standard LDAP interface for
the lookups.

Additionally SSSD should provide an interface to allow other
applications to do Global Catalog lookups. Initially it is sufficient to
offer SID-to-Name and Name-to-SID lookups if SSSD is running on an IPA
server.

### Overview view of the solution {#Overviewviewofthesolution}

#### General components {#Generalcomponents}

##### Service discovery {#Servicediscovery}

1.  DNS lookup for any AD DC
2.  CLDAP query to find the site of the client
3.  DNS lookup for a Global Catalog server from the local site, fall
    back to any Global catalog server

##### Authentication against the Global Catalog {#AuthenticationagainsttheGlobalCatalog}

GSSAPI with keytabs will be used for authentication.

If the SSSD client is joined to an AD the keytab is created during the
join process.

If SSSD is running on an IPA server with trust configured, the keytab
will be generated by samba. It has to be created and updated when trust
is established or the trust password is changed. Additionally there
should be a method to generate the keytab if it does not exist even if
there is no change in the trust state.

#### New NSS-Responder calls for SID-to-Name and Name-to-SID lookups {#NewNSS-RespondercallsforSID-to-NameandName-to-SIDlookups}

Two new calls should be added to the NSS-Responder to give other
applications (the first user would be the FreeIPA directory server) a
simple interface for SID-to-Name and Name-to-SID lookups. It has to be
sorted out if and how those two new call will interact with lookup by
SID feature described in
[\#1559](https://fedorahosted.org/sssd/ticket/1559 "enhancement: [RFE] Use the getpwnam()/getgrnam() interface as a gateway to resolve SID ... (closed: fixed)"){.closed
.ticket} "Use the getpwnam()/getgrnam() interface as a gateway to
resolve SID to Names".

##### Memory cache for the new lookups {#Memorycacheforthenewlookups}

To speed up lookup the new calls should be able to use the memory cache.

### Implementation details {#Implementationdetails}

Since the Global Catalog is just an LDAP server running on a
non-standard port the general LDAP lookup code would not need much
change if any. But resolving the Global Catalog server would be a bit
different because before the actual DNS service record lookup the site
has to be determined.

I think it is sufficient to determine the site on startup and when SSSD
switches from offline to online.

To decode the blob returned by the CLDAP request libndr-nbt from the
samba4-libs package would be useful. Since libndr-krb5pac is already
used in the PAC responder I think it is ok to add this new dependency
here.

#### Environments with trusts {#Environmentswithtrusts}

In an environment with trust it must be possible to handle multiple open
connections to Global Catalogs of different forests.

According to
[[​]{.icon}http://technet.microsoft.com/en-us/library/cc772808%28v=ws.10%29.aspx](http://technet.microsoft.com/en-us/library/cc772808%28v=ws.10%29.aspx){.ext-link}
referrals are used during Kerberos requests to guide the client to the
right KDC. I have not found a similar document for LDAP requests to the
Global Catalog. I have to find out if it is possible to work with
referrals here, too or if it is needed to read the trusted domain
objects
([[​]{.icon}http://msdn.microsoft.com/en-us/library/cc223754.aspx](http://msdn.microsoft.com/en-us/library/cc223754.aspx){.ext-link})
from the Global Catalog.

#### New NSS responder calls {#NewNSSrespondercalls}

### How to test {#Howtotest}

Since the Global Catalog lookups just replace the current lookup methods
SSSD should just behave as before (Regression testing).

Additional the following changes might be visible on the user or admind
level.

#### AD provider {#ADprovider}

If the SSSD client is joined to a Windows domain which is part of a
forest, Global Catalog lookups should be able to resolve all users and
groups in the forest and not only the ones from the joined domain.

#### IPA provider running on a FreeIPA server {#IPAproviderrunningonaFreeIPAserver}

If the FreeIPA server is able to use SSSD for SID-to-Name and
Name-to-SID lookups running winbind on the FreeIPA server is not needed
anymore.

### Author(s) {#Authors}

Sumit Bose
&lt;[[​]{.icon}sbose@redhat.com](mailto:sbose@redhat.com){.mail-link}&gt;