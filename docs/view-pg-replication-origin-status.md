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

Supported Versions: [Current](/docs/current/view-pg-replication-origin-
status.html "PostgreSQL 17 - 54.18. pg_replication_origin_status")
([17](/docs/17/view-pg-replication-origin-status.html "PostgreSQL 17 -
54.18. pg_replication_origin_status")) / [16](/docs/16/view-pg-replication-
origin-status.html "PostgreSQL 16 - 54.18. pg_replication_origin_status") /
[15](/docs/15/view-pg-replication-origin-status.html "PostgreSQL 15 -
54.18. pg_replication_origin_status") / [14](/docs/14/view-pg-replication-
origin-status.html "PostgreSQL 14 - 54.18. pg_replication_origin_status") /
[13](/docs/13/view-pg-replication-origin-status.html "PostgreSQL 13 -
54.18. pg_replication_origin_status")

Development Versions: [18](/docs/18/view-pg-replication-origin-status.html
"PostgreSQL 18 - 54.18. pg_replication_origin_status") /
[devel](/docs/devel/view-pg-replication-origin-status.html "PostgreSQL devel -
54.18. pg_replication_origin_status")

Unsupported versions: [12](/docs/12/view-pg-replication-origin-status.html
"PostgreSQL 12 - 54.18. pg_replication_origin_status") / [11](/docs/11/view-
pg-replication-origin-status.html "PostgreSQL 11 -
54.18. pg_replication_origin_status") / [10](/docs/10/view-pg-replication-
origin-status.html "PostgreSQL 10 - 54.18. pg_replication_origin_status") /
[9.6](/docs/9.6/view-pg-replication-origin-status.html "PostgreSQL 9.6 -
54.18. pg_replication_origin_status") / [9.5](/docs/9.5/view-pg-replication-
origin-status.html "PostgreSQL 9.5 - 54.18. pg_replication_origin_status")

__

54.18. `pg_replication_origin_status`  
---  
[Prev](view-pg-publication-tables.html "54.17. pg_publication_tables")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-replication-slots.html "54.19. pg_replication_slots")  
  
* * *

## 54.18. `pg_replication_origin_status` #

The `pg_replication_origin_status` view contains information about how far
replay for a certain origin has progressed. For more on replication origins
see [Chapter 50](replication-origins.html "Chapter 50. Replication Progress
Tracking").

**Table  54.18. `pg_replication_origin_status` Columns**

Column Type Description  
---  
`local_id` `oid` (references [`pg_replication_origin`](catalog-pg-replication-
origin.html "53.44. pg_replication_origin").`roident`) internal node
identifier  
`external_id` `text` (references [`pg_replication_origin`](catalog-pg-
replication-origin.html "53.44. pg_replication_origin").`roname`) external
node identifier  
`remote_lsn` `pg_lsn` The origin node's LSN up to which data has been
replicated.  
`local_lsn` `pg_lsn` This node's LSN at which `remote_lsn` has been
replicated. Used to flush commit records before persisting data to disk when
using asynchronous commits.  
  
  

* * *

[Prev](view-pg-publication-tables.html "54.17. pg_publication_tables")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-replication-slots.html "54.19. pg_replication_slots")  
---|---|---  
54.17. `pg_publication_tables`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.19. `pg_replication_slots`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-replication-origin-
status.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

