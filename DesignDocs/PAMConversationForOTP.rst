PAM Conversation for OTP/Two-Factor-Authentication
==================================================

Related ticket(s):

-  `​https://fedorahosted.org/sssd/ticket/2335 <https://fedorahosted.org/sssd/ticket/2335>`__

Problem statement
~~~~~~~~~~~~~~~~~

Two-Factor-Authentication (2FA) typically uses a long term password or
PIN and an One-Time-Password (OTP) which in general is generated by a
small device. To be backward compatible and to allow 2FA in existing
application both factors can be entered one after the other in a single
password prompt. This single string is then evaluated by the
authentication backend.

On desktop systems where a single password (One-Factor-Authentication -
1FA) is used this password is often used for other purposes to improve
the user experience. For example to

-  unlock a keyring
-  un-encrypt files or the complete home-directory
-  allow authentication even if the authentication backend is not
   reachable (offline authentication).

These convenience features are not available if 2FA is used with both
factors combined in a single string because there is no general rule
which would allow to split the long-term and the one-time part. Only the
authentication backend knows how to handle it. To make these features
possible again with 2FA the user must enter the two factors individually
into two separate prompts. This design page will show how this can be
achieved with the help of PAM and SSSD.

Use cases
~~~~~~~~~

Unlock user's keyring
^^^^^^^^^^^^^^^^^^^^^

Assuming a user with 2FA enabled which log into a desktop session. If
the two factors are entered into a single prompt the resulting string
cannot be used as a password for the desktop keyring application because
it will change at every login. To not create issues SSSD will
automatically remove the password item from the PAM environment in this
case (see `#2287 <https://fedorahosted.org/sssd/ticket/2287>`__ for
details).

If the two factors are entered separately the first factor, the
long-term password, can but used as a password for the keyring
application because changes will be rare. In this case SSS can put the
long term password into the PAM environment so that the PAM modules of
the keyring application can pick it up at login time so that there is no
need to unlock the keyring in a separate step.

Offline-authentication
^^^^^^^^^^^^^^^^^^^^^^

Assuming a user with 2FA enabled which log into a desktop session which
currently does not have a connection to the central authentication
server. If the two factors are entered into a single prompt the
resulting string can only be processed by the central authentication
server and a loss of connection will make authentication and login
impossible. Even the SSSD offline-authentication feature won't help
because SSSD will only store a hash of the password used for the last
successful authentication and compare it with the hash of the current
password. Since the combined password will change at every login the
current combined password cannot be validated against any previously
used password.

If the two factors are entered separately SSSD can save a hash of the
first factor and can compare the hashes for the first factor when
offline to allow at least access to the local machine. It has to be
noted that the even if krb5\_store\_password\_if\_offline is set to true
SSSD will not try to get a TGT when going online again because in the
general case the second factor (OTP) might be already invalid.

Both use-cases mentioned above might only be working if the first factor
(long-term password) is sufficiently long. A 4-digit PIN used by some
OTP systems is not secure enough to be uses as a password for a keyring
or to allow local access.

Overview of the solution
~~~~~~~~~~~~~~~~~~~~~~~~

One of the design principles of SSSD's PAM module pam\_sss was that it
should not do any decisions on its own but let SSSD do them. As a
consequence, pam\_sss cannot decide which type of password prompt should
be shown to the user but must ask SSSD first. Currently the first
communication between pam\_sss and SSSD's PAM responder happens after
the user entered the password. Hence a new request, a pre-authentication
request, to the PAM responder must be added before the user is prompted
for the password. The pam responder can then relay the request to a
suitable backend where it can be evaluated which type of prompt should
be shown to the user. The result can be send back to pam\_sss in a PAM
response message which is already use to return other types of messages
to pam\_sss. This message can be used to send additional hints like e.g.
type or vendor of the expected OTP hardware token to the user.

Based on the response pam\_sss will ask the user for a single password
or for the two factors in individual prompts. If only the first factor
is entered and the second is empty the input will be treated as a single
password. This might happen is the user accidentally entered both factor
together or if applications or protocols (ssh, ftp) are configured or
can handle only a single password prompt.

To keep the delays due to the new request to a minimum pam\_sss should
only run it, if the backend really supports it. Additionally is should
be possilbe to disable the pre-authentication request completely with a
new option for pam\_sss.

