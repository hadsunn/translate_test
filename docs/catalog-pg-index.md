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

Supported Versions: [Current](/docs/current/catalog-pg-index.html "PostgreSQL
17 - 53.26. pg_index") ([17](/docs/17/catalog-pg-index.html "PostgreSQL 17 -
53.26. pg_index")) / [16](/docs/16/catalog-pg-index.html "PostgreSQL 16 -
53.26. pg_index") / [15](/docs/15/catalog-pg-index.html "PostgreSQL 15 -
53.26. pg_index") / [14](/docs/14/catalog-pg-index.html "PostgreSQL 14 -
53.26. pg_index") / [13](/docs/13/catalog-pg-index.html "PostgreSQL 13 -
53.26. pg_index")

Development Versions: [18](/docs/18/catalog-pg-index.html "PostgreSQL 18 -
53.26. pg_index") / [devel](/docs/devel/catalog-pg-index.html "PostgreSQL
devel - 53.26. pg_index")

Unsupported versions: [12](/docs/12/catalog-pg-index.html "PostgreSQL 12 -
53.26. pg_index") / [11](/docs/11/catalog-pg-index.html "PostgreSQL 11 -
53.26. pg_index") / [10](/docs/10/catalog-pg-index.html "PostgreSQL 10 -
53.26. pg_index") / [9.6](/docs/9.6/catalog-pg-index.html "PostgreSQL 9.6 -
53.26. pg_index") / [9.5](/docs/9.5/catalog-pg-index.html "PostgreSQL 9.5 -
53.26. pg_index") / [9.4](/docs/9.4/catalog-pg-index.html "PostgreSQL 9.4 -
53.26. pg_index") / [9.3](/docs/9.3/catalog-pg-index.html "PostgreSQL 9.3 -
53.26. pg_index") / [9.2](/docs/9.2/catalog-pg-index.html "PostgreSQL 9.2 -
53.26. pg_index") / [9.1](/docs/9.1/catalog-pg-index.html "PostgreSQL 9.1 -
53.26. pg_index") / [9.0](/docs/9.0/catalog-pg-index.html "PostgreSQL 9.0 -
53.26. pg_index") / [8.4](/docs/8.4/catalog-pg-index.html "PostgreSQL 8.4 -
53.26. pg_index") / [8.3](/docs/8.3/catalog-pg-index.html "PostgreSQL 8.3 -
53.26. pg_index") / [8.2](/docs/8.2/catalog-pg-index.html "PostgreSQL 8.2 -
53.26. pg_index") / [8.1](/docs/8.1/catalog-pg-index.html "PostgreSQL 8.1 -
53.26. pg_index") / [8.0](/docs/8.0/catalog-pg-index.html "PostgreSQL 8.0 -
53.26. pg_index") / [7.4](/docs/7.4/catalog-pg-index.html "PostgreSQL 7.4 -
53.26. pg_index") / [7.3](/docs/7.3/catalog-pg-index.html "PostgreSQL 7.3 -
53.26. pg_index") / [7.2](/docs/7.2/catalog-pg-index.html "PostgreSQL 7.2 -
53.26. pg_index") / [7.1](/docs/7.1/catalog-pg-index.html "PostgreSQL 7.1 -
53.26. pg_index")

__

53.26. `pg_index`  
---  
[Prev](catalog-pg-foreign-table.html "53.25. pg_foreign_table")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-inherits.html "53.27. pg_inherits")  
  
* * *

## 53.26. `pg_index` #

The catalog `pg_index` contains part of the information about indexes. The
rest is mostly in [`pg_class`](catalog-pg-class.html "53.11. pg_class").

**Table  53.26. `pg_index` Columns**

Column Type Description  
---  
`indexrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The OID of the [`pg_class`](catalog-pg-class.html
"53.11. pg_class") entry for this index  
`indrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The OID of the [`pg_class`](catalog-pg-class.html
"53.11. pg_class") entry for the table this index is for  
`indnatts` `int2` The total number of columns in the index (duplicates
`pg_class.relnatts`); this number includes both key and included attributes  
`indnkeyatts` `int2` The number of _key columns_ in the index, not counting
any _included columns_ , which are merely stored and do not participate in the
index semantics  
`indisunique` `bool` If true, this is a unique index  
`indnullsnotdistinct` `bool` This value is only used for unique indexes. If
false, this unique index will consider null values distinct (so the index can
contain multiple null values in a column, the default PostgreSQL behavior). If
it is true, it will consider null values to be equal (so the index can only
contain one null value in a column).  
`indisprimary` `bool` If true, this index represents the primary key of the
table (`indisunique` should always be true when this is true)  
`indisexclusion` `bool` If true, this index supports an exclusion constraint  
`indimmediate` `bool` If true, the uniqueness check is enforced immediately on
insertion (irrelevant if `indisunique` is not true)  
`indisclustered` `bool` If true, the table was last clustered on this index  
`indisvalid` `bool` If true, the index is currently valid for queries. False
means the index is possibly incomplete: it must still be modified by
[`INSERT`](sql-insert.html "INSERT")/[`UPDATE`](sql-update.html "UPDATE")
operations, but it cannot safely be used for queries. If it is unique, the
uniqueness property is not guaranteed true either.  
`indcheckxmin` `bool` If true, queries must not use the index until the `xmin`
of this `pg_index` row is below their `TransactionXmin` event horizon, because
the table may contain broken [HOT chains](storage-hot.html "73.7. Heap-Only
Tuples \(HOT\)") with incompatible rows that they can see  
`indisready` `bool` If true, the index is currently ready for inserts. False
means the index must be ignored by [`INSERT`](sql-insert.html
"INSERT")/[`UPDATE`](sql-update.html "UPDATE") operations.  
`indislive` `bool` If false, the index is in process of being dropped, and
should be ignored for all purposes (including HOT-safety decisions)  
`indisreplident` `bool` If true this index has been chosen as “replica
identity” using [`ALTER TABLE ... REPLICA IDENTITY USING INDEX ...`](sql-
altertable.html#SQL-ALTERTABLE-REPLICA-IDENTITY)  
`indkey` `int2vector` (references [`pg_attribute`](catalog-pg-attribute.html
"53.7. pg_attribute").`attnum`) This is an array of `indnatts` values that
indicate which table columns this index indexes. For example, a value of `1 3`
would mean that the first and the third table columns make up the index
entries. Key columns come before non-key (included) columns. A zero in this
array indicates that the corresponding index attribute is an expression over
the table columns, rather than a simple column reference.  
`indcollation` `oidvector` (references [`pg_collation`](catalog-pg-
collation.html "53.12. pg_collation").`oid`) For each column in the index key
(`indnkeyatts` values), this contains the OID of the collation to use for the
index, or zero if the column is not of a collatable data type.  
`indclass` `oidvector` (references [`pg_opclass`](catalog-pg-opclass.html
"53.33. pg_opclass").`oid`) For each column in the index key (`indnkeyatts`
values), this contains the OID of the operator class to use. See
[`pg_opclass`](catalog-pg-opclass.html "53.33. pg_opclass") for details.  
`indoption` `int2vector` This is an array of `indnkeyatts` values that store
per-column flag bits. The meaning of the bits is defined by the index's access
method.  
`indexprs` `pg_node_tree` Expression trees (in `nodeToString()`
representation) for index attributes that are not simple column references.
This is a list with one element for each zero entry in `indkey`. Null if all
index attributes are simple references.  
`indpred` `pg_node_tree` Expression tree (in `nodeToString()` representation)
for partial index predicate. Null if not a partial index.  
  
  

* * *

[Prev](catalog-pg-foreign-table.html "53.25. pg_foreign_table")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-inherits.html "53.27. pg_inherits")  
---|---|---  
53.25. `pg_foreign_table`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.27. `pg_inherits`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-index.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

