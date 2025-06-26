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

Supported Versions: [Current](/docs/current/reference-client.html "PostgreSQL
17 - PostgreSQL Client Applications") ([17](/docs/17/reference-client.html
"PostgreSQL 17 - PostgreSQL Client Applications")) / [16](/docs/16/reference-
client.html "PostgreSQL 16 - PostgreSQL Client Applications") /
[15](/docs/15/reference-client.html "PostgreSQL 15 - PostgreSQL Client
Applications") / [14](/docs/14/reference-client.html "PostgreSQL 14 -
PostgreSQL Client Applications") / [13](/docs/13/reference-client.html
"PostgreSQL 13 - PostgreSQL Client Applications")

Development Versions: [18](/docs/18/reference-client.html "PostgreSQL 18 -
PostgreSQL Client Applications") / [devel](/docs/devel/reference-client.html
"PostgreSQL devel - PostgreSQL Client Applications")

Unsupported versions: [12](/docs/12/reference-client.html "PostgreSQL 12 -
PostgreSQL Client Applications") / [11](/docs/11/reference-client.html
"PostgreSQL 11 - PostgreSQL Client Applications") / [10](/docs/10/reference-
client.html "PostgreSQL 10 - PostgreSQL Client Applications") /
[9.6](/docs/9.6/reference-client.html "PostgreSQL 9.6 - PostgreSQL Client
Applications") / [9.5](/docs/9.5/reference-client.html "PostgreSQL 9.5 -
PostgreSQL Client Applications") / [9.4](/docs/9.4/reference-client.html
"PostgreSQL 9.4 - PostgreSQL Client Applications") /
[9.3](/docs/9.3/reference-client.html "PostgreSQL 9.3 - PostgreSQL Client
Applications") / [9.2](/docs/9.2/reference-client.html "PostgreSQL 9.2 -
PostgreSQL Client Applications") / [9.1](/docs/9.1/reference-client.html
"PostgreSQL 9.1 - PostgreSQL Client Applications") /
[9.0](/docs/9.0/reference-client.html "PostgreSQL 9.0 - PostgreSQL Client
Applications") / [8.4](/docs/8.4/reference-client.html "PostgreSQL 8.4 -
PostgreSQL Client Applications") / [8.3](/docs/8.3/reference-client.html
"PostgreSQL 8.3 - PostgreSQL Client Applications") /
[8.2](/docs/8.2/reference-client.html "PostgreSQL 8.2 - PostgreSQL Client
Applications") / [8.1](/docs/8.1/reference-client.html "PostgreSQL 8.1 -
PostgreSQL Client Applications") / [8.0](/docs/8.0/reference-client.html
"PostgreSQL 8.0 - PostgreSQL Client Applications") /
[7.4](/docs/7.4/reference-client.html "PostgreSQL 7.4 - PostgreSQL Client
Applications") / [7.3](/docs/7.3/reference-client.html "PostgreSQL 7.3 -
PostgreSQL Client Applications") / [7.2](/docs/7.2/reference-client.html
"PostgreSQL 7.2 - PostgreSQL Client Applications") /
[7.1](/docs/7.1/reference-client.html "PostgreSQL 7.1 - PostgreSQL Client
Applications")

__

PostgreSQL Client Applications  
---  
[Prev](sql-values.html "VALUES")  | [Up](reference.html "Part VI. Reference") | Part VI. Reference | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](app-clusterdb.html "clusterdb")  
  
* * *

# PostgreSQL Client Applications

* * *

This part contains reference information for PostgreSQL client applications
and utilities. Not all of these commands are of general utility; some might
require special privileges. The common feature of these applications is that
they can be run on any host, independent of where the database server resides.

When specified on the command line, user and database names have their case
preserved — the presence of spaces or special characters might require
quoting. Table names and other identifiers do not have their case preserved,
except where documented, and might require quoting.

**Table of Contents**

[clusterdb](app-clusterdb.html) — cluster a PostgreSQL database

[createdb](app-createdb.html) — create a new PostgreSQL database

[createuser](app-createuser.html) — define a new PostgreSQL user account

[dropdb](app-dropdb.html) — remove a PostgreSQL database

[dropuser](app-dropuser.html) — remove a PostgreSQL user account

[ecpg](app-ecpg.html) — embedded SQL C preprocessor

[pg_amcheck](app-pgamcheck.html) — checks for corruption in one or more
PostgreSQL databases

[pg_basebackup](app-pgbasebackup.html) — take a base backup of a PostgreSQL
cluster

[pgbench](pgbench.html) — run a benchmark test on PostgreSQL

[pg_config](app-pgconfig.html) — retrieve information about the installed
version of PostgreSQL

[pg_dump](app-pgdump.html) — extract a PostgreSQL database into a script file
or other archive file

[pg_dumpall](app-pg-dumpall.html) — extract a PostgreSQL database cluster into
a script file

[pg_isready](app-pg-isready.html) — check the connection status of a
PostgreSQL server

[pg_receivewal](app-pgreceivewal.html) — stream write-ahead logs from a
PostgreSQL server

[pg_recvlogical](app-pgrecvlogical.html) — control PostgreSQL logical decoding
streams

[pg_restore](app-pgrestore.html) — restore a PostgreSQL database from an
archive file created by pg_dump

[pg_verifybackup](app-pgverifybackup.html) — verify the integrity of a base
backup of a PostgreSQL cluster

[psql](app-psql.html) — PostgreSQL interactive terminal

[reindexdb](app-reindexdb.html) — reindex a PostgreSQL database

[vacuumdb](app-vacuumdb.html) — garbage-collect and analyze a PostgreSQL
database

* * *

[Prev](sql-values.html "VALUES")  | [Up](reference.html "Part VI. Reference") |  [Next](app-clusterdb.html "clusterdb")  
---|---|---  
VALUES  | [Home](index.html "PostgreSQL 16.9 Documentation") |  clusterdb  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/reference-client.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

