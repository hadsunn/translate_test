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

Supported Versions: [Current](/docs/current/auth-password.html "PostgreSQL 17
- 21.5. Password Authentication") ([17](/docs/17/auth-password.html
"PostgreSQL 17 - 21.5. Password Authentication")) / [16](/docs/16/auth-
password.html "PostgreSQL 16 - 21.5. Password Authentication") /
[15](/docs/15/auth-password.html "PostgreSQL 15 - 21.5. Password
Authentication") / [14](/docs/14/auth-password.html "PostgreSQL 14 -
21.5. Password Authentication") / [13](/docs/13/auth-password.html "PostgreSQL
13 - 21.5. Password Authentication")

Development Versions: [18](/docs/18/auth-password.html "PostgreSQL 18 -
21.5. Password Authentication") / [devel](/docs/devel/auth-password.html
"PostgreSQL devel - 21.5. Password Authentication")

Unsupported versions: [12](/docs/12/auth-password.html "PostgreSQL 12 -
21.5. Password Authentication") / [11](/docs/11/auth-password.html "PostgreSQL
11 - 21.5. Password Authentication")

__

21.5. Password Authentication  
---  
[Prev](auth-trust.html "21.4. Trust Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") | Chapter 21. Client Authentication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](gssapi-auth.html "21.6. GSSAPI Authentication")  
  
* * *

## 21.5. Password Authentication #

There are several password-based authentication methods. These methods operate
similarly but differ in how the users' passwords are stored on the server and
how the password provided by a client is sent across the connection.

`scram-sha-256`

    

The method `scram-sha-256` performs SCRAM-SHA-256 authentication, as described
in [RFC 7677](https://datatracker.ietf.org/doc/html/rfc7677). It is a
challenge-response scheme that prevents password sniffing on untrusted
connections and supports storing passwords on the server in a
cryptographically hashed form that is thought to be secure.

This is the most secure of the currently provided methods, but it is not
supported by older client libraries.

`md5`

    

The method `md5` uses a custom less secure challenge-response mechanism. It
prevents password sniffing and avoids storing passwords on the server in plain
text but provides no protection if an attacker manages to steal the password
hash from the server. Also, the MD5 hash algorithm is nowadays no longer
considered secure against determined attacks.

The `md5` method cannot be used with the [db_user_namespace](runtime-config-
connection.html#GUC-DB-USER-NAMESPACE) feature.

To ease transition from the `md5` method to the newer SCRAM method, if `md5`
is specified as a method in `pg_hba.conf` but the user's password on the
server is encrypted for SCRAM (see below), then SCRAM-based authentication
will automatically be chosen instead.

`password`

    

The method `password` sends the password in clear-text and is therefore
vulnerable to password “sniffing” attacks. It should always be avoided if
possible. If the connection is protected by SSL encryption then `password` can
be used safely, though. (Though SSL certificate authentication might be a
better choice if one is depending on using SSL).

PostgreSQL database passwords are separate from operating system user
passwords. The password for each database user is stored in the `pg_authid`
system catalog. Passwords can be managed with the SQL commands [CREATE
ROLE](sql-createrole.html "CREATE ROLE") and [ALTER ROLE](sql-alterrole.html
"ALTER ROLE"), e.g., **`CREATE ROLE foo WITH LOGIN PASSWORD 'secret'`** , or
the psql command `\password`. If no password has been set up for a user, the
stored password is null and password authentication will always fail for that
user.

The availability of the different password-based authentication methods
depends on how a user's password on the server is encrypted (or hashed, more
accurately). This is controlled by the configuration parameter
[password_encryption](runtime-config-connection.html#GUC-PASSWORD-ENCRYPTION)
at the time the password is set. If a password was encrypted using the `scram-
sha-256` setting, then it can be used for the authentication methods `scram-
sha-256` and `password` (but password transmission will be in plain text in
the latter case). The authentication method specification `md5` will
automatically switch to using the `scram-sha-256` method in this case, as
explained above, so it will also work. If a password was encrypted using the
`md5` setting, then it can be used only for the `md5` and `password`
authentication method specifications (again, with the password transmitted in
plain text in the latter case). (Previous PostgreSQL releases supported
storing the password on the server in plain text. This is no longer possible.)
To check the currently stored password hashes, see the system catalog
`pg_authid`.

To upgrade an existing installation from `md5` to `scram-sha-256`, after
having ensured that all client libraries in use are new enough to support
SCRAM, set `password_encryption = 'scram-sha-256'` in `postgresql.conf`, make
all users set new passwords, and change the authentication method
specifications in `pg_hba.conf` to `scram-sha-256`.

* * *

[Prev](auth-trust.html "21.4. Trust Authentication")  | [Up](client-authentication.html "Chapter 21. Client Authentication") |  [Next](gssapi-auth.html "21.6. GSSAPI Authentication")  
---|---|---  
21.4. Trust Authentication  | [Home](index.html "PostgreSQL 16.9 Documentation") |  21.6. GSSAPI Authentication  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/auth-password.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

