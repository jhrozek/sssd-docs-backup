DEPRECATED (moved to sssctl) {#DEPRECATEDmovedtosssctl}
============================

This tool is no longer developed and it's functionality was moved to
sssctl tool.

sss\_confcheck tool {#sss_confchecktool}
===================

Related ticket(s):

-   [[​]{.icon}https://fedorahosted.org/sssd/ticket/2269](https://fedorahosted.org/sssd/ticket/2269){.ext-link}

### Problem statement {#Problemstatement}

There is no easy way to debug the SSSD configuration without having to
look into the debug logs. Moreover the debug logs can be difficult to
understand for people outside SSSD development team. Some common issues
can be identified during static offline analysis of the config files. To
find these issues soon we need a tool that performs this analysis and
provides human readable report.

### Use cases {#Usecases}

-   performing ad-hoc static analysis of the installed SSSD
    configuration
-   performing ad-hoc static analysis of SSSD configuration files
    retrieved from user with some SSSD problems

### Overview of the solution - sss\_confcheck tool {#Overviewofthesolution-sss_confchecktool}

A new tool will be added to sss\_\* tools that will perform static
analysis of SSSD configuration files. This tool can be run without any
parameters in which case it will print a report to the standard output
in the following or similar format:

``` {.wiki}
$ sss_confcheck
Number of identified issues: 1
[rule/allowed_nss_options]: Attribute 'foo' is not allowed in section 'nss'. Check for typos.

Used configuration file:
<Here will be the contents of sssd.conf file>

Number of used configuration override snippets: 2
List of configuration override snippets in order of priority (lowest priority first):
snippet_name_1.conf
snippet_name_2.conf

Content of configuration override snippets:
snippet_name_1.conf:
<content of snippet_name_1.conf>

snippet_name_2.conf:
<content of snippet_name_2.conf>

Merged configuration:
<content of merged configuration (sssd.conf merged with snippets)>
```

Available options:

``` {.wiki}
  ?, --help
  --config-file PATH_CONFIG_FILE                Path to config file that will be checked.
  --snippets-dir PATH_TO_SNIPPETS_DIRECTORY     Path to snippets directory.
  --no-validators                               Do not use validators (no analysis will be made).
  --no-file-content                             Do not print config file or snippet contents.
  --no-snippets                                 Ignore the snippets.
  --silent                                      If no errors are detected, do not print anything.
```

### Implementation details {#Implementationdetails}

The tool will use ding-libs validators feature described in this design
document
[[​]{.icon}https://fedorahosted.org/sssd/wiki/DesignDocs/libini-config-file-checks](https://docs.pagure.org/sssd-test2/DesignDocs/libini-config-file-checks.html){.ext-link}.

### Configuration changes {#Configurationchanges}

No configuration changes.

### How To Test {#HowToTest}

Depending on the capabilities of validators used by SSSD, make an error
in configuration and run sss\_confcheck to see if it was detected.

### Planned features in version 1 - initial version {#Plannedfeaturesinversion1-initialversion}

Validators capabilities:\

-   able to detect typo in option name
-   able to detect typo in section name
-   able to detect option in wrong section

Limitations:

-   printing the resulting configuration (after merging with snippets)
    may not be in the initial version.

### Authors {#Authors}

Michal Židek
[[​]{.icon}mzidek@redhat.com](mailto:mzidek@redhat.com){.mail-link}
