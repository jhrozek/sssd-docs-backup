Commits missing from the master branch:

**Commit**

**Owner**

**Reviewer**

**Patch**

**Status**

~~Support password changes in chpass\_provider = proxy~~

sgallagh

~~Fix queuing bug in proxy provider~~

sgallagh

Merged with "Proxy provider PAM handling"

Use new schema for HBAC service checks

sbose

~~Check ipaEnabledFlag~~

sbose

commit
[eb812bb807d65309c037c6a806b728c637e9b0fa](https://fedorahosted.org/sssd/changeset/eb812bb807d65309c037c6a806b728c637e9b0fa/ "Check ipaEnabledFlag"){.changeset}
applies cleanly

~~Proxy provider PAM handling in child process~~

sgallagh

~~Fix error reporting for be\_pam\_handler~~

sgallagh

[Fix error reporting for
be\_pam\_handler](https://fedorahosted.org/sssd/attachment/wiki/Merges12/0002-Fix-error-reporting-for-be_pam_handler.patch "Attachment '0002-Fix-error-reporting-for-be_pam_handler.patch' in Merges12"){.attachment}[​](https://fedorahosted.org/sssd/raw-attachment/wiki/Merges12/0002-Fix-error-reporting-for-be_pam_handler.patch "Download"){.trac-rawlink}

Merges cleanly

~~Make data provider id\_callback public~~

sgallagh

[Make data provider id\_callback
public](https://fedorahosted.org/sssd/attachment/wiki/Merges12/0001-Make-data-provider-id_callback-public.patch "Attachment '0001-Make-data-provider-id_callback-public.patch' in Merges12"){.attachment}[​](https://fedorahosted.org/sssd/raw-attachment/wiki/Merges12/0001-Make-data-provider-id_callback-public.patch "Download"){.trac-rawlink}

Merges cleanly

~~Move parse\_args() to util~~

sbose

[Move parse\_args() to
util](https://fedorahosted.org/sssd/attachment/wiki/Merges12/0001-Move-parse_args-to-util.patch "Attachment '0001-Move-parse_args-to-util.patch' in Merges12"){.attachment}[​](https://fedorahosted.org/sssd/raw-attachment/wiki/Merges12/0001-Move-parse_args-to-util.patch "Download"){.trac-rawlink}

Merges cleanly

~~Remove signal event if child was terminated by a signal~~

sbose

commit
[209e37c000d1a236263af6dc89ca63909d1b8a45](https://fedorahosted.org/sssd/changeset/209e37c000d1a236263af6dc89ca63909d1b8a45/ "Remove signal event if child was terminated by a signal"){.changeset}
applies cleanly

~~Fix check if LDAP id provider is already initialized~~

sbose

commit
[e2f32ec2253f6034cc6290ed38a4a3a87a374014](https://fedorahosted.org/sssd/changeset/e2f32ec2253f6034cc6290ed38a4a3a87a374014/ "Fix check if LDAP id provider is already initialized"){.changeset}
applies cleanly

~~Reset run\_online\_cb flag even if there are no callbacks~~

sbose

commit
[eb405b4d76371abffebbc4cabb327db24167e02b](https://fedorahosted.org/sssd/changeset/eb405b4d76371abffebbc4cabb327db24167e02b/ "Reset run_online_cb flag even if there are no callbacks"){.changeset}
applies cleanly

~~Set ldap\_search\_timeout default to 5 seconds~~

sgallagh

[Set ldap\_search\_timeout default to 5
seconds](https://fedorahosted.org/sssd/attachment/wiki/Merges12/0001-Set-ldap_search_timeout-default-to-5-seconds.patch "Attachment '0001-Set-ldap_search_timeout-default-to-5-seconds.patch' in Merges12"){.attachment}[​](https://fedorahosted.org/sssd/raw-attachment/wiki/Merges12/0001-Set-ldap_search_timeout-default-to-5-seconds.patch "Download"){.trac-rawlink}

Merges cleanly

~~Remove unused ldap\_offline\_timeout option~~

sgallagh

[Remove unused ldap\_offline\_timeout
option](https://fedorahosted.org/sssd/attachment/wiki/Merges12/0001-Remove-unused-ldap_offline_timeout-option.patch "Attachment '0001-Remove-unused-ldap_offline_timeout-option.patch' in Merges12"){.attachment}[​](https://fedorahosted.org/sssd/raw-attachment/wiki/Merges12/0001-Remove-unused-ldap_offline_timeout-option.patch "Download"){.trac-rawlink}

Merges cleanly

~~Add offline callback to disconnect global SDAP handle~~

sbose

commit
[49942f408c33a91fd99deae7ca2b3005d6fb56fb](https://fedorahosted.org/sssd/changeset/49942f408c33a91fd99deae7ca2b3005d6fb56fb/ "Add offline callback to disconnect global SDAP handle"){.changeset}
applies cleanly

~~Add krb5 SIGTERM handler to ipa auth provider~~

sbose

~~Refactor krb5 SIGTERM handler installation~~

sbose

~~Krb5 locator plugin returns KRB5\_PLUGIN\_NO\_HANDLE~~

sbose

commit
[eea8d1fe65e5985bdba3dda1414497c668887c76](https://fedorahosted.org/sssd/changeset/eea8d1fe65e5985bdba3dda1414497c668887c76/ "Krb5 locator plugin returns KRB5_PLUGIN_NO_HANDLE

To allow a fallback to ..."){.changeset} applies cleanly

~~Add callback to remove krb5 info files when going offline~~

sbose

~~Add run\_callbacks flag~~

sbose

commit
[5f9ccdddd96fe97bc8f99fad2b13f7496e475e13](https://fedorahosted.org/sssd/changeset/5f9ccdddd96fe97bc8f99fad2b13f7496e475e13/ "Add run_callbacks flag"){.changeset}
applies cleanly

~~Refactor krb5\_finalize()~~

sbose

commit
[f28774b98000289ac1e3276fd3c3bb6f6c6a2332](https://fedorahosted.org/sssd/changeset/f28774b98000289ac1e3276fd3c3bb6f6c6a2332/ "Refactor krb5_finalize()"){.changeset}
applies cleanly

~~Add offline callbacks~~

sbose

commit
[c4c4fbee11e865053cfa4c03f4869458f78c9e32](https://fedorahosted.org/sssd/changeset/c4c4fbee11e865053cfa4c03f4869458f78c9e32/ "Add offline callbacks"){.changeset}
applies cleanly

~~Refactor data provider callbacks~~

sbose

commit
[955c7511d1e89b3151e1d280acbddd0f06e88059](https://fedorahosted.org/sssd/changeset/955c7511d1e89b3151e1d280acbddd0f06e88059/ "Refactor data provider callbacks"){.changeset}
applies cleanly

~~Revert "Create kdcinfo and kpasswdinfo file at startup"~~

sbose

[Revert "Create kdcinfo and kpasswdinfo file at
startup"](https://fedorahosted.org/sssd/attachment/wiki/Merges12/0001-Revert-Create-kdcinfo-and-kpasswdinfo-file-at-startu.patch "Attachment '0001-Revert-Create-kdcinfo-and-kpasswdinfo-file-at-startu.patch' in Merges12"){.attachment}[​](https://fedorahosted.org/sssd/raw-attachment/wiki/Merges12/0001-Revert-Create-kdcinfo-and-kpasswdinfo-file-at-startu.patch "Download"){.trac-rawlink}

~~Add ldap\_access\_filter option~~

sgallagh

sbose

[Add ldap\_access\_filter
option](https://fedorahosted.org/sssd/attachment/wiki/Merges12/0001-Add-ldap_access_filter-option.patch "Attachment '0001-Add-ldap_access_filter-option.patch' in Merges12"){.attachment}[​](https://fedorahosted.org/sssd/raw-attachment/wiki/Merges12/0001-Add-ldap_access_filter-option.patch "Download"){.trac-rawlink}

~~Add support for delayed kinit if offline~~

sbose

~~Handle Krb5 password expiration warning~~

sbose

sgallagh

[Handle Krb5 password expiration
warning](https://fedorahosted.org/sssd/attachment/wiki/Merges12/0001-Handle-Krb5-password-expiration-warning.patch "Attachment '0001-Handle-Krb5-password-expiration-warning.patch' in Merges12"){.attachment}[​](https://fedorahosted.org/sssd/raw-attachment/wiki/Merges12/0001-Handle-Krb5-password-expiration-warning.patch "Download"){.trac-rawlink}

On review

~~Try all servers during Kerberos auth~~

jhrozek

sgallagh

N/A

Acked

~~Copy pam data from DBus message~~

sbose

commit
[918c5863cf6f8e7b43c643dd623263df865cc109](https://fedorahosted.org/sssd/changeset/918c5863cf6f8e7b43c643dd623263df865cc109/ "Copy pam data from DBus message

Instead of just using references to the ..."){.changeset} applies
cleanly
