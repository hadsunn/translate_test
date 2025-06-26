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

Supported Versions: [Current](/docs/current/backup-manifest-wal-ranges.html
"PostgreSQL 17 - 77.3. Backup Manifest WAL Range Object")
([17](/docs/17/backup-manifest-wal-ranges.html "PostgreSQL 17 - 77.3. Backup
Manifest WAL Range Object")) / [16](/docs/16/backup-manifest-wal-ranges.html
"PostgreSQL 16 - 77.3. Backup Manifest WAL Range Object") /
[15](/docs/15/backup-manifest-wal-ranges.html "PostgreSQL 15 - 77.3. Backup
Manifest WAL Range Object") / [14](/docs/14/backup-manifest-wal-ranges.html
"PostgreSQL 14 - 77.3. Backup Manifest WAL Range Object") /
[13](/docs/13/backup-manifest-wal-ranges.html "PostgreSQL 13 - 77.3. Backup
Manifest WAL Range Object")

Development Versions: [18](/docs/18/backup-manifest-wal-ranges.html
"PostgreSQL 18 - 77.3. Backup Manifest WAL Range Object") /
[devel](/docs/devel/backup-manifest-wal-ranges.html "PostgreSQL devel -
77.3. Backup Manifest WAL Range Object")

__

77.3. Backup Manifest WAL Range Object  
---  
[Prev](backup-manifest-files.html "77.2. Backup Manifest File Object")  | [Up](backup-manifest-format.html "Chapter 77. Backup Manifest Format") | Chapter 77. Backup Manifest Format | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](appendixes.html "Part VIII. Appendixes")  
  
* * *

## 77.3. Backup Manifest WAL Range Object #

The object which describes a WAL range always has three keys:

`Timeline`

    

The timeline for this range of WAL records, as an integer.

`Start-LSN`

    

The LSN at which replay must begin on the indicated timeline in order to make
use of this backup. The LSN is stored in the format normally used by
PostgreSQL; that is, it is a string consisting of two strings of hexadecimal
characters, each with a length of between 1 and 8, separated by a slash.

`End-LSN`

    

The earliest LSN at which replay on the indicated timeline may end when making
use of this backup. This is stored in the same format as `Start-LSN`.

Ordinarily, there will be only a single WAL range. However, if a backup is
taken from a standby which switches timelines during the backup due to an
upstream promotion, it is possible for multiple ranges to be present, each
with a different timeline. There will never be multiple WAL ranges present for
the same timeline.

* * *

[Prev](backup-manifest-files.html "77.2. Backup Manifest File Object")  | [Up](backup-manifest-format.html "Chapter 77. Backup Manifest Format") |  [Next](appendixes.html "Part VIII. Appendixes")  
---|---|---  
77.2. Backup Manifest File Object  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Part VIII. Appendixes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/backup-manifest-wal-
ranges.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

