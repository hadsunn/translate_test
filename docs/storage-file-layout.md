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

Supported Versions: [Current](/docs/current/storage-file-layout.html
"PostgreSQL 17 - 73.1. Database File Layout") ([17](/docs/17/storage-file-
layout.html "PostgreSQL 17 - 73.1. Database File Layout")) /
[16](/docs/16/storage-file-layout.html "PostgreSQL 16 - 73.1. Database File
Layout") / [15](/docs/15/storage-file-layout.html "PostgreSQL 15 -
73.1. Database File Layout") / [14](/docs/14/storage-file-layout.html
"PostgreSQL 14 - 73.1. Database File Layout") / [13](/docs/13/storage-file-
layout.html "PostgreSQL 13 - 73.1. Database File Layout")

Development Versions: [18](/docs/18/storage-file-layout.html "PostgreSQL 18 -
73.1. Database File Layout") / [devel](/docs/devel/storage-file-layout.html
"PostgreSQL devel - 73.1. Database File Layout")

Unsupported versions: [12](/docs/12/storage-file-layout.html "PostgreSQL 12 -
73.1. Database File Layout") / [11](/docs/11/storage-file-layout.html
"PostgreSQL 11 - 73.1. Database File Layout") / [10](/docs/10/storage-file-
layout.html "PostgreSQL 10 - 73.1. Database File Layout") /
[9.6](/docs/9.6/storage-file-layout.html "PostgreSQL 9.6 - 73.1. Database File
Layout") / [9.5](/docs/9.5/storage-file-layout.html "PostgreSQL 9.5 -
73.1. Database File Layout") / [9.4](/docs/9.4/storage-file-layout.html
"PostgreSQL 9.4 - 73.1. Database File Layout") / [9.3](/docs/9.3/storage-file-
layout.html "PostgreSQL 9.3 - 73.1. Database File Layout") /
[9.2](/docs/9.2/storage-file-layout.html "PostgreSQL 9.2 - 73.1. Database File
Layout") / [9.1](/docs/9.1/storage-file-layout.html "PostgreSQL 9.1 -
73.1. Database File Layout") / [9.0](/docs/9.0/storage-file-layout.html
"PostgreSQL 9.0 - 73.1. Database File Layout") / [8.4](/docs/8.4/storage-file-
layout.html "PostgreSQL 8.4 - 73.1. Database File Layout") /
[8.3](/docs/8.3/storage-file-layout.html "PostgreSQL 8.3 - 73.1. Database File
Layout") / [8.2](/docs/8.2/storage-file-layout.html "PostgreSQL 8.2 -
73.1. Database File Layout")

__

73.1. Database File Layout  
---  
[Prev](storage.html "Chapter 73. Database Physical Storage")  | [Up](storage.html "Chapter 73. Database Physical Storage") | Chapter 73. Database Physical Storage | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](storage-toast.html "73.2. TOAST")  
  
* * *

## 73.1. Database File Layout #

This section describes the storage format at the level of files and
directories.

Traditionally, the configuration and data files used by a database cluster are
stored together within the cluster's data directory, commonly referred to as
`PGDATA` (after the name of the environment variable that can be used to
define it). A common location for `PGDATA` is `/var/lib/pgsql/data`. Multiple
clusters, managed by different server instances, can exist on the same
machine.

The `PGDATA` directory contains several subdirectories and control files, as
shown in [Table 73.1](storage-file-layout.html#PGDATA-CONTENTS-TABLE
"Table 73.1. Contents of PGDATA"). In addition to these required items, the
cluster configuration files `postgresql.conf`, `pg_hba.conf`, and
`pg_ident.conf` are traditionally stored in `PGDATA`, although it is possible
to place them elsewhere.

**Table  73.1. Contents of `PGDATA`**

Item | Description  
---|---  
`PG_VERSION` | A file containing the major version number of PostgreSQL  
`base` | Subdirectory containing per-database subdirectories  
`current_logfiles` | File recording the log file(s) currently written to by the logging collector  
`global` | Subdirectory containing cluster-wide tables, such as `pg_database`  
`pg_commit_ts` | Subdirectory containing transaction commit timestamp data  
`pg_dynshmem` | Subdirectory containing files used by the dynamic shared memory subsystem  
`pg_logical` | Subdirectory containing status data for logical decoding  
`pg_multixact` | Subdirectory containing multitransaction status data (used for shared row locks)  
`pg_notify` | Subdirectory containing LISTEN/NOTIFY status data  
`pg_replslot` | Subdirectory containing replication slot data  
`pg_serial` | Subdirectory containing information about committed serializable transactions  
`pg_snapshots` | Subdirectory containing exported snapshots  
`pg_stat` | Subdirectory containing permanent files for the statistics subsystem  
`pg_stat_tmp` | Subdirectory containing temporary files for the statistics subsystem  
`pg_subtrans` | Subdirectory containing subtransaction status data  
`pg_tblspc` | Subdirectory containing symbolic links to tablespaces  
`pg_twophase` | Subdirectory containing state files for prepared transactions  
`pg_wal` | Subdirectory containing WAL (Write Ahead Log) files  
`pg_xact` | Subdirectory containing transaction commit status data  
`postgresql.auto.conf` | A file used for storing configuration parameters that are set by `ALTER SYSTEM`  
`postmaster.opts` | A file recording the command-line options the server was last started with  
`postmaster.pid` | A lock file recording the current postmaster process ID (PID), cluster data directory path, postmaster start timestamp, port number, Unix-domain socket directory path (could be empty), first valid listen_address (IP address or `*`, or empty if not listening on TCP), and shared memory segment ID (this file is not present after server shutdown)  
  
  

