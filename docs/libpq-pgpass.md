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

Supported Versions: [Current](/docs/current/libpq-pgpass.html "PostgreSQL 17 -
34.16. The Password File") ([17](/docs/17/libpq-pgpass.html "PostgreSQL 17 -
34.16. The Password File")) / [16](/docs/16/libpq-pgpass.html "PostgreSQL 16 -
34.16. The Password File") / [15](/docs/15/libpq-pgpass.html "PostgreSQL 15 -
34.16. The Password File") / [14](/docs/14/libpq-pgpass.html "PostgreSQL 14 -
34.16. The Password File") / [13](/docs/13/libpq-pgpass.html "PostgreSQL 13 -
34.16. The Password File")

Development Versions: [18](/docs/18/libpq-pgpass.html "PostgreSQL 18 -
34.16. The Password File") / [devel](/docs/devel/libpq-pgpass.html "PostgreSQL
devel - 34.16. The Password File")

Unsupported versions: [12](/docs/12/libpq-pgpass.html "PostgreSQL 12 -
34.16. The Password File") / [11](/docs/11/libpq-pgpass.html "PostgreSQL 11 -
34.16. The Password File") / [10](/docs/10/libpq-pgpass.html "PostgreSQL 10 -
34.16. The Password File") / [9.6](/docs/9.6/libpq-pgpass.html "PostgreSQL 9.6
- 34.16. The Password File") / [9.5](/docs/9.5/libpq-pgpass.html "PostgreSQL
9.5 - 34.16. The Password File") / [9.4](/docs/9.4/libpq-pgpass.html
"PostgreSQL 9.4 - 34.16. The Password File") / [9.3](/docs/9.3/libpq-
pgpass.html "PostgreSQL 9.3 - 34.16. The Password File") /
[9.2](/docs/9.2/libpq-pgpass.html "PostgreSQL 9.2 - 34.16. The Password File")
/ [9.1](/docs/9.1/libpq-pgpass.html "PostgreSQL 9.1 - 34.16. The Password
File") / [9.0](/docs/9.0/libpq-pgpass.html "PostgreSQL 9.0 - 34.16. The
Password File") / [8.4](/docs/8.4/libpq-pgpass.html "PostgreSQL 8.4 -
34.16. The Password File") / [8.3](/docs/8.3/libpq-pgpass.html "PostgreSQL 8.3
- 34.16. The Password File") / [8.2](/docs/8.2/libpq-pgpass.html "PostgreSQL
8.2 - 34.16. The Password File") / [8.1](/docs/8.1/libpq-pgpass.html
"PostgreSQL 8.1 - 34.16. The Password File") / [8.0](/docs/8.0/libpq-
pgpass.html "PostgreSQL 8.0 - 34.16. The Password File") /
[7.4](/docs/7.4/libpq-pgpass.html "PostgreSQL 7.4 - 34.16. The Password File")

__

34.16. The Password File  
---  
[Prev](libpq-envars.html "34.15. Environment Variables")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-pgservice.html "34.17. The Connection Service File")  
  
* * *

## 34.16. The Password File #

The file `.pgpass` in a user's home directory can contain passwords to be used
if the connection requires a password (and no password has been specified
otherwise). On Microsoft Windows the file is named
`%APPDATA%\postgresql\pgpass.conf` (where `%APPDATA%` refers to the
Application Data subdirectory in the user's profile). Alternatively, the
password file to use can be specified using the connection parameter
[passfile](libpq-connect.html#LIBPQ-CONNECT-PASSFILE) or the environment
variable `PGPASSFILE`.

This file should contain lines of the following format:

    
    
    _hostname_ :_port_ :_database_ :_username_ :_password_
    

(You can add a reminder comment to the file by copying the line above and
preceding it with `#`.) Each of the first four fields can be a literal value,
or `*`, which matches anything. The password field from the first line that
matches the current connection parameters will be used. (Therefore, put more-
specific entries first when you are using wildcards.) If an entry needs to
contain `:` or `\`, escape this character with `\`. The host name field is
matched to the `host` connection parameter if that is specified, otherwise to
the `hostaddr` parameter if that is specified; if neither are given then the
host name `localhost` is searched for. The host name `localhost` is also
searched for when the connection is a Unix-domain socket connection and the
`host` parameter matches libpq's default socket directory path. In a standby
server, a database field of `replication` matches streaming replication
connections made to the primary server. The database field is of limited
usefulness otherwise, because users have the same password for all databases
in the same cluster.

On Unix systems, the permissions on a password file must disallow any access
to world or group; achieve this by a command such as `chmod 0600 ~/.pgpass`.
If the permissions are less strict than this, the file will be ignored. On
Microsoft Windows, it is assumed that the file is stored in a directory that
is secure, so no special permissions check is made.

* * *

[Prev](libpq-envars.html "34.15. Environment Variables")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](libpq-pgservice.html "34.17. The Connection Service File")  
---|---|---  
34.15. Environment Variables  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.17. The Connection Service File  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-pgpass.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

