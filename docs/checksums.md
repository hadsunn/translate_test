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

Supported Versions: [Current](/docs/current/checksums.html "PostgreSQL 17 -
30.2. Data Checksums") ([17](/docs/17/checksums.html "PostgreSQL 17 -
30.2. Data Checksums")) / [16](/docs/16/checksums.html "PostgreSQL 16 -
30.2. Data Checksums") / [15](/docs/15/checksums.html "PostgreSQL 15 -
30.2. Data Checksums") / [14](/docs/14/checksums.html "PostgreSQL 14 -
30.2. Data Checksums")

Development Versions: [18](/docs/18/checksums.html "PostgreSQL 18 - 30.2. Data
Checksums") / [devel](/docs/devel/checksums.html "PostgreSQL devel -
30.2. Data Checksums")

__

30.2. Data Checksums  
---  
[Prev](wal-reliability.html "30.1. Reliability")  | [Up](wal.html "Chapter 30. Reliability and the Write-Ahead Log") | Chapter 30. Reliability and the Write-Ahead Log | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](wal-intro.html "30.3. Write-Ahead Logging \(WAL\)")  
  
* * *

## 30.2. Data Checksums #

[30.2.1. Off-line Enabling of Checksums](checksums.html#CHECKSUMS-OFFLINE-
ENABLE-DISABLE)

By default, data pages are not protected by checksums, but this can optionally
be enabled for a cluster. When enabled, each data page includes a checksum
that is updated when the page is written and verified each time the page is
read. Only data pages are protected by checksums; internal data structures and
temporary files are not.

Checksums can be enabled when the cluster is initialized using [initdb](app-
initdb.html#APP-INITDB-DATA-CHECKSUMS). They can also be enabled or disabled
at a later time as an offline operation. Data checksums are enabled or
disabled at the full cluster level, and cannot be specified individually for
databases or tables.

The current state of checksums in the cluster can be verified by viewing the
value of the read-only configuration variable [data_checksums](runtime-config-
preset.html#GUC-DATA-CHECKSUMS) by issuing the command `SHOW data_checksums`.

When attempting to recover from page corruptions, it may be necessary to
bypass the checksum protection. To do this, temporarily set the configuration
parameter [ignore_checksum_failure](runtime-config-developer.html#GUC-IGNORE-
CHECKSUM-FAILURE).

### 30.2.1. Off-line Enabling of Checksums #

The [pg_checksums](app-pgchecksums.html "pg_checksums") application can be
used to enable or disable data checksums, as well as verify checksums, on an
offline cluster.

* * *

[Prev](wal-reliability.html "30.1. Reliability")  | [Up](wal.html "Chapter 30. Reliability and the Write-Ahead Log") |  [Next](wal-intro.html "30.3. Write-Ahead Logging \(WAL\)")  
---|---|---  
30.1. Reliability  | [Home](index.html "PostgreSQL 16.9 Documentation") |  30.3. Write-Ahead Logging (WAL)  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/checksums.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

