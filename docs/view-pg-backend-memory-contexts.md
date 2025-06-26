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

Supported Versions: [Current](/docs/current/view-pg-backend-memory-
contexts.html "PostgreSQL 17 - 54.4. pg_backend_memory_contexts")
([17](/docs/17/view-pg-backend-memory-contexts.html "PostgreSQL 17 -
54.4. pg_backend_memory_contexts")) / [16](/docs/16/view-pg-backend-memory-
contexts.html "PostgreSQL 16 - 54.4. pg_backend_memory_contexts") /
[15](/docs/15/view-pg-backend-memory-contexts.html "PostgreSQL 15 -
54.4. pg_backend_memory_contexts") / [14](/docs/14/view-pg-backend-memory-
contexts.html "PostgreSQL 14 - 54.4. pg_backend_memory_contexts")

Development Versions: [18](/docs/18/view-pg-backend-memory-contexts.html
"PostgreSQL 18 - 54.4. pg_backend_memory_contexts") /
[devel](/docs/devel/view-pg-backend-memory-contexts.html "PostgreSQL devel -
54.4. pg_backend_memory_contexts")

__

54.4. `pg_backend_memory_contexts`  
---  
[Prev](view-pg-available-extension-versions.html "54.3. pg_available_extension_versions")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-config.html "54.5. pg_config")  
  
* * *

## 54.4. `pg_backend_memory_contexts` #

The view `pg_backend_memory_contexts` displays all the memory contexts of the
server process attached to the current session.

`pg_backend_memory_contexts` contains one row for each memory context.

**Table  54.4. `pg_backend_memory_contexts` Columns**

Column Type Description  
---  
`name` `text` Name of the memory context  
`ident` `text` Identification information of the memory context. This field is
truncated at 1024 bytes  
`parent` `text` Name of the parent of this memory context  
`level` `int4` Distance from TopMemoryContext in context tree  
`total_bytes` `int8` Total bytes allocated for this memory context  
`total_nblocks` `int8` Total number of blocks allocated for this memory
context  
`free_bytes` `int8` Free space in bytes  
`free_chunks` `int8` Total number of free chunks  
`used_bytes` `int8` Used space in bytes  
  
  

By default, the `pg_backend_memory_contexts` view can be read only by
superusers or roles with the privileges of the `pg_read_all_stats` role.

* * *

[Prev](view-pg-available-extension-versions.html "54.3. pg_available_extension_versions")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-config.html "54.5. pg_config")  
---|---|---  
54.3. `pg_available_extension_versions`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.5. `pg_config`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-backend-memory-
contexts.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

