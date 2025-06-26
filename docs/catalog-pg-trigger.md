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

Supported Versions: [Current](/docs/current/catalog-pg-trigger.html
"PostgreSQL 17 - 53.58. pg_trigger") ([17](/docs/17/catalog-pg-trigger.html
"PostgreSQL 17 - 53.58. pg_trigger")) / [16](/docs/16/catalog-pg-trigger.html
"PostgreSQL 16 - 53.58. pg_trigger") / [15](/docs/15/catalog-pg-trigger.html
"PostgreSQL 15 - 53.58. pg_trigger") / [14](/docs/14/catalog-pg-trigger.html
"PostgreSQL 14 - 53.58. pg_trigger") / [13](/docs/13/catalog-pg-trigger.html
"PostgreSQL 13 - 53.58. pg_trigger")

Development Versions: [18](/docs/18/catalog-pg-trigger.html "PostgreSQL 18 -
53.58. pg_trigger") / [devel](/docs/devel/catalog-pg-trigger.html "PostgreSQL
devel - 53.58. pg_trigger")

Unsupported versions: [12](/docs/12/catalog-pg-trigger.html "PostgreSQL 12 -
53.58. pg_trigger") / [11](/docs/11/catalog-pg-trigger.html "PostgreSQL 11 -
53.58. pg_trigger") / [10](/docs/10/catalog-pg-trigger.html "PostgreSQL 10 -
53.58. pg_trigger") / [9.6](/docs/9.6/catalog-pg-trigger.html "PostgreSQL 9.6
- 53.58. pg_trigger") / [9.5](/docs/9.5/catalog-pg-trigger.html "PostgreSQL
9.5 - 53.58. pg_trigger") / [9.4](/docs/9.4/catalog-pg-trigger.html
"PostgreSQL 9.4 - 53.58. pg_trigger") / [9.3](/docs/9.3/catalog-pg-
trigger.html "PostgreSQL 9.3 - 53.58. pg_trigger") / [9.2](/docs/9.2/catalog-
pg-trigger.html "PostgreSQL 9.2 - 53.58. pg_trigger") /
[9.1](/docs/9.1/catalog-pg-trigger.html "PostgreSQL 9.1 - 53.58. pg_trigger")
/ [9.0](/docs/9.0/catalog-pg-trigger.html "PostgreSQL 9.0 -
53.58. pg_trigger") / [8.4](/docs/8.4/catalog-pg-trigger.html "PostgreSQL 8.4
- 53.58. pg_trigger") / [8.3](/docs/8.3/catalog-pg-trigger.html "PostgreSQL
8.3 - 53.58. pg_trigger") / [8.2](/docs/8.2/catalog-pg-trigger.html
"PostgreSQL 8.2 - 53.58. pg_trigger") / [8.1](/docs/8.1/catalog-pg-
trigger.html "PostgreSQL 8.1 - 53.58. pg_trigger") / [8.0](/docs/8.0/catalog-
pg-trigger.html "PostgreSQL 8.0 - 53.58. pg_trigger") /
[7.4](/docs/7.4/catalog-pg-trigger.html "PostgreSQL 7.4 - 53.58. pg_trigger")
/ [7.3](/docs/7.3/catalog-pg-trigger.html "PostgreSQL 7.3 -
53.58. pg_trigger") / [7.2](/docs/7.2/catalog-pg-trigger.html "PostgreSQL 7.2
- 53.58. pg_trigger")

__

53.58. `pg_trigger`  
---  
[Prev](catalog-pg-transform.html "53.57. pg_transform")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-ts-config.html "53.59. pg_ts_config")  
  
* * *

## 53.58. `pg_trigger` #

The catalog `pg_trigger` stores triggers on tables and views. See [CREATE
TRIGGER](sql-createtrigger.html "CREATE TRIGGER") for more information.

**Table  53.58. `pg_trigger` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`tgrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The table this trigger is on  
`tgparentid` `oid` (references [`pg_trigger`](catalog-pg-trigger.html
"53.58. pg_trigger").`oid`) Parent trigger that this trigger is cloned from
(this happens when partitions are created or attached to a partitioned table);
zero if not a clone  
`tgname` `name` Trigger name (must be unique among triggers of same table)  
`tgfoid` `oid` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) The function to be called  
`tgtype` `int2` Bit mask identifying trigger firing conditions  
`tgenabled` `char` Controls in which [session_replication_role](runtime-
config-client.html#GUC-SESSION-REPLICATION-ROLE) modes the trigger fires. `O`
= trigger fires in “origin” and “local” modes, `D` = trigger is disabled, `R`
= trigger fires in “replica” mode, `A` = trigger fires always.  
`tgisinternal` `bool` True if trigger is internally generated (usually, to
enforce the constraint identified by `tgconstraint`)  
`tgconstrrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The table referenced by a referential integrity
constraint (zero if trigger is not for a referential integrity constraint)  
`tgconstrindid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The index supporting a unique, primary key,
referential integrity, or exclusion constraint (zero if trigger is not for one
of these types of constraint)  
`tgconstraint` `oid` (references [`pg_constraint`](catalog-pg-constraint.html
"53.13. pg_constraint").`oid`) The [`pg_constraint`](catalog-pg-
constraint.html "53.13. pg_constraint") entry associated with the trigger
(zero if trigger is not for a constraint)  
`tgdeferrable` `bool` True if constraint trigger is deferrable  
`tginitdeferred` `bool` True if constraint trigger is initially deferred  
`tgnargs` `int2` Number of argument strings passed to trigger function  
`tgattr` `int2vector` (references [`pg_attribute`](catalog-pg-attribute.html
"53.7. pg_attribute").`attnum`) Column numbers, if trigger is column-specific;
otherwise an empty array  
`tgargs` `bytea` Argument strings to pass to trigger, each NULL-terminated  
`tgqual` `pg_node_tree` Expression tree (in `nodeToString()` representation)
for the trigger's `WHEN` condition, or null if none  
`tgoldtable` `name` `REFERENCING` clause name for `OLD TABLE`, or null if none  
`tgnewtable` `name` `REFERENCING` clause name for `NEW TABLE`, or null if none  
  
  

Currently, column-specific triggering is supported only for `UPDATE` events,
and so `tgattr` is relevant only for that event type. `tgtype` might contain
bits for other event types as well, but those are presumed to be table-wide
regardless of what is in `tgattr`.

### Note

When `tgconstraint` is nonzero, `tgconstrrelid`, `tgconstrindid`,
`tgdeferrable`, and `tginitdeferred` are largely redundant with the referenced
[`pg_constraint`](catalog-pg-constraint.html "53.13. pg_constraint") entry.
However, it is possible for a non-deferrable trigger to be associated with a
deferrable constraint: foreign key constraints can have some deferrable and
some non-deferrable triggers.

### Note

`pg_class.relhastriggers` must be true if a relation has any triggers in this
catalog.

* * *

[Prev](catalog-pg-transform.html "53.57. pg_transform")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-ts-config.html "53.59. pg_ts_config")  
---|---|---  
53.57. `pg_transform`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.59. `pg_ts_config`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-trigger.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

