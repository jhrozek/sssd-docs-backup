Troubleshooting SUDO {#TroubleshootingSUDO}
====================

Check if configuration of sudo and SSSD cooperation is correct {#CheckifconfigurationofsudoandSSSDcooperationiscorrect}
--------------------------------------------------------------

To check whether the basic configuration of sudo and SSSD is correct,
check */etc/nsswitch.conf* and */etc/sssd/sssd.conf* files.

-   **/etc/nsswitch.conf** must say that **sss** module is used for sudo
    service. Look for line like **"sudoers: sss"** (only SSSD is used),
    **"sudoers: files sss"** (local rules first, then SSSD) or similar.
-   **/etc/sssd/sssd.conf** must say that **sudo responder is enabled**.
    Look at \[sssd\] section and search for line **"services: nss, pam,
    sudo"** or similar.
-   In **/etc/sssd/sssd.conf** check that **sudo provider is enabled**.
    Look at \[domain\] section, sudo provider is always enabled for
    ldap, ad and ipa providers, unless this section contains
    "sudo\_provider = none".

Obtaining logs {#Obtaininglogs}
--------------

Logs can provide many useful information when finding a solution for
your troubles.

**a) How do I get sudo logs?**

1.  Open */etc/sudo.conf* and put down the following lines:

    ``` {.wiki}
    Debug sudo /var/log/sudo_debug all@debug
    Debug sudoers.so /var/log/sudo_debug all@debug
    ```

2.  Run *sudo*
3.  File */var/log/sudo\_debug* contains sudo logs

**b) How do I get SSSD logs?**

1.  Open */etc/sssd/sssd.conf* and enable logging by setting a debug
    level in *\[sudo\]* and *\[domain/\$NAME\]* section: *debug\_level =
    0x3ff0*
2.  Restart SSSD
3.  Run sudo
4.  Log files are stored in */var/log/sssd/sssd\_\$NAME.log* (domain
    log) and */var/log/sssd/sssd\_sudo.log* (sudo responder log)

What to look for in the logs {#Whattolookforinthelogs}
----------------------------

**a) SSSD sudo responder -- sssd\_sudo.log:**

-   **Was a rule returned to sudo at all?**

``` {.wiki}
[sssd[sudo]] [sudosrv_get_sudorules_from_cache] (0x0400): Returning $num-rules rules for [user-1@LDAP.PB]
```

-   **What filter was used to fetch rules from cache?**

``` {.wiki}
[sudosrv_get_sudorules_query_cache] (0x0200): Searching sysdb with [(&(objectClass=sudoRule)(|(sudoUser=ALL)(sudoUser=user-1)(sudoUser=#10001)(sudoUser=%group-1)(sudoUser=%user-1)(sudoUser=+*)))]
```

-   You can then use this filter to lookup in SSSD cache to see what
    rules where returned

``` {.wiki}
# yum install ldb-tools
# ldbsearch -H /var/lib/sss/db/cache_$domain.ldb -b cn=sysdb '$filter'
```

-   SSSD cache uses LDAP-like format equal to sudo format descibred in
    *[[​]{.icon}man
    sudoers.ldap](https://www.sudo.ws/man/1.8.15/sudoers.ldap.man.html){.ext-link}*

**b) SSSD domain -- sssd\_\$domain.log**

-   **How many rules were found?**

``` {.wiki}
[sdap_sudo_refresh_load_done] (0x0400): Received $num-rules rules
```

-   **What sudo rules were downloaded from server?**

``` {.wiki}
[sssd[be[LDAP.PB]]] [sysdb_save_sudorule] (0x0400): Adding sudo rule $rule-name
```

-   **Were all matching rules stored?**

``` {.wiki}
[sdap_sudo_refresh_load_done] (0x0400): Sudoers is successfuly stored in cache
```

-   **What filter was used to fetch rules from server?**

``` {.wiki}
[sdap_get_generic_ext_step] (0x0400): calling ldap_search_ext with [(&(objectClass=sudoRole)(|(!(sudoHost=*))(sudoHost=ALL)(sudoHost=client.sssd.pb)(sudoHost=client)(sudoHost=10.34.78.77)(sudoHost=10.34.78.0/24)(sudoHost=2620:52:0:224e:21a:4aff:fe23:1394)(sudoHost=2620:52:0:224e::/64)(sudoHost=fe80::21a:4aff:fe23:1394)(sudoHost=fe80::/64)(sudoHost=+*)(|(sudoHost=*\\*)(sudoHost=*?*)(sudoHost=*\2A*)(sudoHost=*[*]*))))][dc=ldap,dc=pb]
```

-   You can then use ldapsearch with this exact filter to see what rules
    were downloaded

``` {.wiki}
Anonymous bind
ldapsearch -x -H ldap://ldap.example.com -b dc=ldap,dc=example,dc=com '$filter'

Simple bind
ldapsearch -x -D "cn=Directory Manager" -w "$password" -H ldap://ldap.example.com -b dc=ldap,dc=example,dc=com '$filter'

GSSAPI
ldapsearch -Y GSSAPI -H ldap://ldap.example.com -b dc=ldap,dc=example,dc=com '$filter'
```

**c) sudo debug logs -- sudo\_debug**

