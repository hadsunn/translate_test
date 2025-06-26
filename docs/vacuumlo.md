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

Supported Versions: [Current](/docs/current/vacuumlo.html "PostgreSQL 17 -
vacuumlo") ([17](/docs/17/vacuumlo.html "PostgreSQL 17 - vacuumlo")) /
[16](/docs/16/vacuumlo.html "PostgreSQL 16 - vacuumlo") /
[15](/docs/15/vacuumlo.html "PostgreSQL 15 - vacuumlo") /
[14](/docs/14/vacuumlo.html "PostgreSQL 14 - vacuumlo") /
[13](/docs/13/vacuumlo.html "PostgreSQL 13 - vacuumlo")

Development Versions: [18](/docs/18/vacuumlo.html "PostgreSQL 18 - vacuumlo")
/ [devel](/docs/devel/vacuumlo.html "PostgreSQL devel - vacuumlo")

Unsupported versions: [12](/docs/12/vacuumlo.html "PostgreSQL 12 - vacuumlo")
/ [11](/docs/11/vacuumlo.html "PostgreSQL 11 - vacuumlo") /
[10](/docs/10/vacuumlo.html "PostgreSQL 10 - vacuumlo") /
[9.6](/docs/9.6/vacuumlo.html "PostgreSQL 9.6 - vacuumlo") /
[9.5](/docs/9.5/vacuumlo.html "PostgreSQL 9.5 - vacuumlo") /
[9.4](/docs/9.4/vacuumlo.html "PostgreSQL 9.4 - vacuumlo") /
[9.3](/docs/9.3/vacuumlo.html "PostgreSQL 9.3 - vacuumlo") /
[9.2](/docs/9.2/vacuumlo.html "PostgreSQL 9.2 - vacuumlo") /
[9.1](/docs/9.1/vacuumlo.html "PostgreSQL 9.1 - vacuumlo") /
[9.0](/docs/9.0/vacuumlo.html "PostgreSQL 9.0 - vacuumlo") /
[8.4](/docs/8.4/vacuumlo.html "PostgreSQL 8.4 - vacuumlo") /
[8.3](/docs/8.3/vacuumlo.html "PostgreSQL 8.3 - vacuumlo")

__

vacuumlo  
---  
[Prev](oid2name.html "oid2name")  | [Up](contrib-prog-client.html "G.1. Client Applications") | G.1. Client Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-prog-server.html "G.2. Server Applications")  
  
* * *

## vacuumlo

vacuumlo — remove orphaned large objects from a PostgreSQL database

## Synopsis

`vacuumlo` [_`option`_...] _`dbname`_...

## Description

vacuumlo is a simple utility program that will remove any “orphaned” large
objects from a PostgreSQL database. An orphaned large object (LO) is
considered to be any LO whose OID does not appear in any `oid` or `lo` data
column of the database.

If you use this, you may also be interested in the `lo_manage` trigger in the
[lo](lo.html "F.22. lo — manage large objects") module. `lo_manage` is useful
to try to avoid creating orphaned LOs in the first place.

All databases named on the command line are processed.

## Options

vacuumlo accepts the following command-line arguments:

`-l _`limit`_`  
`--limit=_`limit`_`

    

Remove no more than _`limit`_ large objects per transaction (default 1000).
Since the server acquires a lock per LO removed, removing too many LOs in one
transaction risks exceeding [max_locks_per_transaction](runtime-config-
locks.html#GUC-MAX-LOCKS-PER-TRANSACTION). Set the limit to zero if you want
all removals done in a single transaction.

`-n`  
`--dry-run`

    

Don't remove anything, just show what would be done.

`-v`  
`--verbose`

    

Write a lot of progress messages.

`-V`  
`--version`

    

Print the vacuumlo version and exit.

`-?`  
`--help`

    

Show help about vacuumlo command line arguments, and exit.

vacuumlo also accepts the following command-line arguments for connection
parameters:

`-h _`host`_`  
`--host=_`host`_`

    

Database server's host.

`-p _`port`_`  
`--port=_`port`_`

    

Database server's port.

`-U _`username`_`  
`--username=_`username`_`

    

User name to connect as.

`-w`  
`--no-password`

    

Never issue a password prompt. If the server requires password authentication
and a password is not available by other means such as a `.pgpass` file, the
connection attempt will fail. This option can be useful in batch jobs and
scripts where no user is present to enter a password.

`-W`  
`--password`

    

Force vacuumlo to prompt for a password before connecting to a database.

This option is never essential, since vacuumlo will automatically prompt for a
password if the server demands password authentication. However, vacuumlo will
waste a connection attempt finding out that the server wants a password. In
some cases it is worth typing `-W` to avoid the extra connection attempt.

## Environment

`PGHOST`  
`PGPORT`  
`PGUSER`

    

Default connection parameters.

This utility, like most other PostgreSQL utilities, also uses the environment
variables supported by libpq (see [Section 34.15](libpq-envars.html
"34.15. Environment Variables")).

The environment variable `PG_COLOR` specifies whether to use color in
diagnostic messages. Possible values are `always`, `auto` and `never`.

## Notes

vacuumlo works by the following method: First, vacuumlo builds a temporary
table which contains all of the OIDs of the large objects in the selected
database. It then scans through all columns in the database that are of type
`oid` or `lo`, and removes matching entries from the temporary table. (Note:
Only types with these names are considered; in particular, domains over them
are not considered.) The remaining entries in the temporary table identify
orphaned LOs. These are removed.

## Author

Peter Mount `<[peter@retep.org.uk](mailto:peter@retep.org.uk)>`

* * *

[Prev](oid2name.html "oid2name")  | [Up](contrib-prog-client.html "G.1. Client Applications") |  [Next](contrib-prog-server.html "G.2. Server Applications")  
---|---|---  
oid2name  | [Home](index.html "PostgreSQL 16.9 Documentation") |  G.2. Server Applications  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/vacuumlo.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

