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

Supported Versions: [Current](/docs/current/wal-internals.html "PostgreSQL 17
- 30.6. WAL Internals") ([17](/docs/17/wal-internals.html "PostgreSQL 17 -
30.6. WAL Internals")) / [16](/docs/16/wal-internals.html "PostgreSQL 16 -
30.6. WAL Internals") / [15](/docs/15/wal-internals.html "PostgreSQL 15 -
30.6. WAL Internals") / [14](/docs/14/wal-internals.html "PostgreSQL 14 -
30.6. WAL Internals") / [13](/docs/13/wal-internals.html "PostgreSQL 13 -
30.6. WAL Internals")

Development Versions: [18](/docs/18/wal-internals.html "PostgreSQL 18 -
30.6. WAL Internals") / [devel](/docs/devel/wal-internals.html "PostgreSQL
devel - 30.6. WAL Internals")

Unsupported versions: [12](/docs/12/wal-internals.html "PostgreSQL 12 -
30.6. WAL Internals") / [11](/docs/11/wal-internals.html "PostgreSQL 11 -
30.6. WAL Internals") / [10](/docs/10/wal-internals.html "PostgreSQL 10 -
30.6. WAL Internals") / [9.6](/docs/9.6/wal-internals.html "PostgreSQL 9.6 -
30.6. WAL Internals") / [9.5](/docs/9.5/wal-internals.html "PostgreSQL 9.5 -
30.6. WAL Internals") / [9.4](/docs/9.4/wal-internals.html "PostgreSQL 9.4 -
30.6. WAL Internals") / [9.3](/docs/9.3/wal-internals.html "PostgreSQL 9.3 -
30.6. WAL Internals") / [9.2](/docs/9.2/wal-internals.html "PostgreSQL 9.2 -
30.6. WAL Internals") / [9.1](/docs/9.1/wal-internals.html "PostgreSQL 9.1 -
30.6. WAL Internals") / [9.0](/docs/9.0/wal-internals.html "PostgreSQL 9.0 -
30.6. WAL Internals") / [8.4](/docs/8.4/wal-internals.html "PostgreSQL 8.4 -
30.6. WAL Internals") / [8.3](/docs/8.3/wal-internals.html "PostgreSQL 8.3 -
30.6. WAL Internals") / [8.2](/docs/8.2/wal-internals.html "PostgreSQL 8.2 -
30.6. WAL Internals") / [8.1](/docs/8.1/wal-internals.html "PostgreSQL 8.1 -
30.6. WAL Internals") / [8.0](/docs/8.0/wal-internals.html "PostgreSQL 8.0 -
30.6. WAL Internals") / [7.4](/docs/7.4/wal-internals.html "PostgreSQL 7.4 -
30.6. WAL Internals")

__

30.6. WAL Internals  
---  
[Prev](wal-configuration.html "30.5. WAL Configuration")  | [Up](wal.html "Chapter 30. Reliability and the Write-Ahead Log") | Chapter 30. Reliability and the Write-Ahead Log | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logical-replication.html "Chapter 31. Logical Replication")  
  
* * *

## 30.6. WAL Internals #

WAL is automatically enabled; no action is required from the administrator
except ensuring that the disk-space requirements for the WAL files are met,
and that any necessary tuning is done (see [Section 30.5](wal-
configuration.html "30.5. WAL Configuration")).

WAL records are appended to the WAL files as each new record is written. The
insert position is described by a Log Sequence Number (LSN) that is a byte
offset into the WAL, increasing monotonically with each new record. LSN values
are returned as the datatype [`pg_lsn`](datatype-pg-lsn.html "8.20. pg_lsn
Type"). Values can be compared to calculate the volume of WAL data that
separates them, so they are used to measure the progress of replication and
recovery.

WAL files are stored in the directory `pg_wal` under the data directory, as a
set of segment files, normally each 16 MB in size (but the size can be changed
by altering the `--wal-segsize` initdb option). Each segment is divided into
pages, normally 8 kB each (this size can be changed via the `--with-wal-
blocksize` configure option). The WAL record headers are described in
`access/xlogrecord.h`; the record content is dependent on the type of event
that is being logged. Segment files are given ever-increasing numbers as
names, starting at `000000010000000000000001`. The numbers do not wrap, but it
will take a very, very long time to exhaust the available stock of numbers.

It is advantageous if the WAL is located on a different disk from the main
database files. This can be achieved by moving the `pg_wal` directory to
another location (while the server is shut down, of course) and creating a
symbolic link from the original location in the main data directory to the new
location.

The aim of WAL is to ensure that the log is written before database records
are altered, but this can be subverted by disk drives that falsely report a
successful write to the kernel, when in fact they have only cached the data
and not yet stored it on the disk. A power failure in such a situation might
lead to irrecoverable data corruption. Administrators should try to ensure
that disks holding PostgreSQL's WAL files do not make such false reports. (See
[Section 30.1](wal-reliability.html "30.1. Reliability").)

After a checkpoint has been made and the WAL flushed, the checkpoint's
position is saved in the file `pg_control`. Therefore, at the start of
recovery, the server first reads `pg_control` and then the checkpoint record;
then it performs the REDO operation by scanning forward from the WAL location
indicated in the checkpoint record. Because the entire content of data pages
is saved in the WAL on the first page modification after a checkpoint
(assuming [full_page_writes](runtime-config-wal.html#GUC-FULL-PAGE-WRITES) is
not disabled), all pages changed since the checkpoint will be restored to a
consistent state.

To deal with the case where `pg_control` is corrupt, we should support the
possibility of scanning existing WAL segments in reverse order — newest to
oldest — in order to find the latest checkpoint. This has not been implemented
yet. `pg_control` is small enough (less than one disk page) that it is not
subject to partial-write problems, and as of this writing there have been no
reports of database failures due solely to the inability to read `pg_control`
itself. So while it is theoretically a weak spot, `pg_control` does not seem
to be a problem in practice.

* * *

[Prev](wal-configuration.html "30.5. WAL Configuration")  | [Up](wal.html "Chapter 30. Reliability and the Write-Ahead Log") |  [Next](logical-replication.html "Chapter 31. Logical Replication")  
---|---|---  
30.5. WAL Configuration  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 31. Logical Replication  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/wal-internals.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

