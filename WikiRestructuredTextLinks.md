[TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki} in reStructuredText {#TracLinksinreStructuredText}
=========================================================================================

This document illustrates how to use the `:trac:` role in
reStructuredText. The page is written like:

``` {.wiki}
{{{
#!rst 
Examples:

 * Tickets: :trac:`#1` or :trac:`ticket:1`
 * Ticket comments: :trac:`comment:ticket:1:2`
 * Reports: :trac:`{1}` or :trac:`report:1`
 * Changesets: :trac:`r1`, :trac:`[1]` or :trac:`changeset:1`
 * Revision log: :trac:`r1:3`, :trac:`[1:3]` or :trac:`log:@1:3`, :trac:`log:trunk@1:3`
 * Diffs (since version 0.10): :trac:`diff:@20:30`, :trac:`diff:tags/trac-0.9.2/wiki-default//tags/trac-0.9.3/wiki-default` or :trac:`diff:trunk/trac@3538//sandbox/vc-refactoring/trac@3539`
 * Wiki pages: :trac:`CamelCase` or :trac:`wiki:CamelCase`
 * Milestones: :trac:`milestone:1.0`
 * Attachment: :trac:`attachment:ticket:944:attachment.1073.diff`
 * Files: :trac:`source:trunk/COPYING`
 * A specific file revision: :trac:`source:/trunk/COPYING@200`
 * A particular line of a specific file revision: :trac:`source:/trunk/COPYING@200#L25`

An explicit label can be specified, separated from the link by a space:

 * See :trac:`#1 ticket 1` and the :trac:`source:trunk/COPYING license`.
}}}
```

Provided you have docutils installed, the above block will render as:

------------------------------------------------------------------------

<div class="document">

Examples:

> -   Tickets: [\#1](https://fedorahosted.org/sssd/ticket/1){.reference
>     .external} or
>     [ticket:1](https://fedorahosted.org/sssd/ticket/1){.reference
>     .external}
> -   Ticket comments:
>     [comment:ticket:1:2](https://fedorahosted.org/sssd/ticket/1#comment:2){.reference
>     .external}
> -   Reports: [{1}](https://fedorahosted.org/sssd/report/1){.reference
>     .external} or
>     [report:1](https://fedorahosted.org/sssd/report/1){.reference
>     .external}
> -   Changesets: [r1](){.missing .reference .external},
>     [\[1\]](){.missing .reference .external} or
>     [changeset:1](){.missing .reference .external}
> -   Revision log:
>     [r1:3](https://fedorahosted.org/sssd/log/?revs=1-3){.reference
>     .external},
>     [\[1:3\]](https://fedorahosted.org/sssd/log/?revs=1-3){.reference
>     .external} or
>     [log:@1:3](https://fedorahosted.org/sssd/log/?revs=1-3){.reference
>     .external},
>     [log:trunk@1:3](https://fedorahosted.org/sssd/log/trunk?revs=1-3){.reference
>     .external}
> -   Diffs (since version 0.10):
>     [diff:@20:30](https://fedorahosted.org/sssd/changeset?new=30&old=20){.reference
>     .external},
>     [diff:tags/trac-0.9.2/wiki-default//tags/trac-0.9.3/wiki-default](https://fedorahosted.org/sssd/changeset?new_path=tags%2Ftrac-0.9.3%2Fwiki-default&old_path=tags%2Ftrac-0.9.2%2Fwiki-default){.reference
>     .external} or
>     [diff:trunk/trac@3538//sandbox/vc-refactoring/trac@3539](https://fedorahosted.org/sssd/changeset?new=3539&new_path=sandbox%2Fvc-refactoring%2Ftrac&old=3538&old_path=trunk%2Ftrac){.reference
>     .external}
> -   Wiki pages:
>     [CamelCase](https://docs.pagure.org/sssd-test2/CamelCase.html){.reference
>     .external} or
>     [wiki:CamelCase](https://docs.pagure.org/sssd-test2/CamelCase.html){.reference
>     .external}
> -   Milestones:
>     [milestone:1.0](https://fedorahosted.org/sssd/milestone/1.0){.missing
>     .reference .external}
> -   Attachment:
>     [attachment:ticket:944:attachment.1073.diff](){.missing .reference
>     .external}
> -   Files:
>     [source:trunk/COPYING](https://fedorahosted.org/sssd/browser/trunk/COPYING){.reference
>     .external}
> -   A specific file revision:
>     [source:/trunk/COPYING@200](https://fedorahosted.org/sssd/browser/trunk/COPYING?rev=200){.reference
>     .external}
> -   A particular line of a specific file revision:
>     [source:/trunk/COPYING@200\#L25](https://fedorahosted.org/sssd/browser/trunk/COPYING?rev=200#L25){.reference
>     .external}

An explicit label can be specified, separated from the link by a space:

> -   See [ticket 1](https://fedorahosted.org/sssd/ticket/1){.reference
>     .external} and the
>     [license](https://fedorahosted.org/sssd/browser/trunk/COPYING){.reference
>     .external}.

</div>

------------------------------------------------------------------------

Note also that any of the above could have been written using
substitution references and the `trac::` directive:

``` {.wiki}
{{{
#!rst
See |ticket123|.

 .. |ticket123| trac:: ticket:123 this ticket
}}}
```

This renders as:

------------------------------------------------------------------------

<div class="document">

See [this ticket](https://fedorahosted.org/sssd/ticket/123){.reference
.external}.

</div>

------------------------------------------------------------------------

See also:
[WikiRestructuredText](https://docs.pagure.org/sssd-test2/WikiRestructuredText.html){.wiki},
[TracLinks](https://docs.pagure.org/sssd-test2/TracLinks.html){.wiki}
