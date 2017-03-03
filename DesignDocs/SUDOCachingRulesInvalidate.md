Invalidate Cached SUDO Rules {#InvalidateCachedSUDORules}
============================

Related ticket(s):

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2081](https://fedorahosted.org/sssd/ticket/2081){.ext-link}
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2884](https://fedorahosted.org/sssd/ticket/2884){.ext-link}

### Problem statement {#Problemstatement}

Currently sss\_cache can't be used to reliably invalidate sudo rules.

### Use cases {#Usecases}

Usually if admin changes sudo rules he would like to see an effect
immediately.

### Overview of the solution {#Overviewofthesolution}

Sudo rules are stored in sss\_cache. Sometimes *smart* or *full* refresh
of sudo rules is done, but there is no effective way to invalidate them
(see
[[​]{.icon}https://fedorahosted.org/sssd/wiki/DesignDocs/SUDOCachingRules](https://docs.pagure.org/sssd-test2/DesignDocs/SUDOCachingRules.html){.ext-link}).

Solution consists of two steps:

1.  Invalidate sudo rules by setting expiration time to 0 which can
    prevent to use old rules.
2.  Trigger full refresh (and maybe even smart refresh) on demand.

### Implementation details {#Implementationdetails}

#### Invalidating sudo rules {#Invalidatingsudorules}

SSSD provides tool sss\_cache for invalidating items.

``` {.wiki}
$ sss_cache --help
Usage: sss_cache [OPTION...]
  -E, --everything            Invalidate all cached entries except for sudo rules
  -u, --user=STRING           Invalidate particular user
  -U, --users                 Invalidate all users
  -g, --group=STRING          Invalidate particular group
  -G, --groups                Invalidate all groups
  -n, --netgroup=STRING       Invalidate particular netgroup
  -N, --netgroups             Invalidate all netgroups
  -s, --service=STRING        Invalidate particular service
  -S, --services              Invalidate all services
  -a, --autofs-map=STRING     Invalidate particular autofs map
  -A, --autofs-maps           Invalidate all autofs maps
  -h, --ssh-host=STRING       Invalidate particular SSH host
  -H, --ssh-hosts             Invalidate all SSH hosts
  -d, --domain=STRING         Only invalidate entries from a particular domain

Help options:
  -?, --help                  Show this help message
      --usage                 Display brief usage message
```

We need:

-   add option `--sudo-rule=STRING` for invalidating only STRING named
    sudo rule,
-   add option `--sudo-rules` for invalidating all sudo rules,
-   change option `--everything` for invalidating sudo rules too.

For those changes we will provide new function
`sysdb_search_sudo_rule()` in `db/sysdb_sudo.{hc}`.

<div class="code">

    errno_t
    sysdb_search_sudo_rules(TALLOC_CTX *mem_ctx,
                            struct sss_domain_info *domain,
                            const char *filter,
                            const char **attrs,
                            size_t *num_hosts,
                            struct ldb_message ***hosts)
    /* Synopsis is inspired by other `sysdb_search_*()` functions. */

</div>

This new function be able to find sudo rule by given name (via filter).

On the other hand there is function
`sudosrv_get_sudorules_query_cache()` in
`responder/sudo/sudosrv_get_sudorules.c` which has very similar
behavior. Maybe it is candidate for proxy and moving to
`db/sysdb_sudo.{hc}`.

------------------------------------------------------------------------

To Be Done {#ToBeDone}
----------

### Implementation details {#Implementationdetails1}

A more technical extension of the previous section. Might include
low-level details, such as C structures, function synopsis etc. In case
of very trivial features (e.g a new option), this section can be merged
with the previous one.

### Configuration changes {#Configurationchanges}

Does your feature involve changes to configuration, like new options or
options changing values? Summarize them here. There's no need to go into
too many details, that's what man pages are for.

### How To Test {#HowToTest}

This section should explain to a person with admin-level of SSSD
understanding how this change affects run time behaviour of SSSD and how
can an SSSD user test this change. If the feature is internal-only,
please list what areas of SSSD are affected so that testers know where
to focus.

### Authors {#Authors}

Give credit to authors of the design in this section.
