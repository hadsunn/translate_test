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

Supported Versions: [Current](/docs/current/pgtestfsync.html "PostgreSQL 17 -
pg_test_fsync") ([17](/docs/17/pgtestfsync.html "PostgreSQL 17 -
pg_test_fsync")) / [16](/docs/16/pgtestfsync.html "PostgreSQL 16 -
pg_test_fsync") / [15](/docs/15/pgtestfsync.html "PostgreSQL 15 -
pg_test_fsync") / [14](/docs/14/pgtestfsync.html "PostgreSQL 14 -
pg_test_fsync") / [13](/docs/13/pgtestfsync.html "PostgreSQL 13 -
pg_test_fsync")

Development Versions: [18](/docs/18/pgtestfsync.html "PostgreSQL 18 -
pg_test_fsync") / [devel](/docs/devel/pgtestfsync.html "PostgreSQL devel -
pg_test_fsync")

Unsupported versions: [12](/docs/12/pgtestfsync.html "PostgreSQL 12 -
pg_test_fsync") / [11](/docs/11/pgtestfsync.html "PostgreSQL 11 -
pg_test_fsync") / [10](/docs/10/pgtestfsync.html "PostgreSQL 10 -
pg_test_fsync") / [9.6](/docs/9.6/pgtestfsync.html "PostgreSQL 9.6 -
pg_test_fsync") / [9.5](/docs/9.5/pgtestfsync.html "PostgreSQL 9.5 -
pg_test_fsync") / [9.4](/docs/9.4/pgtestfsync.html "PostgreSQL 9.4 -
pg_test_fsync") / [9.3](/docs/9.3/pgtestfsync.html "PostgreSQL 9.3 -
pg_test_fsync") / [9.2](/docs/9.2/pgtestfsync.html "PostgreSQL 9.2 -
pg_test_fsync") / [9.1](/docs/9.1/pgtestfsync.html "PostgreSQL 9.1 -
pg_test_fsync")

__

pg_test_fsync  
---  
[Prev](app-pgrewind.html "pg_rewind")  | [Up](reference-server.html "PostgreSQL Server Applications") | PostgreSQL Server Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pgtesttiming.html "pg_test_timing")  
  
* * *

## pg_test_fsync

pg_test_fsync — determine fastest `wal_sync_method` for PostgreSQL

## Synopsis

`pg_test_fsync` [_`option`_...]

## Description

pg_test_fsync is intended to give you a reasonable idea of what the fastest
[wal_sync_method](runtime-config-wal.html#GUC-WAL-SYNC-METHOD) is on your
specific system, as well as supplying diagnostic information in the event of
an identified I/O problem. However, differences shown by pg_test_fsync might
not make any significant difference in real database throughput, especially
since many database servers are not speed-limited by their write-ahead logs.
pg_test_fsync reports average file sync operation time in microseconds for
each `wal_sync_method`, which can also be used to inform efforts to optimize
the value of [commit_delay](runtime-config-wal.html#GUC-COMMIT-DELAY).

## Options

pg_test_fsync accepts the following command-line options:

`-f`  
`--filename`

    

Specifies the file name to write test data in. This file should be in the same
file system that the `pg_wal` directory is or will be placed in. (`pg_wal`
contains the WAL files.) The default is `pg_test_fsync.out` in the current
directory.

`-s`  
`--secs-per-test`

    

Specifies the number of seconds for each test. The more time per test, the
greater the test's accuracy, but the longer it takes to run. The default is 5
seconds, which allows the program to complete in under 2 minutes.

`-V`  
`--version`

    

Print the pg_test_fsync version and exit.

`-?`  
`--help`

    

Show help about pg_test_fsync command line arguments, and exit.

## Environment

The environment variable `PG_COLOR` specifies whether to use color in
diagnostic messages. Possible values are `always`, `auto` and `never`.

## See Also

[postgres](app-postgres.html "postgres")

* * *

[Prev](app-pgrewind.html "pg_rewind")  | [Up](reference-server.html "PostgreSQL Server Applications") |  [Next](pgtesttiming.html "pg_test_timing")  
---|---|---  
pg_rewind  | [Home](index.html "PostgreSQL 16.9 Documentation") |  pg_test_timing  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pgtestfsync.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

