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

Supported Versions: [Current](/docs/current/basic-archive.html "PostgreSQL 17
- F.6. basic_archive — an example WAL archive module") ([17](/docs/17/basic-
archive.html "PostgreSQL 17 - F.6. basic_archive — an example WAL archive
module")) / [16](/docs/16/basic-archive.html "PostgreSQL 16 -
F.6. basic_archive — an example WAL archive module") / [15](/docs/15/basic-
archive.html "PostgreSQL 15 - F.6. basic_archive — an example WAL archive
module")

Development Versions: [18](/docs/18/basic-archive.html "PostgreSQL 18 -
F.6. basic_archive — an example WAL archive module") /
[devel](/docs/devel/basic-archive.html "PostgreSQL devel - F.6. basic_archive
— an example WAL archive module")

__

F.6. basic_archive — an example WAL archive module  
---  
[Prev](basebackup-to-shell.html "F.5. basebackup_to_shell — example "shell" pg_basebackup module")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](bloom.html "F.7. bloom — bloom filter index access method")  
  
* * *

## F.6. basic_archive — an example WAL archive module #

[F.6.1. Configuration Parameters](basic-archive.html#BASIC-ARCHIVE-
CONFIGURATION-PARAMETERS)

[F.6.2. Notes](basic-archive.html#BASIC-ARCHIVE-NOTES)

[F.6.3. Author](basic-archive.html#BASIC-ARCHIVE-AUTHOR)

`basic_archive` is an example of an archive module. This module copies
completed WAL segment files to the specified directory. This may not be
especially useful, but it can serve as a starting point for developing your
own archive module. For more information about archive modules, see [Chapter
51](archive-modules.html "Chapter 51. Archive Modules").

In order to function, this module must be loaded via
[archive_library](runtime-config-wal.html#GUC-ARCHIVE-LIBRARY), and
[archive_mode](runtime-config-wal.html#GUC-ARCHIVE-MODE) must be enabled.

### F.6.1. Configuration Parameters #

`basic_archive.archive_directory` (`string`)

    

The directory where the server should copy WAL segment files. This directory
must already exist. The default is an empty string, which effectively halts
WAL archiving, but if [archive_mode](runtime-config-wal.html#GUC-ARCHIVE-MODE)
is enabled, the server will accumulate WAL segment files in the expectation
that a value will soon be provided.

These parameters must be set in `postgresql.conf`. Typical usage might be:

    
    
    # postgresql.conf
    archive_mode = 'on'
    archive_library = 'basic_archive'
    basic_archive.archive_directory = '/path/to/archive/directory'
    

### F.6.2. Notes #

Server crashes may leave temporary files with the prefix `archtemp` in the
archive directory. It is recommended to delete such files before restarting
the server after a crash. It is safe to remove such files while the server is
running as long as they are unrelated to any archiving still in progress, but
users should use extra caution when doing so.

### F.6.3. Author #

Nathan Bossart

* * *

[Prev](basebackup-to-shell.html "F.5. basebackup_to_shell — example "shell" pg_basebackup module")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](bloom.html "F.7. bloom — bloom filter index access method")  
---|---|---  
F.5. basebackup_to_shell — example "shell" pg_basebackup module  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.7. bloom — bloom filter index access method  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/basic-archive.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

