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

Supported Versions: [Current](/docs/current/catalog-pg-partitioned-table.html
"PostgreSQL 17 - 53.37. pg_partitioned_table") ([17](/docs/17/catalog-pg-
partitioned-table.html "PostgreSQL 17 - 53.37. pg_partitioned_table")) /
[16](/docs/16/catalog-pg-partitioned-table.html "PostgreSQL 16 -
53.37. pg_partitioned_table") / [15](/docs/15/catalog-pg-partitioned-
table.html "PostgreSQL 15 - 53.37. pg_partitioned_table") /
[14](/docs/14/catalog-pg-partitioned-table.html "PostgreSQL 14 -
53.37. pg_partitioned_table") / [13](/docs/13/catalog-pg-partitioned-
table.html "PostgreSQL 13 - 53.37. pg_partitioned_table")

Development Versions: [18](/docs/18/catalog-pg-partitioned-table.html
"PostgreSQL 18 - 53.37. pg_partitioned_table") / [devel](/docs/devel/catalog-
pg-partitioned-table.html "PostgreSQL devel - 53.37. pg_partitioned_table")

Unsupported versions: [12](/docs/12/catalog-pg-partitioned-table.html
"PostgreSQL 12 - 53.37. pg_partitioned_table") / [11](/docs/11/catalog-pg-
partitioned-table.html "PostgreSQL 11 - 53.37. pg_partitioned_table") /
[10](/docs/10/catalog-pg-partitioned-table.html "PostgreSQL 10 -
53.37. pg_partitioned_table")

__

53.37. `pg_partitioned_table`  
---  
[Prev](catalog-pg-parameter-acl.html "53.36. pg_parameter_acl")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-policy.html "53.38. pg_policy")  
  
* * *

## 53.37. `pg_partitioned_table` #

The catalog `pg_partitioned_table` stores information about how tables are
partitioned.

**Table  53.37. `pg_partitioned_table` Columns**

Column Type Description  
---  
`partrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The OID of the [`pg_class`](catalog-pg-class.html
"53.11. pg_class") entry for this partitioned table  
`partstrat` `char` Partitioning strategy; `h` = hash partitioned table, `l` =
list partitioned table, `r` = range partitioned table  
`partnatts` `int2` The number of columns in the partition key  
`partdefid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The OID of the [`pg_class`](catalog-pg-class.html
"53.11. pg_class") entry for the default partition of this partitioned table,
or zero if this partitioned table does not have a default partition  
`partattrs` `int2vector` (references [`pg_attribute`](catalog-pg-
attribute.html "53.7. pg_attribute").`attnum`) This is an array of `partnatts`
values that indicate which table columns are part of the partition key. For
example, a value of `1 3` would mean that the first and the third table
columns make up the partition key. A zero in this array indicates that the
corresponding partition key column is an expression, rather than a simple
column reference.  
`partclass` `oidvector` (references [`pg_opclass`](catalog-pg-opclass.html
"53.33. pg_opclass").`oid`) For each column in the partition key, this
contains the OID of the operator class to use. See [`pg_opclass`](catalog-pg-
opclass.html "53.33. pg_opclass") for details.  
`partcollation` `oidvector` (references [`pg_collation`](catalog-pg-
collation.html "53.12. pg_collation").`oid`) For each column in the partition
key, this contains the OID of the collation to use for partitioning, or zero
if the column is not of a collatable data type.  
`partexprs` `pg_node_tree` Expression trees (in `nodeToString()`
representation) for partition key columns that are not simple column
references. This is a list with one element for each zero entry in
`partattrs`. Null if all partition key columns are simple references.  
  
  

* * *

[Prev](catalog-pg-parameter-acl.html "53.36. pg_parameter_acl")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-policy.html "53.38. pg_policy")  
---|---|---  
53.36. `pg_parameter_acl`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.38. `pg_policy`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-partitioned-
table.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

