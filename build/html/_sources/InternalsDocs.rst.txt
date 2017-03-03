.. raw:: html

   <div class="wiki-toc">

#. `1. Introduction <#a1.Introduction>`__
#. `2. Active Directory Use Case <#a2.ActiveDirectoryUseCase>`__
#. `3. System Overview <#a3.SystemOverview>`__

   #. `3.1. External Perspective <#a3.1.ExternalPerspective>`__

      #. `3.1.1. SSS Client
         Applications <#a3.1.1.SSSClientApplications>`__

   #. `3.2. Internal Perspective <#a3.2.InternalPerspective>`__

      #. `3.2.1. Control Flow <#a3.2.1.ControlFlow>`__
      #. `3.2.2. Data Flow <#a3.2.2.DataFlow>`__

         #. 

            #. `3.2.2.1. Data Flow (NSS
               Responder) <#a3.2.2.1.DataFlowNSSResponder>`__
            #. `3.2.2.2. Data Flow (PAM
               Responder) <#a3.2.2.2.DataFlowPAMResponder>`__

   #. `3.3. SSSD Components <#a3.3.SSSDComponents>`__

      #. `3.3.1. Processes and Shared
         Objects <#a3.3.1.ProcessesandSharedObjects>`__

         #. `3.3.1.1. SSS Client Library <#a3.3.1.1.SSSClientLibrary>`__
         #. `3.3.1.2. Monitor <#a3.3.1.2.Monitor>`__
         #. `3.3.1.3. Responder <#a3.3.1.3.Responder>`__
         #. `3.3.1.4. Backend (aka Data
            Provider) <#a3.3.1.4.BackendakaDataProvider>`__
         #. `3.3.1.5. Provider Plugin <#a3.3.1.5.ProviderPlugin>`__
         #. `3.3.1.6. Short-Lived Child
            Process <#a3.3.1.6.Short-LivedChildProcess>`__

      #. `3.3.2. Protocols <#a3.3.2.Protocols>`__
      #. `3.3.3. UNIX signals <#a3.3.3.UNIXsignals>`__
      #. `3.3.4. Databases <#a3.3.4.Databases>`__
      #. `3.3.5. Samba Libraries <#a3.3.5.SambaLibraries>`__

#. `4. Advanced Topics <#a4.AdvancedTopics>`__

   #. `4.1. Offline Mode <#a4.1.OfflineMode>`__
   #. `4.2. Multiple Domains and Trust
      Relationships <#a4.2.MultipleDomainsandTrustRelationships>`__

      #. `4.2.1. AD Concepts <#a4.2.1.ADConcepts>`__
      #. `4.2.2. Domain Stanza vs.
         Domain <#a4.2.2.DomainStanzavs.Domain>`__
      #. `4.2.3. SSSD Implementation <#a4.2.3.SSSDImplementation>`__

         #. `4.2.3.1. Subdomains <#a4.2.3.1.Subdomains>`__
         #. `4.2.3.2. Global Catalog (GC) <#a4.2.3.2.GlobalCatalogGC>`__
         #. `4.2.3.3. PAC Responder <#a4.2.3.3.PACResponder>`__

#. `5. SSSD Wrappers <#a5.SSSDWrappers>`__

   #. `5.1. SBus <#a5.1.SBus>`__

      #. `5.1.1. SBus Concepts <#a5.1.1.SBusConcepts>`__

         #. `5.1.1.1. SBus Connections <#a5.1.1.1.SBusConnections>`__
         #. `5.1.1.2. Creating SBus Clients and
            Servers <#a5.1.1.2.CreatingSBusClientsandServers>`__
         #. `5.1.1.3. Sending and Receiving SBus
            Messages <#a5.1.1.3.SendingandReceivingSBusMessages>`__
         #. `5.1.1.4. Describing the SBUS
            interface <#a5.1.1.4.DescribingtheSBUSinterface>`__

      #. `5.1.2. Responder-to-Backend
         API <#a5.1.2.Responder-to-BackendAPI>`__

         #. `5.1.2.1. getAccountInfo <#a5.1.2.1.getAccountInfo>`__

            #. `5.1.2.1.1. Request (NSS/PAM
               Responder->Backend) <#a5.1.2.1.1.RequestNSSPAMResponder-Backend>`__
            #. `5.1.2.1.2. Response (Backend=>NSS/PAM
               Responder) <#a5.1.2.1.2.ResponseBackendNSSPAMResponder>`__

         #. `5.1.2.2. pamHandler <#a5.1.2.2.pamHandler>`__

            #. `5.1.2.2.1. Request (PAM Responder ->
               Backend) <#a5.1.2.2.1.RequestPAMResponder-Backend>`__
            #. `5.1.2.2.2. Response (PAM Responder ->
               Backend) <#a5.1.2.2.2.ResponsePAMResponder-Backend>`__

   #. `5.2. SDAP <#a5.2.SDAP>`__

      #. `5.2.1. SDAP Concepts <#a5.2.1.SDAPConcepts>`__
      #. `5.2.2. Establishing an LDAP
         Connection <#a5.2.2.EstablishinganLDAPConnection>`__
      #. `5.2.3. Performing LDAP
         Operations <#a5.2.3.PerformingLDAPOperations>`__

#. `6. Common Data Structures <#a6.CommonDataStructures>`__

   #. `6.1. tevent\_context <#a6.1.tevent_context>`__
   #. `6.2. confdb\_ctx <#a6.2.confdb_ctx>`__
   #. `6.3. sysdb\_ctx <#a6.3.sysdb_ctx>`__
   #. `6.4. main\_context <#a6.4.main_context>`__

#. `7. Component Details <#a7.ComponentDetails>`__

   #. `7.1. Monitor <#a7.1.Monitor>`__

      #. `7.1.1. Spawning and Registering
         Processes <#a7.1.1.SpawningandRegisteringProcesses>`__

   #. `7.2. SSS Client <#a7.2.SSSClient>`__

      #. `7.2.1. SSS\_CLI <#a7.2.1.SSS_CLI>`__
      #. `7.2.2. NSS Client <#a7.2.2.NSSClient>`__
      #. `7.2.3. PAM Client <#a7.2.3.PAMClient>`__

   #. `7.3. Responder <#a7.3.Responder>`__

      #. `7.3.1. resp\_ctx <#a7.3.1.resp_ctx>`__
      #. `7.3.2. Client-Facing Interactions
         (Generic) <#a7.3.2.Client-FacingInteractionsGeneric>`__
      #. `7.3.3.Common Optimization
         Techniques <#a7.3.3.CommonOptimizationTechniques>`__

         #. `7.3.3.1. Data Provider Request
            Table <#a7.3.3.1.DataProviderRequestTable>`__

   #. `7.4. NSS Responder <#a7.4.NSSResponder>`__

      #. `7.4.1. nss\_ctx <#a7.4.1.nss_ctx>`__
      #. `7.4.2. Client-Facing Interactions
         (NSS) <#a7.4.2.Client-FacingInteractionsNSS>`__
      #. `7.4.3. Backend-Facing Interactions
         (NSS) <#a7.4.3.Backend-FacingInteractionsNSS>`__
      #. `7.4.4. Code Flow (NSS) <#a7.4.4.CodeFlowNSS>`__
      #. `7.4.5. Optimization Techniques
         (NSS) <#a7.4.5.OptimizationTechniquesNSS>`__

         #. `7.4.5.1. Negative Cache <#a7.4.5.1.NegativeCache>`__
         #. `7.4.5.2. Fast Cache (aka
            memcache) <#a7.4.5.2.FastCacheakamemcache>`__

   #. `7.5. PAM Responder <#a7.5.PAMResponder>`__

      #. `7.5.1. pam\_ctx <#a7.5.1.pam_ctx>`__
      #. `7.5.2. Client-Facing Interactions
         (PAM) <#a7.5.2.Client-FacingInteractionsPAM>`__
      #. `7.5.3. Backend-Facing Interactions
         (PAM) <#a7.5.3.Backend-FacingInteractionsPAM>`__
      #. `7.5.4. Code Flow (PAM) <#a7.5.4.CodeFlowPAM>`__
      #. `7.5.5. Optimization Techniques
         (PAM) <#a7.5.5.OptimizationTechniquesPAM>`__

         #. `7.5.5.1. Initgroups Cache <#a7.5.5.1.InitgroupsCache>`__

   #. `7.6. Optimizations Code Flow <#a7.6.OptimizationsCodeFlow>`__
   #. `7.7. Backend <#a7.7.Backend>`__

      #. `7.7.1. Backend Concepts <#a7.7.1.BackendConcepts>`__

         #. `7.7.1.1. Services and
            Servers <#a7.7.1.1.ServicesandServers>`__
         #. `7.7.1.2. Name Resolution <#a7.7.1.2.NameResolution>`__
         #. `7.7.1.3. Configuration
            Lines <#a7.7.1.3.ConfigurationLines>`__

      #. `7.7.2. be\_ctx <#a7.7.2.be_ctx>`__
      #. `7.7.3. Responder-Facing
         Interactions <#a7.7.3.Responder-FacingInteractions>`__

         #. `7.7.3.1. Registering
            Responders <#a7.7.3.1.RegisteringResponders>`__
         #. `7.7.3.2. Receiving SBus
            Messages <#a7.7.3.2.ReceivingSBusMessages>`__

   #. `7.8. AD Provider Plugin <#a7.8.ADProviderPlugin>`__

      #. `7.8.1. AD Provider Plugin:
         id\_provider <#a7.8.1.ADProviderPlugin:id_provider>`__

         #. `7.8.1.1. ad\_id\_ctx <#a7.8.1.1.ad_id_ctx>`__
         #. `7.8.1.2.
            ad\_account\_info\_handler <#a7.8.1.2.ad_account_info_handler>`__
         #. `7.8.1.3. ad\_check\_online <#a7.8.1.3.ad_check_online>`__

      #. `7.8.2. AD Provider Plugin: auth\_provider and
         chpass\_provider <#a7.8.2.ADProviderPlugin:auth_providerandchpass_provider>`__

         #. `7.8.2.1. krb5\_auth\_ctx <#a7.8.2.1.krb5_auth_ctx>`__
         #. `7.8.2.2. krb5\_pam\_handler <#a7.8.2.2.krb5_pam_handler>`__

            #. `7.8.2.2.1. Parent => Child <#a7.8.2.2.1.ParentChild>`__
            #. `7.8.2.2.2. Child=>Parent <#a7.8.2.2.2.ChildParent>`__

         #. `7.8.2.3. kdcinfo files <#a7.8.2.3.kdcinfofiles>`__

      #. `7.8.3. AD Provider Plugin:
         access\_provider <#a7.8.3.ADProviderPlugin:access_provider>`__

         #. `7.8.3.1. ad\_access\_ctx <#a7.8.3.1.ad_access_ctx>`__
         #. `7.8.3.2.
            ad\_access\_handler <#a7.8.3.2.ad_access_handler>`__

#. `8. Tevent Basics <#a8.TeventBasics>`__

   #. `8.1. Events <#a8.1.Events>`__
   #. `8.2. Requests <#a8.2.Requests>`__
   #. `8.3. Subrequests <#a8.3.Subrequests>`__

#. `9. Functions <#a9.Functions>`__

   #. `9.1. SDAP Connection Functions <#a9.1.SDAPConnectionFunctions>`__

      #. `9.1.1.
         sdap\_id\_op\_connect\_send/recv <#a9.1.1.sdap_id_op_connect_sendrecv>`__
      #. `9.1.2.
         sdap\_cli\_connect\_send/recv <#a9.1.2.sdap_cli_connect_sendrecv>`__
      #. `9.1.3.
         be\_resolve\_server\_send/recv <#a9.1.3.be_resolve_server_sendrecv>`__
      #. `9.1.4.
         fo\_resolve\_service\_send/recv <#a9.1.4.fo_resolve_service_sendrecv>`__
      #. `9.1.5.
         resolv\_gethostbyname\_send/recv <#a9.1.5.resolv_gethostbyname_sendrecv>`__
      #. `9.1.6.
         resolv\_gethostbyname\_dns\_send/recv <#a9.1.6.resolv_gethostbyname_dns_sendrecv>`__
      #. `9.1.7.
         sdap\_connect\_send/recv <#a9.1.7.sdap_connect_sendrecv>`__
      #. `9.1.8.
         sss\_ldap\_init\_send/recv <#a9.1.8.sss_ldap_init_sendrecv>`__
      #. `9.1.9.
         sdap\_get\_rootdse\_send/recv <#a9.1.9.sdap_get_rootdse_sendrecv>`__
      #. `9.1.10.
         sdap\_kinit\_send/recv <#a9.1.10.sdap_kinit_sendrecv>`__
      #. `9.1.11.
         sdap\_get\_tgt\_send/recv <#a9.1.11.sdap_get_tgt_sendrecv>`__
      #. `9.1.12. sdap\_auth\_send/recv <#a9.1.12.sdap_auth_sendrecv>`__

   #. `9.2. SDAP Operation Request
      Functions <#a9.2.SDAPOperationRequestFunctions>`__

      #. `9.2.1. users\_get\_send/recv <#a9.2.1.users_get_sendrecv>`__
      #. `9.2.2.
         sdap\_get\_generic\_send/recv <#a9.2.2.sdap_get_generic_sendrecv>`__
      #. `9.2.3.
         sdap\_get\_generic\_ext\_send/recv <#a9.2.3.sdap_get_generic_ext_sendrecv>`__

#. `10. Filesystem Locations <#a10.FilesystemLocations>`__
#. `11. Helpful Links <#a11.HelpfulLinks>`__

.. raw:: html

   </div>

**SSSD Internals (October, 2013)
Author: Yassir Elley**

1. Introduction
===============

The purpose of this document is to give a basic description of the
internals of the SSSD implementation. The material in this document is
accurate as of SSSD 1.10. It is assumed that the reader is already
familiar with the external usage of SSSD. The intended audience of this
document are new contributors to the SSSD project. This document is not
intended to be comprehensive. For additional details on specific
features, please refer to the various `​Design
Documents <https://docs.pagure.org/sssd-test2/DesignDocs.html>`__. This
document does not discuss the details of building, installing, and
debugging SSSD. More information on these topics can be found in the
`​Developer Pages <https://docs.pagure.org/sssd-test2/DevRes.html>`__,
and the
`​Documentation <https://docs.pagure.org/sssd-test2/Documentation.html>`__.
To be most useful, this document should be updated as appropriate, and
reviewed at regular intervals.

In order to better understand the material and make things more
concrete, this document starts by describing a specific use case (and
configuration) that will be discussed throughout the document. The
document starts with a high level end-to-end overview, and then
deep-dives into detailed descriptions. The document is organized into
the following sections:

-  Active Directory Use Case: specifies use case used throughout the
   document
-  System Overview: end-to-end SSSD overview, including short
   descriptions of components
-  Advanced Topics: offline operation, multiple domains, trust
   relationships
-  SSSD Wrappers: SBus, SDAP
-  Common Data Structures: data structures used by each SSSD process
-  Component Details: gory details of each component
-  Appendix: tevent, function descriptions, filesystem locations,
   helpful links

2. Active Directory Use Case
============================

From an SSSD perspective, there are two main Active Directory (AD) use
cases, depending on whether we are directly integrated with AD, or
whether we are indirectly integrated with AD through IPA. For now, this
document only covers the direct AD integration use case.

SSSD consumes DNS, LDAP, and Kerberos services in order to resolve
server names, perform identity lookups, and perform security-related
tasks. In an AD environment, all three services are typically provided
by a single AD server.

In the direct AD integration use case, a host directly joins an AD
domain. At this point, the AD's LDAP service creates a computer account
for the host, and the AD's Kerberos service creates a service principal
and shared secret credentials for the host. After these host credentials
are installed in the host's keytab, the host looks to AD as any other
Windows client, allowing us to leverage existing AD technology. The
preceding steps to join a domain, as well as additional steps that
generate appropriate configuration files, and kick off the master SSSD
process (/usr/sbin/sssd), can all be performed by simply running “realm
join foo.com” as root. For more information on realmd, see `​Realmd
Page <http://www.freedesktop.org/software/realmd/>`__.

For our use case, the SSSD configuration file (*/etc/sssd/sssd.conf*)
simply specifies an NSS Responder, a PAM Responder, and a single Backend
that uses an AD Provider Plugin to communicate with an AD server. We
will use the following values for our use case. Throughout the document,
we will mark these values (and derived values) in red, to indicate that
other values could have been used.

-  the AD domain is named “foo.com”
-  the AD server is named “adserver.foo.com”
-  the AD username and password we will use in our examples is
   "aduser@foo.com" and ”adpass”

Using those values, our use case can be represented by the following
SSSD configuration file:

.. code:: wiki

    [sssd]                # information needed by the monitor is specified in [sssd]
    domains = foo.com       # each domain stanza corresponds to a Backend
    services = nss, pam     # each configured service corresponds to a Responder

    [nss]
    default_shell = /bin/bash

    [pam]               # SSSD should use default values for pam-related options

    [domain/foo.com]        # on this line, foo.com represents a domain stanza
    ad_domain = foo.com             # on this line, foo.com represents an AD domain
    ad_server = adserver.foo.com
    krb5_realm = FOO.COM
    id_provider = ad
    auth_provider = ad
    chpass_provider = ad
    access_provider = ad

Note that one of SSSD's design goals is to allow its configuration file
(*sssd.conf*) to be very short, where configuration values that are
needed (but not provided) are populated by either using default values,
or by using DNS to auto-discover the values.

-  if *ad\_domain* is not specified, it defaults to the value of the
   domain stanza's name (e.g. *foo.com*)
-  if *ad\_server* is not specified, DNS service discovery is used to
   find an appropriate server
-  if *auth\_provider*, *chpass\_provider*, or *access\_provider* are
   not specified, they default to the value of the *id\_provider* (e.g.
   *ad*).

For example, if DNS service discovery were available, the domain
configuration above could have equivalently been written as:

.. code:: wiki

    [domain/foo.com]
    id_provider = ad
    krb5_realm = FOO.COM

3. System Overview
==================

3.1. External Perspective
-------------------------

Fundamentally, SSSD provides identity (NSS) and authentication (PAM)
services to its SSS Client Applications using information stored in
remote servers (e.g. AD Server, IPA Server). SSSD serves as a central
point of enforcement and management for the local machine on which it is
running. SSSD components are able to share consistent state because
multiple technologies are configured in a single configuration file.
SSSD also improves performance by maintaining a local SSSD Cache, and by
the fact that SSSD only needs to maintain a single connection to each of
the remote servers (while servicing multiple SSS Client Applications).
SSSD can optionally use the local SSSD Cache to continue to provide
identity and authentication services to users when they go offline.

*This diagram shows two different SSS Client Applications making NSS/PAM
calls to SSSD. In order to fulfill the request, SSSD either uses a
cached result (by consulting the Cache), or an up-to-date result (by
contacting the AD Server using LDAP/KRB). As such, SSSD is acting in a
server role for the SSS Client Applications, and in a client role with
respect to AD.*

3.1.1. SSS Client Applications
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Through the beauty of the pluggable NSS and PAM frameworks, an SSS
Client Application (e.g. *ls*) is unaware that it is communicating with
an SSS Client Library. An SSS Client Application simply calls a standard
NSS or PAM function, which is mapped by the NSS/PAM runtime to a
module-specific function name, and which is then delivered to an SSS
Client Library (assuming that SSSD configuration has taken place). Note
that we can either refer to a Client Library generically (e.g. “SSS
Client Library”), or we can refer to it specifically (e.g. “NSS Client
Library”).

Examples of NSS-using SSS Client Applications include *ls*, *id*, and
*getent*. These commands call standard NSS functions, which include
settors/gettors for several name databases (e.g. passwd, group, service,
netgroup, etc). An entry in a name database can be retrieved by using an
appropriate key (e.g. name, id, port, etc). Alternatively, the entries
in a name database can be enumerated, although this can be quite
inefficient for large databases. The full API supported by the NSS
Client Library is defined in sss\_nss.exports.

