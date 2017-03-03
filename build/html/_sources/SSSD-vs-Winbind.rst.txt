This is a summary of recent discussion on sssd-devel and freeipa-users
mailing lists.

**Winbind:**

support for cross forest trusts

-  SSSD didn't support trusted domains until 1.10 at all. Starting with
   1.10, trusted domains in a single forest are supported.

can use MS-RPC to handle legacy NT/Samba3 domains

can do NTLM authentication

very exotic crashes sometimes occur, winbind doesn't recover from them

low performance in comparison with nss\_ldap + nscd

the need for system to be a domain member

in environments with several different flavors of Linux, it's wasn't
always possible to use Winbind the same way on all machines; RHEL3's
Samba for example was not quite up to the task

uncomfortable debugging (obscure protocol in comparison with LDAP/krb5)

**SSSD:**

-  more stable and faster than winbind
-  1:1 mapping between ID and AUTH domains
-  if anything goes wrong, it is generally easy to debug, since all
   business logic is in SSSD code
-  option to run without joining the domain

   -  definitely convenient in many cases

In general, some support for Active Directory integration landed in 1.9,
such as support for mapping SIDs to IDs or the Active Directory
provider. More features were introduced in 1.10 such as the ability to
perform site discovery or DNS updates.

**misc:**

-  it is possible to configure winbind with sssd on one system
