.. raw:: html

   <div class="wiki-toc">

#. 

   #. `SUDO Support to SSSD <#SUDOSupporttoSSSD>`__
   #. `DESIGN : <#DESIGN:>`__
   #. `SUDO Plugin <#SUDOPlugin>`__
   #. `SUDO Responder <#SUDOResponder>`__
   #. `SUDO Provider Interface <#SUDOProviderInterface>`__
   #. `LDAP Provider for SUDO <#LDAPProviderforSUDO>`__
   #. `Advantages of this design <#Advantagesofthisdesign>`__

.. raw:: html

   </div>

SUDO Support to SSSD
--------------------

--------------

| 
| This Design document talks about the integration of SUDO support to
  SSSD through plugin system.The SUDO can be used to check whether a
  user have rights to execute the instructions as another user. Using
  this plugin SUDO can be configured to use custom rules and policies.
  So that we can alter authorization rules so as to provide cached
  access to LDAP. This will make it easier to maintain centralized sudo
  rules. The SSSD caches the SUDO policies, so that the SUDO support can
  work better with a LDAP sever.

    To integrate the sudo feature into the System Security Service
    Daemon(SSSD) we must have some components to handle sudo policies
    and authentication at both client side and server side. At the LDAP
    sever side, the schema for storing the sudo policies is available(or
    already implemented). So that, the SUDO rules can be loaded into an
    LDAP server and managed centrally using this schema. The LDAP
    servers follows the SUDO schema specified at the Suborders LDAP
    Manual
    (`​http://www.gratisoft.us/sudo/man/1.8.0/sudoers.ldap.man.html <http://www.gratisoft.us/sudo/man/1.8.0/sudoers.ldap.man.html>`__).
    Any Directory Server can load the described schema and become a
    provider of the centrally managed SUDO rules for the SUDO clients.

| 

DESIGN :
--------

    At the highest level the SUDO feature is implemented as the client
    side SUDO utility and server side SUDO schema as shown below.

|High level design of SUDO system|

    In this level the LDAP server contains centrally managed SUDO schema
    specifying the SUDO rules. The sudo utility at the client side
    queries the LDAP server to authenticate the request. The server
    inspects the query with SUDO schema to determine whether the
    requested user have the right to execute this command. Then returns
    the result back to the client.

When Plugin comes in to action, the SSSD works with this plugin so that
the sudo queries is sent to the LDAP server. On receiving the sudo
command on the runtime the SUDO utility will transfer give the chance
for processing the request to the plugin integrated to the sudo utility
at client side. This is done based on the Plugin-API provided by the
sudo utility. The manual for Plugin-API can be found here
(`​http://www.gratisoft.us/sudo/man/1.8.1/sudo\_plugin.man.html <http://www.gratisoft.us/sudo/man/1.8.1/sudo_plugin.man.html>`__).
The SSSD provides a cached support to SUDO using this plugin.

|SUDO plugin in action|

| The Plug-in is designed as 4 components. They are
| (1). Lightweight plugin for SUDO.
| (2). SUDO responder daemon.
| (3). SUDO provider type.
| (4). LDAP implementation of the SUDO provider type

--------------

SUDO Plugin
-----------

--------------

    The lightweight plugin just forwards the sudo command request from
    the SUDO utility to the SSSD. The plugin is made using the
    plugin-API and connected to the sudo utility at the client side.
    When user types in the command with sudo (eg: sudo ls ) the sudo
    utility gives the chance for execution to the sudo plugin. The
    plugin calls the pam\_authenticate() from the pam library with pam
    service defined for sudo, to verify the user provided information.
    If the pam module returns PAM\_SUCCESS then plugin continues with
    sssd else dies with an error message. If pam authentication is
    successful, then the plugin just forwards the request obtained from
    the sudo utility to the SSSD daemon. The format of this forward
    request is available at `[
    https://fedorahosted.org/sssd/wiki/DesignDocs/SUDOSupport/PluginWireProtocol#THEPLUGINWIREPROTOCOL? <https://docs.pagure.org/sssd-test2/%5B%20https%3A//fedorahosted.org/sssd/wiki/DesignDocs/SUDOSupport/PluginWireProtocol.html#THEPLUGINWIREPROTOCOL>`__]