Examples of PAM-using SSS Client Applications include *login*, *su*, and
*ssh*. These commands call standard PAM functions. However, unlike NSS
functions, PAM functions are called within the context of a PAM
transaction, which maintains the state for the entire transaction
(including any input values set by the caller, such as username, etc). A
typical PAM transaction looks like:

.. raw:: html

   <div class="code">

::

    pam_start("login", "aduser", &pam_conv, &pamh); // initiate pam transaction
    pam_authenticate(pamh, 0);                      // verify identity of user
    ret = pam_acct_mgmt(pamh, 0);                   // determine if user account is valid
    if (ret == PAM_NEW_AUTHTOK_REQD)                // if user password has expired
       pam_chauthtok(pamh, 0);                      // change user password
    pam_setcred(pamh, PAM_ESTABLISH_CRED);          // set user's credentials
    pam_open_session(pamh, 0)                       // initiate session management
    ...                                             // non-pam code
    pam_close_session(pamh, 0)                      // terminate session management
    pam_end(pamh, ret);                             // terminate pam transaction

.. raw:: html

   </div>

The PAM conversation function (pam\_conv), set by the caller, allows the
implementation to communicate directly with the application. For
example, the implementation of PAM functions that use passwords (i.e.
pam\_authenticate, pam\_chauthtok) would use the registered PAM
conversation function to prompt the user for a password.

The full API supported by the PAM Client Library is defined in
pam\_sss.c. Note that the PAM Client Library does not handle the
pam\_start() and pam\_end() calls that surround a pam transaction, but
it handles all of the PAM functions in between.

3.2. Internal Perspective
-------------------------

This section gives an internal system overview of SSSD's control flow
(i.e. messages used for control, configuration, initialization) and
SSSD's data flow (i.e. messages related to data traffic resulting from
client requests).

3.2.1. Control Flow
~~~~~~~~~~~~~~~~~~~

*This diagram shows SSSD's start-up procedure. The diagram only shows a
single NSS Responder for clarity, but keep in mind that our use case
requires two Responders (NSS and PAM).*

#. Monitor process initializes itself, which includes parsing
   configuration file (sssd.conf) and loading it into confdb. After it
   is loaded, the Monitor retrieves and applies Monitor-specific config
   from the confdb.
#. Monitor spawns (i.e. fork/exec) a Backend process for the single
   domain specified in config.
#. Backend process initializes itself, which includes sending *Register*
   message to Monitor, as well as dynamically loading AD Provider
   Plugin.
#. Backend contacts confdb in order to retrieve and apply
   Backend-specific config.
#. Monitor spawns an NSS Responder process (shown), as well as a PAM
   Responder (not shown).
#. Responder process initializes itself, which includes sending
   *Register* message to Monitor, and sending separate *Register*
   message to Backend.
#. Responder contacts confdb in order to retrieve and apply
   Responder-specific config.
#. Monitor periodically sends *Ping* messages to registered processes,
   and restarts them as needed.

3.2.2. Data Flow
~~~~~~~~~~~~~~~~

In this section, we will separately examine the internal data flow for
the NSS Responder and the PAM Responder, since the data flow for the PAM
Responder is more complicated. Note that all of the components in the
Data Flow diagrams are under the SSSD team's control, except for the SSS
Client Application and remote AD Server. Also note that this section
assumes that we are in “online mode”, meaning that SSSD is able to
communicate with the AD Server. In the “offline mode” case, we are only
able to consult the Cache (since the AD Server is not reachable).

3.2.2.1. Data Flow (NSS Responder)
''''''''''''''''''''''''''''''''''

*This diagram shows the data flow generated by an SSS Client Application
making an NSS request to SSSD.*

#. SSS Client Application's request is handled by our dynamically loaded
   NSS Client Library, which consults the fast cache (aka memcache). If
   valid cache entry exists (unexpired), NSS Client Library immediately
   returns cached result to SSS Client Application.
#. If no valid cache entry exists in fast cache, NSS Client Library
   sends client's NSS request to matching NSS Responder.
#. NSS Responder consults Cache. If valid cache entry exists
   (unexpired), NSS Responder immediately returns cached result to SSS
   Client Application (this step not shown above)
#. If no valid cache entry exists, NSS Responder sends *getAccountInfo*
   request message to Backend, asking Backend to update Cache with data
   corresponding to client's NSS request.
#. Backend uses AD Provider Plugin to make LDAP call to remote AD Server
   and to retrieve response from AD Server.
#. Backend updates Cache, and also sends *getAccountInfo* response
   message (containing status) to NSS Responder; this also serves as
   indication that Cache has been updated.
#. NSS Responder reads updated result from Cache.
#. NSS Responder returns updated result to NSS Client Library, which
   passes it to SSS Client Application.

3.2.2.2. Data Flow (PAM Responder)
''''''''''''''''''''''''''''''''''

*This diagram shows the data flow generated by an SSS Client Application
making a PAM request to SSSD*

#. SSS Client Application's request is handled by our dynamically loaded
   PAM Client Library, which sends request to matching PAM Responder.
#. Like the NSS Responder, the PAM Responder sends *getAccountInfo*
   request message to Backend, but only to ask it to update Cache with
   client's group memberships (i.e. initgroups)
#. Backend uses AD Provider Plugin to make LDAP call to remote AD Server
   and to retrieve response.
#. Backend updates Cache, and also sends *getAccountInfo* response
   message (containing status) to PAM Responder; this also serves as
   indication that Cache has been updated.
#. PAM Responder reads updated initgroups information from Cache.
#. PAM Responder sends *pamHandler* request message to Backend
#. Backend uses AD Provider Plugin to retrieve response from Child
   Process, which makes the actual KRB calls; note that the Child
   Process (not shown) will be discussed later in the document
#. Backend sends *pamHandler* response message (containing status) to
   PAM Responder
#. PAM Responder returns updated result to PAM Client Library, which
   passes it to SSS Client Application.

Clearly, the PAM Responder's data flow is different from the NSS
Responder's data flow. The primary difference is that the result of a
*pamHandler* request is not stored in the Cache. The *pamHandler*
response message contains status information, most of which is passed
back to the PAM Client Library. Another difference is that the NSS
Responder sends the Backend only a single request message, corresponding
to the SSS Client's request. In contrast, the PAM Responder sends two
request messages: the first one to find the client's group memberships,
and the second one corresponding to the SSS Client's request. There are
a couple of reasons for this. First, the PAM Responder wants to ensure
that the identity returned by LDAP is the same identity that should be
used for authentication. Second, in the case where multiple domains are
configured, the given identity is tried against each domain, in the same
order as it appears in the *domains* line in sssd.conf. As soon as the
requested identity has group memberships in a particular domain, that
domain is used as **the** authoritative domain for that client request.
Note that complications arising from the use of subdomains will be
discussed later. Additional difference is that while the PAM responder
always downloads the group memberships from the server (if reachable)
even if the cache is up to date. This is to ensure correct authorization
data on login, because group memberships are set on login on a Linux
system.

3.3. SSSD Components
--------------------

3.3.1. Processes and Shared Objects
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Despite the fact that its name suggests there is only a **single**
daemon, the term “SSSD” usually refers to a **set** of daemons and
shared objects that work together to provide identity and authentication
services to SSS Client Applications. The following table summarizes the
SSSD-related processes and shared objects needed for our AD use case
(along with their configuration files). Note that default values are
used for configuration fields that are not specified. A brief
description of these components follows.

+--------------------------------------+--------------------------------------------------------+
| *Component Name*                     | *Component Configuration*                              |
+--------------------------------------+--------------------------------------------------------+
| Shared Object: NSS Client Library    | /etc/nsswitch.conf; using nss\_sss.so module           |
+--------------------------------------+--------------------------------------------------------+
| Shared Object: PAM Client Library    | /etc/pam.d/system-auth; using pam\_sss.so module       |
+--------------------------------------+--------------------------------------------------------+
| Process: Monitor                     | /etc/sssd/sssd.conf: [sssd] stanza                     |
+--------------------------------------+--------------------------------------------------------+
| Process: NSS Responder               | /etc/sssd/sssd.conf: [nss] stanza                      |
+--------------------------------------+--------------------------------------------------------+
| Process: PAM Responder               | /etc/sssd/sssd.conf: [pam] stanza                      |
+--------------------------------------+--------------------------------------------------------+
| Process: Backend                     | /etc/sssd/sssd.conf: [domain/foo.com] stanza           |
+--------------------------------------+--------------------------------------------------------+
| Shared Object: AD Provider Plugin    | /etc/sssd/sssd.conf: [domain/foo.com] provider lines   |
+--------------------------------------+--------------------------------------------------------+
| Process: Short-Lived Child Process   | no config; used to perform blocking operations         |
+--------------------------------------+--------------------------------------------------------+

3.3.1.1. SSS Client Library
^^^^^^^^^^^^^^^^^^^^^^^^^^^

An SSS Client Library is a shared object that is dynamically loaded by
an SSS Client Application in order to communicate with SSSD. While we
have so far been careful to distinguish between the SSS Client
Application and SSS Client Library, from now on, we shall drop the
“Library” and refer to the SSS Client Library as simply SSS Client (or
NSS Client or PAM Client). Indeed, when the code refers to “SSS Client”
(or to identifiers prefixed with “sss\_cli”), it is referring an SSS
Client Library.

3.3.1.2. Monitor
^^^^^^^^^^^^^^^^

The monitor is **the** master SSSD process that spawns other SSSD
processes and ensures they stay alive. It also sends SBus messages to
other SSSD processes if it detects networking status changes. For
example, if SSSD is in offline mode, and the Monitor detects that a
cable has been plugged in, the Monitor sends SBus messages to the other
SSSD processes to go online immediately.

3.3.1.3. Responder
^^^^^^^^^^^^^^^^^^

A Responder is a process that receives requests from an SSS Client
Library, and that returns responses to it. In order to ensure that the
Responder and Cache have a consistent view of user data, most Responders
(e.g. NSS Responder) fulfill the client’s request by retrieving data
from the Cache (although the Cache may need to be updated first). The
PAM Responder is an exception, in that the Backend returns
authentication results directly to the PAM Responder (as opposed to
storing them in the Cache). Having said that, the PAM Responder **does**
store authentication-related data in the Cache, but this is only used
for offline authentication, which will be discussed later in the
document. Note that each Responder (NSS, PAM) runs in its own process.

3.3.1.4. Backend (aka Data Provider)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A Backend is a process that represents a domain stanza (e.g.
[domain/foo.com]) and that uses Provider Plugins to talk to remote
servers (e.g. AD) in order to perform the necessary identity lookups
and/or pam-related tasks. The term “Backend” is synonymous with the term
“Data Provider”. In fact, while some parts of the code use the term
“Backend” (or use “\ *be\_*\ ” prefixes), other parts of the code use
the term “Data Provider” (or use “\ *dp\_*\ ” prefixes) to refer to a
Backend. However, to prevent confusion between a Data Provider and
Provider Plugin, this document uses the term “Backend” for this
component.

A Backend receives a request message from a Responder, processes the
request message by communicating with a remote server, updates the
Cache, and sends a response message to the Responder, which also serves
as an indication that the Cache has been updated. Each domain stanza has
its own Backend process, which dynamically loads one or more Provider
Plugins (aka “Backend Modules”), which do the heavy lifting of
communicating with the remote server. A Backend's configuration
specifies the individual Provider Plugins to be used for each provider
type, as information needed to access the remote server. Think of a
Backend as a container, consisting of several individual provider types,
each of which could potentially be using a different Provider Plugin.

3.3.1.5. Provider Plugin
^^^^^^^^^^^^^^^^^^^^^^^^

A Provider Plugin is a shared object that is dynamically loaded by a
Backend to communicate with remote servers. The role of a provider
plugin is to provide plugin-specific implementations of generic
functions used to handle requests and to determine whether or not we are
in online mode.

Each Provider Plugin has a name (e.g. AD), along with a set of provider
types that it supports (id\_provider, auth\_provider, access\_provider,
chpass\_provider, etc). Each individual provider type could use a
different Provider Plugin (e.g. id\_provider=ldap, auth\_provider=krb5)
or all of the individual provider types could use the same Provider
Plugin (e.g. id\_provider=ad, auth\_provider=ad). You can tell which
Provider Plugins are supported in the code by looking at the names of
the subdirectories of the providers directory (i.e. ad, ipa, krb5, ldap,
proxy, simple). Each provider plugin will require certain additional
configuration information to be specified in sssd.conf (e.g.
“\ *id\_provider=ad*\ ” will require the *ad\_domain* field, which will
be used to locate the actual AD server).

3.3.1.6. Short-Lived Child Process
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

SSSD tries very hard not to make blocking function calls. The main
exception is that we make blocking calls to access our various
databases. However, those calls are expected to return very quickly, so
they do not negatively affect our performance much. However, there are
times when we have no choice but to call external libraries or commands
that only support blocking semantics. For example, all calls to the MIT
Kerberos library are blocking function calls. Similarly, in order to
perform dynamic DNS (DDNS) updates, we call the *nsupdate* command,
which will not necessarily return very quickly. In such scenarios,
rather than having an SSSD process (which is running a tevent main loop)
perform a blocking operation, the SSSD process spawns a short-lived
Child Process, which performs the blocking operation on the parent's
behalf. As soon as the child process is spawned, the parent process
asynchronously sends it a request (using UNIX pipes), and then returns
control to its tevent main loop, thereby maintaining aysnchronous
semantics. The child process then performs the blocking operation.
Later, when the operation is finally complete, the child process sends
the parent process the result (which it asynchronously reads), and then
exits. It may seem inefficient to spawn a new child process each time a
blocking operation needs to performed. However, these blocking
operations are called relatively infrequently. If this were to present a
problem in the future, a dedicated pool of child processes could be
used. Instances in which Child Processes are currently used in the code
include:

-  during gssapi-bind authentication for ldap searches (kerberos
   function calls)
-  during kinit of behalf of user (kerberos function calls)
-  during the update of client records using dynamic dns (*nsupdate*)

3.3.2. Protocols
~~~~~~~~~~~~~~~~

*This diagram shows the protocols used between various SSSD components.*

-  **DBus**: used for local IPC between Responders, Backends, and
   Monitor. Note that SSSD uses SBus (“SSSD DBus”) as a wrapper around
   the DBus library (libdbus), in order to integrate the DBus API with
   the tevent main loop.
-  **LDAP**: used by a Provider Plugin to send LDAP operation requests
   to a remote LDAP server. Note that SSSD uses SDAP (“SSSD LDAP”) as a
   wrapper around the OpenLDAP library (libldap), in order to integrate
   the OpenLDAP API with the tevent main loop.
-  **Kerberos**: used by a Provider Plugin or short-lived Child Process
   to perform Kerberos operations. Since the MIT Kerberos library
   (libkrb5) does not support non-blocking calls, any Kerberos function
   call that requires communicating with a remote Kerberos server (KDC)
   will result in the spawning of a short-lived Child Process. A
   Kerberos function call that operates locally (reading a keytab,
   writing a ccache, parsing names, etc) can be handled directly in the
   Provider Plugin, and does not require a short-lived Child Process to
   be spawned.
-  **DNS**: used by a Provider Plugin to interact with a remote DNS
   server in order to resolve server names (using standard A/AAAA
   address records) or to resolve service names (using domain-specific
   SRV records). While SSSD doesn't use a wrapper around the C-Ares DNS
   library (libcares), it does perform the necessary tasks to integrate
   the library with the tevent main loop.
-  **SSS\_CLI**: an SSSD-specific custom protocol that is used by an SSS
   Client to communicate with its matching Responder. SSS\_CLI is a
   request/response protocol that communicates over raw Unix Domain
   Sockets, using its own TLV-encoding.

3.3.3. UNIX signals
~~~~~~~~~~~~~~~~~~~

Apart from the internal SBUS communication, SSSD also uses UNIX signals
for certain functionality - either for communication with external
utilities or for cases where the SBUS communication might not work, such
as an unresponsive worker process. Below is an overview of the supported
signals and their use. The singal handlers are typically integrated with
the tevent event loop using its ``tevent_add_signal`` call.

SIGTERM
    If a responder or a provider process fails to send a ``pong``
    message to the monitor process after receiving the ``ping`` message,
    the monitor terminates the unresponsive process with a SIGTERM. Also
    used to terminate helper processes (such as the krb5\_child process)
    in case of a timeout.
SIGKILL
    In cases where an unresponsive worker process does not terminate
    after receiving SIGTERM, the monitor forcibly kills it with SIGKILL
SIGUSR1
    Can be handled a sssd\_be process individually or the monitor
    process (in that case, the monitor re-sends the signal to all
    sssd\_be processes it handles). Upon receiving this signal, the
    sssd\_be process transitions into the 'offline' state. This signal
    is mostly useful for testing.
SIGUSR2
    Similar to the SIGUSR1 signal, the SIGUSR2 would cause an sssd\_be
    process to reset the offline status and retry the next request it
    receives against a remote server.
SIGHUP
    Can be delivered to the sssd process. After receiving SIGHUP, the
    monitor rotates its logfile and sends a ``reset`` method to the
    managed processes. The managed processes also rotate logfiles. In
    addition, the sssd\_be processes re-read resolv.conf and the
    sssd\_nss process clears the fast in-memory cache.

3.3.4. Databases
~~~~~~~~~~~~~~~~

*This diagram shows which SSSD components access which SSSD databases.*

-  **Configuration DB (confdb)**: a single memory-mapped LDB database in
   which the parsed contents of the SSSD configuration file are stored
   by the Monitor process, upon initialization. Any SSSD process can
   read from the Configuration DB, while only a few (e.g. Monitor) can
   write to it. The configuration DB is typically found at
   /var/lib/sss/db/config.ldb
-  **System DB (sysdb)**: a per-domain memory-mapped LDB database, which
   caches responses of recently sent requests. The sysdb is written to
   by the Backend, and read by the Responders. Even though this is a
   per-domain database, it is sometimes referred to generally as the
   System Cache. Since our use case only has a single domain, the System
   Cache and System DB refer precisely to the same LDB database. The
   System DB for a domain named "foo.com” is typically found at
   /var/lib/sss/db/cache\_foo.com.ldb
-  **Fast Cache (memcache)**: a single set of memory-mapped cache files,
   from which an SSS Client can retrieve identity (NSS) information
   without having to contact the NSS Responder. The NSS Responder
   populates the memcache files, while the SSS Client reads the memcache
   files. Currently, only two maps that are supported: the password map
   (/var/lib/sss/mc/passwd) and the group map (/var/lib/sss/mc/group).
   If the memcache does not have the necessary information, then the SSS
   Client falls back to using the NSS Responder. Note that this
   mechanism is not used by the PAM Responder. Note also that this Fast
   Cache (memcache) is not considered part of the System Cache (sysdb).

3.3.5. Samba Libraries
~~~~~~~~~~~~~~~~~~~~~~

-  **LDB**: database library that uses an ldap-like data model (although
   schema-less). While using a TDB backend to provide the actual
   storage, LDB manipulates the TDB data into an LDAP-like structure;
   TDB is a very simple in-memory key/value database that stores data in
   binary format and supports transactions. For more information, refer
   to `​LDB
   Tutorial <http://wiki.samba.org/index.php/Samba4/LDBIntro>`__.
-  **Talloc**: a hierarchical memory allocator in which each dynamically
   allocated memory chunk can have a parent, as well as children. When a
   data structure is freed (using talloc\_free), it frees not only
   itself but all of its children as well. Additionally, talloc
   maintains a reference to the allocated data structure's type,
   providing type checking when casting from a void pointer to a typed
   pointer (assuming you perform the cast by calling talloc\_get\_type).
   For more information, refer to `​Talloc
   Tutorial <http://talloc.samba.org/talloc/doc/html/libtalloc__tutorial.html>`__
