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

Supported Versions: [16](/docs/16/oldsnapshot.html "PostgreSQL 16 -
F.24. old_snapshot — inspect old_snapshot_threshold state") /
[15](/docs/15/oldsnapshot.html "PostgreSQL 15 - F.24. old_snapshot — inspect
old_snapshot_threshold state") / [14](/docs/14/oldsnapshot.html "PostgreSQL 14
- F.24. old_snapshot — inspect old_snapshot_threshold state")

__

F.24. old_snapshot — inspect `old_snapshot_threshold` state  
---  
[Prev](ltree.html "F.23. ltree — hierarchical tree-like data type")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pageinspect.html "F.25. pageinspect — low-level inspection of database pages")  
  
* * *

## F.24. old_snapshot — inspect `old_snapshot_threshold` state #

[F.24.1. Functions](oldsnapshot.html#OLDSNAPSHOT-FUNCTIONS)

The `old_snapshot` module allows inspection of the server state that is used
to implement [old_snapshot_threshold](runtime-config-resource.html#GUC-OLD-
SNAPSHOT-THRESHOLD).

### F.24.1. Functions #

`pg_old_snapshot_time_mapping(array_offset OUT int4, end_timestamp OUT
timestamptz, newest_xmin OUT xid) returns setof record`

    

Returns all of the entries in the server's timestamp to XID mapping. Each
entry represents the newest xmin of any snapshot taken in the corresponding
minute.

* * *

[Prev](ltree.html "F.23. ltree — hierarchical tree-like data type")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](pageinspect.html "F.25. pageinspect — low-level inspection of database pages")  
---|---|---  
F.23. ltree — hierarchical tree-like data type  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.25. pageinspect — low-level inspection of database pages  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/oldsnapshot.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

