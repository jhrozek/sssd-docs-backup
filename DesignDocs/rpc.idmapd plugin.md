<div class="wiki-toc">

1.  1.  [rpc.idmapd plugin](#rpc.idmapdplugin)
    2.  [SSS NFS Client (rpc.idmapd plugin) -
        Design](#SSSNFSClientrpc.idmapdplugin-Design)
        1.  [rpc.idmapd - background](#rpc.idmapd-background)
        2.  [SSSD - Responder](#SSSD-Responder)
        3.  [SSSD - NFS Client](#SSSD-NFSClient)
        4.  [Optimisation Techniques](#OptimisationTechniques)
        5.  [Configuration File](#ConfigurationFile)

</div>

rpc.idmapd plugin {#rpc.idmapdplugin}
-----------------

------------------------------------------------------------------------

\

SSS NFS Client (rpc.idmapd plugin) - Design {#SSSNFSClientrpc.idmapdplugin-Design}
-------------------------------------------

The client is named "**sss\_nfs**" (althogh "sss\_idmap" or "idmap"
might have been better names, the term "idmap" is already occupied in
the SSSD world).

### rpc.idmapd - background {#rpc.idmapd-background}

rpc.idmapd runs on NFSv4 servers as a userspace daemon (part of
nfs-utils). Its role is to assist knfsd by providing the following 6
mapping functions:

1.  (user) name to uid
2.  (group) name to gid
3.  uid to (user) name
4.  gid to (group) name
5.  principal (user) name to ids (uid + gid)
    ^([(1)](https://fedorahosted.org/sssd#krbnote))^
6.  principal (user) name to grouplist (groups which user are member of)
    ^([(1)](https://fedorahosted.org/sssd#krbnote))^

rpc.idmapd provides API for developing plugins (loaded by `dlopen(3)`)
which implements the actual mapping process.

On the kernel level, there's a caching mechanism for the responses from
the userspace daemon.

[]{#krbnote .wikianchor}^(1)^ Items 5 + 6 are only relevant for
kerberised NFSv4 servers. At the first stage only there won't be
kerberos support.

### SSSD - Responder {#SSSD-Responder}

The functionality required from the Responder side is a subset of the
functionality provided by existing NSS Responder's commands.

As you can see below (on the client part of the design) - no changes are
needed in the NSS Responder.

### SSSD - NFS Client {#SSSD-NFSClient}

Responder-Facing Interactions (existing NSS Responder commands)

-   `SSS_NSS_GETPWNAM` - map (user) name to uid requests
-   `SSS_NSS_GETGRNAM` - map (group) name to gid requests
-   `SSS_NSS_GETPWUID` - map uid to (user) name requests
-   `SSS_NSS_GETGRGID` - map gid to (group) name requests

The request & reply sent to & from the responder is "standard" in terms
of the NSS Responder.

The client only needs a portion of the reply. Only this portion will be
extracted from the packet (i.e. uid/gid/user name/group name).

### Optimisation Techniques {#OptimisationTechniques}

The optimisation techniques used for the NSS client will be used here as
well. i.e. Fast Cache (memcache) & negative-cache.

It will be possible for the user to disable Fast Cache from the
configuration file. (see below)

### Configuration File {#ConfigurationFile}

The configuration of the client will be part of rpc.idmap config file
(`/etc/idmapd.conf`).