-  **Tevent**: a talloc-based event system that provides a main loop
   that supports the asynchronous processing of several event types
   (e.g. timers, file descriptors). Each SSSD process (Monitor,
   Responder, Backend) is single-threaded, and each process runs its own
   tevent main loop, which dispatches events using registered event
   handlers (and contexts). Tevent also facilitates the writing of
   asynchronous code by introducing the concept of tevent requests,
   where one request can call sub-requests, allowing for better
   modularization of the codebase. Using tevent on top of talloc gives
   us the ability to trivially cancel tevent requests (by simply freeing
   the tevent\_req pointer), which will also automatically free
   resources of all descendant subrequests (e.g. children,
   grandchildren, etc). It is common to cancel a tevent request when an
   associated timer event expires, since this prevents us from waiting
   indefinitely for results. For more information, refer to `​Tevent
   Tutorial <http://tevent.samba.org/tevent_tutorial.html>`__.

4. Advanced Topics
==================

4.1. Offline Mode
-----------------

So far, we have been assuming that SSSD is in online mode, but SSSD can
transition from online mode to offline mode and back again, depending on
whether its AD server is reachable on the network. When reachable, SSSD
is in online mode and remains in online mode, unless the AD server
becomes unreachable (e.g. perhaps because of a temporary failure).
Similarly, once in offline mode, SSSD remains in offline mode, unless
the AD server becomes reachable (more on that in a bit).

When SSSD is in online mode, it receives various requests from the SSS
Client, which it initially fulfills by contacting the AD server and
storing the identity lookup result or authentication artifacts in the
Cache. Authentication artifacts refer to data needed to reproduce an
authentication result when SSSD is offline. Specifically, when a
presented username and password are able to authenticate successfully
(i.e. when we receive PAM\_SUCCESS from an authenticate operation), we
perform a one-way hash on that password and store it in the user's Cache
entry. If we go offline, and we need to re-authenticate the user, the
user again enters the username and password, and we are able to perform
the offline authentication, by hashing the presented password and
comparing it to the authentication artifact in the user's entry. Of
course, while SSSD is in online mode, we never use these authentication
artifacts.

Once a TGT has been acquired (which requires a valid password), SSSD can
automatically renew the TGT at a configurable interval. If the AD server
becomes unreachable, then SSSD enters offline mode, at which time any
registered offline callback functions are called. For example, one
offline callback function disables the regularly scheduled renewal of
TGTs (since contacting the AD server is not possible). While offline,
SSSD can only fulfill requests directly from the Cache. However, if a
cache entry expires while offline, SSSD continues to honor the cache
entry, until SSSD returns to online mode. If the AD server becomes
reachable again, SSSD enters online mode, at which time any registered
online callback functions are called. For example, one online callback
uses the user's plaintext password stored in the kernel's keyring (only
if explicitly enabled by config) to automatically request a TGT upon
entering online mode, without prompting the user for the password.

Since multiple AD servers can be configured (i.e. for failover
purposes), SSSD only goes offline if **none** of the configured AD
servers are reachable. The circumstances under which a server is
considered unreachable include the following:

-  SSSD is unable to resolve server's name
-  SSSD is able to resolve server's name, but is unable to connect to
   service on server
-  SSSD is not connected to the network

Once offline, SSSD attempts to transition back to online mode by
attempting to reconnect every 30 seconds. In addition to this polling,
there are two notification mechanisms used (by the Monitor) that may
result in an earlier transition to online mode. The Monitor uses netlink
to receive notifications from the kernel when networking state has
changed (e.g. cable is plugged in, routing table is changed, etc). If
notified of a change, the Monitor sends SBus messages to all Backends to
*resetOffline* (i.e. before the hard-coded 30 seconds), which means that
they should attempt to retry the next network operation. If successful,
SSSD transitions to online mode; it not successful (e.g. if the remote
server is down), SSSD remains offline. Separately, the Monitor uses
inotify to receive notifications when the DNS configuration in
/etc/resolv.conf has changed. If notified of a change, the Monitor sends
SBus messages to all Responders and Backends to immediately reload
/etc/resolv.conf, which may result in a transition to online mode (i.e.
if failed name resolution had earlier caused the transition to offline
mode). Finally, during initialization, the Monitor registers
tevent\_signal events that are triggered by receiving the SIGUSR1 (go
offline) and SIGUSR2 (go online) signals. If the Monitor receives either
of those signals, it sends SBus messages to all Backends to go offline
or to go online (and reload /etc/resolv.conf), at which time the
appropriate offline or online callbacks are called, respectively. For
the remainder of the document, unless otherwise stated, we assume that
SSSD is in online mode.

4.2. Multiple Domains and Trust Relationships
---------------------------------------------

4.2.1. AD Concepts
~~~~~~~~~~~~~~~~~~

Things are relatively straightforward if we restrict ourselves to a
single domain. In an AD context, this restriction means that only
objects (e.g. users, computers, etc) managed by the domain controller
(DC) for that single domain are able to interact with each other. For
example, a user in Domain A (i.e. User A) can authenticate with DC A,
and attempt to access Service A, after receiving the appropriate
Kerberos service ticket for that service from DC A. Service A's ACL is
then evaluated to see if User A has permission to use Service A. If not,
a query can be made to DC A to obtain User A's group memberships, after
which the ACL could be re-evaluated and a final authorization decision
could be made. However, this only works because DC A has all the
necessary information (keys, group memberships, etc) for each of the
managed objects in its domain (i.e. users, groups, computers, resources,
etc).

An attempt by User A to access Service B (which is not managed by DC A)
would be unsuccessful. DC A would have no way of generating a Kerberos
service ticket for Service B, since there is no shared secret for
Service B in its security principal database. For the same reason,
Service B would be unable to obtain User A's group memberships from DC A
(since AD typically requires authenticated LDAP searches). And why would
Service B even trust the information it received from DC A?

All of these issues are resolved by the introduction of Kerberos trust
relationships, which are used extensively in an AD environment. In fact,
AD is usually deployed in a multi-domain forest topology, with two-way
transitive trust relationships automatically created between each domain
(by default). Creating a trust relationship between two domains involves
setting up a shared secret between the two domains, so that they can
issue cross-domain referrals for each other's users. With regard to the
group membership issue, there are two components to the solution: a
Global Catalog (GC) server, and Privilege Attribute Certificate (PAC)
information. With regard to the GC Server, while each domain maintains
all attributes for each of the managed objects in its domain, the GC
server maintains a partial set of attributes for each object in the
forest (i.e. in any domain in the forest). Also, while a domain's DC
stores and manages its own domain groups (which can only consist of
users from the same domain), the GC stores and manages universal groups
(which can contain accounts from any domain in the forest). Finally, it
would be nice if we just collected the user's group memberships when the
user was authenticated, and then passed that information along in the
Kerberos service tickets. In fact, this is exactly what is done. As part
of user authentication, AD collects the user's group memberships (and
other security-related information) into a PAC, which it then places in
the TGT's AuthorizationData field. Later, when User A requests a service
ticket for Service B, AD copies the PAC from the TGT to the service
ticket. Service B can then extract the PAC when it receives the Service
Ticket, making it easier and faster to come to an authorization
decision.

4.2.2. Domain Stanza vs. Domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before moving on, we need to understand the difference between a domain
stanza and an ad\_domain. A domain stanza identifies a stanza in the
sssd.conf file (e.g. [domain/foo.com]), which specifies the ad\_domain
and other parameters needed by the Backend process that represents this
domain stanza. As such, while the domain stanza and the ad\_domain might
both have the same name, the domain stanza is simply an arbitrary
configuration label. The primary purpose of naming the domain stanza is
so that it can be referenced by the domains line in the [sssd] stanza,
which lists the active domain stanzas for which the Monitor should spawn
Backend processes. While AD has full knowledge of the ad\_domain named
“foo.com”, it knows nothing about the domain stanza named “foo.com”.

4.2.3. SSSD Implementation
~~~~~~~~~~~~~~~~~~~~~~~~~~

Even without trust relationships, we can have multiple domain stanzas in
the configuration, each corresponding to a single Backend (and a single
ad\_domain). In this simpler case, a Responder still needs some way of
determining to which Backend it should forward a particular client
request. If the client request includes a fully-qualified username (i.e.
including a domain name), then the Responder simply selects the Backend
with a matching domain stanza name. If a fully-qualified username is not
used (which is common), the Responder uses each Backend (in the same
order as specified in the [sssd] stanza) to find the username's entry,
stopping as soon as one is found.

Now, let's see what happens when trust relationships are introduced. In
order to deal with multiple domains that have trust relationships
between them, SSSD implements support for three separate, but related,
features:

-  Subdomains
-  Global Catalog
-  PAC Responder

4.2.3.1. Subdomains
^^^^^^^^^^^^^^^^^^^

In the presence of trust relationships between ad\_domains, things get
complicated. Now, a single domain stanza, while still corresponding to a
single Backend, may correspond to multiple ad\_domains (the primary one,
as well as several other ad\_domains with which the primary ad\_domain
has direct or transitive trust relationships). As such, a single domain
stanza (and Backend) can support multiple trusted ad\_domains, which
SSSD refers to as “subdomains” (not to be confused with DNS subdomains,
which require a parent/child relationship). As such, regardless of
whether or not a fully-qualified username is included in the client
request, the Responder sends an SBus message to each Backend (in the
same order as it is specified in the config), asking it to send back the
list of subdomains it supports, and then attempts to find an entry for
the username in each subdomain, stopping as soon as one is found, and
moving on to the next Backend (and its subdomains) if not found. The
concept of subdomains also applies to groups.

4.2.3.2. Global Catalog (GC)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In a single ad\_domain scenario, the Backend can use the standard LDAP
interface of AD to lookup users and groups. However, the LDAP interface
only returns information about the users and groups in that single
ad\_domain. In order to obtain forest-wide information, including
universal group memberships, the Backend uses the GC interface of AD to
lookup users and groups. Note that the GC is essentially an LDAP server
running on a non-standard port.

4.2.3.3. PAC Responder
^^^^^^^^^^^^^^^^^^^^^^

Similar to other Responders, the PAC Responder is an SSSD Process which
is spawned and managed by the Monitor. It registers itself with the
Monitor and the Backend. Unlike other Responders, the PAC Responder is
not called by an SSS Client Library. Rather, it is called by a
short-lived Kerberos Child Process during Kerberos authentication. If a
PAC exists in the Kerberos ticket, the Child Process sends the PAC,
along with the user principal, to the PAC Responder. The PAC Responder
decodes the information in the PAC, such as group membership from
trusted domains, and updates the System Cache accordingly.

Having discussed the subdomains, global catalog, and pac responder
concepts in this section, we will now return to our simplifying
assumption for the remainder of the document: that only a single
ad\_domain (without any trust relationships) is being used.

5. SSSD Wrappers
================

When SSSD calls an external library, it needs to maintain its
tevent-based asynchronous semantics. We have already discussed the case
in which the external library only supports blocking function calls
(e.g. krb5). SSSD simply spawns a Child Process, which will make the
blocking calls and will return the response to SSSD when its done (which
may take some time). In this section, we discuss the case in which the
external library does support non-blocking function calls (e.g. dbus,
openldap). Since such external libraries were likely not written with
the tevent main loop in mind, SSSD uses a wrapper around each external
library in order to integrate it with the tevent main loop. This section
examines the SBus wrapper (for the DBus library) and the SDAP wrapper
(for the OpenLDAP library).

5.1. SBus
---------

5.1.1. SBus Concepts
~~~~~~~~~~~~~~~~~~~~

SBus is a wrapper library used to integrate the D-Bus library with the
tevent main loop. SBus uses UNIX Domain Sockets to send messages between
SBus Clients (which initiate new connections) and SBus Servers (which
accept new connections). Note that SBus does not make use of the D-Bus
message bus, but rather uses the D-Bus protocol in a point-to-point
manner (mostly for data marshalling). Once an SBus connection has been
established between an SBus Client and SBus Server, it becomes a
peer-to-peer situation, in which either end can send and receive SBus
messages. An SBus message is made up of a header and a body.
Essentially, the header contains the method-name and its typed
arguments, while the body contains specific values for each argument. In
addition to this section, more information can be found at [SBus].

5.1.1.1. SBus Connections
^^^^^^^^^^^^^^^^^^^^^^^^^

The fundamental data structure used by SBus (for both SBus Clients and
SBus Servers) is the sbus\_connection object, which represents a
peer-to-peer connection over which messages can be sent and received.
Each peer's sbus\_connection is created with one or more (in the case of
the public DBus API) sbus intefaces, which specify the sbus\_methods
that the peer implements (essentially method/function pairs). These
sbus\_method name/function pairs are extremely useful when examining the
code base, since they specify each process's message processing entry
points. When a peer's socket receives an SBus message that targets one
of its sbus\_method names, the peer executes the corresponding
sbus\_method function.

SSSD has several peer-to-peer connections, where each peer can call
sbus\_methods specified in the other peer's sbus\_interface. If we
examine each sender/receiver pair, the sbus\_methods called by the
sender and implemented by the receiver are as follows (ones in bold are
particularly important):

-  Control Traffic

   -  Monitor => Backend or Responder

      -  *ping*: send messages to registered child processes to
         determine if they are alive
      -  *resInit*: reload /etc/resolv.conf to get address of DNS server
      -  *rotateLogs*: close current debug file; open new debug file
      -  *clearMemcache* (NSS Responder only): reinitialize Fast Cache
         (memcache) maps

   -  Monitor => Backend

      -  *goOffline*: mark process as offline; run any offline callbacks
      -  *resetOffline*: attempt to go online; if successful, run any
         online callbacks

   -  Backend or Responder => Monitor

      -  *getVersion*: called by process to retrieve monitor's version
         number
      -  *RegisterService*: called by process to register itself with
         Monitor

   -  Responder => Backend

      -  *RegisterService*: called by Responder to register itself with
         Backend

-  Data Traffic

   -  **Responder** => **Backend**

      -  ***getAccountInfo*: initiate identity lookup (e.g. getpwnam,
         initgroups, etc)**
      -  ***pamHandler*: initiate pam-related functionality (e.g.
         authentication, acct mgmt, etc)**

   -  Backend => NSS Responder

      -  initgrCheck: send user's group memberships (pre-refresh) to NSS
         Responder, so that it can determine if memberships have changed
         (between pre-refresh and post-refresh), in which case it can
         clean up the memcache accordingly. Note that this is not
         related to the Initgroups Cache (id\_table) maintained by the
         PAM Responder.

5.1.1.2. Creating SBus Clients and Servers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In SSSD, SBus servers are run as part of the Monitor and Backend
processes (but not the Responder processes). Each SBus server can be
characterized by the following:

-  server\_address: well-known socket address on which server listens
   for connections
-  *srv\_init\_fn*: connection initialization function
-  srv\_init\_data: connection initialization private data

An SBus Server creates an sbus\_connection object by calling
*sbus\_new\_server* with the three parameters given above. Once created,
an SBus Server begins listening for new connections at its well-known
server\_address. When it receives a new connection request from a
Process, the SBus Server calls *sbus\_server\_init\_new\_connection*,
which does the following:

-  creates a new per-connection sbus\_connection object
-  uses the previously specified *init\_fn* and init\_pvt\_data to call
   *init\_fn(conn, init\_pvt\_data)*
-  registers the per-server interface (an instance of sbus\_vtable) and
   the initialization private data with a call to ``sbus_new_interface``
   at an object path. This vtable and private data would be used by the
   ``sbus_message_handler`` when a message targeted at the registered
   object path arrives.

An SBus Client creates an sbus\_connection object by calling
*sbus\_client\_init* with the following parameters: server\_address,
intf, conn\_pvt\_data. Once created, an SBus Client can request a
connection to the SBus Server listening at server\_address, after which
it can send messages supported by the SBus Server's sbus\_interface.
Once connected to an SBus Server, that SBus Server can send messages
supported by the SBus Client's sbus\_interface (intf). The
conn\_pvt\_data is opaque data stored with the sbus\_connection object,
that can later be retrieved from the SBus Client. Each SBus Client in
SSSD is associated with its SBus Server's server\_address, its SBus
Client intf, and SBus Client conn\_pvt\_data.

.. code:: wiki

    NSS Responder => Monitor
        server_address: /var/lib/sss/pipes/private/sbus-monitor
        methods:        monitor_nss_methods
        conn_pvt_data:  resp_ctx

    PAM Responder => Monitor
        server_address: /var/lib/sss/pipes/private/sbus-monitor
        methods:        monitor_pam_methods
        conn_pvt_data:  resp_ctx

    Backend => Monitor
        server_address: /var/lib/sss/pipes/private/sbus-monitor
        methods:        monitor_be_methods
        conn_pvt_data:  be_ctx

    NSS Responder => Backend
        server_address: /var/lib/sss/pipes/private/sbus-dp_foo.com (domain_name=foo.com)
        methods:        nss_dp_methods
        conn_pvt_data:  resp_ctx

    PAM Responder => Backend
        server_address: /var/lib/sss/pipes/private/sbus-dp_foo.com (domain_name=foo.com)
        methods:        pam_dp_methods
        conn_pvt_data:  resp_ctx

5.1.1.3. Sending and Receiving SBus Messages
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A sender calls *sbus\_conn\_send*\ (msg, **reply\_handler**, pvt) in
order to send a message, and to register a **reply handler**, which will
handle the reply message. When the message arrives at the receiver, it
calls *sbus\_message\_handler*, which extracts the sbus\_interface and
sbus\_connection registered for that object path, and calls the function
corresponding to the method name, with the request message and
sbus\_connection as inputs. The entry-point function does the following:

-  extracts its private data from the sbus\_connection input
-  extracts request arguments from the request message input
-  performs method-specific processing using inputs to generate outputs
-  creates a reply message that matches the request message (i.e. same
   serial number)
-  appends output arguments to reply message
-  sends back reply message on same sbus\_connection on which it
   received the request

*This figure shows the functions used in the sending and receiving of an
SBus message*

5.1.1.4. Describing the SBUS interface
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Starting with upstream version 1.12, when the SSSD implemented its
public DBus interface, the SSSD switched from hardcoding interface
names, methods etc in the source files directly to only describing the
interfaces in XML files using the `​introspection
format <http://dbus.freedesktop.org/doc/dbus-specification.html#introspection-format>`__,
which are then used to autogenerate message handlers, property getters
and similar. While using generated code might sound odd at first, using
a code generator removes a large amount of code duplication, packing and
unpacking from DBus types to C types or vice versa, or unpacking DBus
message properties (if needed).

The code generator and the generated code are currently used for both
the DBus public interface (which is outside the scope of this page) and
the internal SBUS communication. The internal SBUS code, however, uses
the generated code in a 'raw' mode mostly and still does
packing/unpacking of the parameters on its own. The reason is that the
'raw' code in SSSD predates the code generator, is quite stable and
tested and converting it to the easier handlers with unpacked parameters
might cause functional regressions.

One example of the canonical XML code might be found in the `​unit
tests <https://git.fedorahosted.org/cgit/sssd.git/tree/src/tests/sbus_codegen_tests.xml>`__,
along with the `​corresponding autogenerated
code <https://git.fedorahosted.org/cgit/sssd.git/tree/src/tests/sbus_codegen_tests_generated.c>`__.
The XML files for the internal interfaces, such as the `​Data
Provider <https://git.fedorahosted.org/cgit/sssd.git/tree/src/providers/data_provider_iface.xml>`__
can also be inspected. Since all the internal interfaces use the raw
approach, the autogenerated code is `​quite
terse <https://git.fedorahosted.org/cgit/sssd.git/tree/src/providers/data_provider_iface_generated.c>`__
and the `​interface
handlers <https://git.fedorahosted.org/cgit/sssd.git/tree/src/providers/data_provider_be.c>`__
do the packing and unpacking on their own.

5.1.2. Responder-to-Backend API
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section examines those sbus\_methods exported in the Backend's SBus
Interface that are called by the NSS/PAM Responders. For NSS requests, a
Responder sends a *getAccountInfo* message to the Backend, which handles
it by calling be\_get\_account\_info. For PAM requests, a Responder
sends a *pamHandler* message to the Backend, which handles it by calling
be\_pam\_handler. The be\_methods array of sbus\_method objects specify
the name/function pairs supported by the Backend.