-   **Information about user that is attempting to run sudo**

``` {.wiki}
Mar 31 16:11:15 sudo[22259] settings: debug_flags=all@debug
Mar 31 16:11:15 sudo[22259] settings: run_shell=true
Mar 31 16:11:15 sudo[22259] settings: progname=sudo
Mar 31 16:11:15 sudo[22259] settings: network_addrs=10.71.4.192/255.255.255.0 fe80::250:56ff:feb9:7d6/ffff:ffff:ffff:ffff::
Mar 31 16:11:15 sudo[22259] user_info: user=$username
Mar 31 16:11:15 sudo[22259] user_info: pid=22259
Mar 31 16:11:15 sudo[22259] user_info: ppid=22172
Mar 31 16:11:15 sudo[22259] user_info: pgid=22259
Mar 31 16:11:15 sudo[22259] user_info: tcpgid=22259
Mar 31 16:11:15 sudo[22259] user_info: sid=22172
Mar 31 16:11:15 sudo[22259] user_info: uid=$uid
Mar 31 16:11:15 sudo[22259] user_info: euid=0
Mar 31 16:11:15 sudo[22259] user_info: gid=554801393
Mar 31 16:11:15 sudo[22259] user_info: egid=554801393
Mar 31 16:11:15 sudo[22259] user_info: groups=498,6004,6005,7001,106501,554800513,554801107,554801108,554801393,554801503,554802131,554802244,554807670
Mar 31 16:11:15 sudo[22259] user_info: cwd=/
Mar 31 16:11:15 sudo[22259] user_info: tty=/dev/pts/1
Mar 31 16:11:15 sudo[22259] user_info: host=$hostname
Mar 31 16:11:15 sudo[22259] user_info: lines=31
Mar 31 16:11:15 sudo[22259] user_info: cols=237
```

-   **What data sources are used to fetch sudo rules**

``` {.wiki}
Mar 31 16:11:15 sudo[22259] <- sudo_parseln @ ./fileops.c:178 := sudoers: files sss
```

-   **SSSD plugin starts here**

``` {.wiki}
Mar 31 16:11:15 sudo[22259] <- sudo_sss_open @ ./sssd.c:305 := 0
```

-   **Here is sudo looking for cn=defaults**

``` {.wiki}
Mar 31 16:11:15 sudo[22259] Looking for cn=defaults
```

-   **SSSD is returning rules**

``` {.wiki}
Mar 31 16:11:15 sudo[22259] Received 3 rule(s)
```

-   **...and sudo is evaluating them by matching sudoHost, sudoUser, ...
    attributes to current user**
-   hostname is OK

``` {.wiki}
Mar 31 16:11:15 sudo[22259] sssd/ldap sudoHost 'ALL' ... MATCH!
```