In addition to the authentication dialog the password change dialog
should respect the splitting of the two factors as well.

Implementation details
~~~~~~~~~~~~~~~~~~~~~~

Making sure the PAM calls SSSD the ask for credentials for SSSD users
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

PAM allows to configure multiple different authentication methods but
ideally only ask the user once for a password (or other credentials).
Typically the first configure authentication method will ask for a
password and if the user is not know to the authentication method the
password is passed on to the next authentication method. Obviously this
only works well with a single type of credentials.

In our case we want to prompt the user differently depending on whether
1FA or 2FA is configured for the user. Typically pam\_unix is the first
authentication module to make sure the authentication of local users
(especially root) is not affected by other modules. But since pam\_unix
does not know anything about SSSD users or 2FA we have to make sure that
pam\_unix will not ask for a password for SSSD users. Instead of putting
pam\_sss in front of pam\_unix we would like to use pam\_localuser to
skip pam\_unix for non-local users. A PAM auth configuration might look
like this

.. code:: wiki

    auth        required               pam_env.so
    auth        [default=1 success=ok] pam_localuser.so
    auth        sufficient             pam_unix.so nullok try_first_pass
    auth        requisite              pam_succeed_if.so uid >= 1000 quiet_success
    auth        sufficient             pam_sss.so
    auth        required               pam_deny.so

If the user is in /etc/passwd pam\_localuser will return success and
pam\_unix will be called. Otherwise the next entry (default=1) will be
skipped which is pam\_unix in this case. The next module for a user
which does not come from /etc/passwd if pam\_succeed\_if. I think it is
a good idea to keep the pam\_succeed\_if to keep the separation between
local users (uid < 1000) and remote users (uid >= 1000).

For the time being we keep the PAM password section (for password
changes) as is because it is already used to handle changing the
long-term password.

Handling the two authentication factors
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Both the wire protocol between pam\_ssd and the pam responder and SSSD
internally with the sss\_auth\_token struct handle the credentials as a
blob with a length and a type. Currently the blob contains either the
password or is NULL in case of no password (there is a special usage
where it contains a Kerberos credential cache identification).

Adding the two authentication factor to those structures can be achieve
without modifying them by using a new type for 2FA and creating a blob
which starts with two 32bit unsigned integer value containing the size
of the first and second authentication factor respectively followed by
the first factor and finally the second factor.

.. code:: wiki

    uint32_t | uint32_t | uint8_t[6] | uint8_t[5]
    ---------|----------|------------|-----------
    0x06     | 0x06     | abcdef     | 12345\0

As shown the first and second factor may or may not include a trailing
\\0 in the blob. But calls which decompose the blob into its component
must assure that that there is a trailing \\0 if strings are expected.

With this scheme only packaging and un-packaging the two factors has to
be added to existing or new calls but all other internal handling like
sending the data from the responder to the backends can be left
unchanged.

Backends which should handle 2FA must be made aware of the new
authentication token type.

The pre-authentication request
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The pre-authentication request will follow the same path as the
authentication request with an empty password and with type
SSS\_PAM\_PREAUTH instead of SSS\_PAM\_AUTHENTICATE. It is up to the
backend if and how this request will be handled. Currently only the IPA
auth provider will support the pre-auth request in the sense that it can
send different results base on the expected authentication type (1FA,
2FA) back to the client. Since the IPA provider will basically use the
generic krb5 auth provider the krb5 auth provider will support the
pre-auth request as well.

The IPA provider will send a back a PAM response of the type
SSS\_PAM\_OTP\_INFO in case of 2FA with optional token\_id, vendor name
and challenge so that pam\_sss can give additional hints to the user and
a unsigned 32bit integer value indication the type of the optional data.
This indicator will make it more easy to add more data in future or just
indicate that the user uses 2FA but the backend is offline.

If 2FA is not enabled for the user or errors occur just a PAM\_SUCCESS
will be returned. In this case pam\_sss will just ask for a single
password.

If the backend is offline the PAM responder will tell the client that
only the first factor is needed for local authentication with the help
of a special SSS\_PAM\_OTP\_INFO message. To achieve this the type of
the hashed authentication token in the cache must be saved. Additionally
the length of the second factor should be saved in the cache to allow
splitting a combined password which might be entered by the user
accidentally or via services where special prompting might not be
available like e.g. ssh. If the second factor varies in size this scheme
will fail but saving the length of the first factor will make an offline
attack against the hashed password much easier.