Note that when the Backend receives an incoming SBus message, it creates
a be\_req object, and includes in that object a backend response
callback. Once the Backend has completed processing the request (after
contacting the AD Server, etc) and is ready to return a response to the
Responder, the registered backend response callback is called. More on
this below.

5.1.2.1. getAccountInfo
^^^^^^^^^^^^^^^^^^^^^^^

5.1.2.1.1. Request (NSS/PAM Responder->Backend)
'''''''''''''''''''''''''''''''''''''''''''''''

The *sbus\_method* named *getAccountInfo* is sent by the NSS Responder
and PAM Responder to the Backend for identity lookups. Note that while
the NSS Responder is sending the message in response to an SSS Client
request (e.g. getpwnam, getgrgid, etc), the PAM Responder only sends the
message for group membership retrieval (regardless of the SSS Client
request it is handling). As such, the INITGROUPS operation is handled
differently by the Backend, as noted below.

The *getAccountInfo* request message takes the following four arguments:

.. raw:: html

   <div class="code">

::

    int be_type:    the operation to perform         // e.g. USER, GROUP, INITGROUPS, etc
    int attrs:      attributes to be returned        // e.g. CORE, MEM, ALL
    char *filter:   the elements to select           // e.g. "name=aduser", "idnumber=73", etc
    char *dom_name: the domain name                  // e.g. "foo.com", etc

.. raw:: html

   </div>

For example, an SBus request message representing
getpwnam("aduser@foo.com") includes the following input values:

-  be\_type: BE\_REQ\_USER
-  attrs: BE\_ATTR\_CORE
-  filter: "name=aduser"
-  domain: "foo.com"

As specified in be\_methods, the function on the Backend corresponding
to this sbus\_method name is *be\_get\_account\_info*. For all
operations other than INITGROUPS, *be\_get\_account\_info* specifies
acctinfo\_callback as the backend response callback, after which it
calls *ad\_account\_info\_handler* to do the actual processing (for our
AD use case). Once processing is complete, *acctinfo\_callback* is
called, which prepares the response message and sends it back to the
Responder.

For the INITGROUPS operation, *be\_get\_account\_info* specifies
*acctinfo\_initgroups\_callback* as the backend response callback. In
this case, once processing is complete, *acctinfo\_initgroups\_callback*
is called, which sends an *initgrCheck* SBus message to the NSS
Responder. As mentioned earlier, this allows the NSS Responder to
compare the user's pre-refresh and post-refresh group memberships, so
that it can clean up the memcache accordingly. Once the *initgrCheck*
SBus message has been sent, then *acctinfo\_callback* is called, which
prepares the actual initgroups response message, and sends it back to
the Responder.

5.1.2.1.2. Response (Backend=>NSS/PAM Responder)
''''''''''''''''''''''''''''''''''''''''''''''''

The SBus reply message for the *getAccountInfo* sbus\_method contains
the following three arguments:

.. raw:: html

   <div class="code">

::

    int dp_err:     error code                      // e.g..DP_ERR_OK, DP_ERR_TIMEOUT, DP_ERR_OFFLINE
    int dp_ret:     errno                           // e.g. EOK, EINVAL
    char *err_msg:  error message for logging       // e.g. “Success”, “Out of memory”

.. raw:: html

   </div>

For example, a successful SBus reply message would include the following
output values:

.. code:: wiki

    dp_err:       DP_ERR_OK
    dp_ret:     EOK
    err_msg:    NULL

An unsuccessful SBus reply message might include the following output
values:

.. code:: wiki

    dp_err:       DP_ERR_FATAL
    dp_ret:     EINVAL
    err_msg:    "Internal error”

Note that the actual result of the request is written to the sysdb Cache
by the Backend. The SBus response message is used not only to convey
error/success information, but also to indicate to the Responder that it
can retrieve the up-to-date result from the sysdb Cache. Initially, if
an entry didn't exist in the Cache, it was considered a cache miss, and
it resulted in an update cache request to the Backend. Now that the
Backend has updated the cache, if an entry still doesn't exist in the
Cache, it means that the entry really just doesn't exist.

5.1.2.2. pamHandler
^^^^^^^^^^^^^^^^^^^

5.1.2.2.1. Request (PAM Responder -> Backend)
'''''''''''''''''''''''''''''''''''''''''''''

The sbus\_method named *pamHandler* is sent by the PAM Responder to the
Backend for PAM-related functionality, corresponding to PAM-supported
library calls (e.g. pam\_authenticate, pam\_acct\_mgmt, etc). When a
caller (i.e. an SSS Client Application) calls a PAM function (e.g.
pam\_authenticate) with various inputs, the PAM Client includes a
pam\_items object in its client request to the PAM Responder, which
stores the caller-specified inputs, as well as some additional
information. In turn, when the PAM Responder receives the client request
message, it extracts the many arguments and stores them in a pam\_data
object. Finally, the PAM Responder includes the pam\_data object's many
fields as arguments for the *pamHandler* message. These arguments
include:

.. raw:: html

   <div class="code">

::

    int cmd:                // e.g. SSS_PAM_AUTHENTICATE, etc
    char *domain:           // e.g. "foo.com", etc
    char *user:             // e.g. "aduser", etc
    int authtok_type:       // e.g. PASSWORD, CCFILE, etc
    int *authtok_data:      // e.g. "adpass", etc

.. raw:: html

   </div>

For example, an SBus request message representing
pam\_authenticate("aduser@foo.com", "adpass") includes the following
input values:

.. code:: wiki

    cmd:      SSS_PAM_AUTHENTICATE
    domain:     "foo.com"
    user:       "aduser"
    authtok_type:   SSS_AUTHTOK_TYPE_PASSWD
    authtok_data:   "adpass"

As specified in be\_methods, the function on the Backend corresponding
to this sbus\_method name is *be\_pam\_handler*, which specifies
*be\_pam\_handler\_callback* as its backend response callback, after
which it calls *krb5\_pam\_handler*\ (for the SSS\_PAM\_AUTHENTICATE or
SSS\_PAM\_CHAUTHTOK commands) or *ad\_access\_handler* (for the
SSS\_PAM\_ACCT\_MGMT command). Once processing is complete,
*be\_pam\_handler\_callback* is called, which prepares the response
message and sends it back to the Responder.

