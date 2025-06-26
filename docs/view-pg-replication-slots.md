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

Supported Versions: [Current](/docs/current/view-pg-replication-slots.html
"PostgreSQL 17 - 54.19. pg_replication_slots") ([17](/docs/17/view-pg-
replication-slots.html "PostgreSQL 17 - 54.19. pg_replication_slots")) /
[16](/docs/16/view-pg-replication-slots.html "PostgreSQL 16 -
54.19. pg_replication_slots") / [15](/docs/15/view-pg-replication-slots.html
"PostgreSQL 15 - 54.19. pg_replication_slots") / [14](/docs/14/view-pg-
replication-slots.html "PostgreSQL 14 - 54.19. pg_replication_slots") /
[13](/docs/13/view-pg-replication-slots.html "PostgreSQL 13 -
54.19. pg_replication_slots")

Development Versions: [18](/docs/18/view-pg-replication-slots.html "PostgreSQL
18 - 54.19. pg_replication_slots") / [devel](/docs/devel/view-pg-replication-
slots.html "PostgreSQL devel - 54.19. pg_replication_slots")

Unsupported versions: [12](/docs/12/view-pg-replication-slots.html "PostgreSQL
12 - 54.19. pg_replication_slots") / [11](/docs/11/view-pg-replication-
slots.html "PostgreSQL 11 - 54.19. pg_replication_slots") /
[10](/docs/10/view-pg-replication-slots.html "PostgreSQL 10 -
54.19. pg_replication_slots") / [9.6](/docs/9.6/view-pg-replication-slots.html
"PostgreSQL 9.6 - 54.19. pg_replication_slots") / [9.5](/docs/9.5/view-pg-
replication-slots.html "PostgreSQL 9.5 - 54.19. pg_replication_slots") /
[9.4](/docs/9.4/catalog-pg-replication-slots.html "PostgreSQL 9.4 -
54.19. pg_replication_slots")

__

54.19. `pg_replication_slots`  
---  
[Prev](view-pg-replication-origin-status.html "54.18. pg_replication_origin_status")  | [Up](views.html "Chapter 54. System Views") | Chapter 54. System Views | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](view-pg-roles.html "54.20. pg_roles")  
  
* * *

## 54.19. `pg_replication_slots` #

The `pg_replication_slots` view provides a listing of all replication slots
that currently exist on the database cluster, along with their current state.

For more on replication slots, see [Section 27.2.6](warm-
standby.html#STREAMING-REPLICATION-SLOTS "27.2.6. Replication Slots") and
[Chapter 49](logicaldecoding.html "Chapter 49. Logical Decoding").

**Table  54.19. `pg_replication_slots` Columns**

Column Type Description  
---  
`slot_name` `name` A unique, cluster-wide identifier for the replication slot  
`plugin` `name` The base name of the shared object containing the output
plugin this logical slot is using, or null for physical slots.  
`slot_type` `text` The slot type: `physical` or `logical`  
`datoid` `oid` (references [`pg_database`](catalog-pg-database.html
"53.15. pg_database").`oid`) The OID of the database this slot is associated
with, or null. Only logical slots have an associated database.  
`database` `name` (references [`pg_database`](catalog-pg-database.html
"53.15. pg_database").`datname`) The name of the database this slot is
associated with, or null. Only logical slots have an associated database.  
`temporary` `bool` True if this is a temporary replication slot. Temporary
slots are not saved to disk and are automatically dropped on error or when the
session has finished.  
`active` `bool` True if this slot is currently actively being used  
`active_pid` `int4` The process ID of the session using this slot if the slot
is currently actively being used. `NULL` if inactive.  
`xmin` `xid` The oldest transaction that this slot needs the database to
retain. `VACUUM` cannot remove tuples deleted by any later transaction.  
`catalog_xmin` `xid` The oldest transaction affecting the system catalogs that
this slot needs the database to retain. `VACUUM` cannot remove catalog tuples
deleted by any later transaction.  
`restart_lsn` `pg_lsn` The address (`LSN`) of oldest WAL which still might be
required by the consumer of this slot and thus won't be automatically removed
during checkpoints unless this LSN gets behind more than
[max_slot_wal_keep_size](runtime-config-replication.html#GUC-MAX-SLOT-WAL-
KEEP-SIZE) from the current LSN. `NULL` if the `LSN` of this slot has never
been reserved.  
`confirmed_flush_lsn` `pg_lsn` The address (`LSN`) up to which the logical
slot's consumer has confirmed receiving data. Data corresponding to the
transactions committed before this `LSN` is not available anymore. `NULL` for
physical slots.  
`wal_status` `text` Availability of WAL files claimed by this slot. Possible
values are:

  * `reserved` means that the claimed files are within `max_wal_size`.
  * `extended` means that `max_wal_size` is exceeded but the files are still retained, either by the replication slot or by `wal_keep_size`.
  * `unreserved` means that the slot no longer retains the required WAL files and some of them are to be removed at the next checkpoint. This state can return to `reserved` or `extended`.
  * `lost` means that some required WAL files have been removed and this slot is no longer usable.

The last two states are seen only when [max_slot_wal_keep_size](runtime-
config-replication.html#GUC-MAX-SLOT-WAL-KEEP-SIZE) is non-negative. If
`restart_lsn` is NULL, this field is null.  
`safe_wal_size` `int8` The number of bytes that can be written to WAL such
that this slot is not in danger of getting in state "lost". It is NULL for
lost slots, as well as if `max_slot_wal_keep_size` is `-1`.  
`two_phase` `bool` True if the slot is enabled for decoding prepared
transactions. Always false for physical slots.  
`conflicting` `bool` True if this logical slot conflicted with recovery (and
so is now invalidated). Always NULL for physical slots.  
  
  

* * *

[Prev](view-pg-replication-origin-status.html "54.18. pg_replication_origin_status")  | [Up](views.html "Chapter 54. System Views") |  [Next](view-pg-roles.html "54.20. pg_roles")  
---|---|---  
54.18. `pg_replication_origin_status`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.20. `pg_roles`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/view-pg-replication-
slots.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

