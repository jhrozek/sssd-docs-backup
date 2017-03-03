SSSD
----

**No .k5login file**

**.k5login file including user1**

**.k5login file not including user1**

**Password login (user1->user1)**

Access granted

Access granted

Access granted

**GSSAPI Login (user1->user2)**

Prompted for password

Access granted

Prompted for password

pam\_krb5.so
------------

**No .k5login file**

**.k5login file including user1**

**.k5login file not including user1**

**Password login (user1->user1)**

Access granted

Access granted

Access denied

**GSSAPI Login (user1->user2)**

Prompted for password

Access granted

Prompted for password
