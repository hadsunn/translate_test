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

Supported Versions: [Current](/docs/current/backup-manifest-files.html
"PostgreSQL 17 - 77.2. Backup Manifest File Object") ([17](/docs/17/backup-
manifest-files.html "PostgreSQL 17 - 77.2. Backup Manifest File Object")) /
[16](/docs/16/backup-manifest-files.html "PostgreSQL 16 - 77.2. Backup
Manifest File Object") / [15](/docs/15/backup-manifest-files.html "PostgreSQL
15 - 77.2. Backup Manifest File Object") / [14](/docs/14/backup-manifest-
files.html "PostgreSQL 14 - 77.2. Backup Manifest File Object") /
[13](/docs/13/backup-manifest-files.html "PostgreSQL 13 - 77.2. Backup
Manifest File Object")

Development Versions: [18](/docs/18/backup-manifest-files.html "PostgreSQL 18
- 77.2. Backup Manifest File Object") / [devel](/docs/devel/backup-manifest-
files.html "PostgreSQL devel - 77.2. Backup Manifest File Object")

__

77.2. Backup Manifest File Object  
---  
[Prev](backup-manifest-toplevel.html "77.1. Backup Manifest Top-level Object")  | [Up](backup-manifest-format.html "Chapter 77. Backup Manifest Format") | Chapter 77. Backup Manifest Format | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](backup-manifest-wal-ranges.html "77.3. Backup Manifest WAL Range Object")  
  
* * *

## 77.2. Backup Manifest File Object #

The object which describes a single file contains either a `Path` key or an
`Encoded-Path` key. Normally, the `Path` key will be present. The associated
string value is the path of the file relative to the root of the backup
directory. Files located in a user-defined tablespace will have paths whose
first two components are `pg_tblspc` and the OID of the tablespace. If the
path is not a string that is legal in UTF-8, or if the user requests that
encoded paths be used for all files, then the `Encoded-Path` key will be
present instead. This stores the same data, but it is encoded as a string of
hexadecimal digits. Each pair of hexadecimal digits in the string represents a
single octet.

The following two keys are always present:

`Size`

    

The expected size of this file, as an integer.

`Last-Modified`

    

The last modification time of the file as reported by the server at the time
of the backup. Unlike the other fields stored in the backup, this field is not
used by [pg_verifybackup](app-pgverifybackup.html "pg_verifybackup"). It is
included only for informational purposes.

If the backup was taken with file checksums enabled, the following keys will
be present:

`Checksum-Algorithm`

    

The checksum algorithm used to compute a checksum for this file. Currently,
this will be the same for every file in the backup manifest, but this may
change in future releases. At present, the supported checksum algorithms are
`CRC32C`, `SHA224`, `SHA256`, `SHA384`, and `SHA512`.

`Checksum`

    

The checksum computed for this file, stored as a series of hexadecimal
characters, two for each byte of the checksum.

* * *

[Prev](backup-manifest-toplevel.html "77.1. Backup Manifest Top-level Object")  | [Up](backup-manifest-format.html "Chapter 77. Backup Manifest Format") |  [Next](backup-manifest-wal-ranges.html "77.3. Backup Manifest WAL Range Object")  
---|---|---  
77.1. Backup Manifest Top-level Object  | [Home](index.html "PostgreSQL 16.9 Documentation") |  77.3. Backup Manifest WAL Range Object  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/backup-manifest-files.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

