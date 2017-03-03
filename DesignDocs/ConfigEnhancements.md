Feature Name {#FeatureName}
============

Improve config validation

Related ticket(s):

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2247](https://fedorahosted.org/sssd/ticket/2247){.ext-link}
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2028](https://fedorahosted.org/sssd/ticket/2028){.ext-link}
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/1308](https://fedorahosted.org/sssd/ticket/1308){.ext-link}
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2249](https://fedorahosted.org/sssd/ticket/2249){.ext-link}
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2269](https://fedorahosted.org/sssd/ticket/2269){.ext-link}
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2465](https://fedorahosted.org/sssd/ticket/2465){.ext-link}
-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2687](https://fedorahosted.org/sssd/ticket/2687){.ext-link}
-   ...and more

### Problem statement {#Problemstatement}

Admins should be notified if their configuration is not valid Admins
should have an option to still log in to the system if they do an error
in configuration

### Use cases {#Usecases}

-   Fallback config
    -   With responders, we can use defaults, they are usually paranoid
        enough
    -   With domains, we probably can only fall back to last known good
        (except local domain)
    -   Could we start only responders so that if cached data is
        available, the responders can be used?
-   Last known good (First known good)
    -   For domains
    -   Use-case: admin changes something and wants to still log in
-   Config merging
    -   Deprecate "services" line
    -   Be able to drop domain into /etc/sssd/sssd.conf.d/
-   Config validation
    -   prerequisity: have a common definition of options and
        autogenerate the rest
        -   Autogenerate dp\_opts, man pages and configAPI sources from
            a common location
        -   Look at Samba
    -   ...for that we need to use dp\_opts everywhere

### To do {#Todo}

-   Does ding-libs support config validation?

### Overview of the solution {#Overviewofthesolution}

Describe, without going too low into technical details, what changes
need to happen in SSSD during implementation of this feature. This
section should be understood by a person with understanding of how SSSD
works internally but doesn't have an in-depth understanding of the code.
For example, it's fine to say that we implement a new option `foo` with
a default value `bar`, but don't talk about how is `foo` processed
internally and which structure stores the value of \`foo. In some cases
(internal APIs, refactoring, ...) this section might blend with the next
one.

### Implementation details {#Implementationdetails}

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
