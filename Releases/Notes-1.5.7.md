``` {.wiki}
====== SSSD Security Release 1.5.7 ==========================
=
= Subject:          User impersonation attack
=
= CVE ID#:          CVE-2011-1758
=
= Summary:          The current stable and development version
=                   of SSSD are vulnerable to a user
=                   impersonation attack.
=
= Impact:           moderate
=
= Affects default
=  configuration:   Negative
=
= Introduced with:  1.5.0
=
===============================================================

============
DESCRIPTION

The current stable and development version of SSSD are vulnerable to a
user impersonation attack.

A malicious user can log in as a legitimate user by using a well-known
plain text under specific circumstances.

The user's legitimate credentials are *not* disclosed.

The vulnerability is present if the automatic ticket renewal option is
enabled, and only if a ticket renewal operation for the user has been
recently performed without any further authentication from the
legitimate user taking place since.

The vulnerability is exploitable only if the SSSD daemon is
authenticating in offline mode (servers not reachable), and offline
authentication is enabled.

The vulnerability is rated moderate due to the fact the vulnerability is
present only in non default configurations and the vulnerability is
available only after a very specific set of circumstances materializes.

==================
PATCH AVAILABILITY

A patch addressing this issue is available at:
http://git.fedorahosted.org/git/?p=sssd.git;a=commitdiff_plain;h=fffdae81651b460f3d2c119c56d5caa09b4de42a

===========
WORKAROUND

Disable automatic ticket renewal and flush sssd caches to remove bad
cached credentials.

=======================
ADDITIONAL INFORMATION

The automatic ticket renewal service in SSSD operates by providing the
active credential cache to the kerberos libraries in order to renew the
user's TGT on their behalf by using their existing credentials.
Internally, SSSD treats this as a standard authentication, which upon
success will update the cached credentials of the user.

The side-effect here is that the user's credentials in the context of
this renewal are actually the path to the credential cache file,
instead of their real password. So as a result, the user's cached
credentials have now become a different string.

The security issue is that this new cached-credential string is now
predictable. Another user on the local system would now be capable of
logging in as the first user by performing an 'ls /tmp' and seeing what
the first user's cache file is called.

The problem gets further complicated if the administrators has modified
the SSSD config option 'krb5_ccache_template' to remove the mkstemp()
suffix. This would then make the credential cache's name predictable to
a network attacker as well.

With this release, we no longer erroneously set the credential cache
path as the user's cached credentials, removing this vulnerability and
restoring the user's ability to log in properly in offline mode.

========
CREDITS

Thanks to Marko Myllynen (Red Hat) for reporting and to Stephen
Gallagher for identifying the actual problem.


The SSSD team.

====================================
```
