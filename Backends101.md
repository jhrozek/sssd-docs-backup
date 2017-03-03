(08:40:21 AM) **sgallagh:** Ok, so let's talk SSSD Backends 101\
(08:41:02 AM) **sgallagh:** pzuna: I assume you're planning to build an
open-source backend within our existing framework?\
(08:41:23 AM) **pzuna:** sgallagh: you assume right :)\
(08:41:24 AM) **sgallagh:** (Closed-source backends have a completely
different - and unfinished - interface)\
(08:42:10 AM) **pzuna:** open source backend for winbind, but I just
read in the design docs, that it&apos;s supposed to be somehow a part of
the IPA backend... didn&apos;t have time to read the whole wall of text
there, so I don&apos;t know if I got it right\
(08:42:17 AM) **sgallagh:** Ok, so the first thing to understand is that
we have a set of generic wrapper code for back-ends\
(08:43:52 AM) **sgallagh:** In the SSSD source tree, this is located in
src/providers/data\_provider\_be.c\
(08:44:46 AM) **sgallagh:** There are currently four backend types that
can be implemented.\
(08:45:09 AM) **sgallagh:** ID, AUTH, ACCESS and CHPASS\
(08:46:59 AM) **sgallagh:** in order to provide these interfaces, a
plugin must present a function named
sssm\_&lt;backend\_name&gt;\_&lt;backend\_type&gt;\_init()\
(08:47:11 AM) **sgallagh:** e.g. sssm\_ldap\_id\_init()\
(08:48:54 AM) **sgallagh:** This init function must take a 'struct
be\_ctx \*' as input and return 'struct bet\_ops \*' and 'void \*' to
the caller.\
(08:49:14 AM) **sgallagh:** The bet\_ops are the set of callback points
that the sssd\_be process will invoke to do the heavy lifting\
(08:50:00 AM) **sgallagh:** The definition for 'struct bet\_ops' can be
found in src/providers/dp\_backend.h\
(08:50:41 AM) **sgallagh:** Each backend type can provide up to three
callbacks: handler, check\_online and finalize\
(08:52:06 AM) **sgallagh:** Each of these callbacks receives a single
argument, a 'struct be\_req' (also described in dp\_backend.h)\
(08:54:41 AM) **sgallagh:** The most important piece of the be\_req is
the be\_req-&gt;req\_data void pointer.\
(08:54:48 AM) **pzuna:** sgallagh: what&apos;s supposed to be returned
in the third argument of sssm\_&lt;backend&gt;\_&lt;type&gt;\_init?
(void \*\*pvt\_data)\
(08:55:13 AM) **sgallagh:** pzuna: That's private data for the provider
that you may need. Such as an initialized context.\
(08:55:26 AM) **pzuna:** ok\
(08:55:47 AM) **sgallagh:** That will always be passed back to you as
be\_ctx-&gt;bet\_info\[BET\_ID\].pvt\_bet\_data\
(08:56:00 AM) **sgallagh:** Which you can then re-cast into the
appropriate type\
(08:56:53 AM) **sgallagh:** just a second\
(08:57:07 AM) **pzuna:** ok, I see it in the sssm\_ldap\_id\_init
function, makes sense\
(08:58:50 AM) **sgallagh:** Ok, so the req\_data void pointer\
(08:59:10 AM) **sgallagh:** For ID providers, this needs to be cast to a
'struct be\_acct\_req \*'\
(08:59:48 AM) **sgallagh:** For the other three provider types, this
would be cast to 'struct pam\_data \*'\
(09:01:49 AM) **sgallagh:** So between the pvt\_bet\_data and the
req\_data, you should have all information necessary to perform a user
lookup or a PAM action\
(09:03:12 AM) **sgallagh:** The responsibility of the backend is to
populate the sysdb cache with updated information from the directory\
(09:03:37 AM) **sgallagh:** (I'll get into that more in a bit)\
(09:05:06 AM) **sgallagh:** So once the backend performs an identity
lookup, it needs to do one of two things in the sysdb. If the
user/group/netgroup existed in the directory, then it needs to update
the sysdb cache with the latest information. If the entry did NOT exist,
then the sysdb must be purged of the same entry (if it previously
existed)\
(09:06:08 AM) **sgallagh:** Once the sysdb is updated, the
be\_req-&gt;fn() should be called with a DP\_ERR\_OK for the second
argument, which informs the responders that it's okay to return the
updated information from the cache.\
(09:07:12 AM) **sgallagh:** If for one reason or another the directory
is unreachable, the provider should be marked offline with the
be\_mark\_offline() function and be\_req-&gt;fn() should be called with
DP\_ERR\_OFFLINE\
(09:08:51 AM) **sgallagh:** Behavior for the auth and chpass providers
are very similar, except that instead of caching user data, the
sysdb\_cache\_password() function would be used to store successful
passwords (if and only if cache\_password = true in sssd.conf)\
(09:09:22 AM) **sgallagh:** (sorry, cache\_credentials, not
cache\_password)\
(09:11:04 AM) **sgallagh:** When returning information for AUTH or
CHPASS, you need to send back both DP\_ERR\_OK or DP\_ERR\_OFFLINE as
well as the pam\_result (e.g. PAM\_SUCCESS, PAM\_PERM\_DENIED, etc.).\
(09:11:15 AM) **sgallagh:** (also for ACCESS)\
(09:11:27 AM) **sgallagh:** pzuna: Questions so far?\
(09:12:48 AM) **pzuna:** sgallagh: everything makes sense so far,
I&apos;ll probably have questions when I start implementing the backend
:)\
(09:13:05 AM) **sgallagh:** I'm sure\
(09:13:34 AM) **sgallagh:** The biggest gotcha is that you have to
remember that the ID provider does NOT return results directly\
(09:13:48 AM) **sgallagh:** It always stores them in the sysdb\

