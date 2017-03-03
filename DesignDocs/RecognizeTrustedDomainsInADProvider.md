Recognize trusted domains in AD provider {#RecognizetrusteddomainsinADprovider}
----------------------------------------

Related tickets:

-   [[​]{.icon}RFE Recognize trusted domains in AD
    provider](https://fedorahosted.org/sssd/ticket/364){.ext-link}

### Problem Statement {#ProblemStatement}

With the current LDAP lookups the SSSD AD provider can only find users
and groups in the local domain. With Global Catalog lookups
([[​]{.icon}design
page](https://docs.pagure.org/sssd-test2/DesignDocs/GlobalCatalogLookups.html){.ext-link})
this will be extended to all users and groups of the local forest. Using
the PAC helps to avoid group membership lookups ([[​]{.icon}RFE Use
MS-PAC to retrieve user's group
list](https://fedorahosted.org/sssd/ticket/1558){.ext-link}).

What is missing are lookups of users and groups in trusted forests and
password based authentication of users from trusted forests. For this
the names of the trusted forests and additional suffixes managed by the
forest are needed. The names the

### Overview view of the solution {#Overviewviewofthesolution}

### Implementation details {#Implementationdetails}

### How to test {#Howtotest}

### Author(s) {#Authors}

Sumit Bose
&lt;[[​]{.icon}sbose@redhat.com](mailto:sbose@redhat.com){.mail-link}&gt;
