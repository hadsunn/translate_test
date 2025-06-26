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

Supported Versions: [Current](/docs/current/app-pgchecksums.html "PostgreSQL
17 - pg_checksums") ([17](/docs/17/app-pgchecksums.html "PostgreSQL 17 -
pg_checksums")) / [16](/docs/16/app-pgchecksums.html "PostgreSQL 16 -
pg_checksums") / [15](/docs/15/app-pgchecksums.html "PostgreSQL 15 -
pg_checksums") / [14](/docs/14/app-pgchecksums.html "PostgreSQL 14 -
pg_checksums") / [13](/docs/13/app-pgchecksums.html "PostgreSQL 13 -
pg_checksums")

Development Versions: [18](/docs/18/app-pgchecksums.html "PostgreSQL 18 -
pg_checksums") / [devel](/docs/devel/app-pgchecksums.html "PostgreSQL devel -
pg_checksums")

Unsupported versions: [12](/docs/12/app-pgchecksums.html "PostgreSQL 12 -
pg_checksums")

__

pg_checksums  
---  
[Prev](pgarchivecleanup.html "pg_archivecleanup")  | [Up](reference-server.html "PostgreSQL Server Applications") | PostgreSQL Server Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](app-pgcontroldata.html "pg_controldata")  
  
* * *

## pg_checksums

pg_checksums — enable, disable or check data checksums in a PostgreSQL
database cluster

## Synopsis

`pg_checksums` [_`option`_...] [[ `-D` | `--pgdata` ]_`datadir`_]

## Description

pg_checksums checks, enables or disables data checksums in a PostgreSQL
cluster. The server must be shut down cleanly before running pg_checksums.
When verifying checksums, the exit status is zero if there are no checksum
errors, and nonzero if at least one checksum failure is detected. When
enabling or disabling checksums, the exit status is nonzero if the operation
failed.

When verifying checksums, every file in the cluster is scanned. When enabling
checksums, each relation file block with a changed checksum is rewritten in-
place. Disabling checksums only updates the file `pg_control`.

## Options

The following command-line options are available:

`-D _`directory`_`  
`--pgdata=_`directory`_`

    

Specifies the directory where the database cluster is stored.

`-c`  
`--check`

    

Checks checksums. This is the default mode if nothing else is specified.

`-d`  
`--disable`

    

Disables checksums.

`-e`  
`--enable`

    

Enables checksums.

`-f _`filenode`_`  
`--filenode=_`filenode`_`

    

Only validate checksums in the relation with filenode _`filenode`_.

`-N`  
`--no-sync`

    

By default, `pg_checksums` will wait for all files to be written safely to
disk. This option causes `pg_checksums` to return without waiting, which is
faster, but means that a subsequent operating system crash can leave the
updated data directory corrupt. Generally, this option is useful for testing
but should not be used on a production installation. This option has no effect
when using `--check`.

`-P`  
`--progress`

    

Enable progress reporting. Turning this on will deliver a progress report
while checking or enabling checksums.

`-v`  
`--verbose`

    

Enable verbose output. Lists all checked files.

`-V`  
`--version`

    

Print the pg_checksums version and exit.

`-?`  
`--help`

    

Show help about pg_checksums command line arguments, and exit.

## Environment

`PGDATA`

    

Specifies the directory where the database cluster is stored; can be
overridden using the `-D` option.

`PG_COLOR`

    

Specifies whether to use color in diagnostic messages. Possible values are
`always`, `auto` and `never`.

## Notes

Enabling checksums in a large cluster can potentially take a long time. During
this operation, the cluster or other programs that write to the data directory
must not be started or else data loss may occur.

When using a replication setup with tools which perform direct copies of
relation file blocks (for example [pg_rewind](app-pgrewind.html "pg_rewind")),
enabling or disabling checksums can lead to page corruptions in the shape of
incorrect checksums if the operation is not done consistently across all
nodes. When enabling or disabling checksums in a replication setup, it is thus
recommended to stop all the clusters before switching them all consistently.
Destroying all standbys, performing the operation on the primary and finally
recreating the standbys from scratch is also safe.

If pg_checksums is aborted or killed while enabling or disabling checksums,
the cluster's data checksum configuration remains unchanged, and pg_checksums
can be re-run to perform the same operation.

* * *

[Prev](pgarchivecleanup.html "pg_archivecleanup")  | [Up](reference-server.html "PostgreSQL Server Applications") |  [Next](app-pgcontroldata.html "pg_controldata")  
---|---|---  
pg_archivecleanup  | [Home](index.html "PostgreSQL 16.9 Documentation") |  pg_controldata  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/app-pgchecksums.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