|image2|

--------------

SUDO Responder
--------------

--------------

The request forwarded by plugin reaches SSSD which gives the request to
the SUDO responder daemon. First of all, the responder performs a
look-up against the SSSD's cache or sysdb. The result of this lookup can
be either a cache-hit or a cache-miss or an expired entry. If the entry
exists in the cache and is not expired, we will immediately reply to the
plugin module with the answer that shows whether the user can be
authenticated to run the specified command as SUDO user. There the sudo
request ends. In the case of a cache-miss, the SUDO responder needs to
get the latest SUDO schema information from the LDAP server. So that the
request for contacting the LDAP server is given to LDAP provider. When
the entry in the cache is found to be expired the same step as in the
cache miss is followed.

|SUDO responder checks the cache|

--------------

SUDO Provider Interface
-----------------------

--------------

Sudo provider provides a interface to write/update the schema obtained
from the LDAP server through LDAP provider. In the case of a cache miss
or expired cache the sudo responder contacts the LDAP provider to get
the schema from server and the returned schema is used to serve the SUDO
request from the sudo utility. and this result is passed to the SUDO
provider which writes this data to the offline cache in the SSSD. So
that the next request before the expiration time can be served without
any LDAP searches. SO that the over all efficiency of SUDO operation
increases by the use of SSSD and its offline cache.

The provider defines the communication protocol and functional interface
for actual back end and the responder.

--------------

LDAP Provider for SUDO
----------------------

--------------

In case of a cache miss or expired entry in the cache the SUDO need to
connect to the LDAP sever to update the offline schema in the cache. The
LDAP provider will deal with all the issues related to connecting the
LDAP server, Sending LDAP queries and receiving schema from the LDAP
server etc. Sudo provider gets this request from the responder. The
result obtained ( schema from LDAP server ) is returned to the sudo
responder.

The LDAP Provider has existing interfaces for 1) Identity, 2)
Authentication, 3) Access-control and 4) Password-change. The design
adds one more component to it. It is 5) SUDO policy. This component
deals with the back end and provider issues.

|SUDO provider connects to LDAP server|

--------------

Advantages of this design
-------------------------

--------------

This design allows us to load any SUDO implementation into the back-end
daemon and have it 1) work properly and 2) be completely self-contained,
so that the SUDO Responder doesn't need to know which is running. i.e
without any additional burden to the SUDO responder we can connect it to
any server system with valid SUDO implementation.

.. |High level design of SUDO system| image:: https://fedorahosted.org/sssd/raw-attachment/wiki/DesignDocs/SUDOSupport/sssd1.png
   :target: https://fedorahosted.org/sssd/attachment/wiki/DesignDocs/SUDOSupport/sssd1.png
.. |SUDO plugin in action| image:: https://fedorahosted.org/sssd/raw-attachment/wiki/DesignDocs/SUDOSupport/SUDO2.png
   :target: https://fedorahosted.org/sssd/attachment/wiki/DesignDocs/SUDOSupport/SUDO2.png
.. |image2| image:: https://fedorahosted.org/sssd/raw-attachment/wiki/DesignDocs/SUDOSupport/sudoPlugin.png
   :target: https://fedorahosted.org/sssd/attachment/wiki/DesignDocs/SUDOSupport/sudoPlugin.png
.. |SUDO responder checks the cache| image:: https://fedorahosted.org/sssd/raw-attachment/wiki/DesignDocs/SUDOSupport/SUDO4.png
   :target: https://fedorahosted.org/sssd/attachment/wiki/DesignDocs/SUDOSupport/SUDO4.png
.. |SUDO provider connects to LDAP server| image:: https://fedorahosted.org/sssd/raw-attachment/wiki/DesignDocs/SUDOSupport/SUDO6.png
   :target: https://fedorahosted.org/sssd/attachment/wiki/DesignDocs/SUDOSupport/SUDO6.png
