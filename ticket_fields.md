fedorahosted migration {#fedorahostedmigration}
----------------------

We need to migrate from Trac before fedorahosted.org shuts down. This
page lists what we currently use from trac and can be used to list
options.

### Trac fields we use {#Tracfieldsweuse}

-   **summary** - needed
-   **long description** - needed
-   **type (defect/rfe/task)** - needed
-   **priority** - needed
-   **milestone** - needed
-   component (nss, pam, ldap, ...) - not really used, so not needed
-   blocked-by/blocking - rarely used
-   sensitive - would be really nice to have
-   **patch submitted (yes/no)** - used, would be nice to have some
    indication like this
-   **design link** - used
-   tests update - unused
-   coverity bug - rarely used
-   **red hat bugzilla** - used and needed
-   **keywords** - sometimes used (for easyfix)
-   design review - unused
-   fedora test page - unused
-   chosen - unused
-   candidate to push out - unused
-   release notes - rarely used
-   temp mark - unused

### Proposed Trac replacements {#ProposedTracreplacements}

Here is a unstructured discussion on what can we replace Trac with.

#### github.com

-   Pros:
    -   widely used
    -   we already have a mirror there
-   Cons:
    -   no custom fields in tickets and no way to add then except labels
    -   closed
-   Missing features:
    -   custom fields in tickets, especially for RHBZ

#### pagure.io

-   Pros:
    -   open and developed by Fedora community, so the chance of having
        something implemented is larger than with github
-   Cons:
    -   very immature
-   Missing features
    -   custom fields
    -   no way to CC to ticket except adding a comment
    -   not sure if PRs can be replied to by mail, needs to be
        investigated
-   Tickets filed:
    -   [[​]{.icon}Arbitrary ticket
        metadata](https://pagure.io/pagure/issue/1308){.ext-link}
    -   [[​]{.icon}Watch / follow / subscribe to
        issues](https://pagure.io/pagure/issue/1293){.ext-link}
    -   [[​]{.icon}Adding a mailing list address to any project to
        receive updates from
        issues](https://pagure.io/pagure/issue/1258){.ext-link}
    -   [[​]{.icon}Ability to be CCed in
        bugs](https://pagure.io/pagure/issue/746){.ext-link}
    -   [[​]{.icon}pull-request/email
        integration](https://pagure.io/pagure/issue/15){.ext-link}

#### self-hosted

-   Pros:
    -   we have control over the instance
-   Cons:
    -   we need to maintainer the instance..