-   if something does not match, you will see line ending := false; you
    need to guess the test from function name

``` {.wiki}
Mar 31 16:11:15 sudo[22259] <- user_in_group @ ./pwutil.c:1010 := false
```

Common questions {#Commonquestions}
----------------

**a) Setting global options with cn=defaults when sudo rules are stored
on an IPA server**

To immitate global options, create a rule named cn=defaults in LDAP tree
or rule named defaults in IPA and set sudoOption attribute as you wish.

**b) !authenticate does not work**

A common problem is when you set !authenticate option to a specific rule
but "sudo -l" command that lists all rules still requires
authentication. If you want "sudo -l" to be password-less you need to
set !authenticate also in cn=defaults.

**c) it takes too long to update rules**

Look at man sssd-sudo to see how sudo rules are cached in SSSD.

**d) what is alternative to options in command definition in sudoers**

In sudoers, you can define an allowed command together with many
options, such as:

``` {.wiki}
%wheel  ALL=(ALL) ROLE=unconfined_r TYPE=unconfined_t ALL
john    ALL=(ALL) NOPASSWD: ALL
```

These all have their equivalent as a sudo option that can be placed in
*sudoOption* attribute. Usually it is only lower cased value of this
command option, with an exception of *NOPASSWD* which is referenced as
*authenticate*. See *SUDOERS OPTIONS* section of *sudoers.5* manual page
for more information.

Known issues {#Knownissues}
------------

**Problems with IPA-AD trust when fully qualified names are required for
IPA**

**Fixed in 1.14.0**:
[[​]{.icon}https://fedorahosted.org/sssd/ticket/2919](https://fedorahosted.org/sssd/ticket/2919){.ext-link}

In configurations that requires IPA users and groups to use fully
qualified names (i.e. username@IPA.DOMAIN and groupname@IPA.DOMAIN) sudo
is not able to resolve the users or groups in sudo rules correctly.

Example configuration:

``` {.wiki}
[sssd]
domains = IPA.DOMAIN
default_domain_suffix = AD.DOMAIN
```

Or:

``` {.wiki}
[domain/IPA.DOMAIN]
use_fully_qualified_names = True
```

**Sudo rule won't work since 1.13.4 if it contains non-POSIX group with
IPA provider**

**Won't fix, intentional**:
[[​]{.icon}https://fedorahosted.org/sssd/ticket/3046](https://fedorahosted.org/sssd/ticket/3046){.ext-link}

We switched to IPA sudo rules schema stored at "cn=sudo" in SSSD 1.13.4.
The slapi-nis plugin that is used to generate the compat tree
"ou=sudoers" unfold members of non-posix group and stores each as
"sudoUser: member" value. This makes sudo rules work even with non-POSIX
group if the compat tree is used.

To re-enable this functionality, you can switch SSSD to fetch sudo rules
from the compat tree again by setting ldap\_sudo\_search\_base to
"ou=sudoers,dc=example,dc=com".

The correct way to reference a non-POSIX group in sudo rule is to
include it by a POSIX one which is referenced by sudo as "sudorule
---&gt; posix group &lt;--- non-posix group".

Asking for help {#Askingforhelp}
---------------

Most of the sudo related user cases that we have in past years was
actually only a misconfiguration of sudo rule or the client system. If
you are not able to track down the issue yourself, feel free to ask one
of the developers on SSSD mailing list or IRC. To speed things up,
please prepare the following information:

-   Description of the problem and what have you found out. You should
    at least know whether the issue lies on sudo (rules are send to sudo
    but it unexpectedly rejects access) or sssd (the rule is not even
    send to sudo) side with the use of previous debugging information.
-   sudo and SSSD logs
-   LDIF of rules that are expected to work but don't
-   Any additional information you deemed helpful -- e.g. group
    membership, output of the following commands:
    -   id \$user
    -   getent group \$group
    -   getent netgroup \$netgroup

Supported versions {#Supportedversions}
------------------

Sudo integration is supported since version 1.8.6 of sudo itself and
version 1.9 of sssd.