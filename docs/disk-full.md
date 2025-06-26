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

Supported Versions: [16](/docs/16/disk-full.html "PostgreSQL 16 - 29.2. Disk
Full Failure") / [15](/docs/15/disk-full.html "PostgreSQL 15 - 29.2. Disk Full
Failure") / [14](/docs/14/disk-full.html "PostgreSQL 14 - 29.2. Disk Full
Failure") / [13](/docs/13/disk-full.html "PostgreSQL 13 - 29.2. Disk Full
Failure")

Unsupported versions: [12](/docs/12/disk-full.html "PostgreSQL 12 - 29.2. Disk
Full Failure") / [11](/docs/11/disk-full.html "PostgreSQL 11 - 29.2. Disk Full
Failure") / [10](/docs/10/disk-full.html "PostgreSQL 10 - 29.2. Disk Full
Failure") / [9.6](/docs/9.6/disk-full.html "PostgreSQL 9.6 - 29.2. Disk Full
Failure") / [9.5](/docs/9.5/disk-full.html "PostgreSQL 9.5 - 29.2. Disk Full
Failure") / [9.4](/docs/9.4/disk-full.html "PostgreSQL 9.4 - 29.2. Disk Full
Failure") / [9.3](/docs/9.3/disk-full.html "PostgreSQL 9.3 - 29.2. Disk Full
Failure") / [9.2](/docs/9.2/disk-full.html "PostgreSQL 9.2 - 29.2. Disk Full
Failure") / [9.1](/docs/9.1/disk-full.html "PostgreSQL 9.1 - 29.2. Disk Full
Failure") / [9.0](/docs/9.0/disk-full.html "PostgreSQL 9.0 - 29.2. Disk Full
Failure") / [8.4](/docs/8.4/disk-full.html "PostgreSQL 8.4 - 29.2. Disk Full
Failure") / [8.3](/docs/8.3/disk-full.html "PostgreSQL 8.3 - 29.2. Disk Full
Failure") / [8.2](/docs/8.2/disk-full.html "PostgreSQL 8.2 - 29.2. Disk Full
Failure") / [8.1](/docs/8.1/disk-full.html "PostgreSQL 8.1 - 29.2. Disk Full
Failure") / [8.0](/docs/8.0/disk-full.html "PostgreSQL 8.0 - 29.2. Disk Full
Failure") / [7.4](/docs/7.4/disk-full.html "PostgreSQL 7.4 - 29.2. Disk Full
Failure") / [7.3](/docs/7.3/disk-full.html "PostgreSQL 7.3 - 29.2. Disk Full
Failure")

__

29.2. Disk Full Failure  
---  
[Prev](disk-usage.html "29.1. Determining Disk Usage")  | [Up](diskusage.html "Chapter 29. Monitoring Disk Usage") | Chapter 29. Monitoring Disk Usage | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](wal.html "Chapter 30. Reliability and the Write-Ahead Log")  
  
* * *

## 29.2. Disk Full Failure #

The most important disk monitoring task of a database administrator is to make
sure the disk doesn't become full. A filled data disk will not result in data
corruption, but it might prevent useful activity from occurring. If the disk
holding the WAL files grows full, database server panic and consequent
shutdown might occur.

If you cannot free up additional space on the disk by deleting other things,
you can move some of the database files to other file systems by making use of
tablespaces. See [Section 23.6](manage-ag-tablespaces.html
"23.6. Tablespaces") for more information about that.

### Tip

Some file systems perform badly when they are almost full, so do not wait
until the disk is completely full to take action.

If your system supports per-user disk quotas, then the database will naturally
be subject to whatever quota is placed on the user the server runs as.
Exceeding the quota will have the same bad effects as running out of disk
space entirely.

* * *

[Prev](disk-usage.html "29.1. Determining Disk Usage")  | [Up](diskusage.html "Chapter 29. Monitoring Disk Usage") |  [Next](wal.html "Chapter 30. Reliability and the Write-Ahead Log")  
---|---|---  
29.1. Determining Disk Usage  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 30. Reliability and the Write-Ahead Log  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/disk-full.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