For each database in the cluster there is a subdirectory within
`PGDATA``/base`, named after the database's OID in `pg_database`. This
subdirectory is the default location for the database's files; in particular,
its system catalogs are stored there.

Note that the following sections describe the behavior of the builtin `heap`
[table access method](tableam.html "Chapter 63. Table Access Method Interface
Definition"), and the builtin [index access methods](indexam.html
"Chapter 64. Index Access Method Interface Definition"). Due to the extensible
nature of PostgreSQL, other access methods might work differently.

Each table and index is stored in a separate file. For ordinary relations,
these files are named after the table or index's _filenode_ number, which can
be found in `pg_class`.`relfilenode`. But for temporary relations, the file
name is of the form `t _`BBB`_ __`FFF`_`, where _`BBB`_ is the backend ID of
the backend which created the file, and _`FFF`_ is the filenode number. In
either case, in addition to the main file (a/k/a main fork), each table and
index has a _free space map_ (see [Section 73.3](storage-fsm.html "73.3. Free
Space Map")), which stores information about free space available in the
relation. The free space map is stored in a file named with the filenode
number plus the suffix `_fsm`. Tables also have a _visibility map_ , stored in
a fork with the suffix `_vm`, to track which pages are known to have no dead
tuples. The visibility map is described further in [Section 73.4](storage-
vm.html "73.4. Visibility Map"). Unlogged tables and indexes have a third
fork, known as the initialization fork, which is stored in a fork with the
suffix `_init` (see [Section 73.5](storage-init.html "73.5. The Initialization
Fork")).

### Caution

Note that while a table's filenode often matches its OID, this is _not_
necessarily the case; some operations, like `TRUNCATE`, `REINDEX`, `CLUSTER`
and some forms of `ALTER TABLE`, can change the filenode while preserving the
OID. Avoid assuming that filenode and table OID are the same. Also, for
certain system catalogs including `pg_class` itself, `pg_class`.`relfilenode`
contains zero. The actual filenode number of these catalogs is stored in a
lower-level data structure, and can be obtained using the
`pg_relation_filenode()` function.

When a table or index exceeds 1 GB, it is divided into gigabyte-sized
_segments_. The first segment's file name is the same as the filenode;
subsequent segments are named filenode.1, filenode.2, etc. This arrangement
avoids problems on platforms that have file size limitations. (Actually, 1 GB
is just the default segment size. The segment size can be adjusted using the
configuration option `--with-segsize` when building PostgreSQL.) In principle,
free space map and visibility map forks could require multiple segments as
well, though this is unlikely to happen in practice.

A table that has columns with potentially large entries will have an
associated _TOAST_ table, which is used for out-of-line storage of field
values that are too large to keep in the table rows proper.
`pg_class`.`reltoastrelid` links from a table to its TOAST table, if any. See
[Section 73.2](storage-toast.html "73.2. TOAST") for more information.

The contents of tables and indexes are discussed further in [Section
73.6](storage-page-layout.html "73.6. Database Page Layout").

Tablespaces make the scenario more complicated. Each user-defined tablespace
has a symbolic link inside the `PGDATA``/pg_tblspc` directory, which points to
the physical tablespace directory (i.e., the location specified in the
tablespace's `CREATE TABLESPACE` command). This symbolic link is named after
the tablespace's OID. Inside the physical tablespace directory there is a
subdirectory with a name that depends on the PostgreSQL server version, such
as `PG_9.0_201008051`. (The reason for using this subdirectory is so that
successive versions of the database can use the same `CREATE TABLESPACE`
location value without conflicts.) Within the version-specific subdirectory,
there is a subdirectory for each database that has elements in the tablespace,
named after the database's OID. Tables and indexes are stored within that
directory, using the filenode naming scheme. The `pg_default` tablespace is
not accessed through `pg_tblspc`, but corresponds to `PGDATA``/base`.
Similarly, the `pg_global` tablespace is not accessed through `pg_tblspc`, but
corresponds to `PGDATA``/global`.

The `pg_relation_filepath()` function shows the entire path (relative to
`PGDATA`) of any relation. It is often useful as a substitute for remembering
many of the above rules. But keep in mind that this function just gives the
name of the first segment of the main fork of the relation — you may need to
append a segment number and/or `_fsm`, `_vm`, or `_init` to find all the files
associated with the relation.

Temporary files (for operations such as sorting more data than can fit in
memory) are created within `PGDATA``/base/pgsql_tmp`, or within a `pgsql_tmp`
subdirectory of a tablespace directory if a tablespace other than `pg_default`
is specified for them. The name of a temporary file has the form `pgsql_tmp
_`PPP`_._`NNN`_`, where _`PPP`_ is the PID of the owning backend and _`NNN`_
distinguishes different temporary files of that backend.

* * *

[Prev](storage.html "Chapter 73. Database Physical Storage")  | [Up](storage.html "Chapter 73. Database Physical Storage") |  [Next](storage-toast.html "73.2. TOAST")  
---|---|---  
Chapter 73. Database Physical Storage  | [Home](index.html "PostgreSQL 16.9 Documentation") |  73.2. TOAST  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/storage-file-layout.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

