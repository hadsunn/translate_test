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

Supported Versions: [Current](/docs/current/archive-module-init.html
"PostgreSQL 17 - 51.1. Initialization Functions") ([17](/docs/17/archive-
module-init.html "PostgreSQL 17 - 51.1. Initialization Functions")) /
[16](/docs/16/archive-module-init.html "PostgreSQL 16 - 51.1. Initialization
Functions") / [15](/docs/15/archive-module-init.html "PostgreSQL 15 -
51.1. Initialization Functions")

Development Versions: [18](/docs/18/archive-module-init.html "PostgreSQL 18 -
51.1. Initialization Functions") / [devel](/docs/devel/archive-module-
init.html "PostgreSQL devel - 51.1. Initialization Functions")

__

51.1. Initialization Functions  
---  
[Prev](archive-modules.html "Chapter 51. Archive Modules")  | [Up](archive-modules.html "Chapter 51. Archive Modules") | Chapter 51. Archive Modules | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](archive-module-callbacks.html "51.2. Archive Module Callbacks")  
  
* * *

## 51.1. Initialization Functions #

An archive library is loaded by dynamically loading a shared library with the
[archive_library](runtime-config-wal.html#GUC-ARCHIVE-LIBRARY)'s name as the
library base name. The normal library search path is used to locate the
library. To provide the required archive module callbacks and to indicate that
the library is actually an archive module, it needs to provide a function
named `_PG_archive_module_init`. The result of the function must be a pointer
to a struct of type `ArchiveModuleCallbacks`, which contains everything that
the core code needs to know to make use of the archive module. The return
value needs to be of server lifetime, which is typically achieved by defining
it as a `static const` variable in global scope.

    
    
    typedef struct ArchiveModuleCallbacks
    {
        ArchiveStartupCB startup_cb;
        ArchiveCheckConfiguredCB check_configured_cb;
        ArchiveFileCB archive_file_cb;
        ArchiveShutdownCB shutdown_cb;
    } ArchiveModuleCallbacks;
    typedef const ArchiveModuleCallbacks *(*ArchiveModuleInit) (void);
    

Only the `archive_file_cb` callback is required. The others are optional.

* * *

[Prev](archive-modules.html "Chapter 51. Archive Modules")  | [Up](archive-modules.html "Chapter 51. Archive Modules") |  [Next](archive-module-callbacks.html "51.2. Archive Module Callbacks")  
---|---|---  
Chapter 51. Archive Modules  | [Home](index.html "PostgreSQL 16.9 Documentation") |  51.2. Archive Module Callbacks  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/archive-module-init.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

