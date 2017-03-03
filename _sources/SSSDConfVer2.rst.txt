.. code:: wiki

    [sssd]
    config_file_version = 2
    services = nss, pam
    domains = mybox.example.com, ldap.example.com, ipa.example.com, nis.example.com
    # sbus_timeout = 300

    [nss]
    nss_filter_groups = root
    nss_filter_users = root
    nss_entry_cache_timeout = 30
    nss_enum_cache_timeout = 30

    [domain/mybox.example.com]
    domain_type = local
    enumerate = true
    min_id = 1000
    # max_id = 2000

    local_default_shell = /bin/bash
    local_default_homedir = /home

    # Possible overrides
    # id_provider = local
    # auth_provider = local
    # authz_provider = local
    # passwd_provider = local

    [domain/ldap.example.com]
    domain_type = ldap
    server = ldap.example.com, ldap3.example.com, 10.0.0.2
    # ldap_uri = ldaps://ldap.example.com:9093
    # ldap_use_tls = ssl
    ldap_user_search_base = ou=users,dc=ldap,dc=example,dc=com
    enumerate = false

    # Possible overrides
    # id_provider = ldap
    # id_server = ldap2.example.com
    # auth_provider = krb5
    # auth_server = krb5.example.com 
    # krb5_realm = KRB5.EXAMPLE.COM

    [domain/ipa.example.com]
    domain_type = ipa
    server = ipa.example.com, ipa2.example.com
    enumerate = false

    # Possible overrides
    # id_provider = ldap
    # id_server = ldap2.example.com
    # auth_provider = krb5
    # auth_server = krb5.example.com 
    # krb5_realm = KRB5.EXAMPLE.COM

    [domain/nis.example.com]
    id_provider = proxy
    proxy_lib = nis
    auth_provider = proxy
    proxy_auth_target = nis_pam_proxy
