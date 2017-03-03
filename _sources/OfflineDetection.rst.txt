On this page I collect some idea about offline detection in sssd and
possible implementations.

There are two main areas, how to detect if we are offline and how to
detect that we are online again. When the sssd starts it should always
assume that it is online and all configured service are available. This
means that we do not need to save the offline/online state to some
persistent storage.

How to detect that we are offline
---------------------------------

Not only system running sssd as a whole can be offline, but single
services can be offline for different reasons, too. Thus the offline
state needs to be detect for each service independently. The most
generic way is to define a service timeout in each backend. If a request
to a service last longer than the configured timeout the backend will
cancel the request and returns with an error message that the service is
temporarily unavailable. It is up to the backend to decide if there is
some additional cleanup necessary or not. For example the kerberos
backend might single the corresponding child process that it should
terminate to release system resources.

Identity component
~~~~~~~~~~~~~~~~~~

Calls the the NSS (Name Service Switch) system are in general quite
frequent and may slow down the system performance considerably if
timeouts are involved in each query. Accordingly it make sense to save
the offline state to answer all further calls from the cache. To avoid
unnecessary state switches due to short glitches in the network a
counter and a threshold value should be defined. If a single NSS call
fails due to a timeout it will increment the counter. If a NSS call is
successful it will set the counter to 0. If the counter reaches the
threshold value the backend is marked offline. Additionally it will set
an offline flag in the PONG response to the monitor.

AuthN, AuthZ component
~~~~~~~~~~~~~~~~~~~~~~

Authentication request in general do not occur very often and require a
user interaction. A not too large timeout is acceptable here. An
authentication request should always try to reach the corresponding
network service before falling back to the cache. Like in the NSS case a
successful online authentication set the offline counter of the backend
to 0 and a failed authentication due to a timeout should increment it.
Other PAM request (authorization/access control) should behave similar
except that they should not try to reach the network server if the
offline counter is above the threshold but should consult the cache
immediately.

On systems with a large number of authentication request per time where
the pending request will consume a large amount of system resources a
global online/offline switch, as suggested by Simo, might help.

How to detect that we are online again
--------------------------------------

There are a number of different way to detect changes in a system with
respect to the network. Unfortunately most of them are not portable and
will not cover all possible cases of coming back online we are
interested in. But although it might be nice to switch back from offline
to online as soon as the service is available again, I'm wondering if
this is really necessary.

AuthN, AuthZ component
~~~~~~~~~~~~~~~~~~~~~~

Because each authentication request is first send to the network service
before going to the cache, authentications automatically will be done
online if the service is available again. If the backend is marked
offline the offline counter will set set to 0.

Identity component
~~~~~~~~~~~~~~~~~~

If the sssd is answering NSS calls from the cache, i.e. the system id
offline with respect to the id provider backened, it is in my opinion
not necessary to switch to the online status as soon as the
corresponding network service becomes available again. For example a
successful online authentication will reset the offline counter of the
backend and sets the id provider to the online status again. But this
will only work if either the system is completely offline or
authentication and id are provided by the same backend. If
authentication and id provider are different, e.g. LDAP for id and
kerberos for authentication, and only the LDAP server is not available
for some time, the authentication backend will not change its state and
therefore the monitor will see no change in the status of this backend
and send no signal to the other backends.

To catch all case the id backend needs to check to online state on its
own. This can be done event based or time based. For the former when
offline every NSS call is counted and every Nth call is send to the
network service to see if it is online again. For the time based scheme
a request to the network service is scheduled for some time in the
future and if the request failed a new one is scheduled. If either case
a state change will be signaled to the monitor by the online flag in the
PONG reply and the monitor can act accordingly.