Since the pre-auth request is an additional round-trip from pam\_sss to
the KDC and back it might delay the logon process a bit. To avoid this
in environments where only 1FA is used and option the pam\_sss,
*disable\_preauth*, can disable the pre\_auth request completely.
Additionally I would suggest a more dynamic solution where is pre-auth
request is only send if a special file, e.g.
/var/lib/sssd/pubconf/do\_pam\_preauth, exits. The IPA provider can
create this file at startup if 2FA is supported.

Special use of the first factor (long term password)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Cached password hash for offline-authentication
'''''''''''''''''''''''''''''''''''''''''''''''

If authentication was successful, the *cache\_credentials* option is set
to *true* and the first factor has at least
*`minimal\_password\_length <https://fedorahosted.org/sssd#minimal_password_length>`__*
SSSD will saved a hashed version of the first factor to the user's cache
entry as it is done for the 1FA password.

PAM
'''

If authentication is successful and the *forward\_pass* option is given
for pam\_sss the first factor will be saved in the PAM\_AUTHTOK item so
that other modules in the PAM stack can use it. **QUESTION: shall
we(authconfig) add forward\_pass by default? Currently is it not.**

Configuration changes
~~~~~~~~~~~~~~~~~~~~~

pam\_sss
^^^^^^^^

New options:

-  *disable\_preauth* will unconditionally disable the
   pre-authentication request
-  *use\_2fa* will always ask for two authentication factor, might be
   only useful for testing

sssd.conf
^^^^^^^^^

New option:

-   *minimal\_password\_length* will let the pam responder only save a
   hash of the password if it has a minimal length. Additionally it
   might indicate to pam\_sss to remove passwords from the PAM
   environment which are shorter. **Question: We can limit this option
   to the first factor of a 2FA authentication. Although it might be
   useful for 1FA passwords as well it might introduce a regression to
   existing installations.**

Changing the first factor
^^^^^^^^^^^^^^^^^^^^^^^^^

It is already possible to change the long-term password (first factor),
the current scheme will not be changed here.

How To Test
~~~~~~~~~~~

Prerequisites
^^^^^^^^^^^^^

Create an user with 2FA/OTP authentication as e.g. described in
`​http://www.freeipa.org/page/V4/OTP#Configuration <http://www.freeipa.org/page/V4/OTP#Configuration>`__

Login prompt
^^^^^^^^^^^^

If 2FA is enabled for a user there should be two separate prompts for
the two authentication factors for services which can support special
prompting. This includes e.g. gdm and su. ssh can only support this if
*`ChallengeResponseAuthentication? <https://docs.pagure.org/sssd-test2/ChallengeResponseAuthentication.html>`__*
is enabled on the server side. Nevertheless even if
*`ChallengeResponseAuthentication? <https://docs.pagure.org/sssd-test2/ChallengeResponseAuthentication.html>`__*
is not enabled ssh should allow login if both factors are given at the
password prompt in a single string.

For users without 2FA the single password prompt should be seen.

.. code:: wiki

    # su - otpuser
    First factor:
    Second factor:
    sh$

.. code:: wiki

    # su - user
    Password:
    sh$

If both factors are entered at the *First factor* prompt and the second
factor prompt is empty, authentication should be successful but it
cannot be expected that the user's keyring is unlocked or that
offline-authentication will be available.

Unlocking user's keyring
^^^^^^^^^^^^^^^^^^^^^^^^

If an otpuser logs in with gdm and enters the two authentication factors
separately in the expected prompts the keyring of the user should be
unlocked automatically and no additional password prompt should be seen
after logging in.

Offline authentication
^^^^^^^^^^^^^^^^^^^^^^

If an otpuser logs in with an application which supports special
prompting, e.g. gdm or su, and the SSSD configuration option
*cache\_credentials* is set to *True* SSSD will save a hash of the first
factor in the cache to allow offline authentication. If later on the
system goes offline authentication should still be possible with the
first authentication factor. Only a prompt for the first factor should
be shown by application which supports special prompting.

Authors
~~~~~~~

Sumit Bose <`​sbose@redhat.com <mailto:sbose@redhat.com>`__>
