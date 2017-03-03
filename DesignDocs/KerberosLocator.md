<div class="wiki-toc">

1.  [Kerberos Locator Plugin](#KerberosLocatorPlugin)
    1.  [Old Design](#OldDesign)
        1.  [Limitations](#Limitations)
    2.  [New Design](#NewDesign)
        1.  [Locator Plugin](#LocatorPlugin)
        2.  [Locator Responder](#LocatorResponder)
            1.  [Locator Responder-Client Wire
                Protocol](#LocatorResponder-ClientWireProtocol)
                1.  [Request](#Request)
                2.  [Replies](#Replies)
                    1.  [Reply Address Data](#ReplyAddressData)
                    2.  [Reply Address Data String
                        representation](#ReplyAddressDataStringrepresentation)
            2.  [Responder Behavior](#ResponderBehavior)
        3.  [Kerberos Provider Extensions](#KerberosProviderExtensions)
            1.  [SBUS Protocol](#SBUSProtocol)
            2.  [Address Resolution](#AddressResolution)

</div>

Kerberos Locator Plugin {#KerberosLocatorPlugin}
=======================

Old Design {#OldDesign}
----------

The current Kerberos locator plugin functions as follows:

1.  The krb5 provider would write a file,
    `/var/lib/sss/pubconf/kdcinfo.REALM` consisting of a single line,
    the IP address and port of the KDC being used.
2.  The kerberos locator plugin would read in this file and return the
    IP address and port to the requesting application.

### Limitations {#Limitations}

-   The locator provides only a single address and is only updated when
    the krb5 provider in the SSSD service connects to a new KDC.
-   If the KDC we last authenticated against becomes unreachable, but
    other KDCs in a failover configuration remain up, applications
    relying on libkrb5 will fail to access those failover servers.

New Design {#NewDesign}
----------

### Locator Plugin {#LocatorPlugin}

The Kerberos locator plugin will be reinvented as an sss\_client object.
It will retain minimal logic in itself except as follows:

1.  It will communicate across a socket to the Locator Responder
    (sssd\_locator).
2.  We will optionally implement an in-memory cache similar to that of
    the NSS clients.
3.  This communication and caching will support retrieving multiple
    address/port pairs in a single transaction.

### Locator Responder {#LocatorResponder}

#### Locator Responder-Client Wire Protocol {#LocatorResponder-ClientWireProtocol}

##### Request {#Request}

  ------- ---------------------
  Bytes   Function
  0-4     Message Length
  4-7     Locate Service Type
  9-11    Socket Type
  12-15   Protocol Family
  16-19   Length of realm
  20-XX   Realm
  ------- ---------------------

##### Replies {#Replies}

  ------- -----------------------
  Bytes   Function
  0-3     Length of the message
  4-7     Number of addresses
  8-X     Address Data
  ------- -----------------------

A reply with zero addresses should be interpreted by the client as SSSD
not being aware of the requested realm. This should be treated as
KRB5\_PLUGIN\_NO\_HANDLE.

###### Reply Address Data {#ReplyAddressData}

  ------- ----------------------------------
  Bytes   Function
  0-3     Port
  4-7     Size of address
  8-X     String representation of address
  ------- ----------------------------------

###### Reply Address Data String representation {#ReplyAddressDataStringrepresentation}

-   IPv4: numbers-and-dots notation as supported by inet\_aton(3)
-   IPv6: hexadecimal string format as supported by inet\_pton(3)
-   This is done so the string can be passed directly to getaddrinfo()
    in the locator plugin.

#### Responder Behavior {#ResponderBehavior}

The responder will receive requests from the locator plugin. It will
parse the realm from the wire protocol and use that to determine which
(if any) KRB5 auth or chpass provider is available for that realm. It
will then query that provider via the SBUS to get an appropriate list of
addresses. Once this reply is made, the responder will answer the
locator plugin client.

The responder MUST enqueue multiple requests for the same realm
together, so that fewer trips to the provider will be required.

Once the responder returns, the results SHOULD be added to an in-memory
cache similar to that offered by the NSS responder.

For compatibility with applications that have older versions of the
locator still loaded, the responder MUST write out a
`/var/lib/sss/pubconf/kdcinfo.REALM` file containing the first address
in the set returned from the provider.

### Kerberos Provider Extensions {#KerberosProviderExtensions}

#### SBUS Protocol {#SBUSProtocol}

TBD

#### Address Resolution {#AddressResolution}

The provider SHOULD reply with potential addresses even if the provider
is in offline mode. This is to ensure that the locator plugin can
accurately return data if the KDCs become available again before the
SSSD notices (by performing an online authentication or password-change)

If the provider is online, it MUST return the KDC it last communicated
with as the first address in the response list. The provider MUST return
up to N-1 (configurable) total addresses from its available pool. For
example, if the configuration specifies

``` {.wiki}
krb5_locator_addresses = 3
```

and the KDC is online, it MUST return the KDC it is connected to,
followed by the next two servers in the failover list, or fewer if only
one or two exist in total.

TBD
