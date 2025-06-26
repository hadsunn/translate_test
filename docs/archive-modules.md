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

Supported Versions: [Current](/docs/current/archive-modules.html "PostgreSQL
17 - Chapter 51. Archive Modules") ([17](/docs/17/archive-modules.html
"PostgreSQL 17 - Chapter 51. Archive Modules")) / [16](/docs/16/archive-
modules.html "PostgreSQL 16 - Chapter 51. Archive Modules") /
[15](/docs/15/archive-modules.html "PostgreSQL 15 - Chapter 51. Archive
Modules")

Development Versions: [18](/docs/18/archive-modules.html "PostgreSQL 18 -
Chapter 51. Archive Modules") / [devel](/docs/devel/archive-modules.html
"PostgreSQL devel - Chapter 51. Archive Modules")

__

Chapter 51. Archive Modules  
---  
[Prev](replication-origins.html "Chapter 50. Replication Progress Tracking")  | [Up](server-programming.html "Part V. Server Programming") | Part V. Server Programming | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](archive-module-init.html "51.1. Initialization Functions")  
  
* * *

## Chapter 51. Archive Modules

**Table of Contents**

[51.1. Initialization Functions](archive-module-init.html)

[51.2. Archive Module Callbacks](archive-module-callbacks.html)

    

[51.2.1. Startup Callback](archive-module-callbacks.html#ARCHIVE-MODULE-
STARTUP)

[51.2.2. Check Callback](archive-module-callbacks.html#ARCHIVE-MODULE-CHECK)

[51.2.3. Archive Callback](archive-module-callbacks.html#ARCHIVE-MODULE-
ARCHIVE)

[51.2.4. Shutdown Callback](archive-module-callbacks.html#ARCHIVE-MODULE-
SHUTDOWN)

PostgreSQL provides infrastructure to create custom modules for continuous
archiving (see [Section 26.3](continuous-archiving.html "26.3. Continuous
Archiving and Point-in-Time Recovery \(PITR\)")). While archiving via a shell
command (i.e., [archive_command](runtime-config-wal.html#GUC-ARCHIVE-COMMAND))
is much simpler, a custom archive module will often be considerably more
robust and performant.

When a custom [archive_library](runtime-config-wal.html#GUC-ARCHIVE-LIBRARY)
is configured, PostgreSQL will submit completed WAL files to the module, and
the server will avoid recycling or removing these WAL files until the module
indicates that the files were successfully archived. It is ultimately up to
the module to decide what to do with each WAL file, but many recommendations
are listed at [Section 26.3.1](continuous-archiving.html#BACKUP-ARCHIVING-WAL
"26.3.1. Setting Up WAL Archiving").

Archiving modules must at least consist of an initialization function (see
[Section 51.1](archive-module-init.html "51.1. Initialization Functions")) and
the required callbacks (see [Section 51.2](archive-module-callbacks.html
"51.2. Archive Module Callbacks")). However, archive modules are also
permitted to do much more (e.g., declare GUCs and register background
workers).

The `contrib/basic_archive` module contains a working example, which
demonstrates some useful techniques.

* * *

[Prev](replication-origins.html "Chapter 50. Replication Progress Tracking")  | [Up](server-programming.html "Part V. Server Programming") |  [Next](archive-module-init.html "51.1. Initialization Functions")  
---|---|---  
Chapter 50. Replication Progress Tracking  | [Home](index.html "PostgreSQL 16.9 Documentation") |  51.1. Initialization Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/archive-modules.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

