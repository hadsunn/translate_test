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

Supported Versions: [Current](/docs/current/auth-trust.html "PostgreSQL 17 -
21.4. Trust Authentication") ([17](/docs/17/auth-trust.html "PostgreSQL 17 -
21.4. Trust Authentication")) / [16](/docs/16/auth-trust.html "PostgreSQL 16 -
21.4. Trust Authentication") / [15](/docs/15/auth-trust.html "PostgreSQL 15 -
21.4. Trust Authentication") / [14](/docs/14/auth-trust.html "PostgreSQL 14 -
21.4. Trust Authentication") / [13](/docs/13/auth-trust.html "PostgreSQL 13 -
21.4. Trust Authentication")

Development Versions: [18](/docs/18/auth-trust.html "PostgreSQL 18 -
21.4. Trust Authentication") / [devel](/docs/devel/auth-trust.html "PostgreSQL
devel - 21.4. Trust Authentication")

Unsupported versions: [12](/docs/12/auth-trust.html "PostgreSQL 12 -
21.4. Trust Authentication") / [11](/docs/11/auth-trust.html "PostgreSQL 11 -
21.4. Trust Authentication")

__

21.4. Trust Authentication  
---  
[Prev](auth-methods.html "21.3. Authentication Methods")  | [Up](client-authentication.html "Chapter 21. Client Authentication") | Chapter 21. Client Authentication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](auth-password.html "21.5. Password Authentication")  
  
* * *

## 21.4. Trust Authentication #

When `trust` authentication is specified, PostgreSQL assumes that anyone who
can connect to the server is authorized to access the database with whatever
database user name they specify (even superuser names). Of course,
restrictions made in the `database` and `user` columns still apply. This
method should only be used when there is adequate operating-system-level
protection on connections to the server.

`trust` authentication is appropriate and very convenient for local
connections on a single-user workstation. It is usually _not_ appropriate by
itself on a multiuser machine. However, you might be able to use `trust` even
on a multiuser machine, if you restrict access to the server's Unix-domain
socket file using file-system permissions. To do this, set the
`unix_socket_permissions` (and possibly `unix_socket_group`) configuration
parameters as described in [Section 20.3](runtime-config-connection.html
"20.3. Connections and Authentication"). Or you could set the
`unix_socket_directories` configuration parameter to place the socket file in
a suitably restricted directory.

Setting file-system permissions only helps for Unix-socket connections. Local
TCP/IP connections are not restricted by file-system permissions. Therefore,
if you want to use file-system permissions for local security, remove the
`host ... 127.0.0.1 ...` line from `pg_hba.conf`, or change it to a
non-`trust` authentication method.

`trust` authentication is only suitable for TCP/IP connections if you trust
every user on every machine that is allowed to connect to the server by the
`pg_hba.conf` lines that specify `trust`. It is seldom reasonable to use
`trust` for any TCP/IP connections other than those from localhost
(127.0.0.1).

* * *

[Prev](auth-methods.html "21.3. Authentication Methods")  | [Up](client-authentication.html "Chapter 21. Client Authentication") |  [Next](auth-password.html "21.5. Password Authentication")  
---|---|---  
21.3. Authentication Methods  | [Home](index.html "PostgreSQL 16.9 Documentation") |  21.5. Password Authentication  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/auth-trust.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

