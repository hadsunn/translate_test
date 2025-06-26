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

Supported Versions: [Current](/docs/current/dblink.html "PostgreSQL 17 -
F.12. dblink — connect to other PostgreSQL databases")
([17](/docs/17/dblink.html "PostgreSQL 17 - F.12. dblink — connect to other
PostgreSQL databases")) / [16](/docs/16/dblink.html "PostgreSQL 16 -
F.12. dblink — connect to other PostgreSQL databases") /
[15](/docs/15/dblink.html "PostgreSQL 15 - F.12. dblink — connect to other
PostgreSQL databases") / [14](/docs/14/dblink.html "PostgreSQL 14 -
F.12. dblink — connect to other PostgreSQL databases") /
[13](/docs/13/dblink.html "PostgreSQL 13 - F.12. dblink — connect to other
PostgreSQL databases")

Development Versions: [18](/docs/18/dblink.html "PostgreSQL 18 - F.12. dblink
— connect to other PostgreSQL databases") / [devel](/docs/devel/dblink.html
"PostgreSQL devel - F.12. dblink — connect to other PostgreSQL databases")

Unsupported versions: [12](/docs/12/dblink.html "PostgreSQL 12 - F.12. dblink
— connect to other PostgreSQL databases") / [11](/docs/11/dblink.html
"PostgreSQL 11 - F.12. dblink — connect to other PostgreSQL databases") /
[10](/docs/10/dblink.html "PostgreSQL 10 - F.12. dblink — connect to other
PostgreSQL databases") / [9.6](/docs/9.6/dblink.html "PostgreSQL 9.6 -
F.12. dblink — connect to other PostgreSQL databases") /
[9.5](/docs/9.5/dblink.html "PostgreSQL 9.5 - F.12. dblink — connect to other
PostgreSQL databases") / [9.4](/docs/9.4/dblink.html "PostgreSQL 9.4 -
F.12. dblink — connect to other PostgreSQL databases") /
[9.3](/docs/9.3/dblink.html "PostgreSQL 9.3 - F.12. dblink — connect to other
PostgreSQL databases") / [9.2](/docs/9.2/dblink.html "PostgreSQL 9.2 -
F.12. dblink — connect to other PostgreSQL databases") /
[9.1](/docs/9.1/dblink.html "PostgreSQL 9.1 - F.12. dblink — connect to other
PostgreSQL databases") / [9.0](/docs/9.0/dblink.html "PostgreSQL 9.0 -
F.12. dblink — connect to other PostgreSQL databases") /
[8.4](/docs/8.4/dblink.html "PostgreSQL 8.4 - F.12. dblink — connect to other
PostgreSQL databases") / [8.3](/docs/8.3/dblink.html "PostgreSQL 8.3 -
F.12. dblink — connect to other PostgreSQL databases")

__

F.12. dblink — connect to other PostgreSQL databases  
---  
[Prev](cube.html "F.11. cube — a multi-dimensional cube data type")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-connect.html "dblink_connect")  
  
* * *

## F.12. dblink — connect to other PostgreSQL databases #

[dblink_connect](contrib-dblink-connect.html) — opens a persistent connection
to a remote database

[dblink_connect_u](contrib-dblink-connect-u.html) — opens a persistent
connection to a remote database, insecurely

[dblink_disconnect](contrib-dblink-disconnect.html) — closes a persistent
connection to a remote database

[dblink](contrib-dblink-function.html) — executes a query in a remote database

[dblink_exec](contrib-dblink-exec.html) — executes a command in a remote
database

[dblink_open](contrib-dblink-open.html) — opens a cursor in a remote database

[dblink_fetch](contrib-dblink-fetch.html) — returns rows from an open cursor
in a remote database

[dblink_close](contrib-dblink-close.html) — closes a cursor in a remote
database

[dblink_get_connections](contrib-dblink-get-connections.html) — returns the
names of all open named dblink connections

[dblink_error_message](contrib-dblink-error-message.html) — gets last error
message on the named connection

[dblink_send_query](contrib-dblink-send-query.html) — sends an async query to
a remote database

[dblink_is_busy](contrib-dblink-is-busy.html) — checks if connection is busy
with an async query

[dblink_get_notify](contrib-dblink-get-notify.html) — retrieve async
notifications on a connection

[dblink_get_result](contrib-dblink-get-result.html) — gets an async query
result

[dblink_cancel_query](contrib-dblink-cancel-query.html) — cancels any active
query on the named connection

[dblink_get_pkey](contrib-dblink-get-pkey.html) — returns the positions and
field names of a relation's primary key fields

[dblink_build_sql_insert](contrib-dblink-build-sql-insert.html) — builds an
INSERT statement using a local tuple, replacing the primary key field values
with alternative supplied values

[dblink_build_sql_delete](contrib-dblink-build-sql-delete.html) — builds a
DELETE statement using supplied values for primary key field values

[dblink_build_sql_update](contrib-dblink-build-sql-update.html) — builds an
UPDATE statement using a local tuple, replacing the primary key field values
with alternative supplied values

`dblink` is a module that supports connections to other PostgreSQL databases
from within a database session.

See also [postgres_fdw](postgres-fdw.html "F.38. postgres_fdw — access data
stored in external PostgreSQL servers"), which provides roughly the same
functionality using a more modern and standards-compliant infrastructure.

* * *

[Prev](cube.html "F.11. cube — a multi-dimensional cube data type")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](contrib-dblink-connect.html "dblink_connect")  
---|---|---  
F.11. cube — a multi-dimensional cube data type  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink_connect  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/dblink.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

