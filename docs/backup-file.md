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

Supported Versions: [Current](/docs/current/backup-file.html "PostgreSQL 17 -
26.2. File System Level Backup") ([17](/docs/17/backup-file.html "PostgreSQL
17 - 26.2. File System Level Backup")) / [16](/docs/16/backup-file.html
"PostgreSQL 16 - 26.2. File System Level Backup") / [15](/docs/15/backup-
file.html "PostgreSQL 15 - 26.2. File System Level Backup") /
[14](/docs/14/backup-file.html "PostgreSQL 14 - 26.2. File System Level
Backup") / [13](/docs/13/backup-file.html "PostgreSQL 13 - 26.2. File System
Level Backup")

Development Versions: [18](/docs/18/backup-file.html "PostgreSQL 18 -
26.2. File System Level Backup") / [devel](/docs/devel/backup-file.html
"PostgreSQL devel - 26.2. File System Level Backup")

Unsupported versions: [12](/docs/12/backup-file.html "PostgreSQL 12 -
26.2. File System Level Backup") / [11](/docs/11/backup-file.html "PostgreSQL
11 - 26.2. File System Level Backup") / [10](/docs/10/backup-file.html
"PostgreSQL 10 - 26.2. File System Level Backup") / [9.6](/docs/9.6/backup-
file.html "PostgreSQL 9.6 - 26.2. File System Level Backup") /
[9.5](/docs/9.5/backup-file.html "PostgreSQL 9.5 - 26.2. File System Level
Backup") / [9.4](/docs/9.4/backup-file.html "PostgreSQL 9.4 - 26.2. File
System Level Backup") / [9.3](/docs/9.3/backup-file.html "PostgreSQL 9.3 -
26.2. File System Level Backup") / [9.2](/docs/9.2/backup-file.html
"PostgreSQL 9.2 - 26.2. File System Level Backup") / [9.1](/docs/9.1/backup-
file.html "PostgreSQL 9.1 - 26.2. File System Level Backup") /
[9.0](/docs/9.0/backup-file.html "PostgreSQL 9.0 - 26.2. File System Level
Backup") / [8.4](/docs/8.4/backup-file.html "PostgreSQL 8.4 - 26.2. File
System Level Backup") / [8.3](/docs/8.3/backup-file.html "PostgreSQL 8.3 -
26.2. File System Level Backup") / [8.2](/docs/8.2/backup-file.html
"PostgreSQL 8.2 - 26.2. File System Level Backup") / [8.1](/docs/8.1/backup-
file.html "PostgreSQL 8.1 - 26.2. File System Level Backup") /
[8.0](/docs/8.0/backup-file.html "PostgreSQL 8.0 - 26.2. File System Level
Backup") / [7.4](/docs/7.4/backup-file.html "PostgreSQL 7.4 - 26.2. File
System Level Backup") / [7.3](/docs/7.3/backup-file.html "PostgreSQL 7.3 -
26.2. File System Level Backup") / [7.2](/docs/7.2/backup-file.html
"PostgreSQL 7.2 - 26.2. File System Level Backup") / [7.1](/docs/7.1/backup-
file.html "PostgreSQL 7.1 - 26.2. File System Level Backup")

__

26.2. File System Level Backup  
---  
[Prev](backup-dump.html "26.1. SQL Dump")  | [Up](backup.html "Chapter 26. Backup and Restore") | Chapter 26. Backup and Restore | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](continuous-archiving.html "26.3. Continuous Archiving and Point-in-Time Recovery \(PITR\)")  
  
* * *

## 26.2. File System Level Backup #

An alternative backup strategy is to directly copy the files that PostgreSQL
uses to store the data in the database; [Section 19.2](creating-cluster.html
"19.2. Creating a Database Cluster") explains where these files are located.
You can use whatever method you prefer for doing file system backups; for
example:

    
    
    tar -cf backup.tar /usr/local/pgsql/data
    

There are two restrictions, however, which make this method impractical, or at
least inferior to the pg_dump method:

  1. The database server _must_ be shut down in order to get a usable backup. Half-way measures such as disallowing all connections will _not_ work (in part because `tar` and similar tools do not take an atomic snapshot of the state of the file system, but also because of internal buffering within the server). Information about stopping the server can be found in [Section 19.5](server-shutdown.html "19.5. Shutting Down the Server"). Needless to say, you also need to shut down the server before restoring the data.

  2. If you have dug into the details of the file system layout of the database, you might be tempted to try to back up or restore only certain individual tables or databases from their respective files or directories. This will _not_ work because the information contained in these files is not usable without the commit log files, `pg_xact/*`, which contain the commit status of all transactions. A table file is only usable with this information. Of course it is also impossible to restore only a table and the associated `pg_xact` data because that would render all other tables in the database cluster useless. So file system backups only work for complete backup and restoration of an entire database cluster.

An alternative file-system backup approach is to make a “consistent snapshot”
of the data directory, if the file system supports that functionality (and you
are willing to trust that it is implemented correctly). The typical procedure
is to make a “frozen snapshot” of the volume containing the database, then
copy the whole data directory (not just parts, see above) from the snapshot to
a backup device, then release the frozen snapshot. This will work even while
the database server is running. However, a backup created in this way saves
the database files in a state as if the database server was not properly shut
down; therefore, when you start the database server on the backed-up data, it
will think the previous server instance crashed and will replay the WAL log.
This is not a problem; just be aware of it (and be sure to include the WAL
files in your backup). You can perform a `CHECKPOINT` before taking the
snapshot to reduce recovery time.

If your database is spread across multiple file systems, there might not be
any way to obtain exactly-simultaneous frozen snapshots of all the volumes.
For example, if your data files and WAL log are on different disks, or if
tablespaces are on different file systems, it might not be possible to use
snapshot backup because the snapshots _must_ be simultaneous. Read your file
system documentation very carefully before trusting the consistent-snapshot
technique in such situations.

If simultaneous snapshots are not possible, one option is to shut down the
database server long enough to establish all the frozen snapshots. Another
option is to perform a continuous archiving base backup ([Section
26.3.2](continuous-archiving.html#BACKUP-BASE-BACKUP "26.3.2. Making a Base
Backup")) because such backups are immune to file system changes during the
backup. This requires enabling continuous archiving just during the backup
process; restore is done using continuous archive recovery ([Section
26.3.4](continuous-archiving.html#BACKUP-PITR-RECOVERY "26.3.4. Recovering
Using a Continuous Archive Backup")).

Another option is to use rsync to perform a file system backup. This is done
by first running rsync while the database server is running, then shutting
down the database server long enough to do an `rsync --checksum`.
(`--checksum` is necessary because `rsync` only has file modification-time
granularity of one second.) The second rsync will be quicker than the first,
because it has relatively little data to transfer, and the end result will be
consistent because the server was down. This method allows a file system
backup to be performed with minimal downtime.

Note that a file system backup will typically be larger than an SQL dump.
(pg_dump does not need to dump the contents of indexes for example, just the
commands to recreate them.) However, taking a file system backup might be
faster.

* * *

[Prev](backup-dump.html "26.1. SQL Dump")  | [Up](backup.html "Chapter 26. Backup and Restore") |  [Next](continuous-archiving.html "26.3. Continuous Archiving and Point-in-Time Recovery \(PITR\)")  
---|---|---  
26.1. SQL Dump  | [Home](index.html "PostgreSQL 16.9 Documentation") |  26.3. Continuous Archiving and Point-in-Time Recovery (PITR)  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/backup-file.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

