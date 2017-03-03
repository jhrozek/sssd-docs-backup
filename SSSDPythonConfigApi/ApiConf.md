`/etc/sssd/sssd.api.conf`

``` {.wiki}
# Format:
# option = type, subtype[, default]

[service]
# Options available to all services
debug_level = int, None, 0
command = str, None
reconnection_retries = int, None, 3

[sssd]
# Monitor service
config_file_version = int, 2
services = list, str, None, nss, pam
domains = list, str, None
sbus_timeout = int, None, -1
re_expression = str, None, (?P<name>[^@]+)@?(?P<domain>[^@]*$)
full_name_format = str, None, %1$s@%2$s

[nss]
# Name service
nss_enum_cache_timeout = int, None, 120
nss_entry_cache_timeout = int, None, 600
nss_entry_cache_no_wait_timeout = int, None, 0
nss_entry_negative_timeout = int, None, 15
nss_filter_users = list, str, None, root
nss_filter_groups = list, str, None, root
nss_filter_users_in_groups = bool, None, true

[pam]
# Authentication service

[provider]
#Available provider types
id_provider = str, None
auth_provider = str, None
authz_provider = str, None
passwd_provider = str, None

[domain]
# Options available to all domains
debug_level = int, None, 0
min_id = int, None, 1000
max_id = int, None, 0
timeout = int, None, 0
magic_private_groups = bool, None, false
enumerate = bool, None, true
cache_credentials = bool, None, false
use_fully_qualified_names = bool, None, false
```

`/etc/sssd/sssd.api.d/sssd-ldap.conf`

``` {.wiki}
[provider/ldap]
ldap_uri = str, None, ldap://localhost
ldap_schema = str, None, rfc2307
ldap_default_bind_dn = str, None
ldap_default_authtok_type = str, None
ldap_default_authtok = str, None
ldap_network_timeout = int, None, 5
ldap_opt_timeout = int, None, 5
ldap_tls_reqcert = str, None

[provider/ldap/id]
ldap_user_search_base = str, None
ldap_user_object_class = str, None, posixAccount
ldap_user_name = str, None, uid
ldap_user_uid_number = str, None, uidNumber
ldap_user_gid_number = str, None, gidNumber
ldap_user_gecos = str, None, gecos
ldap_user_homedir = str, None, homeDirectory
ldap_user_shell = str, None, loginShell
ldap_user_uuid = str, None, nsUniqueId
ldap_user_principal = str, None, krbPrincipalName
ldap_user_fullname = str, None, cn
ldap_user_memberof = str, None, memberOf
ldap_group_search_base = str, None
ldap_group_object_class = str, None, posixGroup
ldap_group_name = str, None, cn
ldap_group_gid_number = str, None, gidNumber
ldap_group_member = str, None
ldap_group_UUID = str, None, nsUniqueId
ldap_force_upper_case_realm = bool, None, False
```
