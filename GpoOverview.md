### GPO Overview {#GPOOverview}

Group Policy is a Windows feature that enables administrators to
centrally manage policies for users and computers in an AD environment.
A Group Policy Object (GPO) represents a collection of policy settings
(i.e. name/value pairs) that are stored on a Domain Controller (DC), and
that can be applied to policy targets (i.e. computers and users). When a
computer boots up or a user logs in (and at periodic intervals
thereafter), GPO software on the client computer uses LDAP to identify
the GPOs that apply to the policy target, uses SMB/CIFS to retrieve each
GPO's policy settings (that it knows how to process), and stores the
policy settings in a local store. At some later time, an enforcement
mechanism reads the policy settings from the local store, and enforces
the policy settings.

Determining which policy settings are applicable for a given policy
target depends on the policy target's type (i.e. computer or user), and
the policy target's location in the AD hierarchy (i.e. the site, domain,
and OU(s) under which the policy target resides). By default, GPOs
applicable to both the computer and the user are applied. However, an
administrative option can be set on a GPO that results in the GPO's
user-based policy settings being ignored. Additionally, a GPO can never
be **directly** linked to a policy target (i.e. computer or user).
Instead, a policy target inherits the policy settings of GPOs linked to
its enclosing site, domain, and OU. This inheritance sometimes results
in conflicts, meaning that two policy settings have the same name but
different values. In case of conflict, the OU has the highest priority,
followed by domain, followed by site. There is no concept of
fine-grained merging; a conflicting policy setting with lower priority
is discarded completely. Note that an administrative option to disable
inheritance can be set at any site, domain, and/or OU.

A GPO is identified by a gpo-guid, and it contains a set of Client Side
Extensions (CSEs), each identified by a cse-guid. A CSE represents a
class of policy settings (e.g. "Security Settings", "Registry Settings",
etc) that can be retrieved, parsed, and stored by a specific client-side
module (corresponding to the cse-guid). Note that both a CSE plugin
module and its corresponding CSE enforcement mechanism must have
knowledge of where the policy settings are being stored (and in what
format)." Note also that a cse-guid's policy settings are ignored if no
GPO Plugin Module has been registered for that cse-guid. Additionally,
note that policy settings are not retrieved if the DC's policy version
matches the cached policy version (since nothing has changed on the DC).
Since policy settings are typically not changed frequently, this means
that only the GPO version file typically needs to be retrieved (to
perform the version check) and that policy settings don't need to be
retrieved (unless they have changed).

A GPO's information is stored in two locations. A GPO's metadata (e.g.
version, cse-guids, etc) are stored as attributes in an LDAP
groupPolicyContainer object on the DC's LDAP server. A GPO's policy
settings are stored in a set of CSE-specific files on the DC's SMB/CIFS
file server (in the SYSVOL file share).

The following diagram provides a simplified summary of how this
information is stored on the DC. Note that each site/domain/ou may be
associated with multiple GPOs, with each GPO associated with multiple
CSEs, with each CSE associated with multiple policy settings.

``` {.wiki}
- LDAP
  - site/domain/ou
    - list of gpo-guids
  - gpo
    - gpo-guid
    - list of cse-guids
- SMB/CIFS
  - SYSVOL/<domain>/Policies/<gpo-guid>/<cse-specific-file>
    - cse-specific policy settings (name/value pairs)
    - for example:
      - Allow Logon Locally = <allowed-user-sid>*, <allowed-group-sid>*
      - Deny Logon Locally  = <denied-user-sid>*,  <denied-group-sid>*
```
