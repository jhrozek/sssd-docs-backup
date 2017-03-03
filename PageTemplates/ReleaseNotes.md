Highlights {#Highlights}
----------

-   Manually cherry-picked important commits

Packaging Changes {#PackagingChanges}
-----------------

``` {.wiki}
git diff previoustag..newtag -- contrib/sssd.spec.in
```

Documentation Changes {#DocumentationChanges}
---------------------

``` {.wiki}
git diff previoustag..newtag -- src/man
```

Tickets Fixed {#TicketsFixed}
-------------

``` {.wiki}
[[TicketQuery(milestone=$MILESTONE&resolution=fixed)]]
```

Detailed Changelog {#DetailedChangelog}
------------------

``` {.wiki}
git shortlog previoustag..newtag
```
