[InterTrac](https://docs.pagure.org/sssd-test2/InterTrac.html){.wiki} Links {#InterTracLinks}
===========================================================================

Trac supports a convenient way to refer to resources of other Trac
servers, from within the Wiki markup, since version 0.10.

Definitions {#Definitions}
-----------

An [InterTrac](https://docs.pagure.org/sssd-test2/InterTrac.html){.wiki}
link can be seen as a scoped
[TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki}.
It is used for referring to a Trac resource (Wiki page, changeset,
ticket, ...) located in another Trac environment.

List of Active [InterTrac](https://docs.pagure.org/sssd-test2/InterTrac.html){.wiki} Prefixes {#ListofActiveInterTracPrefixes}
---------------------------------------------------------------------------------------------

<div class="system-message">

**Error: Macro InterTrac(None) failed**
    'unicode' object does not support item assignment

</div>

Link Syntax {#LinkSyntax}
-----------

Simply use the name of the other Trac environment as a prefix, followed
by a colon, ending with the resource located in the other environment.

``` {.wiki}
<target_environment>:<TracLinks>
```

The other resource is specified using a regular
[TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki},
of any flavor.

That target environment name is either the real name of the environment,
or an alias for it. The aliases are defined in `trac.ini` (see below).
The prefix is case insensitive.

If the
[InterTrac](https://docs.pagure.org/sssd-test2/InterTrac.html){.wiki}
link is enclosed in square brackets (like `[th:WikiExtrasPlugin]`), the
[InterTrac](https://docs.pagure.org/sssd-test2/InterTrac.html){.wiki}
prefix is removed in the displayed link, like a normal link resolver
would be (i.e. the above would be displayed as `WikiExtrasPlugin`).

For convenience, there's also some alternative short-hand form, where
one can use an alias as an immediate prefix for the identifier of a
ticket, changeset or report: (e.g. `#T234`, `[T1508]`, `[trac 1508]`,
...)

Examples {#Examples}
--------

It is necessary to setup a configuration for the
[InterTrac](https://docs.pagure.org/sssd-test2/InterTrac.html){.wiki}
facility. This configuration has to be done in the
[TracIni](https://docs.pagure.org/sssd-test2/TracIni.html){.wiki} file,
`[intertrac]` section.

Example configuration:

``` {.wiki}
...
[intertrac]
# -- Example of setting up an alias:
t = trac

# -- Link to an external Trac:
trac.title = Edgewall's Trac for Trac
trac.url = http://trac.edgewall.org
```

The `.url` is mandatory and is used for locating the other Trac. This
can be a relative URL in case that Trac environment is located on the
same server.

The `.title` information will be used for providing an useful tooltip
when moving the cursor over an
[InterTrac](https://docs.pagure.org/sssd-test2/InterTrac.html){.wiki}
links.

Finally, the `.compat` option can be used to activate or disable a
*compatibility* mode:

-   If the targeted Trac is running a version below
    [[​]{.icon}0.10](http://trac.edgewall.org/intertrac/milestone%3A0.10 "milestone:0.10 in Trac project trac"){.ext-link}
    ([[​]{.icon}r3526](http://trac.edgewall.org/intertrac/r3526 "r3526 in Trac project trac"){.ext-link}
    to be precise), then it doesn't know how to dispatch an
    [InterTrac](https://docs.pagure.org/sssd-test2/InterTrac.html){.wiki}
    link, and it's up to the local Trac to prepare the correct link. Not
    all links will work that way, but the most common do. This is called
    the compatibility mode, and is `true` by default.
-   If you know that the remote Trac knows how to dispatch
    [InterTrac](https://docs.pagure.org/sssd-test2/InterTrac.html){.wiki}
    links, you can explicitly disable this compatibility mode and then
    *any*
    [TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki}
    can become an
    [InterTrac](https://docs.pagure.org/sssd-test2/InterTrac.html){.wiki}
    link.

Now, given the above configuration, one could create the following
links:

-   to this
    [InterTrac](https://docs.pagure.org/sssd-test2/InterTrac.html){.wiki}
    page:
    -   `trac:wiki:InterTrac`
        [[​]{.icon}trac:wiki:InterTrac](http://trac.edgewall.org/intertrac/wiki%3AInterTrac "wiki:InterTrac in Trac project trac"){.ext-link}
    -   `t:wiki:InterTrac` t:wiki:InterTrac
    -   Keys are case insensitive: `T:wiki:InterTrac` T:wiki:InterTrac
-   to the ticket
    [\#234](https://fedorahosted.org/sssd/ticket/234 "task: Create common option description mechanism (reopened)"){.reopened
    .ticket}:
    -   `trac:ticket:234`
        [[​]{.icon}trac:ticket:234](http://trac.edgewall.org/intertrac/ticket%3A234 "ticket:234 in Trac project trac"){.ext-link}
    -   `trac:#234`
        [[​]{.icon}trac:\#234](http://trac.edgewall.org/intertrac/%23234 "#234 in Trac project trac"){.ext-link}
    -   `#T234` \#T234
-   to the changeset [\[1912\]]{.missing .changeset}:
    -   `trac:changeset:1912`
        [[​]{.icon}trac:changeset:1912](http://trac.edgewall.org/intertrac/changeset%3A1912 "changeset:1912 in Trac project trac"){.ext-link}
    -   `[T1912]` \[T1912\]
-   to the log range
    [\[3300:3330\]](https://fedorahosted.org/sssd/log/?revs=3300-3330){.source}:
    **(Note: the following ones need `trac.compat=false`)**
    -   `trac:log:@3300:3330`
        [[​]{.icon}trac:log:@3300:3330](http://trac.edgewall.org/intertrac/log%3A%403300%3A3330 "log:@3300:3330 in Trac project trac"){.ext-link}
    -   `[trac 3300:3330]` [[​]{.icon}\[trac
        3300:3330\]](http://trac.edgewall.org/intertrac/log%3A/%403300%3A3330 "log:/@3300:3330 in Trac project trac"){.ext-link}
-   finally, to link to the start page of a remote trac, simply use its
    prefix followed by ':', inside an explicit link. Example:
    `[th: Trac Hacks]` (*since 0.11; note that the* remote *Trac has to
    run 0.11 for this to work*)

The generic form `intertrac_prefix:module:id` is translated to the
corresponding URL `<remote>/module/id`, shorthand links are specific to
some modules (e.g. \#T234 is processed by the ticket module) and for the
rest (`intertrac_prefix:something`), we rely on the
[TracSearch\#quickjump](https://docs.pagure.org/sssd-test2/TracSearch.html#quickjump){.wiki}
facility of the remote Trac.

------------------------------------------------------------------------

See also:
[TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki},
[InterWiki](https://docs.pagure.org/sssd-test2/InterWiki.html){.wiki}
