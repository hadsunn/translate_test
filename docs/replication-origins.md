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

Supported Versions: [Current](/docs/current/replication-origins.html
"PostgreSQL 17 - Chapter 50. Replication Progress Tracking")
([17](/docs/17/replication-origins.html "PostgreSQL 17 -
Chapter 50. Replication Progress Tracking")) / [16](/docs/16/replication-
origins.html "PostgreSQL 16 - Chapter 50. Replication Progress Tracking") /
[15](/docs/15/replication-origins.html "PostgreSQL 15 -
Chapter 50. Replication Progress Tracking") / [14](/docs/14/replication-
origins.html "PostgreSQL 14 - Chapter 50. Replication Progress Tracking") /
[13](/docs/13/replication-origins.html "PostgreSQL 13 -
Chapter 50. Replication Progress Tracking")

Development Versions: [18](/docs/18/replication-origins.html "PostgreSQL 18 -
Chapter 50. Replication Progress Tracking") / [devel](/docs/devel/replication-
origins.html "PostgreSQL devel - Chapter 50. Replication Progress Tracking")

Unsupported versions: [12](/docs/12/replication-origins.html "PostgreSQL 12 -
Chapter 50. Replication Progress Tracking") / [11](/docs/11/replication-
origins.html "PostgreSQL 11 - Chapter 50. Replication Progress Tracking") /
[10](/docs/10/replication-origins.html "PostgreSQL 10 -
Chapter 50. Replication Progress Tracking") / [9.6](/docs/9.6/replication-
origins.html "PostgreSQL 9.6 - Chapter 50. Replication Progress Tracking") /
[9.5](/docs/9.5/replication-origins.html "PostgreSQL 9.5 -
Chapter 50. Replication Progress Tracking")

__

Chapter 50. Replication Progress Tracking  
---  
[Prev](logicaldecoding-two-phase-commits.html "49.10. Two-phase Commit Support for Logical Decoding")  | [Up](server-programming.html "Part V. Server Programming") | Part V. Server Programming | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](archive-modules.html "Chapter 51. Archive Modules")  
  
* * *

## Chapter 50. Replication Progress Tracking

Replication origins are intended to make it easier to implement logical
replication solutions on top of [logical decoding](logicaldecoding.html
"Chapter 49. Logical Decoding"). They provide a solution to two common
problems:

  * How to safely keep track of replication progress

  * How to change replication behavior based on the origin of a row; for example, to prevent loops in bi-directional replication setups

Replication origins have just two properties, a name and an ID. The name,
which is what should be used to refer to the origin across systems, is free-
form `text`. It should be used in a way that makes conflicts between
replication origins created by different replication solutions unlikely; e.g.,
by prefixing the replication solution's name to it. The ID is used only to
avoid having to store the long version in situations where space efficiency is
important. It should never be shared across systems.

Replication origins can be created using the function
[`pg_replication_origin_create()`](functions-admin.html#PG-REPLICATION-ORIGIN-
CREATE); dropped using [`pg_replication_origin_drop()`](functions-
admin.html#PG-REPLICATION-ORIGIN-DROP); and seen in the
[`pg_replication_origin`](catalog-pg-replication-origin.html
"53.44. pg_replication_origin") system catalog.

One nontrivial part of building a replication solution is to keep track of
replay progress in a safe manner. When the applying process, or the whole
cluster, dies, it needs to be possible to find out up to where data has
successfully been replicated. Naive solutions to this, such as updating a row
in a table for every replayed transaction, have problems like run-time
overhead and database bloat.

Using the replication origin infrastructure a session can be marked as
replaying from a remote node (using the
[`pg_replication_origin_session_setup()`](functions-admin.html#PG-REPLICATION-
ORIGIN-SESSION-SETUP) function). Additionally the LSN and commit time stamp of
every source transaction can be configured on a per transaction basis using
[`pg_replication_origin_xact_setup()`](functions-admin.html#PG-REPLICATION-
ORIGIN-XACT-SETUP). If that's done replication progress will persist in a
crash safe manner. Replay progress for all replication origins can be seen in
the [`pg_replication_origin_status`](view-pg-replication-origin-status.html
"54.18. pg_replication_origin_status") view. An individual origin's progress,
e.g., when resuming replication, can be acquired using
[`pg_replication_origin_progress()`](functions-admin.html#PG-REPLICATION-
ORIGIN-PROGRESS) for any origin or
[`pg_replication_origin_session_progress()`](functions-admin.html#PG-
REPLICATION-ORIGIN-SESSION-PROGRESS) for the origin configured in the current
session.

In replication topologies more complex than replication from exactly one
system to one other system, another problem can be that it is hard to avoid
replicating replayed rows again. That can lead both to cycles in the
replication and inefficiencies. Replication origins provide an optional
mechanism to recognize and prevent that. When configured using the functions
referenced in the previous paragraph, every change and transaction passed to
output plugin callbacks (see [Section 49.6](logicaldecoding-output-plugin.html
"49.6. Logical Decoding Output Plugins")) generated by the session is tagged
with the replication origin of the generating session. This allows treating
them differently in the output plugin, e.g., ignoring all but locally-
originating rows. Additionally the [`filter_by_origin_cb`](logicaldecoding-
output-plugin.html#LOGICALDECODING-OUTPUT-PLUGIN-FILTER-ORIGIN
"49.6.4.7. Origin Filter Callback") callback can be used to filter the logical
decoding change stream based on the source. While less flexible, filtering via
that callback is considerably more efficient than doing it in the output
plugin.

* * *

[Prev](logicaldecoding-two-phase-commits.html "49.10. Two-phase Commit Support for Logical Decoding")  | [Up](server-programming.html "Part V. Server Programming") |  [Next](archive-modules.html "Chapter 51. Archive Modules")  
---|---|---  
49.10. Two-phase Commit Support for Logical Decoding  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 51. Archive Modules  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/replication-origins.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

