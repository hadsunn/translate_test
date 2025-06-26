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

Supported Versions: [Current](/docs/current/backup-manifest-toplevel.html
"PostgreSQL 17 - 77.1. Backup Manifest Top-level Object")
([17](/docs/17/backup-manifest-toplevel.html "PostgreSQL 17 - 77.1. Backup
Manifest Top-level Object")) / [16](/docs/16/backup-manifest-toplevel.html
"PostgreSQL 16 - 77.1. Backup Manifest Top-level Object") /
[15](/docs/15/backup-manifest-toplevel.html "PostgreSQL 15 - 77.1. Backup
Manifest Top-level Object") / [14](/docs/14/backup-manifest-toplevel.html
"PostgreSQL 14 - 77.1. Backup Manifest Top-level Object") /
[13](/docs/13/backup-manifest-toplevel.html "PostgreSQL 13 - 77.1. Backup
Manifest Top-level Object")

Development Versions: [18](/docs/18/backup-manifest-toplevel.html "PostgreSQL
18 - 77.1. Backup Manifest Top-level Object") / [devel](/docs/devel/backup-
manifest-toplevel.html "PostgreSQL devel - 77.1. Backup Manifest Top-level
Object")

__

77.1. Backup Manifest Top-level Object  
---  
[Prev](backup-manifest-format.html "Chapter 77. Backup Manifest Format")  | [Up](backup-manifest-format.html "Chapter 77. Backup Manifest Format") | Chapter 77. Backup Manifest Format | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](backup-manifest-files.html "77.2. Backup Manifest File Object")  
  
* * *

## 77.1. Backup Manifest Top-level Object #

The backup manifest JSON document contains the following keys.

`PostgreSQL-Backup-Manifest-Version`

    

The associated value is always the integer 1.

`Files`

    

The associated value is always a list of objects, each describing one file
that is present in the backup. No entries are present in this list for the WAL
files that are needed in order to use the backup, or for the backup manifest
itself. The structure of each object in the list is described in [Section
77.2](backup-manifest-files.html "77.2. Backup Manifest File Object").

`WAL-Ranges`

    

The associated value is always a list of objects, each describing a range of
WAL records that must be readable from a particular timeline in order to make
use of the backup. The structure of these objects is further described in
[Section 77.3](backup-manifest-wal-ranges.html "77.3. Backup Manifest WAL
Range Object").

`Manifest-Checksum`

    

This key is always present on the last line of the backup manifest file. The
associated value is a SHA256 checksum of all the preceding lines. We use a
fixed checksum method here to make it possible for clients to do incremental
parsing of the manifest. While a SHA256 checksum is significantly more
expensive than a CRC32C checksum, the manifest should normally be small enough
that the extra computation won't matter very much.

* * *

[Prev](backup-manifest-format.html "Chapter 77. Backup Manifest Format")  | [Up](backup-manifest-format.html "Chapter 77. Backup Manifest Format") |  [Next](backup-manifest-files.html "77.2. Backup Manifest File Object")  
---|---|---  
Chapter 77. Backup Manifest Format  | [Home](index.html "PostgreSQL 16.9 Documentation") |  77.2. Backup Manifest File Object  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/backup-manifest-
toplevel.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

