<div class="wiki-toc">

1.  1.  [LDAP Referrals](#LDAPReferrals)
        1.  [Pre-requisites](#Pre-requisites)
            1.  [sdap\_id\_op enhancements](#sdap_id_openhancements)
        2.  [Single-entry lookup](#Single-entrylookup)
        3.  [Multiple-entry lookup](#Multiple-entrylookup)
        4.  [Optimizations](#Optimizations)
        5.  [Relationship to multiple search
            bases](#Relationshiptomultiplesearchbases)
        6.  [Questions needing research](#Questionsneedingresearch)
        7.  [Stuff to Test](#StufftoTest)

</div>

LDAP Referrals {#LDAPReferrals}
--------------

### Pre-requisites {#Pre-requisites}

#### sdap\_id\_op enhancements {#sdap_id_openhancements}

1.  Disentangle sdap\_id\_op setup from failover configuration
2.  Handle async resolver needs for referrals. We need to look up
    referred servers and take the first IP returned by DNS.
3.  Add idle disconnection timer for connections (see Ticket
    [\#1036](https://fedorahosted.org/sssd/ticket/1036 "enhancement: [RFE] close LDAP connection to the server when idle for some ... (closed: fixed)"){.closed
    .ticket}, needs to have its priority bumped up). We don't want to be
    hanging onto referred servers forever.

### Single-entry lookup {#Single-entrylookup}

1.  Perform lookup on standard server connection
2.  Get referral reply
3.  Acquire sdap connection to the referred server
4.  Perform lookup on referred server
5.  Repeat as needed until referral depth limit is reached

### Multiple-entry lookup {#Multiple-entrylookup}

First approximation: just process each referral as a series of
single-entry lookups, gathering all results at the end.

### Optimizations {#Optimizations}

1.  Keep lookup cache/hashtable of entries pointing to the same referred
    entry (I suspect the value is low here, as the chance of multiple
    replies referring to the same entry is unlikely).
2.  In the case of multiple referred entries to the same LDAP server,
    can we bundle them into single requests? (Probably not. Referrals
    will end up requiring BASE searches. Most LDAP servers don't support
    subtree searches on DN)
3.  Keep a hash/lookup table of sdap\_id\_op links. Don't reconnect
    unless we have to (such as when performing auth via LDAP simple
    bind).
    1.  Keep separate sdap\_id\_op links for ID and AUTH. ID always uses
        the default bind credentials, AUTH can drop the bind and
        reconnect.

### Relationship to multiple search bases {#Relationshiptomultiplesearchbases}

Only the primary server will need multiple bases. The referrals will end
up as base searches, thereby ignoring the multiple search base values.

Referrals should *ignore* the base filtering of ticket
[\#960](https://fedorahosted.org/sssd/ticket/960 "defect: ldap_*_search_base doesn't fully limit the group / netgroup search base ... (closed: fixed)"){.closed
.ticket}.

How do we handle originalDN? I think we need to save originalDN as it
would have appeared on the primary server, not the referred server.

Research: how are we doing this now? I remember that we hit this before
when dealing with referrals. Did we solve it for all referral types or
only some?

Finally, related to the search filtering, ticket
[\#960](https://fedorahosted.org/sssd/ticket/960 "defect: ldap_*_search_base doesn't fully limit the group / netgroup search base ... (closed: fixed)"){.closed
.ticket} should do its filtering based on the originalDN value, not the
referred DN.

### Questions needing research {#Questionsneedingresearch}

1.  Do all referrals give a complete answer? (i.e. If they refer
    locally, is it relative?)
    -   [[​]{.icon}http://www.ietf.org/rfc/rfc3296.txt](http://www.ietf.org/rfc/rfc3296.txt){.ext-link}
        says that "The ref attribute values SHOULD NOT be used as a
        relative name-component of an entry's DN \[RFC2253\]."
2.  Can we keep a connection open to rebind? i.e. If we're performing
    AUTH, do we have to open a new socket connection to perform a new
    simple bind, or can we drop and bind again?)
3.  How do we treat unreachable referral servers?
    1.  As missing entries. This might cause cache issues with flaky
        networks, as we always treat missing entries as definitive
        deletion of the entry for our cache. I believe this is how
        things are handled now with the openldap internal referral
        chasing, but I need to research this.
    2.  Any unreachable referral server results in SSSD going offline.
        This is potentially chaotic, as it introduces multiple points of
        failure resulting in offline operation.
    3.  Flag unreachable entries as "complete", thereby having SSSD rely
        on their presence or abscence in the cache. While this sounds
        nice in theory, I think this would probably be very difficult to
        get right, especially with enumeration. I recommend deferring
        this as a future optimization and going with one of the other
        approaches (or possibly make the other approaches into an
        sssd.conf option).
4.  How do we handle nested referrals?
    -   Option: Handle all referrals at a particular depth before
        descending further. This can help avoid attempts to create
        duplicate sdap\_id\_ops. The downside to this approach is that
        situations where entries are coming from multiple servers will
        only ever function as quickly as the slowest server in the set.
    -   Option: Track nestings as additional subreq levels. Add careful
        sdap\_id\_op acquisition locking and proceed into nestings as
        quickly as they are available. This is more complicated to get
        right, but probably will provide a noticeable gain in complex
        setups.

### Stuff to Test {#StufftoTest}

1.  Entry referrals
    1.  Same server different DN
    2.  Different server same DN
    3.  Different server different DN
2.  Subtree referrals
    1.  Same server different DN
    2.  Different server different DN
3.  Referral on bind attempt (referred AUTH)
4.  Referred password change