5.1.2.2.2. Response (PAM Responder -> Backend)
''''''''''''''''''''''''''''''''''''''''''''''

The SBus reply message for the *pamHandler* sbus\_method contains the
pam status, followed by an array of responses, with each response
consisting of a response type and response message. Note that after the
Responder receives the responses, it includes them in its reply to the
SSS Client (after filtering out certain response types).

The pam\_status argument (defined by the PAM library) can take one of
many values, including the following (I have omitted the “PAM\_”
prefixes): SUCCESS, PERM\_DENIED, ACCT\_EXPIRED, AUTHINFO\_UNAVAIL,
NEW\_AUTHTOK\_REQD, CRED\_ERROR, CRED\_UNAVAIL, SYSTEM\_ERR, AUTH\_ERR

Let us examine some responses, each consisting of a {type, message}
tuple. Some responses are intended for consumption by the SSS Client.
These response types are documented in sss\_cli.h. Examples include:

-  {SSS\_PAM\_USER\_INFO, SSS\_PAM\_USER\_INFO\_OFFLINE\_CHPASS}
-  {SSS\_PAM\_SYSTEM\_INFO, “The user account is expired on the AD
   server"}
-  {SSS\_PAM\_ENV\_ITEM, “KRB5CCNAME=/run/user/...”}
-  {SSS\_PAM\_DOMAIN\_NAME, <domain>}
-  {SSS\_OTP, NULL}

Other responses are filtered out by the PAM Responder, as they are not
intended for the SSS Client. Examples include:

-  {SSS\_KRB\_INFO\_TGT\_LIFETIME, <time>}
-  {SSS\_KRB5\_INFO\_UPN, <upn>}

5.2. SDAP
---------

5.2.1. SDAP Concepts
~~~~~~~~~~~~~~~~~~~~

SDAP (“SSSD LDAP”) is a wrapper around the OpenLDAP library. It is used
to integrate the OpenLDAP API with the tevent main loop. It is also used
to provide additional support for failover (among other things).
Specifically, when an OpenLDAP connection is made to a particular LDAP
server's IP address, OpenLDAP maintains only the server's hostname as
part of its connection state. OpenLDAP periodically resolves the host
name using DNS, which could result in the connection being transparently
switched to another server with the same hostname, but different IP
address (i.e. no server affinity).

On the other hand, once an SDAP connection is made to a particular LDAP
server's IP address, SDAP maintains the server's IP address as part of
its connection state, meaning that the connection remains with that
server (until it expires or goes offline). This allows us to have
semantics where we failover only when that particular server fails
(rather than having to deal with intermittent failures). Note that SDAP
also maintains an LDAP URI as part of its connection state, in order to
make certificate comparisons when TLS is used.

All of this is possible because SDAP connects to the LDAP server itself
(rather than relying on OpenLDAP to make the connection) and simply
passing the resulting file descriptor to OpenLDAP using ldap\_init\_fd
(when available). By owning the connection, SDAP has full control over
how it wants to deal with failover, DNS resolution, etc.

SDAP represents a connection to the LDAP server using the
sdap\_id\_conn\_data object. Once a connection is established (typically
on the first operation request), it can be used multiple times to
transfer LDAP operation requests and responses until the connection
expires (or we go offline). For each LDAP operation request (e.g. bind,
search, etc) , two objects are created: one for the operation request
itself (sdap\_op) and one for keeping track of retrying the operation
request (sdap\_id\_op).

5.2.2. Establishing an LDAP Connection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Establishing an LDAP connection (*sdap\_cli\_connect\_send*) is a
multi-step process that involves the DNS server, the LDAP server, and
the KDC. The steps involved are as follows:

-  *be\_resolve\_server\_send*: retrieve addressing information
   (ip/port) for AD's LDAP service
-  *sdap\_connect\_send*: connect to server; register incoming message
   handler (*sdap\_ldap\_result*)
-  *sdap\_cli\_rootdse\_step*: attempt to anonymously retrieve the LDAP
   server's rootDSE
-  *sdap\_cli\_kinit\_step*: obtain a TGT from a KDC (after retrieving
   its addressing information)
-  *sdap\_cli\_auth\_step*: perform an LDAP bind (either sasl or
   simple); if we were unable to retrieve rootDSE info earlier
   (anonymously), we try to retrieve it again now that we're
   authenticated

5.2.3. Performing LDAP Operations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once an authenticated connection has been established, including
registering the *sdap\_ldap\_result* handler for incoming messages, we
can start sending LDAP operations over the connection. The OpenLDAP API
allows most operations to be performed with either synchronous or
asynchronous funcions. In order to perform a synchronous LDAP operation,
the appropriate synchronous API call is made (e.g.
ldap\_search\_ext\_s), and we block on that call until it completes (or
times out).

In order to perform an asynchronous LDAP operation, the appropriate
asynchronous API call is made (e.g. ldap\_search\_ext), which returns a
message id. We then call sdap\_op\_add, which creates an sdap\_op object
representing the operation (msgid,
callback=\ *sdap\_get\_generic\_ext\_done*, and callback arg=req w/
sdap\_get\_generic\_ext\_state), and which adds the sdap\_op object to
the sdap handle's list of sdap\_op objects.

Later, when a response is received on the fd, the tevent main loop calls
the handler we registered when establishing the connection (i.e.
*sdap\_ldap\_result*), which calls *ldap\_result* with that message id
in order to poll the library to check whether results have been
received. If results have not been received, *ldap\_result* returns 0,
in which case we try polling for results again later on. If results have
been received, *ldap\_result* returns an LDAPMessage, which we proceed
to process by calling *sdap\_process\_message*. We extract the msgid
from the message, and iterate through our sdap\_handle's list of
sdap\_op objects until we find an sdap\_op with a matching msgid, at
which point we add the message to the op's list and call the sdap\_op's
callback, passing it the LDAP message and the callback's arg. This
callback switches on the msgtype of the message. If the reply message is
a SEARCH\_ENTRY, then we call the parse\_cb registered earlier (as part
of sdap\_get\_generic\_ext\_send). For sdap\_get\_generic\_send, the
parse\_cb is *sdap\_get\_generic\_parse\_entry*. We then add a timer
event to process the next reply after the timer expires. If the reply
message is a SEARCH\_RESULT, then we simply call *ldap\_parse\_result*.

6. Common Data Structures
=========================

This section describes some important data structures that are used by
each of the SSSD Processes. In order to have a more readable
description, the text below uses the term “Process” with a capital 'P'
to interchangeably mean either the Monitor process, the Responder
processes, or the Backend process. Exceptions to this rule are noted.

When it first starts, a Process calls the following functions:

.. raw:: html

   <div class="code">

::

    server_setup()                  // creates main_context (includes tevent_ctx and confdb_ctx)
    <process-specific>_init()       // creates process-specific context
    server_loop()                   // calls tevent_loop_wait on tevent_ctx (to start the main loop)

.. raw:: html

   </div>

6.1. tevent\_context
--------------------

The purpose of a Process's tevent\_context is to contain the events that
are to be monitored by that Process's main loop. As such, the primary
interaction that a Process has with its tevent\_context is to add/remove
events. During startup, a Process calls the following tevent-related
functions:

.. raw:: html

   <div class="code">

::

    server_setup
            tevent_context_init     // creates singleton tevent_context
    <process-specific> init
            tevent_add_*            // adds some events to tevent_context
    server_loop
            tevent_loop_wait        // starts main loop using tevent_context

.. raw:: html

   </div>

Note that tevent\_loop\_wait initially monitors only the events in its
just-populated tevent\_context input argument. Once a Process's main
loop has started, it adds additional events to its tevent\_context as
needed. Of the four types of events, the SSSD code primarily adds
tevent\_fd and tevent\_timer events, using the *tevent\_add\_fd* and
*tevent\_add\_timer* functions.

6.2. confdb\_ctx
----------------

The purpose of a Process's confdb\_ctx is to allow the Process to
interact with the Config DB (config.ldb). As such, the primary
interaction that a Process has with the Config DB is to get or set
configuration information, using functions such as *confdb\_get\_int*
and *confdb\_set\_bool*.

There is a single system-wide Config DB, which is initialized by the
Monitor before it spawns the other processes. As part of its
initialization, the Monitor calls load\_configuration, which contains
the confdb initialization code (specifically *confdb\_init\_db*). The
load\_configuration function reads the configuration text file
(sssd.conf), parses it, and uses *ldb\_add* to store the parsed values
into the Config DB. As such, any changes made to sssd.conf after the
Monitor has started will require the Monitor to be restarted. The
Monitor parses sssd.conf using libiniconfig, resulting in minimal
validation of configuration values; any additional validation is left to
the SSSD code. However, once dinglibs adds support for schema
validation, SSSD should be able to take advantage of it (since
libiniconfig is based on dinglibs).

Once the Config DB has been initially populated, a Process's
initialization code calls *confdb\_init()*, which internally calls
*ldb\_connect()* to connect to the Config DB, and which returns a new
confdb\_ctx that is needed for subsequent confdb calls. All of the
gettor functions that interact with the confdb take the confdb\_ctx as
one of their input arguments. Generic accessor functions are provided in
confdb.h, while plugin-specific accessor functions are also provided
(e.g. ad\_opts.h).

In summary, the following confdb-related functions are called during
startup:

-  **load\_configuration (only called by Monitor)** *initializes Config
   DB*
-  server\_setup (called by all Processes)

   -  **confdb\_init** *creates singleton confdb\_ctx*

-  <process-specific> init

   -  **confdb\_get\_\*** *retrieves config info from Config DB*

6.3. sysdb\_ctx
---------------

The purpose of a Process's sysdb\_ctx is to allow the Process to
interact with a domain's system cache (i.e. to get/set cached
information for a domain). The exception to this is the Monitor process,
which only initializes a sysdb\_ctx in order to allow the sysdb to be
upgraded at startup, which is typically needed when an upgrade to a new
SSSD version results in changes to the internal db schema). As such,
only a Responder/Backend process maintains a reference to its
sysdb\_ctx.

The sysdb\_ctx field is primarily accessed through the sss\_domain\_info
structure that encapsulates it. As such, a Process first calls
confdb\_get\_domains, and then passes all of the configured
sss\_domain\_info structures to sysdb\_init, which creates a separate
sysdb (i.e. ldb database) for each domain. Since our use case has only a
single domain, there is only a single system-wide sysdb, in which case
the terms sysdb and system cache refer to the same ldb database.

Individual entries in the sysdb cache are referenced using the
sysdb\_attrs structure, which represents an entry that can have multiple
multi-valued attributes, and which is created by sysdb\_new\_attrs. It
is by using the sysdb\_attrs API that a Process can get/set cached
values. Accessor functions are provided in sysdb.h (e.g.
sysdb\_attrs\_get\_string, sysdb\_attrs\_add\_string). Using the gettor
functions is self-explanatory, but care must be taken when using the
settor functions, to ensure that they are written in a transactional
manner (data completely stored or not stored at all). To this end, a
Process wanting to write information to the cache would make calls
similar to the following (with each call taking the sysdb\_ctx as an
input argument):

.. raw:: html

   <div class="code">

::

    sysdb_transaction_start(); // set entries using either the sysdb_attrs API or directly using the ldb API (ldb_modify, etc).
    sysdb_transaction_commit();
    if (error) 
       sysdb_transaction_cancel();

.. raw:: html

   </div>

6.4. main\_context
------------------

As mentioned earlier, when it first starts, a Process performs some
initialization tasks, including

-  server\_setup
-  <process-specific> init function (e.g. nss\_init, pam\_init,
   be\_process\_init)
-  server\_loop

In brief, server\_setup creates a main\_context, the process-specific
init function creates a process-specific context (i.e. nss\_ctx,
pam\_ctx, be\_ctx), and the server\_loop function simply calls
tevent\_loop\_wait in order to start the main loop.

The main\_context essentially contains an appropriately initialized
tevent\_context and confdb\_ctx (described earlier), which each Process
will need in order to make tevent or confdb function calls. Rather than
containing a pointer to the main\_context, each process-specific context
contains direct pointers to the tevent\_context and confdb\_ctx
components of the main\_context (why??). The server\_loop function calls
tevent\_loop\_wait using the main\_context's tevent\_context as input.
Since the process-specific context's tevent\_context and the
main\_context's tevent\_context are pointing to the same object, the
main loop will be able to see events added to the process-specific
tevent\_context.

::


    Monitor                     Responder          Backend

    load_configuration()
    server_setup()
    monitor_process_init()

        add_new_provider() => fork/exec ==============================> server_setup()
                                            be_process_init()
                                        server_loop()

        add_new_service() => fork/exec=====> server_setup()
                                 nss/pam_process_init()
                             sss_process_init()
                             server_loop()

    server_loop()

7. Component Details
====================

This section looks more closely at the SSSD components, including
process-specific data structures and functions, as well as inter-process
communication. The following components are discussed, where each
component uses its process-specific init function to produce its
process-specific context:

+-----------------+------------------------------------+------------------------------+
| *component*     | *process-specific init function*   | *process-specific context*   |
+-----------------+------------------------------------+------------------------------+
| Monitor         | *monitor\_process\_init*           | mt\_ctx                      |
+-----------------+------------------------------------+------------------------------+
| NSS Responder   | *nss\_process\_init*               | nss\_ctx                     |
+-----------------+------------------------------------+------------------------------+
| PAM Responder   | *pam\_process\_init*               | pam\_ctx                     |
+-----------------+------------------------------------+------------------------------+
| Backend         | *be\_process\_init*                | be\_ctx                      |
+-----------------+------------------------------------+------------------------------+

7.1. Monitor
------------

The monitor is the master SSSD process that is executed when
/usr/sbin/sssd is run. The Monitor's context (struct mt\_ctx) is created
during startup by *monitor\_process\_init()* and is used to store
Monitor-relevant information, such as a list of *mt\_svc* objects
representing spawned processes. The role of the Monitor is:

-  to parse the config file and load config info into the confdb for
   SSSD processes to access
-  to monitor networking changes and act on them accordingly
-  to spawn a Backend process for each domain specified in the config
-  to spawn a Responder process for each service specified in the config
   (e.g. NSS, PAM)
-  to receive SBus messages (primarily RegisterService) from Responders
   and Backends
-  to periodically ping all Responders and Backends, and to restart them
   if unable to ping

In addition to this section, more information can be found in [Monitor].

7.1.1. Spawning and Registering Processes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The SBus server running as part of the Monitor is characterized by the
following:

.. code:: wiki

    server_address:       /var/lib/sss/pipes/private/sbus-monitor
    server_intf:        monitor_server_interface
    srv_init_fn:        ''monitor_service_init''
    srv_init_data:      mt_ctx

Soon after this SBus server is created, the Monitor spawns the Backend
processes (one per domain) by calling *add\_new\_provider*, which does
the following:

-  retrieves relevant config info, and uses it to populate mt\_svc
   object, which includes the mt\_ctx, sbus\_connection, as well as ping
   parameters
-  builds the command line needed to start the process
-  forks the process

   -  the child process execs the command line, spawning the process
   -  the parent process:

      -  adds the mt\_svc object to its mt\_ctx->svc\_list
      -  sets up a timer, which periodically pings the process to assess
         if it is reachable

The newly spawned child process does two monitor-related things during
initialization:

-  sends a connection request to the Monitor, specifying child process's
   sbus\_interface
-  identifies itself by sending a RegisterService message to the Monitor

In response to the connection request, the parent process (i.e. the
Monitor) performs generic SBus initialization, but also performs
Monitor-specific SBus initialization by calling
*monitor\_service\_init(conn, mt\_ctx)*, which creates a mon\_init\_conn
object that represents a temporary connection for a Monitor client, and
includes the conn, the mt\_ctx, and a 10-second tevent\_timer (by which
time the child process must identify itself by sending a
*RegisterService* message). This mon\_init\_conn object is then set as
the new sbus\_connections's private data.

In response to the incoming RegisterService message, the corresponding
client\_registration method is called (with the request message and
sbus\_connection as inputs) which does the following:

-  retrieves mon\_init\_conn object from sbus\_connection
-  cancels the 10-second tevent timer (since the RegisterService message
   has been received)
-  retrieves request args, extracted from request message (i.e. sender
   name, sender version)
-  finds sender's mt\_svc in mon\_init\_conn->mt\_ctx->svc\_list
-  sets mt\_ctx->conn to the value of mon\_init\_conn->conn (i.e. conn
   is no longer temporary)
-  marks process as started
-  calls add\_new\_service for each Responder, which spawns each
   Responder in a similar manner:

   -  sends a connection request to the Monitor, specifying Responder's
      sbus\_interface
   -  identifies itself by sending a RegisterService message to the
      Monitor

-  creates a reply message that matches the request message, indicating
   success
-  appends output arguments to reply message (i.e. monitor version)
-  sends back reply message on same sbus\_connection on which it
   received the request

Once initialization is complete, all Backends and Responders should be
registered with the Monitor, allowing the Monitor to send periodic pings
to each process. If the Monitor is unable to contact a child process
three times, the Monitor restarts the child process.

7.2. SSS Client
---------------

An SSS Client sends request messages to a matched Responder, and
receives back a corresponding response message. A request message
includes a command and command-specific input, while a response message
includes a status code and command-specific output. The SSS Clients
(e.g. NSS Client, PAM Client) use common code to send request messages
to a matching Responder, and receive responses from a matching
Responder, using the SSS\_CLI protocol. This common code makes a
blocking call to send the request message and receive the response
message. The reason blocking calls are made is that, unlike the other
SSSD Components, SSS Clients do not use the tevent main loop, since we
have no control over the SSSD Client Application in which the SSS Client
is running.

7.2.1. SSS\_CLI
~~~~~~~~~~~~~~~

Before moving on, let's examine the SSS\_CLI protocol. In this
client-server protocol, the Responder plays the server role and the SSS
Client plays the client role. On the client side, the SSS\_CLI protocol
code is common among all the various types of SSS Clients (e.g. NSS
Client, PAM Client); this client-side code can be found at
sss\_client/common.c. On the server side, the SSS\_CLI protocol code is
common among all the various types of Responders (e.g. NSS Responder,
PAM Responder); this server-side code can be found at
responder\_common.c

SSS\_CLI is a request/response protocol that communicates over raw Unix
Domain Sockets, using its own TLV-encoding. Note that the SSS Client
only supports synchronous I/O, so it may block (e.g. while waiting for a
response). On the other hand, the Responder supports asynchronous I/O
using its tevent main loop, so it will not block (e.g. while waiting to
read from a client).

On the server side, the commands supported by the Responder will vary
depending on the type of Responder. The commands supported by the NSS
Responder are defined in nsssrv\_cmd.c, while the commands supported by
the PAM Responder are defined in pamsrv\_cmd.c.

On the client side, the commands available to all SSS Clients are
defined by an sss\_cli\_command enumeration in sss\_cli.h. The SSS
Client's request message essentially consists of this command, along
with various command-relevant data (e.g. command=SSS\_PAM\_AUTHENTICATE,
data=username/password). The response message essentially consists of
the same command, along with the reply data, and an errno value. The
encoding formats of the request and response messages are defined in
common.c. The SSS Client calls sss\_cli\_send\_req in order to send the
request, and sss\_cli\_recv\_rep in order to receive the reply.

Note that the SSS Client and Responder reference the same header file
(sss\_cli.h) for command names. Indeed, it is the shared command name
(e.g. SSS\_PAM\_AUTHENTICATE) that ties the SSS Client and Responder
together.

7.2.2. NSS Client
~~~~~~~~~~~~~~~~~

As mentioned earlier, the API supported by the NSS Client is defined in
sss\_nss.exports. It includes settors/gettor for several name databases
(e.g. passwd, group, etc). While these functions take different input
arguments, they all return an nss\_status enumeration (e.g. SUCCESS,
UNAVAIL, NOTFOUND, TRYAGAIN, etc).

When a caller (i.e. SSS Client Application) calls one of these
functions, the NSS Client determines if the request is related to the
passwd or group database. If so, the NSS Client consults the memcache
(i.e. Fast Cache) to see if the request can be fulfilled immediately. If
not, or if the cache entry is not valid, the NSS client extracts the
caller's arguments, creates a request message, and uses common client
functions to interact with an NSS Responder. After it receives a
response, it extracts the status and results (e.g. struct passwd), and
returns them to the caller.

7.2.3. PAM Client
~~~~~~~~~~~~~~~~~

As mentioned earlier, the API supported by the PAM Client is defined in
pam\_sss.c. It includes a set of functions, each of which takes a
pam\_handle object as input, and returns an integer representing the
pam\_status. These functions include:

.. code:: wiki

    pam_sm_open_session:   initiate session management
    pam_sm_authenticate:     verify identity of user (typically requires password)
    pam_sm_setcred:      set user's credentials
    pam_sm_acct_mgmt:    determine if user's account is valid (e.g. password/account expiration)
    pam_sm_chauthtok:    change the user's authentication token (i.e. password)
    pam_sm_close_session: terminate session management

When a caller (i.e. an SSS Client Application) calls ones of these
functions, the PAM Client extracts the caller's arguments (e.g.
pam\_user) from the pam handle, prompts the caller for a password (if
needed), and creates a request message using common client functions to
interact with a PAM Responder. After it receives a response, it extracts
the pam\_status from the response. At this point, if the pam\_status is
PAM\_SUCCESS, then PAM Client simply returns PAM\_SUCCESS to the caller,
which can expect that the operation was successful. If not successful,
the PAM Client's behavior will depend on the particular pam\_status
(e.g. display error message, etc).

One complication that arises is when a user is successfully
authenticated (after contacting the AD Server), but the user's password
has expired. Since the authentication succeeds, the PAM Client's
authentication code would normally ignore the fact that the password has
expired, knowing that the account management code would discover this
for itself (but only after contacting the AD Server). However, since we
already have this information at the time of authentication, we optimize
the situation by having the authentication code set a flag in the pam
handle (for consumption by the account management code) indicating that
the user's password has expired (and there is no need to contact the AD
Server again to establish this fact).

7.3. Responder
--------------

In this section, we describe the common functionality shared by both NSS
and PAM Responders. Subsequent sections will discuss Responder-specific
functionality.

The role of a Responder is:

-  to receive request messages from a matching SSS Client
-  to fulfill the requests in one of two ways, by either:

   -  directly retrieving a valid cached result from the sysdb Cache, or
   -  asking the Backend to update the sysdb Cache (e.g. after
      contacting the remote AD server), and then retrieving an
      up-to-date result from the sysdb Cache

-  to send back response messages to the matching SSS Client

7.3.1. resp\_ctx
~~~~~~~~~~~~~~~~

The (Generic) Responder's context (resp\_ctx) is created at startup by
sss\_process\_init(). The resp\_ctx data structure represents a common
set of Responder information that is referenced by a number of other
responder-related data structures. At startup, an NSS Responder or PAM
Responder calls nss\_process\_init() or pam\_process\_init(), which both
internally call sss\_process\_init() with Responder-specific arguments.
Note that some fields of the resp\_ctx apply only to the Responder's
client-facing interface, some fields apply only to the Responder's
backend-facing interface, and some fields apply to both. When
sss\_process\_init() is called, the actions that take place include:

-  retrieving config information from the confdb (including all domain
   stanzas)
-  registering the Responder with the Monitor, by sending it a
   RegisterService SBus message
-  registering the Responder with the Backend, by sending it a
   RegisterService SBus message
-  initializing connections to each per-domain sysdb cache (only one for
   our use case)
-  creating a socket and listening for client connections
-  creating a dp request hash table (an optimization technique discussed
   later)

7.3.2. Client-Facing Interactions (Generic)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As mentioned earlier, an SSS Client communicates with its matching
Responder using our SSS\_CLI protocol. In order to set up a listening
server socket, the Responder retrieves an fd by calling
set\_unix\_socket, (which internally makes the standard socket, bind,
listen calls), and which then registers the fd with the main loop (along
with its accept\_fd\_handler, and READ flag). Once the Responder
receives a connection from an SSS Client, the main loop dutifully calls
accept\_fd\_handler, which, in turn, calls the standard accept call,
which returns a new fd for message traffic, and registers the new fd
with the main loop (along with its client\_fd\_handler and READ flag).
This new fd (and client\_fd\_handler) will be used for the duration of
the connection, while the original fd remains listening for new
connections. When the SSS Client sends a request message to the
Responder, the main loop notices that the Responder's client socket is
ready for READ, and calls client\_fd\_handler, which results in
client\_recv being called. After processing the command (i.e. consulting
cache, forwarding to backend, etc), the Responder registers the fd with
the main loop (along with its client\_fd\_handler, but this time, with a
WRITE flag). When the socket is available for writing, the main loop
calls client\_fd\_handler, which, this time (as a result of the WRITE
flag), calls client\_send to send a response to the SSS Client.

As opposed to the resp\_ctx object (which represents the entire
Responder process), the cli\_ctx object (client\_context) represents
per-client information. For example, the single file descriptor which
listens for connections from SSS Clients is stored in the resp\_ctx,
while the per-client information (such as the file descriptor used to
exchange data with a client, a client's request/response messages, etc)
is stored in cli\_ctx.

7.3.3.Common Optimization Techniques
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Much of a Responder's functionality has to do with implementing
performance-enhancing optimizations. In addition to the sysdb system
cache, there are several additional optimizations used in the Responder
code. In this section, we examine the optimizations that are common to
both the NSS and PAM Responder. Responder-specific optimizations will be
discussed in their corresponding sections. After receiving an SSS Client
request, both Responders only resort to making SBus method calls to the
Backend if none of the optimization techniques they support can fulfill
the request.

7.3.3.1. Data Provider Request Table
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A Data Provider request table (dp\_request\_table) hashtable is
maintained by a Responder to prevent it from sending identical requests
to the Backend. For example, when a user logs in to a local machine,
several different programs may call *getpwnam(“aduser”)* in order to
retrieve the user's uid and gid. Assuming an empty sysdb cache, the
first such request received by a Responder will be sent over SBus to the
Backend and the request will be stored in the Responder's
dp\_request\_table. If a second **identical** request is received by the
Responder, the Responder will notice that an existing request for the
same information is already in progress, and it will register the second
request (and any subsequent identical requests) to be called back when
the results are ready (so that they receive the same reply information).
Note that a dp\_request\_table is an in-memory data structure, resulting
in the NSS Responder and PAM Responder processes maintaining their own
separate dp\_request\_tables.

7.4. NSS Responder
------------------

This section examines the commands and optimization techniques supported
by the NSS Responder, as well as its overall code flow.

7.4.1. nss\_ctx
~~~~~~~~~~~~~~~

The NSS Responder's context (nss\_ctx) is created at startup by
nss\_process\_init(), which takes several actions, including:

-  calling sss\_process\_init() with Responder-specific arguments,
   including supported commands and supported SBus methods
-  initializing idmap\_ctx
-  initializing Responder-specific optimizations (see NSS Optimizations
   section)
-  retrieving Responder-specific config information from the confdb

7.4.2. Client-Facing Interactions (NSS)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The commands supported by the NSS Responder are defined in
nsssrv\_cmd.c. These commands (and their inputs) are extracted from the
packet sent to the Responder by the SSS Client. After processing the
command, the NSS Responder returns a packet to the SSS Client containing
command output and/or an error message. As such, each command has its
own name, function, input, and output (very similar to a function
prototype). For example, if the SSS Client Application is making a call
with the function prototype of: struct passwd \*getpwnam(foo\_name),
then the SSS Client sends a packet to the Responder containing the input
(foo\_name), along with an integer representing the command name
(getpwnam); and the SSS Client expects to receive a packet from the
Responder containing the same command integer, the output (struct
passwd), as well as a status code.

7.4.3. Backend-Facing Interactions (NSS)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The NSS Responder communicates with the Backend using a single SBus
method named *getAccountInfo*. For *getAccountInfo*, the outgoing SBus
request message is constructed by sss\_dp\_get\_account\_msg and “sent”
by sbus\_conn\_send. The incoming SBus reply message is “received” by
sss\_dp\_get\_reply.

7.4.4. Code Flow (NSS)
~~~~~~~~~~~~~~~~~~~~~~

This section examines the NSS Responder's code flow. As with most of the
code, an NSS Responder's basic code-flow has a “send” phase and a “recv”
phase. In the “send” phase, the NSS Responder reads a packet from the
client socket, processes it, and, assuming no optimization, writes an
SBus message to the backend socket (or “be socket”). In the “recv”
phase, the NSS Responder reads the SBus message reply from the backend
socket, processes the reply (which typically includes getting the actual
result from the updated Cache), and writes a reply packet to the client
socket. Of course, the contents of the incoming and outgoing client
packets, as well as the contents of the outgoing and incoming SBus
messages are command-specific. Note that the same responder-specific
search function (which has been underlined below) is called twice, once
for the “send” part (when check\_provider = TRUE), and once for the
“recv” part (when check\_provider = FALSE).

::



    "send" phase (NSS: getAccountInfo)

      main loop notices client socket is READABLE; calls client_fd_handler 

     handler receives packet on client socket           // client_recv: uses read syscall 
     extracts command from packet                       // sss_packet_get_cmd 
     executes function that matches command             // sss_cmd_execute 
     extracts command-specific input from packet            // e.g. username 
      calls command-specific search function (“send” part)  
     tries to fulfill request using NSS Responder optimizations 
     creates SBus message for Backend               // sss_dp_get_account_msg 
     enqueues request (adds tevent_fd[WRITE] to ev)         // sss_dp_internal_get_send 
     returns control to main loop 

     main loop notices be socket is WRITEABLE; calls sbus_watch_handler 
     handler writes SBus message on backend socket              // client_send: uses write syscall 

::


    "recv" phase (NSS: getAccountInfo)

      main loop notices be socket is readable; calls  sss_dp_internal_get_done   

     handler extracts arguments from reply message          //  sss_dp_get_reply  
     performs error processing (if needed) 
      calls command-specific search function (“recv” part)  
     retrieves updated information from sysdb cache         //  sysdb_getpwnam  
     sets responder-specific optimizations (for next time) 
     modifies existing client socket's flags, so that it is WRITEABLE 

      main loop notices client socket is writeable; calls  client_fd_handler   

      handler writes reply packet on client socket          //  client_send  


7.4.5. Optimization Techniques (NSS)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

7.4.5.1. Negative Cache
^^^^^^^^^^^^^^^^^^^^^^^

A negative cache is maintained by an NSS Responder to store information
about operations that have not been successful. For example, when
performing an identity lookup against a remote AD Server, an NSS
Responder may determine that no such identity exists. At that point, an
NSS Responder would put that information into its negative cache for
some period of time (configurable with the entry\_negative\_timeout
field). If a subsequent request came in within that time period for the
same identity lookup, the NSS Responder would immediately return a
result to the client indicating that no such identity exists (without
going to the Backend). Since a negative cache is intended for identity
lookups, it would seem that it should be also be used by the PAM
Responder when it is looking up identities (i.e. when it is calling
initgroups). WhilE this is not currently the case, it is expected that
the PAM Responder will start using the negative cache in the near
future. Note that a negative cache is an in-memory data structure.

7.4.5.2. Fast Cache (aka memcache)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A Fast Cache is a set of memory-mapped cache files, from which an SSS
Client can retrieve identity (NSS) information without having to contact
the NSS Responder. This was described earlier in the document.

7.5. PAM Responder
------------------

This section examines the commands and optimization techniques supported
by the PAM Responder, as well as its overall code flow. Regardless of
the PAM request sent by the SSS Client (e.g. pam\_authenticate), the PAM
responder always starts by determining the user's group memberships. It
does this by internally calling initgroups on each domain stanza, until
it finds a match. Once a match is found, the PAM Responder knows which
domain to use, which identity to use, and the groups to which the
identity belongs. In our use case, there is only a single domain, so if
calling initgroups against our domain fails, then the whole client
request fails. Note that the presence of subdomains makes this more
complicated, but that has been discussed earlier in the document.

7.5.1. pam\_ctx
~~~~~~~~~~~~~~~

The PAM Responder's context (pam\_ctx) is created at startup by
pam\_process\_init(), which takes several actions, including:

-  calling sss\_process\_init with Responder-specific arguments,
   including supported commands
-  initializing Responder-specific optimizations (see Optimizations
   section)
-  retrieving Responder-specific config information from the confdb

7.5.2. Client-Facing Interactions (PAM)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The commands supported by the PAM Responder are defined in
pamsrv\_cmd.c. These commands (and their inputs) are extracted from the
packet sent to the Responder by the SSS Client. After processing the
command, the PAM Responder returns a packet to the SSS Client containing
command output and/or an error message. As such, each command has its
own name, function, input, and output (very similar to a function
prototype). For example, if the SSS Client Application is making a call
with the function prototype of: int pam\_authenticate(pamh, flags), then
the SSS Client sends a packet to the Responder containing the command
name (pam\_authenticate) and input (username); and the SSS Client
expects to receive a packet from the Responder containing the command
name (pam\_authenticate), the output (e.g. user\_info, text\_message,
etc), as well as a status code.

7.5.3. Backend-Facing Interactions (PAM)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The PAM Responder communicates with the Backend using two SBus methods:
*getAccountInfo* (for initgroups) and *pamHandler* (for pam-related
functionality). The *getAccountInfo* request message is identical to
that discussed in the NSS Responder section, except that the operation
to perform (be\_type) is always INITGROUPS. As such, we will only
examine the *pamHandler* SBus message in this section.

For *pamHandler*, the outgoing SBus request message is constructed by
pam\_dp\_send\_req and “sent” by sbus\_conn\_send. The incoming SBus
reply message is “received” by sss\_dp\_get\_reply.

7.5.4. Code Flow (PAM)
~~~~~~~~~~~~~~~~~~~~~~

This section examines the PAM Responder's code flow. The code flow for
*getAccountInfo* is very similar to that discussed in the NSS Responder
section. In this section, we will focus on examining *pamHandler*'s code
flow (which begins with the end of *getAccountInfo*'s flow). However,
for the sake of clarity, we show the entire code flow, including both
*getAccountInfo* and *pamHandler*.

The differences between the NSS:\ *getAccountInfo* and
PAM:\ *getAccountInfo* are as follows:

-  PAM code uses PAM Responder-specific optimizations (not NSS
   Responder-specific ones)
-  PAM code uses a different “search” function
-  PAM code doesn't return a reply packet to the SSS Client after
   getting the initgroups result; rather, it makes a second SBus method
   call (*pamHandler*)

** "send" phase (PAM: *getAccountInfo*) **

::

      main loop notices client socket is READABLE; calls client_fd_handler 

#. ::

       handler receives packet on client socket  // client_recv: uses read syscall

#. ::

       extracts command from packet          // sss_packet_get_cmd 

#. ::

       executes function that matches command        // sss_cmd_execute 

#. ::

       extracts command-specific input from packet   // e.g. username

#. ::

       calls pam_check_user_search (“send” part)

#. ::

       tries to fulfill request using responder-specific optimizations 

#. ::

       creates SBus message for Backend      // sss_dp_get_account_msg 

#. ::

       enqueues request (adds tevent_fd[WRITE] to ev)    // sss_dp_internal_get_send 

#. ::

       returns control to main loop 

::

      main loop notices be socket is WRITEABLE; calls sbus_watch_handler  

10. ::

        handler writes SBus message on backend socket // client_send: uses write syscall 

 **“recv” phase (PAM: *getAccountInfo* )**

::

      main loop notices be socket is readable; calls sss_dp_internal_get_done  

#. ::

        handler extracts arguments from reply message    //  sss_dp_get_reply  

#. ::

        performs error processing (if needed) 

#. ::

        calls  pam_check_user_search  (recv part) 

#. ::

        retrieves updated information from sysdb cache   //  sysdb_getpwnam  

#. ::

        ets responder-specific optimizations (for next time) 

#. ::

        calls  pam_dom_forwarder  

**"send" phase (*pamHandler*)**

**pam\_check\_user\_search (recv part) returns; code calls
pam\_dom\_forwarder**

#. ::

        creates SBus message for Backend             // pam_dp_send_req 

#. ::

         enqueues request (adds tevent_fd[WRITE] to ev       // pam_dp_send_req 

#. ::

        returns control to main loop 

::

      main loop notices be socket is WRITEABLE; calls sbus_watch_handler  

4. ::

        handler writes SBus message on backend socket            // client_send: uses write syscall 

 **"recv" phase (*pamHandler*)**

::

      main loop notices be socket is readable; calls pam_dp_process_reply 

5. ::

         handler extracts arguments from reply message       // dp_unpack_pam_response 

6. ::

         construct reply massage                     // pam_reply 

7. ::

         performs error processing (if needed) 

8. ::

         sets responder-specific optimizations (for next time) 

9. ::

         modifies existing client socket's flags, so that it is WRITEABLE 

::

       NSS: main loop notices client socket is writeable; calls client_fd_handler  

10. ::

          handler writes reply packet on client socket        // client_send 

7.5.5. Optimization Techniques (PAM)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

7.5.5.1. Initgroups Cache
^^^^^^^^^^^^^^^^^^^^^^^^^

The Initgroups Cache (id\_table) is maintained by the PAM Responder in
order to store initgroups information for some (usually very short)
period of time (configurable with the pam\_id\_timeout field) . While
the PAM Responder does not initially consult the sysdb cache before
going to the Backend, the PAM Responder does initially consult the
intigroups cache. If it finds a valid entry in the initgroups cache, the
PAM Responder does not send an internal initgroups request to the
Backend. The reason for this cache is that a full PAM conversation
typically includes multiple PAM requests sent by an SSS Client in quick
succession (one for authentication, another for account management,
etc). Having the Responder send a separate initgroups request for each
PAM request would be inefficient and unnecessary. Note that the
initgroups cache is an in-memory data structure used by the PAM
Responder. This mechanism is not used by the NSS Responder.

7.6. Optimizations Code Flow
----------------------------

Having discussed both NSS and PAM Optimizations, this section walks
through a couple of flowcharts showing how these optimizations come into
play in the code flow. These flow charts only cover the optimizations
performed during the “send” and “recv” phase of identity lookups (i.e.
NSS Responder and initgroups part of PAM Responder), not authentication
or other pam-related functionality. We first look at optimizations
performed during the “send” phase and then at optimizations performed
(or set for next time) during the “receive” phase.

*Optimizations performed during the "send" phase*

While the flowchart is fairly self-explanatory, there are a few things
to note:

-  flowchart assumes that the function matching a client command has
   been executed, and we are now seeing if we can avoid going to the
   Backend using these optimization techniques
-  if there is a valid entry in the initgroups cache, that is a good
   thing (list of group memberships)
-  if there is a valid entry in the negative cache, that is a bad thing
   (“user didn't exist last time”)
-  if there isn't a valid entry in the initgroups cache, it does not
   consult the sysdb Cache
-  the dp\_request\_table optimization is only used if there are dp
   requests to be made (i.e. our optimizations have failed and message
   needs to be sent to the Backend).
-  all dp requests (even the first one) are registered as callbacks

*Optimizations performed during the "recv" phase*

While the flowchart is fairly self-explanatory, there are a few things
to note:

-  each of the registered callbacks receives their own copy of the
   return args
-  if the PAM Responder finds a valid entry in sysdb cache, it adds
   entry to initgroups\_cache
-  NSS Responder again checks if entry should be dismissed because it
   exists in the negative cache
-  if NSS Responder does not find a valid entry in sysdb cache, it adds
   an entry to the negative cache, and deletes an entry from the
   memcache (fast cache).
-  the memcache is not being updated anywhere here (it only gets updated
   when the Backend sends an initgrCheck SBus message to the NSS
   Responder).

7.7. Backend
------------

In this section, we describe the functionality of a Backend, which
represent a domain stanza (e.g. [domain/foo.com]. Recall that a domain
stanza specifies the individual Provider Plugins to be used for each
provider type, as well as information needed to access the remote server
(e.g. ad\_domain=foo.com). As such, for each domain stanza in the
configuration, the Monitor spawns a separate Backend process, and each
Backend process dynamically loads its configured provider plugins. The
role of a provider plugin is to provide plugin-specific implementations
of generic functions (bet\_ops) used to handle request messages, to
perform check\_online operations, and to perform finalize operations.
Additionally, a provider plugin retrieves plugin-specific configuration
(pvt\_bet\_data), which it passes to each of the above functions.

The role of a Backend (aka “Data Provider”) is:

-  to receive SBus request messages from Backend clients (e.g.
   Responders)
-  to fulfill the requests, by calling the appropriate function
   registered by a Provider Plugin
-  to send back SBus response messages to Backend clients
-  to update the sysdb Cache with fresh results from the remote server

7.7.1. Backend Concepts
~~~~~~~~~~~~~~~~~~~~~~~

7.7.1.1. Services and Servers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

SSSD distinguishes between services and servers, in that a single server
(i.e. IP address) can host multiple services (i.e. ports). In the code,
a service (e.g. LDAP) is represented using an fo\_service object, while
each server that supports that service is represented by fo\_server
objects. A list of servers associated with a service are specified in
the configuration. For example, in our use case, an AD Provider Plugin
is capable of consuming the LDAP, GC, and KRB services on one or more AD
Servers (as specified by the ad\_users and ad\_backup\_users
configuration fields). A Backend implements service failover by
automatically switching to a different server if a server is
unreachable.

If we are able to successfully resolve a server and establish an
authenticated connection, SSSD enters online mode, and that connection
can be re-used to transfer requests and responses, until the connection
expires (or we go offline).

If we are unable to resolve a server on the service's list, that server
is marked offline for all services, and we try to resolve the next
server on the service's list. If we are unable to resolve any of the
servers on the service's list, then SSSD enters offline mode. If we are
able to resolve a server on the service's list, we then attempt to
connect to the service (e.g. LDAP) on that server. If successful, we
continue processing. If unsuccessful, that server is marked offline, but
only for that service. Since only that one service (e.g. LDAP) is marked
offline, the other services (e.g. KRB) on that server are still
considered online. The failover mechanism then automatically tries to
connect to the same service on the next server on the service's list of
servers. If we are unable to connect to any of the servers on the
service's list of servers, then SSSD enters offline mode.

Put another way, here is the algorithm for resolving and connecting to a
service:

#. retrieve service's list of servers
#. resolve next server on list
#. if successful, goto step 5; else, mark server offline for all
   services
#. if more servers on list, goto step 2; else, SSSD enters offline mode;
   DONE
#. connect to service on resolved server
#. if successful, DONE; else, mark server offline for that service
#. if more servers on list, goto step 2; else, SSSD enters offline mode;
   DONE

7.7.1.2. Name Resolution
^^^^^^^^^^^^^^^^^^^^^^^^

Name resolution of a server (i.e. obtaining its IP address) is
accomplished in different ways, depending on how the server is specified
in the configuration:

-  if server specified by IP address, we're done (no resolution is
   required)
-  if server specified by hostname, we resolve the server using DNS
   address records (A/AAAA)
-  if server specified with the “\_srv\_” string, we resolve the service
   using DNS SRV records

A Backend's Provider Plugin uses the external c-ares library to
communicate with a DNS Server, in order to resolve a service's server
names. The address of the DNS server is retrieved from /etc/resolv.conf.

In order to resolve a server on a service's list, a Backend calls
be\_resolve\_server\_send and includes the service's name as input. This
function retrieves the list of servers (primary and secondary)
associated with the service name input. For servers that support
resolution using SRV records, the service name is resolved by calling
resolv\_srv\_send; otherwise, the server name is resolved by calling
fo\_resolve\_service\_server. In either case, if the resolution is
successful, an fo\_server object is returned, which includes the desired
addressing information in server\_common->rhostent. If unsuccessful, the
recv function indicates that there was an error, in which case upstream
callers typically mark the server as being offline (be\_mark\_offline).

7.7.1.3. Configuration Lines
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

As we saw in an earlier example, a domain stanza (represented by a
Backend) includes several provider lines, such as “id\_provider = ad”.
Internally, the information corresponding to a single provider line is
stored in the be\_ctx as a bet\_info array element, which includes the
following information:

.. code:: wiki

    bet_type       // the provider type (e.g. BET_ID, BET_AUTH, etc)
    bet_ops      // plugin-specific functions used to handle requests, check_online, and finalize
    pvt_bet_data     // plugin-specific data passed to plugin-specific functions (see above)
    mod_name     // the provider plugin's name (e.g. AD, IPA)
    req_queue    // a bet_queue item, which includes a be_req and be_req_fn

The bet\_ops field (and pvt\_bet\_data arg field) are particularly
important, as they specify the actual plug-in specific functions (and
args) that are called by the Backend to invoke plug-in specific
functionality. The bet\_ops structure for each provider line contains
three plug-in specific function pointers:

-  check\_online: determines whether SSSD is in “online mode” (i.e.
   whether remote server is reachable on the network); this function
   pointer is only used by bet\_info[BET\_ID]. This function is called
   by check\_if\_online, which uses the results of check\_online to
   determine whether the Backend has transitioned to “online mode”, in
   which case the Backend runs any registered online callbacks. The
   check\_if\_online function itself is called by
   data\_provider\_res\_init and data\_provider\_reset\_offline (i.e.
   the sbus\_method functions that handle resInit and *resetOffline*
   SBus messages, respectively).
-  handler: provides the guts of the provider type's functionality; for
   example, the handler for bet\_info[BET\_ID] would implement identity
   lookups (e.g. contact the remote server, retrieve data, etc), while
   the handler for bet\_info[BET\_AUTH] would implement authentication
   processing.
-  finalize: used to terminate the be\_req and clean up any internal
   data; this is optional

The provider line that specifies “id\_provider = ad” indicates two
things: “id\_provider” indicates that we are dealing with a bet\_type of
BET\_ID, and “ad” indicates that we should dynamically load
“libsss\_ad.so”, and we should use the bet\_ops and pvt\_bet\_data
specified by the AD provider plugin. In other words, “id\_provider = ad”
results in the creation of the following data structure:

.. code:: wiki

    bet_info[BET_ID] = 
             bet_type   BET_ID
             bet_ops    ad_id_ops
             pvt_bet_data   ad_opts.id_ctx
             mod_name   "ad"    

For example, our use case uses four provider lines (id\_provider,
auth\_provider, access\_provider, and chpass\_provider). These are
stored in the be\_ctx as an array of bet\_info data structures:

-  bet\_info[BET\_ID]
-  bet\_info[BET\_AUTH]
-  bet\_info[BET\_ACCESS]
-  bet\_info[BET\_CHPASS]

In theory, each provider line can reference a different provider plugin,
resulting in multiple libraries being dynamically loaded. For example,
“id\_provider = ldap”, “auth\_provider=krb5” would result in both
libsss\_ldap.so and libsss\_krb5.so being dynamically loaded, with
bet\_info[BET\_ID] populated with LDAP-specific operations, and
bet\_info[BET\_AUTH] populated with KRB5-specific operations. Having
said that, it is now more common to use layered provider plugins (e.g.
AD, IPA) which greatly simplify configuration for an AD or IPA
environment. Indeed, our use case is configured by specifying
“id\_provider = ad” (i.e. identity lookups are handled by the AD
provider plugin) and “auth\_provider = ad” (i.e. authentication
processing is handled by the AD provider plugin). In this case, only a
single library (libsss\_ad.so) would be dynamically loaded, but it would
internally make calls to the same shared code used by the LDAP and KRB5
provider plugins.

7.7.2. be\_ctx
~~~~~~~~~~~~~~

A Backend Process has a single Backend context (be\_ctx), which it
shares with the various entities internal to the Backend that need it.
The be\_ctx is created at startup by be\_process\_init, at which time
several actions take place, including:

-  retrieving config information from the confdb (mostly related to
   Backend's domain stanza)
-  setting up the failover service
-  initializing failover *allows backend to auto-switch to different
   server if current server fails*
-  initializing connection to sysdb cache for Backend's domain stanza
-  registering the Backend with the Monitor, by sending it a
   RegisterService SBus message
-  exporting sbus methods supported by the Backend (to be called by
   Responders or Monitor)
-  loading and initializing provider plugins (aka Backend Modules), as
   specified in configuration

   -  this includes initializing the array of bet\_info structures with
      plugin-specific values

7.7.3. Responder-Facing Interactions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

7.7.3.1. Registering Responders
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Responder interacts with the Backend using SBus. For our use case,
there are three Backend clients (NSS Responder, PAM Responder, Monitor).
The SBus server running as part of the Backend is characterized by the
following:

.. code:: wiki

    server_address:       /var/lib/sss/pipes/private/sbus-dp_foo.com (domain_name=foo.com)
    server_intf:        be_interface
    srv_init_fn:        be_client_init
    srv_init_data:      be_ctx

When a Responder process is spawned by the monitor, it does two
Backend-related things during initialization:

-  sends a connection request to the Backend, specifying Responder's
   sbus\_interface
-  registers itself with the Backend by sending a RegisterService
   message to the Backend

In response to the connection request, the Backend performs generic SBus
initialization, but also performs Backend-specific SBus initialization
by calling be\_client\_init(conn, be\_ctx), which creates a be\_client
object that represents a Backend client connection (which starts off
uninitialized). This be\_client object includes the conn, the be\_ctx,
and a 5-second tevent\_timer (by which time the Responder must identify
itself by sending a RegisterService message). This be\_client object is
then set as the sbus\_connections's private data.

In response to the incoming RegisterService message, the corresponding
client\_registration method is called (with the request message and
sbus\_connection as inputs) which does the following:

-  retrieves be\_client object from sbus\_connection
-  cancels the 5-second tevent timer (because the RegisterService
   message has been received)
-  retrieves request args, extracted from request message (i.e. sender
   name, sender version)
-  marks Backend client as initialized
-  creates a reply message that matches the request message, indicating
   success
-  appends output arguments to reply message (i.e. backend version)
-  sends back reply message on same sbus\_connection on which it
   received the request

Once initialization is complete, all Responders should be registered
with the Backend.

Unlike the Responders, the Monitor process (which is also a Backend
client) does not need to register itself with the Backend. This is
because the Backend has already registered itself with the Monitor, and
therefore the Backend already has access to the Monitor's
sbus\_interface.

7.7.3.2. Receiving SBus Messages
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A Backend is capable of receiving the SBus methods (name/function pairs)
that were exported during its startup (be\_process\_init). The functions
associated with each sbus method name are generic (i.e. not
provider-plugin-specific). However, each function corresponds to a
particular provider plugin type. For example, *getAccountInfo* is used
for identity lookups and is therefore associated with the identity
provider. When the Backend receives an SBus message that targets one of
its sbus\_method names, the Backend executes the corresponding generic
function. In turn, this generic function executes the handler function
registered for the particular provider plugin type associated with this
SBus method. For example, since *getAccountInfo* is associated with the
identity provider (i.e. BET\_ID), we would extract its handler function
from bet\_info[BET\_ID]->bet\_ops->handler (which was registered by
be\_process\_init). We would also extract the argument with which to
call the handler from bet\_info[BET\_ID]->pvt\_bet\_data.

Since our use case uses only the NSS and PAM Responders, we will only be
looking at the SBus methods sent by those Responders: *getAccountInfo*
(for identity lookups) and *pamHandler* (for pam-related functionality).

-  sbus\_method name: “\ *getAccountInfo*\ ”

   -  generic function: be\_get\_account\_info
   -  provider\_plugin type: BET\_ID
   -  plugin/type-specific handler function:
      bet\_info[BET\_ID]->bet\_ops->handler
   -  plugin/type-specific handler argument:
      bet\_info[BET\_ID]->pvt\_bet\_data

-  sbus\_method\_name: “\ *pamHandler*\ ”

   -  generic function: be\_pam\_handler
   -  provider\_plugin type: BET\_AUTH
   -  plugin/type-specific handler function:
      bet\_info[BET\_AUTH]->bet\_ops->handler
   -  plugin/type-specific handler argument:
      bet\_info[BET\_AUTH]->pvt\_bet\_data

7.8. AD Provider Plugin
-----------------------

The AD Provider Plugin supports the following provider types, which are
initialized by corresponding functions in ad\_init.c:

::

    id_provider        // initialized by sssm_ad_id_init

::

    auth_provider          // initialized by sssm_ad_auth_init

::

    chpass_provider        // initialized by sssm_ad_chpass_init

::

    access_provider        // initialized by sssm_ad_access_init

The ad\_options global variable is used to maintain the configuration
options for the various provider types supported by the AD Provider
Plugin. This includes:

-  basic configuration: ad\_domain, ad\_server, krb5\_keytab,
   ad\_enable\_dns\_sites, etc
-  id\_provider configuration: sdap service, gc service, etc
-  auth/chpass\_provider configuration: principal name, service name,
   keytab\_name, krb5 service
-  dynamic dns updates configuration

Since our use case uses the AD Provider Plugin for all provider lines,
each bet\_info array will be populated with the following AD-specific
information:

-  bet\_info[BET\_ID]

   -  bet\_ops: ad\_id\_ops
   -  pvt\_bet\_data: ad\_options.id\_ctx

-  bet\_info[BET\_AUTH]

   -  bet\_ops: ad\_auth\_ops
   -  pvt\_bet\_data: ad\_options.auth\_ctx

-  bet\_info[BET\_CHPASS]

   -  bet\_ops: ad\_chpass\_ops
   -  pvt\_bet\_data: ad\_options.auth\_ctx

-  bet\_info[BET\_ACCESS]

   -  bet\_ops: ad\_access\_ops
   -  pvt\_bet\_data: access\_ctx

The remainder of this section will examine each provider line in turn,
focussing on the functionality implemented by each line's bet\_ops
functions. Note that the first three provider lines use fields from
ad\_options as the pvt\_bet\_data argument that is passed in to the
corresponding bet\_ops functions.

7.8.1. AD Provider Plugin: id\_provider
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this section, we examine the AD Provider Plugin's implementation of
the id\_provider type, including the AD-specific bet\_ops and
pvt\_bet\_data that are used. Unlike the other provider types, the
bet\_ops for the id\_provider type includes values set for the
check\_online and finalize function pointers.

-  bet\_ops:

   -  check\_online: ad\_check\_online
   -  handler: ad\_account\_info\_handler
   -  finalize: ad\_shutdown

-  pvt\_bet\_data: ad\_opts.id\_ctx (of type ad\_id\_ctx)

7.8.1.1. ad\_id\_ctx
^^^^^^^^^^^^^^^^^^^^

The ad\_id\_ctx is created as part of the initialization that takes
place when the AD Provider Plugin is dynamically loaded for an
id\_provider line, at which time several actions take place, including:

-  retrieving relevant config info
-  initializing failover
-  initialized dynamic dns updates
-  setting up sdap child process
-  setting up various sdap options
-  setting up tasks
-  setting up id mapping object
-  setting up tls
-  setting up srv lookup plugin
-  setting up periodic refresh of expired records

7.8.1.2. ad\_account\_info\_handler
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This function is used to fulfill an identity lookup request. In this
section, we will use getpwnam(“aduser@foo.com”) as our example. It is
called by be\_get\_account\_info, which is the generic sbus\_method
function that handles *getAccountInfo* messages, the details of which
have been previously discussed.

This function is called with a be\_req input argument, from which it
extracts two important things:

-  ad\_id\_ctx, which includes relevant config info, etc
-  be\_acct\_req, which includes the input values sent in the SBus
   request message (entry\_type, attr\_type, filter and domain).

Next, an entry\_type-specific function is called (e.g.
users\_get\_send), which does the following:

-  creates an sdap\_id\_op object to represent the operation request
   (using sdap\_id\_op\_create)
-  establishes LDAP connection by sending a connection request (or
   re-uses existing connection)

   -  multi-step process, including resolving, connecting, and binding
      to an LDAP server

-  sends an operation request (and receives response) over the LDAP
   connection

   -  performs ldap search using the be\_acct\_req fields as input
      params (sdap\_get\_generic\_send).

7.8.1.3. ad\_check\_online
^^^^^^^^^^^^^^^^^^^^^^^^^^

This function determines whether the Backend is in “online mode”. This
function is called with a be\_req input argument, from which it extracts
the ad\_id\_ctx, after which it attempts to connect to the LDAP server.
If the LDAP server is reachable, this function sets its output to
DP\_ERR\_OK; otherwise, it sets its output to DP\_ERR\_OFFLINE.

7.8.2. AD Provider Plugin: auth\_provider and chpass\_provider
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Since the auth\_provider and chpass\_provider for the AD Provider Plugin
have many similarities, we will discuss them together in this section.
Both providers use the same bet\_ops and pvt\_bet\_data.

-  bet\_ops:

   -  handler: krb5\_pam\_handler

-  pvt\_bet\_data: ad\_opts.auth\_ctx (of type krb5\_auth\_ctx)

7.8.2.1. krb5\_auth\_ctx
^^^^^^^^^^^^^^^^^^^^^^^^

The krb5\_auth\_ctx is created as part of the initialization that takes
place when the AD Provider Plugin is dynamically loaded for an
auth\_provider line or chpass provider line, at which time several
actions take place, including:

-  retrieving relevant config info
-  forcing krb5\_servers to match ad\_servers
-  forcing krb5\_realm to match ad\_krb5\_realm
-  setting up krb5 child process

7.8.2.2. krb5\_pam\_handler
^^^^^^^^^^^^^^^^^^^^^^^^^^^

This function is used to fulfill an authentication request, or to
fulfill a change password request. For these requests, it is called by
be\_pam\_handler, which is the generic sbus\_method function that
handles *pamHandler* messages, the details of which have been previously
discussed.

This function is called with a be\_req input argument, from which it
extracts two important things:

-  krb5\_ctx, which includes relevant config info, etc
-  pam\_data, which includes the many input values sent in the SBus
   request message (e.g. cmd, user, authtok, etc).

This function performs the following high-level tasks:

-  retrieves several attributes for this user from the domain-specific
   sysdb (e.g. upn, uid, gid, etc)
-  obtains addressing information for the KDC (which is also the kpasswd
   server in AD)
-  forks a krb5\_child, which will make the blocking krb5 api calls
-  performs an asynchronous write to send the appropriate request
   information to the krb5\_child
-  performs an asynchronous read to receive the response from the
   krb5\_child

Next, the function calls be\_resolve­\_server to get the addressing
information for the KDC. Since the IP address of the LDAP service and
the KRB5 service is the same (i.e. that of the AD service), resolving
the KRB5 service may not require going to DNS, since we may already have
the information from resolving the LDAP service. Note that, in order to
make the Kerberos library aware of which IP address to use for the AD
server, we call write\_krb5info\_file, which writes a kdcinfo file to
the filesystem, which is later read by the Kerberos library. More info
on the kdcinfo files can be found in a separate subsection below.

In order to avoid blocking on synchronous Kerberos calls, this function
then spawns a krb5\_child process and sends it the relevant input (e.g.
username, password, new password) using its write pipe. The krb\_child
makes the appropriate Kerberos library calls (to perform the
authentication or password change), after which it returns a response to
the calling process's read pipe, at which time the krb5\_child process
exits.

7.8.2.2.1. Parent => Child
''''''''''''''''''''''''''

The information sent from the AD Provider Plugin to the krb5\_child
process includes:

-  cmd *e.g. SSS\_PAM\_AUTHENTICATE, SSS\_PAM\_CHAUTHTOK*
-  upn *(from sysdb)*
-  validate *whether TGT validation is desired (default: TRUE)*
-  is\_offline *whether SSSD is offline*
-  send\_pac *whether to send PAC to PAC Responder (for AD, always
   TRUE)*
-  ccname *credentials cache name*
-  keytab *keytab name (used for TGT validation)*
-  authtok *current password*
-  newauthtok *new password (only used by chpass\_provider; not by
   auth\_provider)*

For an authentication request, the krb5\_child process uses the
krb5\_principal (parsed from upn) and specified password to obtain
authentication credentials (i.e. TGT) from the ticket-granting service
on the AD KDC. If successful, and if validate is set to TRUE, the
krb5\_child process proceeds to locally validate the TGT using the
specified keytab. As part of validation, if send\_pac is set to TRUE,
the krb5\_child extracts the PAC from the TGT and sends the PAC (along
with the user principal) to the PAC Responder, which decodes the PAC
information, such as group memberships from trusted domains, and updates
the System Cache accordingly. Finally, the authentication credentials
(i.e. TGT) are stored in the specified credentials cache for that
principal.

For a password change request, the krb5\_child process also uses the
krb5\_principal and password, but uses it to get change password
credentials from the password-change service on the AD KDC. If
successful, and with valid change password credentials in hand, the
krb5\_child then asks the password-change service to change the password
to the specified new password, after which it obtains it sends an
authentication request (as above), by which a new TGT is obtained from
the ticket-granting service, and stored in the credentials cache for
that principal.

7.8.2.2.2. Child=>Parent
''''''''''''''''''''''''

While it is processing, the krb5\_child process can add pam responses to
the pam\_data object's response list (resp\_list), where each response
consists of a {type,length,value} tuple. It is this response\_list which
is returned from the child to its parent after it has completed
processing. After receiving the responses, the parent passes the
responses back to the Responder, which passes back the responses (after
filtering some of them out) to the Client Library, which acts upon them
in some way. As such, these responses may be for consumption by the
parent, the Responder, and/or the Client Library.

For example, the krb5\_child may wish to convey an error message to the
Client Library, indicating that a password change request has failed
(b/c the wrong password was entered for authentication). In this case,
the krb5\_child would append the following response to the response
list, which the Client Library could use to display an error message to
the SSS Client Application.

-  type: SSS\_PAM\_USER\_INFO
-  len: data\_length
-  data:

   -  resp\_type: SSS\_PAM\_USER\_INFO\_CHPASS\_ERROR
   -  len: err\_len
   -  user\_error\_message: “Old password not accepted”

As another example, the krb5\_child may wish to convey some data (e.g.
TGT lifetime) to the parent. In this case, the krb5\_child might also
append the following response to the response list, which the parent
(i.e. AD Provider Plugin) could use as a parameter when adding the TGT
to a renew table.

-  type: SSS\_KRB5\_INFO\_TGT\_LIFETIME
-  len: data-length
-  data: value of tgt lifetime

7.8.2.3. kdcinfo files
^^^^^^^^^^^^^^^^^^^^^^

The SSSD might discover additional KDC or Kadmin servers that are not
defined in krb5.conf. However, it would still be prudent if tools like
kinit or kpasswd could talk to the same servers the SSSD talks to. To
this end, the SSSD implements a plugin for libkrb5, located in the
`​sssd\_krb5\_locator\_plugin.c <https://git.fedorahosted.org/cgit/sssd.git/tree/src/krb5_plugin/sssd_krb5_locator_plugin.c>`__
file. When a new KDC is discovered, the sssd\_be process writes the IP
address of this KDC into a file under the /var/lib/sss/pubconf
directory. With the help of the locator plugin, libkrb5 is able to read
these files in the pubconf directory and use the KDC servers discovered
by the SSSD.

7.8.3. AD Provider Plugin: access\_provider
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this section, we examine the AD Provider Plugin's implementation of
the access\_provider type, including the AD-specific bet\_ops and
pvt\_bet\_data that are used.

-  bet\_ops:

   -  handler: ad\_access\_handler

-  pvt\_bet\_data: access\_ctx (of type ad\_access\_ctx)

7.8.3.1. ad\_access\_ctx
^^^^^^^^^^^^^^^^^^^^^^^^

The ad\_access\_ctx is created as part of the initialization that takes
place when the AD Provider Plugin is dynamically loaded for an
access\_provider line, at which time several actions take place,
including:

-  setting up sdap\_access\_ctx for checking expired/locked accounts

7.8.3.2. ad\_access\_handler
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This function is used to fulfill an access check request, such as
determining whether the password of "aduser@foo.com" has expired. It is
called for account management requests by be\_pam\_handler, which is the
generic sbus\_method function that handles *pamHandler* messages, the
details of which have been previously discussed.

This function is called with a be\_req input argument, from which it
extracts two important things:

-  access\_ctx, which includes relevant config info, etc
-  pam\_data, which includes the many input values sent in the SBus
   request message (e.g. cmd, user, authtok, etc).

Currently, the ad\_access\_handler simply calls sdap\_access\_send,
which determines whether or not the account is expired/locked, and
returns the result.

8. Tevent Basics
================

This section examines events and requests based on file descriptors.

8.1. Events
-----------

The tevent library provides a main loop implementation capable of
supporting various types of events, of which we focus here on fd-based
events. A tevent\_fd object encapsulates an fd, a set of flags (e.g.
READ, WRITE), an event handler, and handler data. As with all events, a
tevent\_fd is managed by the tevent main loop, which monitors the events
in its event context. When an event fires (e.g. fd becomes readable),
the main loop calls the corresponding event handler callback, which uses
the handler data to continue where it left off. When the main loop calls
a handler, the main loop can not call a second handler until control has
been returned to it by the first handler.

In the tevent model, the handler code is responsible for performing
socket operations (e.g. accept, send, recv, etc) on a file descriptor,
while the main loop is responsible for polling the file descriptors to
determine which one is ready to send or recv data. When we call
tevent\_add\_fd(ev, talloc\_ctx, fd, flags, handler, data), we are
simply asking the main loop to call the handler with the arg, when the
specified fd is able to read or write (as specified by the flags).

8.2. Requests
-------------

The tevent library also supports generic asynchronous functions, by
providing tevent request helper functions (and a naming convention).
Unlike synchronous functions, which provide callers with a single
interface that accepts inputs and returns outputs, asynchronous
functions provide two interfaces for a particular computation: one to
“send” the request (i.e. accept inputs) and another to “receive” the
response (i.e. return outputs). As such, a tevent request's
"implementation" refers to the code that implements the tevent request
(e.g. comp\_send and comp\_recv), while a tevent request's "caller"
refers to the code that calls comp\_send or comp\_recv. The tevent
library includes support for nested requests, in which the
"implementation" of one tevent request can be a "caller" for a different
tevent request. This allows for better modularization of the codebase.
This also enables the cancelling of a top-level request to result in the
cancelling of all its nested requests.

The implementation of a tevent request is responsible for creating a
tevent\_req object, specifying data (used to hold inputs/outputs;
private to the implementation) that the implementation may need to
maintain, and determining whether or not the request has completed
successfully. In addition, since the caller is not aware of the data
details, the implementation has to provide a recv function so that the
caller can extract the relevant outputs from the state.

The caller of a tevent request specifies its inputs when issuing a
request, and also specifies a callback function (and argument) to be
called when the request has completed. This callback function is
typically used by the caller to receive the response (using the
implementation-provided recv function). Note that the caller is not
concerned with the details of the implementation (e.g. whether network
I/O was required, whether the request was fulfilled by cache, etc), as
long as the tevent request's send/recv contract (e.g. input/output) is
maintained.

Let's look at the naming convention used by tevent requests for an
example **"comp"** computation (note that this naming convention is not
always precisely followed in the SSSD code):

-  the implementation of the comp computation:

   -  specifies public interface for caller consumption:

      -  ***comp***\ *\_send(mem\_ctx, inputs)*: used by caller to
         specify inputs for request
      -  ***comp***\ *\_recv(req, outputs)*: used by caller to receive
         outputs of request

   -  specifies private details for internal consumption by
      implementation

      -  ***comp***\ *\_state: object used to pass around inputs/outputs
         between internal functions*

-  the caller of the **comp** computation:

   -  calls the public interface with inputs/outputs
   -  ***comp***\ *\_done: specifies callback function and callback
      argument*

The following example illustrates the material presented in this
section. In this example, we are using **“read\_bytes”** as the example
computation. The implementation implements the caller-accessible
**read\_bytes\_send** and **read\_bytes**\ *\_recv* functions, as well
as its own internal functions (such as
***read\_bytes***\ \_\ *handler*). The caller calls the public interface
with inputs/outputs, and also specifies the callback function.

Implementation Code

.. raw:: html

   <div class="code">

::

    struct tevent_req *read_bytes_send(mem_ctx, ev, fd) {
           ...
           req = tevent_req_create(mem_ctx, &state, struct read_bytes_state);
           state->fd = fd;
           state->buf = talloc_size(state, BUFSIZE);
           state->len = 0;
           fde = tevent_add_fd(ev, state, fd, TEVENT_FD_READ, read_bytes_handler, req);
           return req;
    }

.. raw:: html

   </div>

.. raw:: html

   <div class="code">

::

    void read_bytes_handler(struct tevent_context *ev, struct tevent_fd *fde, void *pvt) {
         ...
         req = talloc_get_type(pvt, struct tevent_req);
         state = tevent_req_data(req, struct read_bytes_state);
         read(state->fd, buf, BUFSIZE);
         return;
    }

.. raw:: html

   </div>

.. raw:: html

   <div class="code">

::

    int read_bytes_recv(req, mem_ctx, uint8_t **buf, ssize_t *len) {
        ...
        state = tevent_req_data(req, struct read_bytes_state);
        *buf = talloc_steal(mem_ctx, state->buf);
        *len = state->len;
        return EOK;
    }

.. raw:: html

   </div>

Caller Code

.. raw:: html

   <div class="code">

::

    void caller_func(fd, caller_data) {
         ...
         tevent_req *req = read_bytes_send(mem_ctx, ev, fd)
         tevent_req_set_callback(req, caller_func_complete, caller_data);
    }

.. raw:: html

   </div>

.. raw:: html

   <div class="code">

::

    int caller_func_complete(tevent_req *req) {
        ...
        caller_data = tevent_req_callback_data(req, struct caller_data);
         ... do something with caller_data ...
         read_bytes_recv(req, state, &dp_error);
          return dp_error;
    }

.. raw:: html

   </div>

Note the distinction between an event handler and a request callback.
While they are both similar in function, the tevent main loop is only
aware of the events and handlers in the event context that it is
monitoring. A tevent request is not managed by the main loop. Rather,
the request's implementation determines when the request has completed,
resulting in the request's callback being called, which uses the
callback data to continue where it left off. Unlike an event, a tevent
request is quite flexible, as it represents a generic asynchronous
function call. Also, when a main loop calls a handler, the main loop can
not call a second handler until control has been returned to it by the
first handler. However, the first handler's code may “send” a tevent
request, which may itself “send” a second tevent request, and so on, all
before returning control to the main loop.

Additionally, an event's handler and handler\_data are registered using
one of the tevent\_add\_\* functions; when the event is triggered, the
main loop calls event->handler(..., event->handler\_data), just as we
would expect. In other words, the handler and handler\_data that we
registered are the same handler and handler\_data that are called. In
contrast, since a request's callback and callback data are registered
using tevent\_req\_set\_callback(req, callback, callback\_data), you
might expect the code to call callback(callback\_data). However, this is
not the case; the code calls the tevent request's callback with the
tevent request as a parameter, and the callback\_data needs to be
extracted from the tevent request. In other words, the code calls
callback(req); the callback function then needs to extract the callback
data from the req using tevent\_req\_callback\_data(req, ...).

8.3. Subrequests
----------------

If the async computation relies on a sub-computation taking place before
the async function can make progress, it can create a request with its
state, and then register the subcomputation by creating a subrequest
(representing the subcomputation) and setting the subrequest's callback
to a function which will allow the original computation to make
progress. For example, you will often see the following pattern in the
codebase (note that the code listing can be read from top to bottom,
almost as if the calls were synchronous):

.. raw:: html

   <div class="code">

::

    comp_send(memctx, inputs)
            req = tevent_req_create(memctx, &state, struct comp_state);
            ...populate state's input fields (using inputs)...
            subreq = subcomp_send(...);
            tevent_req_set_callback(subreq, comp_done, req);
            return req;

    comp_done(subreq)
            req = tevent_req_callback_data(subreq, tevent_req)
             comp_state = tevent_req_data(req, comp_state)
             ...populate state's output fields by calling comp_recv(subreq, *state->outputs)...
             ...call tevent_req_done or tevent_req_error, as appropriate...

.. raw:: html

   </div>

In order to examine a nested chain of subrequests, it can be useful to
create a diagram to help visualize it. The following diagram displays
two such Kerberos-related visualizations. It is left as an exercise for
the reader to create an SDAP-related visualization! ;)

*This diagram presents a visualization of the AD Provider Plugin's
implementation of AUTH (top) and ACCT\_MGMT (bottom). Several
abbreviations are used here, including: BR=be\_resolve\_server,
HAN\_CHILD=handle\_child, WR=write\_pipe, RD=read\_pipe, ID\_OP =
sdap\_id\_op, GG=sdap\_get\_generic. Also note that be\_resolve\_server
makes several additional calls, which we have not shown.*

9. Functions
============

This section provides documentation for several functions. We refer
below to the entire computation as if it were a synchronous function,
receiving logical inputs (i.e. comp\_send), and returning logical ouputs
(comp\_recv). This makes it easier to see the function's input/output
characteristics.

9.1. SDAP Connection Functions
------------------------------

This section describes several of the functions called in order to
establish an authenticated LDAP connection. The call stack looks as
follows:

-  **sdap\_id\_op\_connect\_send**

   -  sdap\_cli\_connect\_send

      -  be\_resolve\_server\_send

         -  fo\_resolve\_service\_send

            -  resolv\_gethostbyname\_send

               -  resolv\_gethostbyname\_dns\_send

      -  sdap\_connect\_send ****
      -  sdap\_cli\_rootdse\_step

         -  **sdap\_get\_rootdse\_send**

      -  sdap\_cli\_kinit\_step

         -  **sdap\_kinit\_send**

            -  be\_resolve\_server\_send
            -  sdap\_get\_tgt\_send ****

      -  sdap\_cli\_auth\_step

         -  **sdap\_auth\_send**

9.1.1. sdap\_id\_op\_connect\_send/recv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Logical Input: sdap\_id\_op object

Logical Output:

-  if successful, returns

   -  reply\_count
   -  reply (sysdb\_attrs)
   -  op created and added to sh->ops

Summary: This function initiates an LDAP connection, manages the
connection cache, and calls *sdap\_cli\_connect\_send* to do the heavy
lifting.

9.1.2. sdap\_cli\_connect\_send/recv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Logical Input: sdap\_options, sdap\_service, skip\_rootdse, force\_tls,
skip\_auth

Logical Output:

-  can\_retry boolean
-  sdap\_handle
-  sdap\_server\_opts

Summary: This functions attempts to perform multiple tasks in order to
establish a server connection for the specified sdap\_service. This
function is called by ad\_check\_online in order to determine if we are
able to connect to server (in which case we are in online mode).
Internally, it makes the following calls to perform these tasks:

-  calls be\_resolve\_server to obtain addressing information for a
   server that supports the service
-  calls sdap\_connect\_send to establish a connection to the resolved
   server
-  calls sdap\_cli\_rootdse\_step to read rootDSE info from the resolved
   server (if anonymous access allowed)
-  calls cli\_kinit\_step to obtain addressing information for a KDC and
   to obtain a TGT from it
-  calls cli\_auth\_step performs an LDAP bind (either sasl or simple);
   also, it we were unable to read rootDSE info anonymously, we try to
   read it again now that we're authenticated

9.1.3. be\_resolve\_server\_send/recv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Logical Input: be\_ctx, service\_name, first\_retry

Logical Output:

-  if able to resolve an fo\_server in fo\_service->server\_list

   -  set request done; output can be retrieved from state->srv
   -  calls any cbs associated with service; for AD provider, this is
      ad\_resolve\_cb(service)

      -  sets service->sdap->uri=ldap: *srv-name; populates sockaddr
         with ip and LDAP\_PORT*
      -  sets service->gc->uri=ldap: *srv-name:3268; populates sockaddr
         with ip and GC\_PORT*

-  if unable to resolve any fo\_server in fo\_service->server\_list

-  set request error to EIO, indicating that caller should mark us as
   offline (be\_mark\_offline)

Summary: attempts to resolve each server associated with service\_name's
fo\_service, until server resolution succeeds or there are no more
servers to resolve; if successful, calls any callbacks associated with
service and returns resolved fo\_server;

9.1.4. fo\_resolve\_service\_send/recv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Logical Input: resolv\_ctx, fo\_ctx, fo\_service

Logical Output:

-  if able to resolve hostname

   -  set fo\_server->common->status to SERVER\_NAME\_RESOLVED
   -  set request done; output can be retrieved from state->server

-  if unable to resolve hostname for fo\_server

   -  set fo\_server->common->status to SERVER\_NOT\_WORKING
   -  set request error to EAGAIN, indicating that the caller should try
      the next fo\_server (if any)

Summary: For next server on fo\_service->server\_list, if server
supports resolution using SRV records, perform resolution by calling
resolv\_srv\_send; otherwise, perform resolution by calling
fo\_resolve\_service\_server. If resolution successful, return
fo\_server, which includes the desired addressing information in
fo\_server->server\_common->rhostent. If unsuccessful, return EAGAIN,
indicating that caller should try next fo\_server (if any).

Internals: While a name resolution request is being processed, if a
second identical request is received (i.e. for the same server name),
the Backend will notice that an existing request for the same
information is already in progress, and it will register the second
request (and any subsequent identical requests) to be called back when
the results are ready (so that they receive the same reply information).
While the Responder is able to maintain a single dp\_request\_table to
perform a similar function, the Backend has to maintain a separate
request list for each server.

9.1.5. resolv\_gethostbyname\_send/recv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Logical Input: res\_ctx, name, family\_order, db

Logical Output: status, rhostent, error

Summary: Attempts to resolve server name using each host database in the
specified db list, until successful. If successful, returns the rhostent
object (containing IP address) and returns EOK; if unsuccessful, returns
embedded error. In all cases, returns query status and how many times
query timed out.

Internals: If server name is an IP address, returns a fake hostent
structure populated with IP address. Translates family\_order input to
family before calling subsequent functions. If first family doesn't
work, tries second family.

9.1.6. resolv\_gethostbyname\_dns\_send/recv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Logical Input:res\_ctx, name, family Logical Ouput: status, timeouts,
rhostent, error

Summary: Sends a DNS query for the specified server name over the DNS
connection represented by the specified resolv\_ctx's channel. If
successful, returns the rhostent object (containing the IP address
associated with specified server name); if domain name not found, sets
error to ENOENT; else sets error corresponding to status. In all cases,
returns query status and how many times query timed out.

Internals: This function registers a callback function
(resolv\_gethostbyname\_dns\_query\_done) with the c-ares library to be
called by the library when the query has completed or failed. When
called, the callback function parses the response (using
resolv\_gethostbyname\_dns\_parse) and retrieves the hostent object.

9.1.7. sdap\_connect\_send/recv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Logical Input: uri (ldap://server-name:port) and sockaddr (popoulated
with ip-address and port)

Logical Output:

-  if connection successfully established,

   -  set ldap connection callbacks
   -  set various options on ldap handle
   -  if not using start\_tls, set request done; sdap\_handle output can
      be retreived from state->sh
   -  if using start\_tls, calls ldap\_start\_tls, sdap\_set\_connected,
      sdap\_op\_add

Summary: This function establishes a connection to the LDAP server,
obtains the resulting LDAP handle, and registers a pair of connection
callbacks with the LDAP handle. These tasks are implemented in different
ways, depending on whether the system's OpenLDAP library supports the
ldap\_init\_fd call, and whether it supports the LDAP\_OPT\_CONNECT\_CB
option. In this description, we will assume that both are supported.

This function establishes the LDAP connection by calling
sss\_ldap\_init\_send, which returns an initialized LDAP handle. After
the connection has been established, sdap\_sys\_connect\_done registers
a pair of callbacks with OpenLDAP, such that OpenLDAP will call the add
connection callback (sdap\_ldap\_connect\_callback\_add) after a
connection is established, and will call the delete connection callback
(sdap\_ldap\_connect\_callback\_del) after a connection is closed. Since
we have just established a connection, the add\_connection\_callback is
called, which registers a handler (*sdap\_ldap\_result*) to handle
incoming responses.

At this point, several options are set on the LDAP handle (e.g. version,
timeouts, etc).

At this point, if TLS was not requested, we don't consider the connected
to be connected (i.e. we don't call sdap\_set\_connected); it will be
considered connected after the bind call succeeds. However, if TLS was
requested, we call ldap\_start\_tls, call sdap\_set\_connected, and call
sdap\_add\_op(sdap\_connect\_done). sdap\_connect\_done calls
ldap\_parse\_result to parse the StartTLS result.

9.1.8. sss\_ldap\_init\_send/recv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Logical Input: uri (ldap://server-name:port) and sockaddr (popoulated
with ip-address and port)

Logical Output: if successful, returns LDAP handle and file descriptor
for LDAP socket

Summary: creates a socket fd, connects to the ip-address of an LDAP
server, and initializes OpenLDAP by passing the connected fd to
ldap\_init\_fd, which returns an opaque LDAP structure, which is to be
used in subsequent OpenLDAP calls.

Internals: This function establishes an LDAP connection using the given
IP address and URI:

-  fd = socket(...);
-  connect(fd, ip-address, ...)
-  ldap\_init\_fd(fd, uri)

9.1.9. sdap\_get\_rootdse\_send/recv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Logical Input: sdap options, sdap handle

Logical Output: if successful, returns set of sysdb\_attrs

Summary: This function retrieves several attributes from the LDAP
server's rootdse by calling sdap\_get\_generic\_send with the following
inputs:

-  search\_base:[]
-  filter: [(objectclass=\*)];
-  attrs:
   [\*,altServer,namingContexts,supported{Control,Extension,Features,LDAPVersion,SASLMechanisms},
   domainControllerFunctionality,defaultNamingContext,
   last,highestCommitted}USN]

9.1.10. sdap\_kinit\_send/recv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Logical Input: sdap handle, krb\_service\_name, keytab, principal, realm

Logical Output: expire\_time

Summary: This function first calls be\_resolve\_server\_send to obtain
addressing information for a Kerberos server (KDC) that supports the
given service (i.e. as specified by krb\_service\_name). If successful,
this function then calls sdap\_get\_tgt\_send to obtain a TGT for the
host principal from the resolved KDC server from the previous step.

9.1.11. sdap\_get\_tgt\_send/recv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Logical Input: realm, principal, keytab, lifetime, timeout

Logical Output: result, krb5\_error\_code, ccname, expire\_time\_out

Brief: This function attempts to obtain a TGT from the KDC for the host
principal, using the host's key entry (in its key table) to perform the
necessary authentication.

Internals: In order to avoid blocking on synchronous Kerberos calls,
this function spawns an ldap\_child process, and sends it a TGT request
message (consisting of the realm, principal, and keytab) using its write
pipe. The ldap\_child makes the necessary Kerberos library calls to
attempt to get a TGT, and returns a response to the calling process's
read pipe, at which time the ldap\_child process exits.

Kerberos library calls used by ldap\_child include:

-  krb5\_init\_context: create a krb5 library context
-  krb5\_parse\_name: convert a string principal name to a
   krb5\_principal structure

   -  krb5\_unparse\_name: convert a krb5\_principal structure to a
      string representation

-  krb5\_kt\_default: resolve the default key table

   -  krb5\_kt\_start\_seq\_get: start a sequential retrieval of key
      table entries
   -  krb5\_kt\_next\_entry: retrieve the next entry from the keytable
   -  krb5\_free\_keytab\_entry\_contents: free the contents of a key
      table entry
   -  krb5\_kt\_end\_seq\_get: release a keytab cursor

-  krb5\_get\_init\_creds\_opt\_set\_address\_list: set address
   restrictions in initial credential options

   -  krb5\_get\_init\_creds\_opt\_set\_forwardable: set/unset
      forwardable flag in initial cred options
   -  krb5\_get\_init\_creds\_opt\_set\_proxiable: set/unset proxiable
      flag in initial credential options
   -  krb5\_get\_init\_creds\_opt\_set\_tkt\_life: set the ticket
      lifetime in initial cred options
   -  krb5\_get\_init\_creds\_opt\_set\_canonicalize: set/unset
      canonicalize flag in init cred options

-  krb5\_get\_init\_creds\_keytab: get initial credentials using a key
   table (request TGT)
-  krb5\_cc\_resolve: resolve a credential cache name

   -  krb5\_cc\_initialize: initialize a credential cache
   -  krb5\_cc\_store\_cred: store credentials in a credential cache

-  krb5\_get\_time\_offset: return the time offsets from the os context

9.1.12. sdap\_auth\_send/recv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Logical Input: sdap\_handle, sasl\_mech, sasl\_user, user\_dn, authtok

Logical Output: if successful, returns EOK and (for simple bind only) an
sdap\_ppolicy\_data object if unsuccessful, returns ERR\_AUTH\_FAILED

Brief: This function peforms an LDAP bind by calling either
sdap\_sasl\_bind or sdap\_simple\_bind (based on whether the specified
sasl\_mech is non-NULL). If the bind is successful, and we were not able
to read the rootDSE during unauthenticated bind, we try to read the
rootDSE again now that we're authenticated.

If sasl\_mech is specified, sdap\_sasl\_bind is called with the
specified sasl\_mech and sasl\_user. For the AD use case, the value for
sasl\_mech is obtained from the ldap\_sasl\_mech configuration field
(which is typically GSSAPI). The value for sasl\_user is obtained from
the ldap\_sasl\_authid configuration field. Internally, we make a
blocking call to ldap\_sasl\_interactive\_bind\_s.

If sasl\_mech is not specified, sdap\_simple\_bind is called with the
specified user\_dn and with a password retrieved from the specified
authtok. In an AD use case, the value for the specified user\_dn is
obtained from the ldap\_default\_bind\_dn configuration field. The value
for the specified password is obtained from the ldap\_default\_authtok
configuration field. Internally, we make a call to ldap\_sasl\_bind. If
it succeeds, we set the sdap handle to the connected state.

9.2. SDAP Operation Request Functions
-------------------------------------

9.2.1. users\_get\_send/recv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Logical Input: sdap\_id\_ctx, sdap\_domain, sdap\_id\_conn\_ctx, name,
filter\_type

Logical Output:

-  returns dp\_error and sdap\_ret

Summary: This function is called in order to handle a USER request (i.e.
getpw\*) with the specified inputs.

Internals: This function creates an sdap\_id\_op object to represent the
operation request. It then uses the specified inputs to create an LDAP
filter.

-  creates an sdap\_id\_op object to represent the operation request
   (using sdap\_id\_op\_create)
-  establishes LDAP connection by sending a connection request (or
   re-uses cached connection)

   -  multi-step process, including connecting and binding to an LDAP
      server

-  sends an operation request (and receives response) over the LDAP
   connection

   -  performs asynchronous ldap search using the be\_acct\_req fields
      as input params (sdap\_get\_generic\_send).

9.2.2. sdap\_get\_generic\_send/recv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Logical Input: sdap handle (including sdap\_op objects), search\_base,
scope, filter, attrs

Logical Output:

-  if successful, returns

   -  reply\_count
   -  reply (sysdb\_attrs)
   -  op created and added to sh->ops

Summary: This function performs an asynchronous ldap search operation by
calling ldap\_search\_ext with the specified inputs, which include where
to start the search (base), how deep to search (scope), what to match on
(filter), and which attributes to return (attrs). If successful, the
recv function returns the specified attributes of entries matching the
specified filter. If unsuccessful, the recv function indicates that
there was an error.

9.2.3. sdap\_get\_generic\_ext\_send/recv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Logical Input: sdap handle, search\_base, scope, filter, attrs,
parse\_cb

Logical Output:

-  if successful

   -  set request done; output can be retrieved from state->sreply

-  else returns error

Summary: This function performs an asynchronous ldap search operation by
calling ldap\_search\_ext with the specified inputs, obtaining the
resulting msgid, and created an sdap\_op object using the msgid.

Internals: The recv function is called when the ldap response messages
(corresponding to the search request) are received. Note that a search
request can generate several *search entry* responses
(LDAP\_RES\_SEARCH\_ENTRY), followed by a single *search done* response
(LDAP\_RES\_SEARCH\_RESULT). For each *search entry* response that is
received, we call the specified parse\_cb function (e.g.
sdap\_get\_generic\_parse\_entry), which parses the response and adds
the returned attributes to an sdap\_reply object. If a *search done*
response is received, then we call the standard ldap\_parse\_result
function to parse the response, primarily to extract the error message
(if any).

10. Filesystem Locations
========================

This section describes the locations of the primary source code and
installation artifacts for each component.

+----------------------+----------------------------------+--------------------------------------+-------------------------+
| *Component*          | *Source File Location*           | *Installation Location*              | *Log File and Prefix*   |
+----------------------+----------------------------------+--------------------------------------+-------------------------+
| NSS Client Library   | sss\_client/nss\_\*.c            | /usr/lib64/security/nss\_sss.so      | n/a                     |
+----------------------+----------------------------------+--------------------------------------+-------------------------+
| PAM Client Library   | sss\_client/pam\_sss.c           | /usr/lib64/security/pam\_sss.so      | n/a                     |
+----------------------+----------------------------------+--------------------------------------+-------------------------+
| Monitor              | monitor/monitor.c                | /usr/sbin/sssd                       | sssd.log;               |
+----------------------+----------------------------------+--------------------------------------+-------------------------+
| NSS Responder        | responder/nss/nsssrv.c           | /usr/libexec/sssd/sssd\_nss          | sssd\_nss.log;          |
+----------------------+----------------------------------+--------------------------------------+-------------------------+
| PAM Responder        | responder/pam/pamsrv.c           | /usr/libexec/sssd/sssd\_pam          | sssd\_pam.log;          |
+----------------------+----------------------------------+--------------------------------------+-------------------------+
| Backend              | providers/data\_provider\_be.c   | /usr/libexec/sssd/sssd\_be           | sssd\_foo.com.log;      |
+----------------------+----------------------------------+--------------------------------------+-------------------------+
| AD Provider Plugin   | providers/ad/ad\_init.c          | /usr/lib64/sssd/libsss\_ad.so        | n/a                     |
+----------------------+----------------------------------+--------------------------------------+-------------------------+
| Config DB            | confdb/confdb.c                  | /var/lib/sss/db/config.ldb           | n/a                     |
+----------------------+----------------------------------+--------------------------------------+-------------------------+
| System DB            | db/sysdb.c                       | /var/lib/sss/db/cache\_foo.com.ldb   | n/a                     |
+----------------------+----------------------------------+--------------------------------------+-------------------------+

11. Helpful Links
=================

-  SSSD Overview Video

   -  Presented by Stephen Gallagher-
      `​http://www.youtube.com/user/opensourceidm <http://www.youtube.com/user/opensourceidm>`__

-  SSSD Wiki -
   `​https://fedorahosted.org/sssd/wiki/ <https://fedorahosted.org/sssd/wiki/>`__

   -  This is the main repository for SSSD information. It includes:

      -  [Design Docs] -
         `​https://fedorahosted.org/sssd/wiki/DesignDocs <https://docs.pagure.org/sssd-test2/DesignDocs.html>`__
      -  [Developer Pages] -
         `​https://fedorahosted.org/sssd/wiki/DevRes <https://docs.pagure.org/sssd-test2/DevRes.html>`__

         -  such as Developer Tips and Tutorials

      -  [Documentation] -
         `​https://fedorahosted.org/sssd/wiki/Documentation <https://docs.pagure.org/sssd-test2/Documentation.html>`__

         -  such as Man Pages, Deployment Guides, Conference
            Presentations

-  Realmd Page -
   `​http://www.freedesktop.org/software/realmd/ <http://www.freedesktop.org/software/realmd/>`__

   -  [Realmd Page] This is the main repository for Realmd information.
      Among other things, it includes man pages, as well as an
      Administrative Guide.

-  Samba Components

   -  [Talloc Tutorial] -
      `​http://talloc.samba.org/talloc/doc/html/libtalloc\_\_tutorial.html <http://talloc.samba.org/talloc/doc/html/libtalloc__tutorial.html>`__
   -  [Tevent Tutorial] -
      `​http://tevent.samba.org/tevent\_tutorial.html <http://tevent.samba.org/tevent_tutorial.html>`__
   -  [LDB Tutorial] -
      `​http://wiki.samba.org/index.php/Samba4/LDBIntro <http://wiki.samba.org/index.php/Samba4/LDBIntro>`__

-  FreeIPA Design Proposals (out-of-date)

   -  SSSD was originally conceived of as the IPAv2 Client, so these
      documents are useful in understanding the initial client design.
      However, keep in mind that these documents are out-of-date. For
      example, the sections on Policy Kit Back-End Daemon (PKBED) and
      the Info Pipe Daemon (IPD) are not relevant to SSSD. Also, the
      Service Controller Daemon in these documents refers to what later
      became known as the SSSD Monitor process.

      -  [Design Overview]
         `​http://www.freeipa.org/page/V2/IPA\_Client\_Design\_Overview <http://www.freeipa.org/page/V2/IPA_Client_Design_Overview>`__
      -  [Monitor]
         `​http://www.freeipa.org/page/SSSD/Service\_Controller\_Daemon <http://www.freeipa.org/page/SSSD/Service_Controller_Daemon>`__
      -  [SBus]
         `​http://www.freeipa.org/page/SSSD/SBUS <http://www.freeipa.org/page/SSSD/SBUS>`__
