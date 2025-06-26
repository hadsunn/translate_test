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

Supported Versions: [Current](/docs/current/archive-module-callbacks.html
"PostgreSQL 17 - 51.2. Archive Module Callbacks") ([17](/docs/17/archive-
module-callbacks.html "PostgreSQL 17 - 51.2. Archive Module Callbacks")) /
[16](/docs/16/archive-module-callbacks.html "PostgreSQL 16 - 51.2. Archive
Module Callbacks") / [15](/docs/15/archive-module-callbacks.html "PostgreSQL
15 - 51.2. Archive Module Callbacks")

Development Versions: [18](/docs/18/archive-module-callbacks.html "PostgreSQL
18 - 51.2. Archive Module Callbacks") / [devel](/docs/devel/archive-module-
callbacks.html "PostgreSQL devel - 51.2. Archive Module Callbacks")

__

51.2. Archive Module Callbacks  
---  
[Prev](archive-module-init.html "51.1. Initialization Functions")  | [Up](archive-modules.html "Chapter 51. Archive Modules") | Chapter 51. Archive Modules | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](reference.html "Part VI. Reference")  
  
* * *

## 51.2. Archive Module Callbacks #

[51.2.1. Startup Callback](archive-module-callbacks.html#ARCHIVE-MODULE-
STARTUP)

[51.2.2. Check Callback](archive-module-callbacks.html#ARCHIVE-MODULE-CHECK)

[51.2.3. Archive Callback](archive-module-callbacks.html#ARCHIVE-MODULE-
ARCHIVE)

[51.2.4. Shutdown Callback](archive-module-callbacks.html#ARCHIVE-MODULE-
SHUTDOWN)

The archive callbacks define the actual archiving behavior of the module. The
server will call them as required to process each individual WAL file.

### 51.2.1. Startup Callback #

The `startup_cb` callback is called shortly after the module is loaded. This
callback can be used to perform any additional initialization required. If the
archive module has any state, it can use `state->private_data` to store it.

    
    
    typedef void (*ArchiveStartupCB) (ArchiveModuleState *state);
    

### 51.2.2. Check Callback #

The `check_configured_cb` callback is called to determine whether the module
is fully configured and ready to accept WAL files (e.g., its configuration
parameters are set to valid values). If no `check_configured_cb` is defined,
the server always assumes the module is configured.

    
    
    typedef bool (*ArchiveCheckConfiguredCB) (ArchiveModuleState *state);
    

If `true` is returned, the server will proceed with archiving the file by
calling the `archive_file_cb` callback. If `false` is returned, archiving will
not proceed, and the archiver will emit the following message to the server
log:

    
    
    WARNING:  archive_mode enabled, yet archiving is not configured
    

In the latter case, the server will periodically call this function, and
archiving will proceed only when it returns `true`.

### 51.2.3. Archive Callback #

The `archive_file_cb` callback is called to archive a single WAL file.

    
    
    typedef bool (*ArchiveFileCB) (ArchiveModuleState *state, const char *file, const char *path);
    

If `true` is returned, the server proceeds as if the file was successfully
archived, which may include recycling or removing the original WAL file. If
`false` is returned, the server will keep the original WAL file and retry
archiving later. _`file`_ will contain just the file name of the WAL file to
archive, while _`path`_ contains the full path of the WAL file (including the
file name).

### 51.2.4. Shutdown Callback #

The `shutdown_cb` callback is called when the archiver process exits (e.g.,
after an error) or the value of [archive_library](runtime-config-wal.html#GUC-
ARCHIVE-LIBRARY) changes. If no `shutdown_cb` is defined, no special action is
taken in these situations. If the archive module has any state, this callback
should free it to avoid leaks.

    
    
    typedef void (*ArchiveShutdownCB) (ArchiveModuleState *state);
    

* * *

[Prev](archive-module-init.html "51.1. Initialization Functions")  | [Up](archive-modules.html "Chapter 51. Archive Modules") |  [Next](reference.html "Part VI. Reference")  
---|---|---  
51.1. Initialization Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Part VI. Reference  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/archive-module-
callbacks.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

