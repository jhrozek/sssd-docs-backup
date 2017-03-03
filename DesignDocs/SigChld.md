<div class="wiki-toc">

1.  1.  [Common SIGCHLD handler](#CommonSIGCHLDhandler)
    2.  [Alternate Proposal](#AlternateProposal)
        1.  [struct sss\_child\_ctx
            \*child\_ctx](#structsss_child_ctxchild_ctx)
            1.  [members](#members)
        2.  [struct sss\_sigchild\_ctx
            \*sigchld\_ctx](#structsss_sigchild_ctxsigchld_ctx)
            1.  [members](#members1)
            2.  [Function](#Function)
        3.  [sss\_child\_register](#sss_child_register)
            1.  [Prototype](#Prototype)
            2.  [Function](#Function1)
        4.  [sss\_child\_handler](#sss_child_handler)
            1.  [Prototype](#Prototype1)
            2.  [Function](#Function2)
        5.  [sss\_child\_fn\_t](#sss_child_fn_t)
            1.  [Prototype](#Prototype2)
        6.  [sss\_child\_destructor](#sss_child_destructor)

</div>

This design page is related to the following ticket:
[[​]{.icon}https://fedorahosted.org/sssd/ticket/1004](https://fedorahosted.org/sssd/ticket/1004){.ext-link}

Common SIGCHLD handler {#CommonSIGCHLDhandler}
----------------------

I took some inspiration in the SIGUSR1 signal handling in
data\_provider\_be.c. The SIGUSR1 signal is apparently used to force
offline behavior on providers.

DP backend enables providers to register callbacks for the
online/offline event. I thought it would be a good idea to make SIGCHLD
handling consistent with what is already in place.

For online/offline event, these functions are defined:

be\_add\_online\_cb

be\_run\_online\_cb

be\_add\_offline\_cb

be\_run\_offline\_cb

They give providers the option to register additional callbacks to
handle these event in their own way. The list of callbacks is stored on
the backend context (struct be\_ctx).

However there is one difference between the SIGCHLD and SIGUSR1
scenarios: online/offline callbacks are called serially - always all of
them. While the SIGCHLD handler has to invoke callbacks for the
appropriate PIDs only. This means we can't use the underlying callbacks
handling functions already in place (be\_run\_cb and be\_run\_cb\_step).

I propose creating new similar functions (be\_run\_sigchld\_cb and
be\_run\_sigchld\_cb\_step). They would work in a similar manner to the
previously mentioned (be\_run\_cb and be\_run\_cb\_step respectively)
with the difference that:

1.  each step would check with waitpid first and invoke the callback
    only if the child has exited

<!-- -->

2.  we would use tevent\_immediate events instead of timers (as
    discussed on IRC with Stephen)

Advantages of this approach:

1.  consistent with online/offline callbacks for providers

<!-- -->

2.  relatively easy to implement

Alternate Proposal {#AlternateProposal}
------------------

### struct sss\_child\_ctx \*child\_ctx {#structsss_child_ctxchild_ctx}

#### members

-   `pid_t pid`
-   `sss_child_cb_fn cb`
-   `void *pvt`
-   `struct sss_sigchild_ctx *sigchld_ctx`

### struct sss\_sigchild\_ctx \*sigchld\_ctx {#structsss_sigchild_ctxsigchld_ctx}

#### members {#members1}

-   `struct tevent_context *ev`
-   `hash_table_t *children`
-   `int options`

#### Function {#Function}

This object should be initialized at process startup time. The
hash\_table should be initialized with `sss_hash_create()` to maintain
talloc compatibility. This hash should be keyed by integer (the PID) and
should contain `struct sss_child_ctx *` objects as its values. The
`options` member should be a bitmask allowing WUNTRACED and/or
WCONTINUED. The handler will ALWAYS add WNOHANG.

### sss\_child\_register

#### Prototype {#Prototype}

``` {.wiki}
errno_t sss_child_register(TALLOC_CTX *memctx,
                           struct sss_sigchild_ctx *sigchld_ctx,
                           pid_t pid,
                           sss_child_fn_t cb,
                           void *pvt,
                           struct sss_child_ctx **child_ctx);
```

#### Function {#Function1}

This function registers a callback with private data in a hash table
contained within sigchld\_ctx. It constructs a `struct sss_child_ctx *`
consisting of the pid, cb and pvt. It will also create a destructor for
this object which will remove the entry from the hash. This is so that
it the consumer can choose when to stop monitoring the child (such as if
the `waitpid()` call returned SIGSTOP/SIGCONT or other non-terminating
results. It can also be used to programmatically change the callback at
need.

### sss\_child\_handler

#### Prototype {#Prototype1}

``` {.wiki}
void
sss_child_handler(struct tevent_context *ev,
                  struct tevent_signal *se,
                  int signum,
                  int count,
                  void *siginfo,
                  void *private_data);
```

#### Function {#Function2}

This is the master SIGCHLD handler. It would be invoked any time that
the process receives a SIGCHLD signal.

When the signal is removed, it should call
`waitpid(-1, &status, WNOHANG & sigchld_ctx->options);` repeatedly until
`waitpid()` returns 0. For each child received, the pid should be looked
up in the hash table and the matching callback should be invoked.

### sss\_child\_fn\_t

#### Prototype {#Prototype2}

``` {.wiki}
typedef void (*sss_child_fn_t)(int pid, int wait_status, void *pvt);
```

### sss\_child\_destructor

Talloc\_destructor to remove a `struct sss_child_ctx *` from the hash
table of the `struct sss_sigchild_ctx *` that contains it.