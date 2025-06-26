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

Supported Versions: [Current](/docs/current/catalog-pg-class.html "PostgreSQL
17 - 53.11. pg_class") ([17](/docs/17/catalog-pg-class.html "PostgreSQL 17 -
53.11. pg_class")) / [16](/docs/16/catalog-pg-class.html "PostgreSQL 16 -
53.11. pg_class") / [15](/docs/15/catalog-pg-class.html "PostgreSQL 15 -
53.11. pg_class") / [14](/docs/14/catalog-pg-class.html "PostgreSQL 14 -
53.11. pg_class") / [13](/docs/13/catalog-pg-class.html "PostgreSQL 13 -
53.11. pg_class")

Development Versions: [18](/docs/18/catalog-pg-class.html "PostgreSQL 18 -
53.11. pg_class") / [devel](/docs/devel/catalog-pg-class.html "PostgreSQL
devel - 53.11. pg_class")

Unsupported versions: [12](/docs/12/catalog-pg-class.html "PostgreSQL 12 -
53.11. pg_class") / [11](/docs/11/catalog-pg-class.html "PostgreSQL 11 -
53.11. pg_class") / [10](/docs/10/catalog-pg-class.html "PostgreSQL 10 -
53.11. pg_class") / [9.6](/docs/9.6/catalog-pg-class.html "PostgreSQL 9.6 -
53.11. pg_class") / [9.5](/docs/9.5/catalog-pg-class.html "PostgreSQL 9.5 -
53.11. pg_class") / [9.4](/docs/9.4/catalog-pg-class.html "PostgreSQL 9.4 -
53.11. pg_class") / [9.3](/docs/9.3/catalog-pg-class.html "PostgreSQL 9.3 -
53.11. pg_class") / [9.2](/docs/9.2/catalog-pg-class.html "PostgreSQL 9.2 -
53.11. pg_class") / [9.1](/docs/9.1/catalog-pg-class.html "PostgreSQL 9.1 -
53.11. pg_class") / [9.0](/docs/9.0/catalog-pg-class.html "PostgreSQL 9.0 -
53.11. pg_class") / [8.4](/docs/8.4/catalog-pg-class.html "PostgreSQL 8.4 -
53.11. pg_class") / [8.3](/docs/8.3/catalog-pg-class.html "PostgreSQL 8.3 -
53.11. pg_class") / [8.2](/docs/8.2/catalog-pg-class.html "PostgreSQL 8.2 -
53.11. pg_class") / [8.1](/docs/8.1/catalog-pg-class.html "PostgreSQL 8.1 -
53.11. pg_class") / [8.0](/docs/8.0/catalog-pg-class.html "PostgreSQL 8.0 -
53.11. pg_class") / [7.4](/docs/7.4/catalog-pg-class.html "PostgreSQL 7.4 -
53.11. pg_class") / [7.3](/docs/7.3/catalog-pg-class.html "PostgreSQL 7.3 -
53.11. pg_class") / [7.2](/docs/7.2/catalog-pg-class.html "PostgreSQL 7.2 -
53.11. pg_class") / [7.1](/docs/7.1/catalog-pg-class.html "PostgreSQL 7.1 -
53.11. pg_class")

__

53.11. `pg_class`  
---  
[Prev](catalog-pg-cast.html "53.10. pg_cast")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-collation.html "53.12. pg_collation")  
  
* * *

## 53.11. `pg_class` #

The catalog `pg_class` describes tables and other objects that have columns or
are otherwise similar to a table. This includes indexes (but see also
[`pg_index`](catalog-pg-index.html "53.26. pg_index")), sequences (but see
also [`pg_sequence`](catalog-pg-sequence.html "53.47. pg_sequence")), views,
materialized views, composite types, and TOAST tables; see `relkind`. Below,
when we mean all of these kinds of objects we speak of “relations”. Not all of
`pg_class`'s columns are meaningful for all relation kinds.

**Table  53.11. `pg_class` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`relname` `name` Name of the table, index, view, etc.  
`relnamespace` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) The OID of the namespace that contains this
relation  
`reltype` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) The OID of the data type that corresponds to this
table's row type, if any; zero for indexes, sequences, and toast tables, which
have no `pg_type` entry  
`reloftype` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) For typed tables, the OID of the underlying composite
type; zero for all other relations  
`relowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the relation  
`relam` `oid` (references [`pg_am`](catalog-pg-am.html "53.3. pg_am").`oid`)
If this is a table or an index, the access method used (heap, B-tree, hash,
etc.); otherwise zero (zero occurs for sequences, as well as relations without
storage, such as views)  
`relfilenode` `oid` Name of the on-disk file of this relation; zero means this
is a “mapped” relation whose disk file name is determined by low-level state  
`reltablespace` `oid` (references [`pg_tablespace`](catalog-pg-tablespace.html
"53.56. pg_tablespace").`oid`) The tablespace in which this relation is
stored. If zero, the database's default tablespace is implied. Not meaningful
if the relation has no on-disk file, except for partitioned tables, where this
is the tablespace in which partitions will be created when one is not
specified in the creation command.  
`relpages` `int4` Size of the on-disk representation of this table in pages
(of size `BLCKSZ`). This is only an estimate used by the planner. It is
updated by [`VACUUM`](sql-vacuum.html "VACUUM"), [`ANALYZE`](sql-analyze.html
"ANALYZE"), and a few DDL commands such as [`CREATE INDEX`](sql-
createindex.html "CREATE INDEX").  
`reltuples` `float4` Number of live rows in the table. This is only an
estimate used by the planner. It is updated by [`VACUUM`](sql-vacuum.html
"VACUUM"), [`ANALYZE`](sql-analyze.html "ANALYZE"), and a few DDL commands
such as [`CREATE INDEX`](sql-createindex.html "CREATE INDEX"). If the table
has never yet been vacuumed or analyzed, `reltuples` contains `-1` indicating
that the row count is unknown.  
`relallvisible` `int4` Number of pages that are marked all-visible in the
table's visibility map. This is only an estimate used by the planner. It is
updated by [`VACUUM`](sql-vacuum.html "VACUUM"), [`ANALYZE`](sql-analyze.html
"ANALYZE"), and a few DDL commands such as [`CREATE INDEX`](sql-
createindex.html "CREATE INDEX").  
`reltoastrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) OID of the TOAST table associated with this table,
zero if none. The TOAST table stores large attributes “out of line” in a
secondary table.  
`relhasindex` `bool` True if this is a table and it has (or recently had) any
indexes  
`relisshared` `bool` True if this table is shared across all databases in the
cluster. Only certain system catalogs (such as [`pg_database`](catalog-pg-
database.html "53.15. pg_database")) are shared.  
`relpersistence` `char` `p` = permanent table/sequence, `u` = unlogged
table/sequence, `t` = temporary table/sequence  
`relkind` `char` `r` = ordinary table, `i` = index, `S` = sequence, `t` =
TOAST table, `v` = view, `m` = materialized view, `c` = composite type, `f` =
foreign table, `p` = partitioned table, `I` = partitioned index  
`relnatts` `int2` Number of user columns in the relation (system columns not
counted). There must be this many corresponding entries in
[`pg_attribute`](catalog-pg-attribute.html "53.7. pg_attribute"). See also
`pg_attribute`.`attnum`.  
`relchecks` `int2` Number of `CHECK` constraints on the table; see
[`pg_constraint`](catalog-pg-constraint.html "53.13. pg_constraint") catalog  
`relhasrules` `bool` True if table has (or once had) rules; see
[`pg_rewrite`](catalog-pg-rewrite.html "53.45. pg_rewrite") catalog  
`relhastriggers` `bool` True if table has (or once had) triggers; see
[`pg_trigger`](catalog-pg-trigger.html "53.58. pg_trigger") catalog  
`relhassubclass` `bool` True if table or index has (or once had) any
inheritance children or partitions  
`relrowsecurity` `bool` True if table has row-level security enabled; see
[`pg_policy`](catalog-pg-policy.html "53.38. pg_policy") catalog  
`relforcerowsecurity` `bool` True if row-level security (when enabled) will
also apply to table owner; see [`pg_policy`](catalog-pg-policy.html
"53.38. pg_policy") catalog  
`relispopulated` `bool` True if relation is populated (this is true for all
relations other than some materialized views)  
`relreplident` `char` Columns used to form “replica identity” for rows: `d` =
default (primary key, if any), `n` = nothing, `f` = all columns, `i` = index
with `indisreplident` set (same as nothing if the index used has been dropped)  
`relispartition` `bool` True if table or index is a partition  
`relrewrite` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) For new relations being written during a DDL
operation that requires a table rewrite, this contains the OID of the original
relation; otherwise zero. That state is only visible internally; this field
should never contain anything other than zero for a user-visible relation.  
`relfrozenxid` `xid` All transaction IDs before this one have been replaced
with a permanent (“frozen”) transaction ID in this table. This is used to
track whether the table needs to be vacuumed in order to prevent transaction
ID wraparound or to allow `pg_xact` to be shrunk. Zero
(`InvalidTransactionId`) if the relation is not a table.  
`relminmxid` `xid` All multixact IDs before this one have been replaced by a
transaction ID in this table. This is used to track whether the table needs to
be vacuumed in order to prevent multixact ID wraparound or to allow
`pg_multixact` to be shrunk. Zero (`InvalidMultiXactId`) if the relation is
not a table.  
`relacl` `aclitem[]` Access privileges; see [Section 5.7](ddl-priv.html
"5.7. Privileges") for details  
`reloptions` `text[]` Access-method-specific options, as “keyword=value”
strings  
`relpartbound` `pg_node_tree` If table is a partition (see `relispartition`),
internal representation of the partition bound  
  
  

Several of the Boolean flags in `pg_class` are maintained lazily: they are
guaranteed to be true if that's the correct state, but may not be reset to
false immediately when the condition is no longer true. For example,
`relhasindex` is set by [`CREATE INDEX`](sql-createindex.html "CREATE INDEX"),
but it is never cleared by [`DROP INDEX`](sql-dropindex.html "DROP INDEX").
Instead, [`VACUUM`](sql-vacuum.html "VACUUM") clears `relhasindex` if it finds
the table has no indexes. This arrangement avoids race conditions and improves
concurrency.

* * *

[Prev](catalog-pg-cast.html "53.10. pg_cast")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-collation.html "53.12. pg_collation")  
---|---|---  
53.10. `pg_cast`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.12. `pg_collation`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-class.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

