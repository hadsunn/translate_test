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

Supported Versions: [Current](/docs/current/contrib-dblink-connect-u.html
"PostgreSQL 17 - dblink_connect_u") ([17](/docs/17/contrib-dblink-
connect-u.html "PostgreSQL 17 - dblink_connect_u")) / [16](/docs/16/contrib-
dblink-connect-u.html "PostgreSQL 16 - dblink_connect_u") /
[15](/docs/15/contrib-dblink-connect-u.html "PostgreSQL 15 -
dblink_connect_u") / [14](/docs/14/contrib-dblink-connect-u.html "PostgreSQL
14 - dblink_connect_u") / [13](/docs/13/contrib-dblink-connect-u.html
"PostgreSQL 13 - dblink_connect_u")

Development Versions: [18](/docs/18/contrib-dblink-connect-u.html "PostgreSQL
18 - dblink_connect_u") / [devel](/docs/devel/contrib-dblink-connect-u.html
"PostgreSQL devel - dblink_connect_u")

Unsupported versions: [12](/docs/12/contrib-dblink-connect-u.html "PostgreSQL
12 - dblink_connect_u") / [11](/docs/11/contrib-dblink-connect-u.html
"PostgreSQL 11 - dblink_connect_u") / [10](/docs/10/contrib-dblink-
connect-u.html "PostgreSQL 10 - dblink_connect_u") / [9.6](/docs/9.6/contrib-
dblink-connect-u.html "PostgreSQL 9.6 - dblink_connect_u") /
[9.5](/docs/9.5/contrib-dblink-connect-u.html "PostgreSQL 9.5 -
dblink_connect_u") / [9.4](/docs/9.4/contrib-dblink-connect-u.html "PostgreSQL
9.4 - dblink_connect_u") / [9.3](/docs/9.3/contrib-dblink-connect-u.html
"PostgreSQL 9.3 - dblink_connect_u") / [9.2](/docs/9.2/contrib-dblink-
connect-u.html "PostgreSQL 9.2 - dblink_connect_u") / [9.1](/docs/9.1/contrib-
dblink-connect-u.html "PostgreSQL 9.1 - dblink_connect_u") /
[9.0](/docs/9.0/contrib-dblink-connect-u.html "PostgreSQL 9.0 -
dblink_connect_u") / [8.4](/docs/8.4/contrib-dblink-connect-u.html "PostgreSQL
8.4 - dblink_connect_u") / [8.3](/docs/8.3/contrib-dblink-connect-u.html
"PostgreSQL 8.3 - dblink_connect_u")

__

dblink_connect_u  
---  
[Prev](contrib-dblink-connect.html "dblink_connect")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") | F.12. dblink — connect to other PostgreSQL databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-disconnect.html "dblink_disconnect")  
  
* * *

## dblink_connect_u

dblink_connect_u — opens a persistent connection to a remote database,
insecurely

## Synopsis

    
    
    dblink_connect_u(text connstr) returns text
    dblink_connect_u(text connname, text connstr) returns text
    

## Description

`dblink_connect_u()` is identical to `dblink_connect()`, except that it will
allow non-superusers to connect using any authentication method.

If the remote server selects an authentication method that does not involve a
password, then impersonation and subsequent escalation of privileges can
occur, because the session will appear to have originated from the user as
which the local PostgreSQL server runs. Also, even if the remote server does
demand a password, it is possible for the password to be supplied from the
server environment, such as a `~/.pgpass` file belonging to the server's user.
This opens not only a risk of impersonation, but the possibility of exposing a
password to an untrustworthy remote server. Therefore, `dblink_connect_u()` is
initially installed with all privileges revoked from `PUBLIC`, making it un-
callable except by superusers. In some situations it may be appropriate to
grant `EXECUTE` permission for `dblink_connect_u()` to specific users who are
considered trustworthy, but this should be done with care. It is also
recommended that any `~/.pgpass` file belonging to the server's user _not_
contain any records specifying a wildcard host name.

For further details see `dblink_connect()`.

* * *

[Prev](contrib-dblink-connect.html "dblink_connect")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") |  [Next](contrib-dblink-disconnect.html "dblink_disconnect")  
---|---|---  
dblink_connect  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink_disconnect  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-dblink-
connect-u.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

