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

Supported Versions: [Current](/docs/current/backup.html "PostgreSQL 17 -
Chapter 26. Backup and Restore") ([17](/docs/17/backup.html "PostgreSQL 17 -
Chapter 26. Backup and Restore")) / [16](/docs/16/backup.html "PostgreSQL 16 -
Chapter 26. Backup and Restore") / [15](/docs/15/backup.html "PostgreSQL 15 -
Chapter 26. Backup and Restore") / [14](/docs/14/backup.html "PostgreSQL 14 -
Chapter 26. Backup and Restore") / [13](/docs/13/backup.html "PostgreSQL 13 -
Chapter 26. Backup and Restore")

Development Versions: [18](/docs/18/backup.html "PostgreSQL 18 -
Chapter 26. Backup and Restore") / [devel](/docs/devel/backup.html "PostgreSQL
devel - Chapter 26. Backup and Restore")

Unsupported versions: [12](/docs/12/backup.html "PostgreSQL 12 -
Chapter 26. Backup and Restore") / [11](/docs/11/backup.html "PostgreSQL 11 -
Chapter 26. Backup and Restore") / [10](/docs/10/backup.html "PostgreSQL 10 -
Chapter 26. Backup and Restore") / [9.6](/docs/9.6/backup.html "PostgreSQL 9.6
- Chapter 26. Backup and Restore") / [9.5](/docs/9.5/backup.html "PostgreSQL
9.5 - Chapter 26. Backup and Restore") / [9.4](/docs/9.4/backup.html
"PostgreSQL 9.4 - Chapter 26. Backup and Restore") /
[9.3](/docs/9.3/backup.html "PostgreSQL 9.3 - Chapter 26. Backup and Restore")
/ [9.2](/docs/9.2/backup.html "PostgreSQL 9.2 - Chapter 26. Backup and
Restore") / [9.1](/docs/9.1/backup.html "PostgreSQL 9.1 - Chapter 26. Backup
and Restore") / [9.0](/docs/9.0/backup.html "PostgreSQL 9.0 -
Chapter 26. Backup and Restore") / [8.4](/docs/8.4/backup.html "PostgreSQL 8.4
- Chapter 26. Backup and Restore") / [8.3](/docs/8.3/backup.html "PostgreSQL
8.3 - Chapter 26. Backup and Restore") / [8.2](/docs/8.2/backup.html
"PostgreSQL 8.2 - Chapter 26. Backup and Restore") /
[8.1](/docs/8.1/backup.html "PostgreSQL 8.1 - Chapter 26. Backup and Restore")
/ [8.0](/docs/8.0/backup.html "PostgreSQL 8.0 - Chapter 26. Backup and
Restore") / [7.4](/docs/7.4/backup.html "PostgreSQL 7.4 - Chapter 26. Backup
and Restore") / [7.3](/docs/7.3/backup.html "PostgreSQL 7.3 -
Chapter 26. Backup and Restore") / [7.2](/docs/7.2/backup.html "PostgreSQL 7.2
- Chapter 26. Backup and Restore") / [7.1](/docs/7.1/backup.html "PostgreSQL
7.1 - Chapter 26. Backup and Restore")

__

Chapter 26. Backup and Restore  
---  
[Prev](logfile-maintenance.html "25.3. Log File Maintenance")  | [Up](admin.html "Part III. Server Administration") | Part III. Server Administration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](backup-dump.html "26.1. SQL Dump")  
  
* * *

## Chapter 26. Backup and Restore

**Table of Contents**

[26.1. SQL Dump](backup-dump.html)

    

[26.1.1. Restoring the Dump](backup-dump.html#BACKUP-DUMP-RESTORE)

[26.1.2. Using pg_dumpall](backup-dump.html#BACKUP-DUMP-ALL)

[26.1.3. Handling Large Databases](backup-dump.html#BACKUP-DUMP-LARGE)

[26.2. File System Level Backup](backup-file.html)

[26.3. Continuous Archiving and Point-in-Time Recovery (PITR)](continuous-
archiving.html)

    

[26.3.1. Setting Up WAL Archiving](continuous-archiving.html#BACKUP-ARCHIVING-
WAL)

[26.3.2. Making a Base Backup](continuous-archiving.html#BACKUP-BASE-BACKUP)

[26.3.3. Making a Base Backup Using the Low Level API](continuous-
archiving.html#BACKUP-LOWLEVEL-BASE-BACKUP)

[26.3.4. Recovering Using a Continuous Archive Backup](continuous-
archiving.html#BACKUP-PITR-RECOVERY)

[26.3.5. Timelines](continuous-archiving.html#BACKUP-TIMELINES)

[26.3.6. Tips and Examples](continuous-archiving.html#BACKUP-TIPS)

[26.3.7. Caveats](continuous-archiving.html#CONTINUOUS-ARCHIVING-CAVEATS)

As with everything that contains valuable data, PostgreSQL databases should be
backed up regularly. While the procedure is essentially simple, it is
important to have a clear understanding of the underlying techniques and
assumptions.

There are three fundamentally different approaches to backing up PostgreSQL
data:

  * SQL dump

  * File system level backup

  * Continuous archiving

Each has its own strengths and weaknesses; each is discussed in turn in the
following sections.

* * *

[Prev](logfile-maintenance.html "25.3. Log File Maintenance")  | [Up](admin.html "Part III. Server Administration") |  [Next](backup-dump.html "26.1. SQL Dump")  
---|---|---  
25.3. Log File Maintenance  | [Home](index.html "PostgreSQL 16.9 Documentation") |  26.1. SQL Dump  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/backup.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

