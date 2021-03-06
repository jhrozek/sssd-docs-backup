.. raw:: html

   <div class="wiki-toc">

#. 

   #. `Kerberos <#Kerberos>`__

      #. `Automatic TGT Acquisition <#AutomaticTGTAcquisition>`__
      #. `Automatic Ticket Renewal <#AutomaticTicketRenewal>`__

.. raw:: html

   </div>

Kerberos
--------

Automatic TGT Acquisition
~~~~~~~~~~~~~~~~~~~~~~~~~

You probably already know all about how the System Security Services
Daemon can make your offline life easier by enabling cached-credential
login to your system while you don’t have access to the central
authentication servers.

What you might not know, however, is that when using SSSD to perform
Kerberos auth, it’s also possible to configure it to automatically
acquire your network credentials when you go online. By setting the
‘krb5\_store\_password\_if\_offline’ option to ‘True’ in the
[domain/DOMAINNAME] sections of sssd.conf, you can configure SSSD to
store a user’s password when they log in while offline (for example,
working from home). Then later, if access to the network KDC is restored
(for example, connecting to the VPN), SSSD will perform a kinit on your
behalf to automatically acquire a TGT for single-sign-on with your
network resources.

Now, some of you will be saying to yourselves: “Wait, doesn’t this mean
that my password is being stored on the system in a readable way?”. This
is true but not the whole story. Yes, the password is stored on the
system in such a way that SSSD (and theoretically the root user on the
system, with some effort) can read the password. Without doing so, there
would be no way for us to acquire the ticket granting ticket on your
behalf. However, we do store the password in the most secure way
possible: in the kernel keyring. This makes it very difficult for root
to gain access to this password and essentially impossible for any
non-root process. The risk factor is not zero, which explains why this
is an optional feature, disabled by default. However, in the common
laptop case (where it’s assumed that the owner of the laptop is likely
to be its only user), this security/convenience trade-off is probably
worthwhile.

Automatic Ticket Renewal
~~~~~~~~~~~~~~~~~~~~~~~~

The second advanced Kerberos feature I’d like to discuss today is
automatic ticket renewal. User processes sometimes need access to the
user’s Kerberos credentials, even when the user is no longer logged in.
An example might be a regular cron job that the user wants to run every
day a few hours after leaving work. With traditional Kerberos
configurations, this user would be forced to remember to manually renew
his Kerberos credentials before leaving for the day, to ensure that the
expiration time on his TGT did not expire before his cron job completed.

With SSSD 1.5.0 and later, it can be configured to automatically renew
Kerberos tickets for the full renewable life of the TGT. This is
different from the automatic TGT acquisition above, as we do not need to
store the user’s Kerberos password to accomplish this. It does require
some additional configuration on the KDC server, however.

If the KDC permits users to request “renewable” TGT tickets, then what
it is allowing the user to do is to use their current TGT in place of
their password in order to acquire an updated TGT (with a later
expiration).

SSSD 1.5.0 and later can set two options to enable it to automatically
renew the user’s TGT for as long as the KDC permits.

The first option is krb5\_renewable\_lifetime. When set, it specifies
the maximum renewable duration that the SSSD will attempt to request
from the KDC. Note that this is only a request, and the KDC itself may
choose to return a much shorter duration, or disallow renewals entirely.

Assuming that a renewable ticket was granted, the second option is
krb5\_renew\_interval. This option specifies how often the SSSD should
poll to see if any of the user TGTs have gone beyond 50% of their
current lifetime. If they have, SSSD will perform a TGT renewal on the
user’s behalf, extending the lifetime of the TGT.
