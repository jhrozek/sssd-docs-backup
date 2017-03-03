Troubleshooting DNS update issues {#TroubleshootingDNSupdateissues}
=================================

Check SSSD configuration {#CheckSSSDconfiguration}
------------------------

First of all, check if options `dyndns_update`,
`dyndns_refresh_interval`, `dyndns_update_ptr`, and `dyndns_ttl` have
desired values in `/etc/sssd/sssd.conf`.

Default values depend on selected provider. For Active directory see
`man 5 sssd-ad`, for FreeIPA see `man 5 sssd-ipa` etc. For further
information please see `man 5 sssd.conf`.

Make SSSD logs useful {#MakeSSSDlogsuseful}
---------------------

Set `debug_level=8` (or higher) so the log shows exact messages from
`nsupdate` tool.

In the logs, look for trailer `-- Begin nsupdate message --` and
messages beneath it. This is the interesing part.

Try nsupdate yourself {#Trynsupdateyourself}
---------------------

For easier debugging you can run `nsupdate` yourself. Copy&paste input
for `nsupdate` from logs to a separate file and play with it (e.g. add
`debug` statement to the input).

1.  Obtain machine ticket: `$ kinit -kt`
2.  Run nsupdate: `$ nsupdate -g /tmp/commands_copied_from_log_file`

Verify DNS configuration {#VerifyDNSconfiguration}
------------------------

As a first step, `nsupdate` auto-detects DNS zone name and server
responsible for the DNS zone. This information is printed out if `debug`
statement is present in nsupdate's input.

It looks like this:

``` {.wiki}
Reply from SOA query:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id:  32531
;; flags: qr rd ra; QUESTION: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 0
;; QUESTION SECTION:
;name.to.be.updated.example.com.    IN  SOA

;; AUTHORITY SECTION:
example.com.        0   IN  SOA ns01.example.com. noc.example.com. 2016072000 300 180 604800 600

Found zone name: example.com
The master is: ns01.example.com
Sending update to 192.0.2.1#53
```

Check that:

-   The `Found zone name` must match zone name configured on DNS
    servers.
-   `The master is` must contain name of Primary Master DNS server which
    accepts DNS updates. This value is taken from `MNAME` field in the
    `SOA` record.
-   Message `Sending update to` contains correct IP address of the
    Primary Master DNS server.

If any of the above is not correct the problem is likely not caused by
SSSD but by DNS configuration:

-   Double-check SOA record for particular zone in DNS.
-   Make sure that servers listed in `/etc/resolv.conf` return correct
    answers.

Check DNS server's logs {#CheckDNSserverslogs}
-----------------------

The DNS server can reply with multiple various error codes. Look for
trailer `Reply from update query:` (it might appear multiple times) and
check all `status` codes:

``` {.wiki}
Reply from update query:
;; ->>HEADER<<- opcode: UPDATE, status: REFUSED, id:  10871
```

In this case server replied with error `REFUSED`. Most likely, the
access controls on the DNS server do not allow this particular client to
issue DNS updates for given DNS name/type/etc. Check logs at Primary
Master DNS server and see what information got logged there.
