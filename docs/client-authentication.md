[ ![PostgreSQL Elephant Logo](/media/img/about/press/elephant.png) ](/)

  * [Home](/ "Home")
  * [About](/about/ "About")
  * [Download](/download/ "Download")
  * [Documentation](/docs/ "Documentation")
  * [Community](/community/ "Community")
  * [Developers](/developer/ "Developers")
  * [Support](/support/ "Support")
  * [Donate](/about/donate/ "Donate")
  * [Your account](/account/ "Your account")

__

May 8, 2025: [ PostgreSQL 17.5, 16.9, 15.13, 14.18, and 13.21 Released! ](/about/news/postgresql-175-169-1513-1418-and-1321-released-3072/) | [ PostgreSQL 18 Beta 1 Released! ](/about/news/postgresql-18-beta-1-released-3070/)

[Documentation](/docs/ "Documentation") -> [PostgreSQL
16](/docs/16/index.html)

Supported Versions: [Current](/docs/current/client-authentication.html
"PostgreSQL 17 - Chapter 21. Client Authentication") ([17](/docs/17/client-
authentication.html "PostgreSQL 17 - Chapter 21. Client Authentication")) /
[16](/docs/16/client-authentication.html "PostgreSQL 16 - Chapter 21. Client
Authentication") / [15](/docs/15/client-authentication.html "PostgreSQL 15 -
Chapter 21. Client Authentication") / [14](/docs/14/client-authentication.html
"PostgreSQL 14 - Chapter 21. Client Authentication") / [13](/docs/13/client-
authentication.html "PostgreSQL 13 - Chapter 21. Client Authentication")

Development Versions: [18](/docs/18/client-authentication.html "PostgreSQL 18
- Chapter 21. Client Authentication") / [devel](/docs/devel/client-
authentication.html "PostgreSQL devel - Chapter 21. Client Authentication")

Unsupported versions: [12](/docs/12/client-authentication.html "PostgreSQL 12
- Chapter 21. Client Authentication") / [11](/docs/11/client-
authentication.html "PostgreSQL 11 - Chapter 21. Client Authentication") /
[10](/docs/10/client-authentication.html "PostgreSQL 10 - Chapter 21. Client
Authentication") / [9.6](/docs/9.6/client-authentication.html "PostgreSQL 9.6
- Chapter 21. Client Authentication") / [9.5](/docs/9.5/client-
authentication.html "PostgreSQL 9.5 - Chapter 21. Client Authentication") /
[9.4](/docs/9.4/client-authentication.html "PostgreSQL 9.4 -
Chapter 21. Client Authentication") / [9.3](/docs/9.3/client-
authentication.html "PostgreSQL 9.3 - Chapter 21. Client Authentication") /
[9.2](/docs/9.2/client-authentication.html "PostgreSQL 9.2 -
Chapter 21. Client Authentication") / [9.1](/docs/9.1/client-
authentication.html "PostgreSQL 9.1 - Chapter 21. Client Authentication") /
[9.0](/docs/9.0/client-authentication.html "PostgreSQL 9.0 -
Chapter 21. Client Authentication") / [8.4](/docs/8.4/client-
authentication.html "PostgreSQL 8.4 - Chapter 21. Client Authentication") /
[8.3](/docs/8.3/client-authentication.html "PostgreSQL 8.3 -
Chapter 21. Client Authentication") / [8.2](/docs/8.2/client-
authentication.html "PostgreSQL 8.2 - Chapter 21. Client Authentication") /
[8.1](/docs/8.1/client-authentication.html "PostgreSQL 8.1 -
Chapter 21. Client Authentication") / [8.0](/docs/8.0/client-
authentication.html "PostgreSQL 8.0 - Chapter 21. Client Authentication") /
[7.4](/docs/7.4/client-authentication.html "PostgreSQL 7.4 -
Chapter 21. Client Authentication") / [7.3](/docs/7.3/client-
authentication.html "PostgreSQL 7.3 - Chapter 21. Client Authentication") /
[7.2](/docs/7.2/client-authentication.html "PostgreSQL 7.2 -
Chapter 21. Client Authentication") / [7.1](/docs/7.1/client-
authentication.html "PostgreSQL 7.1 - Chapter 21. Client Authentication")

__

Chapter 21. Client Authentication  
---  
[Prev](runtime-config-short.html "20.18. Short Options")  | [Up](admin.html "Part III. Server Administration") | Part III. Server Administration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](auth-pg-hba-conf.html "21.1. The pg_hba.conf File")  
  
* * *

## Chapter 21. Client Authentication

**Table of Contents**

[21.1. The `pg_hba.conf` File](auth-pg-hba-conf.html)

[21.2. User Name Maps](auth-username-maps.html)

[21.3. Authentication Methods](auth-methods.html)

[21.4. Trust Authentication](auth-trust.html)

[21.5. Password Authentication](auth-password.html)

[21.6. GSSAPI Authentication](gssapi-auth.html)

[21.7. SSPI Authentication](sspi-auth.html)

[21.8. Ident Authentication](auth-ident.html)

[21.9. Peer Authentication](auth-peer.html)

[21.10. LDAP Authentication](auth-ldap.html)

[21.11. RADIUS Authentication](auth-radius.html)

[21.12. Certificate Authentication](auth-cert.html)

[21.13. PAM Authentication](auth-pam.html)

[21.14. BSD Authentication](auth-bsd.html)

[21.15. Authentication Problems](client-authentication-problems.html)

When a client application connects to the database server, it specifies which
PostgreSQL database user name it wants to connect as, much the same way one
logs into a Unix computer as a particular user. Within the SQL environment the
active database user name determines access privileges to database objects —
see [Chapter 22](user-manag.html "Chapter 22. Database Roles") for more
information. Therefore, it is essential to restrict which database users can
connect.

### Note

As explained in [Chapter 22](user-manag.html "Chapter 22. Database Roles"),
PostgreSQL actually does privilege management in terms of “roles”. In this
chapter, we consistently use _database user_ to mean “role with the `LOGIN`
privilege”.

_Authentication_ is the process by which the database server establishes the
identity of the client, and by extension determines whether the client
application (or the user who runs the client application) is permitted to
connect with the database user name that was requested.

PostgreSQL offers a number of different client authentication methods. The
method used to authenticate a particular client connection can be selected on
the basis of (client) host address, database, and user.

PostgreSQL database user names are logically separate from user names of the
operating system in which the server runs. If all the users of a particular
server also have accounts on the server's machine, it makes sense to assign
database user names that match their operating system user names. However, a
server that accepts remote connections might have many database users who have
no local operating system account, and in such cases there need be no
connection between database user names and OS user names.

* * *

[Prev](runtime-config-short.html "20.18. Short Options")  | [Up](admin.html "Part III. Server Administration") |  [Next](auth-pg-hba-conf.html "21.1. The pg_hba.conf File")  
---|---|---  
20.18. Short Options  | [Home](index.html "PostgreSQL 16.9 Documentation") |  21.1. The `pg_hba.conf` File  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/client-authentication.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

