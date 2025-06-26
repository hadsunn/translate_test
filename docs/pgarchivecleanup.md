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

Supported Versions: [Current](/docs/current/pgarchivecleanup.html "PostgreSQL
17 - pg_archivecleanup") ([17](/docs/17/pgarchivecleanup.html "PostgreSQL 17 -
pg_archivecleanup")) / [16](/docs/16/pgarchivecleanup.html "PostgreSQL 16 -
pg_archivecleanup") / [15](/docs/15/pgarchivecleanup.html "PostgreSQL 15 -
pg_archivecleanup") / [14](/docs/14/pgarchivecleanup.html "PostgreSQL 14 -
pg_archivecleanup") / [13](/docs/13/pgarchivecleanup.html "PostgreSQL 13 -
pg_archivecleanup")

Development Versions: [18](/docs/18/pgarchivecleanup.html "PostgreSQL 18 -
pg_archivecleanup") / [devel](/docs/devel/pgarchivecleanup.html "PostgreSQL
devel - pg_archivecleanup")

Unsupported versions: [12](/docs/12/pgarchivecleanup.html "PostgreSQL 12 -
pg_archivecleanup") / [11](/docs/11/pgarchivecleanup.html "PostgreSQL 11 -
pg_archivecleanup") / [10](/docs/10/pgarchivecleanup.html "PostgreSQL 10 -
pg_archivecleanup") / [9.6](/docs/9.6/pgarchivecleanup.html "PostgreSQL 9.6 -
pg_archivecleanup") / [9.5](/docs/9.5/pgarchivecleanup.html "PostgreSQL 9.5 -
pg_archivecleanup") / [9.4](/docs/9.4/pgarchivecleanup.html "PostgreSQL 9.4 -
pg_archivecleanup") / [9.3](/docs/9.3/pgarchivecleanup.html "PostgreSQL 9.3 -
pg_archivecleanup") / [9.2](/docs/9.2/pgarchivecleanup.html "PostgreSQL 9.2 -
pg_archivecleanup") / [9.1](/docs/9.1/pgarchivecleanup.html "PostgreSQL 9.1 -
pg_archivecleanup") / [9.0](/docs/9.0/pgarchivecleanup.html "PostgreSQL 9.0 -
pg_archivecleanup")

__

pg_archivecleanup  
---  
[Prev](app-initdb.html "initdb")  | [Up](reference-server.html "PostgreSQL Server Applications") | PostgreSQL Server Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](app-pgchecksums.html "pg_checksums")  
  
* * *

## pg_archivecleanup

pg_archivecleanup — clean up PostgreSQL WAL archive files

## Synopsis

`pg_archivecleanup` [_`option`_...] _`archivelocation`_ _`oldestkeptwalfile`_

## Description

pg_archivecleanup is designed to be used as an `archive_cleanup_command` to
clean up WAL file archives when running as a standby server (see [Section
27.2](warm-standby.html "27.2. Log-Shipping Standby Servers")).
pg_archivecleanup can also be used as a standalone program to clean WAL file
archives.

To configure a standby server to use pg_archivecleanup, put this into its
`postgresql.conf` configuration file:

    
    
    archive_cleanup_command = 'pg_archivecleanup _archivelocation_ %r'
    

where _`archivelocation`_ is the directory from which WAL segment files should
be removed.

When used within [archive_cleanup_command](runtime-config-wal.html#GUC-
ARCHIVE-CLEANUP-COMMAND), all WAL files logically preceding the value of the
`%r` argument will be removed from _`archivelocation`_. This minimizes the
number of files that need to be retained, while preserving crash-restart
capability. Use of this parameter is appropriate if the _`archivelocation`_ is
a transient staging area for this particular standby server, but _not_ when
the _`archivelocation`_ is intended as a long-term WAL archive area, or when
multiple standby servers are recovering from the same archive location.

When used as a standalone program all WAL files logically preceding the
_`oldestkeptwalfile`_ will be removed from _`archivelocation`_. In this mode,
if you specify a `.partial` or `.backup` file name, then only the file prefix
will be used as the _`oldestkeptwalfile`_. This treatment of `.backup` file
name allows you to remove all WAL files archived prior to a specific base
backup without error. For example, the following example will remove all files
older than WAL file name `000000010000003700000010`:

    
    
    pg_archivecleanup -d archive 000000010000003700000010.00000020.backup
    
    pg_archivecleanup:  keep WAL file "archive/000000010000003700000010" and later
    pg_archivecleanup:  removing file "archive/00000001000000370000000F"
    pg_archivecleanup:  removing file "archive/00000001000000370000000E"
    

pg_archivecleanup assumes that _`archivelocation`_ is a directory readable and
writable by the server-owning user.

## Options

pg_archivecleanup accepts the following command-line arguments:

`-d`

    

Print lots of debug logging output on `stderr`.

`-n`

    

Print the names of the files that would have been removed on `stdout`
(performs a dry run).

`-V`  
`--version`

    

Print the pg_archivecleanup version and exit.

`-x` _`extension`_

    

Provide an extension that will be stripped from all file names before deciding
if they should be deleted. This is typically useful for cleaning up archives
that have been compressed during storage, and therefore have had an extension
added by the compression program. For example: `-x .gz`.

`-?`  
`--help`

    

Show help about pg_archivecleanup command line arguments, and exit.

## Environment

The environment variable `PG_COLOR` specifies whether to use color in
diagnostic messages. Possible values are `always`, `auto` and `never`.

## Notes

pg_archivecleanup is designed to work with PostgreSQL 8.0 and later when used
as a standalone utility, or with PostgreSQL 9.0 and later when used as an
archive cleanup command.

pg_archivecleanup is written in C and has an easy-to-modify source code, with
specifically designated sections to modify for your own needs

## Examples

On Linux or Unix systems, you might use:

    
    
    archive_cleanup_command = 'pg_archivecleanup -d /mnt/standby/archive %r 2>>cleanup.log'
    

where the archive directory is physically located on the standby server, so
that the `archive_command` is accessing it across NFS, but the files are local
to the standby. This will:

  * produce debugging output in `cleanup.log`

  * remove no-longer-needed files from the archive directory

* * *

[Prev](app-initdb.html "initdb")  | [Up](reference-server.html "PostgreSQL Server Applications") |  [Next](app-pgchecksums.html "pg_checksums")  
---|---|---  
initdb  | [Home](index.html "PostgreSQL 16.9 Documentation") |  pg_checksums  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pgarchivecleanup.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

