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

Supported Versions: [Current](/docs/current/view-pg-config.html "PostgreSQL 17
- 54.5. pg_config") ([17](/docs/17/view-pg-config.html "PostgreSQL 17 -
54.5. pg_config")) / [16](/docs/16/view-pg-config.html "PostgreSQL 16 -
54.5. pg_config") / [15](/docs/15/view-pg-config.html "PostgreSQL 15 -
54.5. pg_config") / [14](/docs/14/view-pg-config.html "PostgreSQL 14 -
54.5. pg_config") / [13](/docs/13/view-pg-config.html "PostgreSQL 13 -
54.5. pg_config")

Development Versions: [18](/docs/18/view-pg-config.html "PostgreSQL 18 -
54.5. pg_config") / [devel](/docs/devel/view-pg-config.html "PostgreSQL devel
- 54.5. pg_config")

Unsupported versions: [12](/docs/12/view-pg-config.html "PostgreSQL 12 -
54.5. pg_config") / [11](/docs/11/view-pg-config.html "PostgreSQL 11 -
54.5. pg_config") / [10](/docs/10/view-pg-config.html "PostgreSQL 10 -
54.5. pg_config") / [9.6](/docs/9.6/view-pg-config.html "PostgreSQL 9.6 -
54.5. pg_config")

__

54.5. `pg_config`  
---  
[Prev](view-pg-backend-memory-contexts.html "54.4. pg_backend_memory_contexts")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-cursors.html "54.6. pg_cursors")  
  
* * *

## 54.5. `pg_config` #

The view `pg_config` describes the compile-time configuration parameters of
the currently installed version of PostgreSQL. It is intended, for example, to
be used by software packages that want to interface to PostgreSQL to
facilitate finding the required header files and libraries. It provides the
same basic information as the [pg_config](app-pgconfig.html "pg_config")
PostgreSQL client application.

By default, the `pg_config` view can be read only by superusers.

**Table  54.5. `pg_config` Columns**

Column Type Description  
---  
`name` `text` The parameter name  
`setting` `text` The parameter value  
  
  

* * *

[Prev](view-pg-backend-memory-contexts.html "54.4. pg_backend_memory_contexts")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-cursors.html "54.6. pg_cursors")  
---|---|---  
54.4. `pg_backend_memory_contexts`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.6. `pg_cursors`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-config.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

