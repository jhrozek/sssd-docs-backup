  ------------ ----------------------------------------------------------------------- ---------------- ----------------
  **Author**   **Patch**                                                               **Reviewer**     **Status**
  jhrozek      ~~Use service discovery in backends (sssd 1.2)~~                        mnagy or sbose   Acked
  jhrozek      ~~Use all available servers in LDAP provider~~                          sgallagh         Acked
  jhrozek      ~~Improve the offline authentication message~~                          sgallagh         Acked
  mnagy        ~~Make ldap simple bind asynchronous~~                                  sgallagh, simo   Deferred
  sbose        ~~Add more warnings about nearly expired passwords~~                    jhrozek          Acked
  sbose        ~~Handle krb5 password expiration warning~~                             sgallagh         Acked
  sbose        ~~Add support for delayed kinit if offline (sssd-1-2 only)~~            sgallagh         Acked
  sbose        Add retry option to pam\_sss                                            jhrozek          Needs revision
  sbose        ~~Create kdcinfo and kpasswdinfo file at startup~~                      sgallagh         Acked
  sgallagh     ~~Add callback when the ID provider switches from offline to online~~   sbose            Acked
  sgallagh     ~~Properly set up SIGCHLD handlers~~                                    sbose            Acked
  sgallagh     ~~Add dynamic DNS updates to FreeIPA~~                                  jhrozek, mnagy   Acked
  sgallagh     ~~Clean up kdcinfo and kpasswdinfo files when exiting~~                 jhrozek          Acked
  sgallagh     ~~Make krb5\_kpasswd available for any krb5 provider~~                  jhrozek          Acked
  sgallagh     ~~Fix segfault in GSSAPI reconnect code~~                               dpal, jhrozek    Acked
  ------------ ----------------------------------------------------------------------- ---------------- ----------------


