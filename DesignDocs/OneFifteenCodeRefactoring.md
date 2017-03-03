Code refactoring for the 1.15 release {#Coderefactoringforthe1.15release}
=====================================

Related ticket(s):

-   please see inline

Problem statement {#Problemstatement}
-----------------

SSSD is being very actively developed, adding several major features in
each release. We need to make sure the code stays maintainable and
adding new features in the upcoming release won't increase the cost of
maintaining SSSD long-term.

Since SSSD releases are primarily being driven by Fedora and RHEL
releases, the Red Hat employed developers have a fixed amount of time
for code refactoring. Of course, community members and developers are
free to submit their patches on their schedule -- although discussion on
the list would be needed prior to merging any refactoring to not disrupt
SSSD release quality for everyone.

Use cases {#Usecases}
---------

A typical use-case would be: "A feature X depends on module Y that
either is missing some functionality that is missing or a module that
has outlived its initial design. Changing Y in that module would allow
us to implement X more easily or with less maintenance effort in the
future".

The goal is to prepare the code for upcoming features without
regressing, so testing after the refactoring is done is mandatory. We
should consider also doing an upstream (pre)release to make it easier to
test the changes.

Proposed items to be refactored {#Proposeditemstoberefactored}
-------------------------------

This section lists the proposed tickets along with justifications, scope
and test impact.

Given the fixed amount of time, each refactoring has a scope, expressed
in just three high-level buckets - large (a couple of weeks, might take
most of the time of the refactoring "sprint"), medium (a week to two
weeks) or small (a couple of days, up to a week). Each item also lists
the affected modules or functionality, so that we know where we need to
improve tests.

### Use the shared `cache_req` module for responder look-ups {#Usethesharedcache_reqmoduleforresponderlook-ups}

Currently each responder (except the InfoPipe responder and several
parts of the NSS responder) copy the logic that checks the cache and
contacts the Data Provider if needed. In 1.15, we should add the missing
functionality into the cache\_req module and convert the existing
responders (especially those that look up users and groups, not
necessarily other objects like autofs maps or hosts..) to cache\_req.

#### Benefit to SSSD {#BenefittoSSSD}

In 1.15, we should look at allowing lookups from trusted domain with a
shortname. But we need to take performance into account and avoid
cycling over all domains including their LDAP server. Then we could
switch to checking the caches of all domains first before checking each
domain's cache and then its server.

This goal is tracked by
[[​]{.icon}https://fedorahosted.org/sssd/ticket/843](https://fedorahosted.org/sssd/ticket/843){.ext-link}
(Login time increases strongly if more than one domain is configured)
and ultimately by
[[​]{.icon}https://fedorahosted.org/sssd/ticket/3001](https://fedorahosted.org/sssd/ticket/3001){.ext-link}
(\[RFE\] Short name input format with SSSD for users from all domains
when domain autodiscovery is used).

#### Tracking tickets {#Trackingtickets}

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/3151](https://fedorahosted.org/sssd/ticket/3151){.ext-link} -
    cache\_req: complete the needs of NSS responders
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1126](https://fedorahosted.org/sssd/ticket/1126){.ext-link} -
    Reuse cache\_req() in responder code

#### Testing {#Testing}

We already have NSS and PAM responder tests. We need to extend them
further to make sure all codepaths we change are tested.

#### Scope {#Scope}

Large

### Refactor group lookups for better performance {#Refactorgrouplookupsforbetterperformance}

The `sdap_async_groups.c` module grew organically over time. At the
moment, the module is quite hard to read and repeats some potentially
expensive operations (like looping over all attributes or all members)
several times.

In order to improve performance, we should refactor this module and test
it extensively.

#### Benefit to SSSD {#BenefittoSSSD1}

The `sdap_async_groups.c` module would be better maintainable and we
would remove some performance bottlenecks from the code.

#### Tracking tickets {#Trackingtickets1}

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/3211](https://fedorahosted.org/sssd/ticket/3211){.ext-link} -
    Refactor the sdap\_async\_groups.c module

#### Testing {#Testing1}

LDAP group lookups can be tested using integration tests, "just" all
cases we change must have corresponding test cases.

#### Scope {#Scope1}

Medium

### Refactor the sdap\_id\_ops.c module {#Refactorthesdap_id_ops.cmodule}

The `sdap_id_ops.c` module was written in time where SSSD only supported
a single domain. One of the things that are repeatedly biting us is that
the module can set the fail over status of the whole domain to offline.
Moreover, the module has no tests and is not easy to read.

At this time, it's not clear whether the refactoring would just result
in documenting and testing the module or if it would be worth for
example making the module return error codes for connection errors and
let the caller handle the errors. Alternatively, we might decide to do
even more work and let the fail over code work per-domain, not per-back
end, which probably wouldn't be doable in the given scope. More research
is needed.

#### Benefit to SSSD {#BenefittoSSSD2}

The module would be better maintainable (currently there are some
codepaths where we even don't know why they were added anymore..), have
tests and we would work towards removing issues with trusted domains
setting SSSD to the offline mode.

#### Tracking tickets {#Trackingtickets2}

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1507](https://fedorahosted.org/sssd/ticket/1507){.ext-link} -
    Investigate terminating connections in sdap\_ops.c and comment the
    code some more

Other related tickets include:

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2767](https://fedorahosted.org/sssd/ticket/2767){.ext-link} -
    The sdap\_op code always ends request with EAGAIN
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2976](https://fedorahosted.org/sssd/ticket/2976){.ext-link} -
    sdap code can mark the whole sssd\_be offline

#### Testing {#Testing2}

Currently upstream has only basic tests with the integration tests.
Downstream has tests for fail over as well.

#### Scope {#Scope2}

Medium to large, depending on what changes we decide to do.

### Provide a way to pass intermediate data between requests {#Provideawaytopassintermediatedatabetweenrequests}

As long as a request is confined within a single domain, we can pass
around `sysdb_attrs` or a similar data structure between different
requests and avoid a costly cache writes. However, when a request must
include processing in two different domain types, for example an IPA
domain that includes overrides, the only way to pass intermediate data
is to call a sysdb transaction and save the data to cache so that
another request can read them.

#### Benefit to SSSD {#BenefittoSSSD3}

Performance benefit in case SSSD must call identity lookup requests from
different domains.

#### Tracking tickets {#Trackingtickets3}

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2943](https://fedorahosted.org/sssd/ticket/2943){.ext-link} -
    Split out the requests for IPA users and groups that include
    overrides into reusable requests

#### Testing {#Testing3}

Unfortunately, there are no upstream tests for requests that include
overrides. Testing would be provided by downstream tests.

#### Scope {#Scope3}

Medium to large

### Upstream the PoC tests that utilize Samba AD for AD provider testing {#UpstreamthePoCteststhatutilizeSambaADforADprovidertesting}

At the moment, we don't have any upstream tests for the AD provider and
we rely on downstream and manual testing completely. Nikolai Kondrashov
wrote a proof-of-concept patches that provisions an AD DC server
provided by the Samba project using the cwrap wrapper libraries. The
scope of this effort would be to upstream this work.

#### Benefit to SSSD {#BenefittoSSSD4}

SSSD integration tests would allow us to write tests for the AD
provider.

#### Tracking tickets {#Trackingtickets4}

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2818](https://fedorahosted.org/sssd/ticket/2818){.ext-link} -
    Investigate if Samba4 in Fedora can be used for SSSD CI

#### Testing {#Testing4}

Some basic tests like looking up a user or a group would be part of this
effort.

#### Scope {#Scope4}

Medium

### Decrease the functionality of the monitor process {#Decreasethefunctionalityofthemonitorprocess}

SSSD is gradually moving to socket-activated services and in general
more self-contained services rather than implementing a service manager
in the monitor process. The scope of this work would be to further
decrease the dependence of services on the monitor process, such as
moving the register functionality to the services themselves.
Ultimately, the monitor process would perform one-time tasks such as
converting the configuration from INI to confdb and exit.

Other work might include a fallback configuration or starting the
services and domains even without having them explicitly enumerated in
the services section.

#### Benefit to SSSD {#BenefittoSSSD5}

Socket-activatable services would be better manageable by SSSD.

#### Tracking tickets {#Trackingtickets5}

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2231](https://fedorahosted.org/sssd/ticket/2231){.ext-link} -
    RFE: Drop the monitor process

#### Testing {#Testing5}

There are no upstream test for this functionality at the moment. Some
service restart tests exist in downstream, though.

#### Scope {#Scope5}

Medium to large, but hopefully this task could be split into several
smaller tasks.

### Memory cache changes {#Memorycachechanges}

There are several improvements to the memory cache that we have been
discussing lately, including a memory cache for by-SID lookups or having
the memory cache respect case insensitive domains. The goal of this task
would be to investigate what needs to be changed in the memory cache in
order to implement these improvements.

#### Benefit to SSSD {#BenefittoSSSD6}

Better performance through leveraging memory cache for SID lookups and
lookups in case insensitive domains.

#### Tracking tickets {#Trackingtickets6}

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/3193](https://fedorahosted.org/sssd/ticket/3193){.ext-link} -
    \[RFE\] Support aliases in the memory cache
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2727](https://fedorahosted.org/sssd/ticket/2727){.ext-link} -
    Add a memcache for SID-by-id lookups

#### Testing {#Testing6}

We already have tests for memory cache which could be extended. Tests
for by-SID lookups would probably require us to add the Samba-based
tests first.

#### Scope {#Scope6}

Probably large, but more investigation is needed.

### SBUS API Improvements {#SBUSAPIImprovements}

Our internal d-bus interface got a lot of new functionality to properly
support D-Bus on public level. The
[InfoPipe?](https://docs.pagure.org/sssd-test2/InfoPipe.html){.missing
.wiki} responder has grown and also our internal communication between
responders and providers has become more advanced.

The more we use it, the more it seems that the API that takes care of
managing/terminating/error sbus requests is not optimal, since it
requires a lot of glue code and often requires several output places and
return code.

We should base sbus handlers on tevent to make sure there is only one
output place and return code (when tevent request finishes) and we
should also improve and simplify API that is used by handlers.

#### Benefit to SSSD {#BenefittoSSSD7}

SSSD depends on D-Bus (and thus on sbus) more and more and we will keep
adding new functionality. Reducing the amount of code that needs to be
added and simplified logic will helps us to develop more stable code
more quickly.

#### Tracking tickets {#Trackingtickets7}

-   none currently

#### Testing {#Testing7}

Sbus is currently heavily tested. We may want to add new tests for
new/changed API.

#### Scope {#Scope7}

Small.

### Failover refactoring {#Failoverrefactoring}

Failover mechanism wasn't prepared for subdomains and we run into
troubles every now and then. We added several workarounds for cases
where the original code wasn't sufficient but it made the code just more
confused. At this moment nobody understands it but bugs keeps comming.

We should have a separate failover context for each domain, instead of
one per whole backend. It must be possible to set different srv
mechanism for each context. DNS resolver and cache should be shared
between contexts.

#### Benefit to SSSD {#BenefittoSSSD8}

We remove old and problematic code that knowbody understands. We can
improve site discovery for trusted domains and we can have better
control over subdomain server resolution.

#### Tracking tickets {#Trackingtickets8}

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2393](https://fedorahosted.org/sssd/ticket/2393){.ext-link}
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2394](https://fedorahosted.org/sssd/ticket/2394){.ext-link}

#### Testing {#Testing8}

Downstream tests should remain functional, but upstream test will become
invalid.

#### Scope {#Scope8}

Probably out of four week scope.

How To Test {#HowToTest}
-----------

Run all available upstream and downstream tests, if possible, extend the
upstream tests.
