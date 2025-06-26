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

Supported Versions: [Current](/docs/current/catalog-pg-attribute.html
"PostgreSQL 17 - 53.7. pg_attribute") ([17](/docs/17/catalog-pg-attribute.html
"PostgreSQL 17 - 53.7. pg_attribute")) / [16](/docs/16/catalog-pg-
attribute.html "PostgreSQL 16 - 53.7. pg_attribute") / [15](/docs/15/catalog-
pg-attribute.html "PostgreSQL 15 - 53.7. pg_attribute") /
[14](/docs/14/catalog-pg-attribute.html "PostgreSQL 14 - 53.7. pg_attribute")
/ [13](/docs/13/catalog-pg-attribute.html "PostgreSQL 13 -
53.7. pg_attribute")

Development Versions: [18](/docs/18/catalog-pg-attribute.html "PostgreSQL 18 -
53.7. pg_attribute") / [devel](/docs/devel/catalog-pg-attribute.html
"PostgreSQL devel - 53.7. pg_attribute")

Unsupported versions: [12](/docs/12/catalog-pg-attribute.html "PostgreSQL 12 -
53.7. pg_attribute") / [11](/docs/11/catalog-pg-attribute.html "PostgreSQL 11
- 53.7. pg_attribute") / [10](/docs/10/catalog-pg-attribute.html "PostgreSQL
10 - 53.7. pg_attribute") / [9.6](/docs/9.6/catalog-pg-attribute.html
"PostgreSQL 9.6 - 53.7. pg_attribute") / [9.5](/docs/9.5/catalog-pg-
attribute.html "PostgreSQL 9.5 - 53.7. pg_attribute") /
[9.4](/docs/9.4/catalog-pg-attribute.html "PostgreSQL 9.4 -
53.7. pg_attribute") / [9.3](/docs/9.3/catalog-pg-attribute.html "PostgreSQL
9.3 - 53.7. pg_attribute") / [9.2](/docs/9.2/catalog-pg-attribute.html
"PostgreSQL 9.2 - 53.7. pg_attribute") / [9.1](/docs/9.1/catalog-pg-
attribute.html "PostgreSQL 9.1 - 53.7. pg_attribute") /
[9.0](/docs/9.0/catalog-pg-attribute.html "PostgreSQL 9.0 -
53.7. pg_attribute") / [8.4](/docs/8.4/catalog-pg-attribute.html "PostgreSQL
8.4 - 53.7. pg_attribute") / [8.3](/docs/8.3/catalog-pg-attribute.html
"PostgreSQL 8.3 - 53.7. pg_attribute") / [8.2](/docs/8.2/catalog-pg-
attribute.html "PostgreSQL 8.2 - 53.7. pg_attribute") /
[8.1](/docs/8.1/catalog-pg-attribute.html "PostgreSQL 8.1 -
53.7. pg_attribute") / [8.0](/docs/8.0/catalog-pg-attribute.html "PostgreSQL
8.0 - 53.7. pg_attribute") / [7.4](/docs/7.4/catalog-pg-attribute.html
"PostgreSQL 7.4 - 53.7. pg_attribute") / [7.3](/docs/7.3/catalog-pg-
attribute.html "PostgreSQL 7.3 - 53.7. pg_attribute") /
[7.2](/docs/7.2/catalog-pg-attribute.html "PostgreSQL 7.2 -
53.7. pg_attribute") / [7.1](/docs/7.1/catalog-pg-attribute.html "PostgreSQL
7.1 - 53.7. pg_attribute")

__

53.7. `pg_attribute`  
---  
[Prev](catalog-pg-attrdef.html "53.6. pg_attrdef")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-authid.html "53.8. pg_authid")  
  
* * *

## 53.7. `pg_attribute` #

The catalog `pg_attribute` stores information about table columns. There will
be exactly one `pg_attribute` row for every column in every table in the
database. (There will also be attribute entries for indexes, and indeed all
objects that have [`pg_class`](catalog-pg-class.html "53.11. pg_class")
entries.)

The term attribute is equivalent to column and is used for historical reasons.

**Table  53.7. `pg_attribute` Columns**

Column Type Description  
---  
`attrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The table this column belongs to  
`attname` `name` The column name  
`atttypid` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) The data type of this column (zero for a dropped
column)  
`attlen` `int2` A copy of `pg_type.typlen` of this column's type  
`attnum` `int2` The number of the column. Ordinary columns are numbered from 1
up. System columns, such as `ctid`, have (arbitrary) negative numbers.  
`attcacheoff` `int4` Always -1 in storage, but when loaded into a row
descriptor in memory this might be updated to cache the offset of the
attribute within the row  
`atttypmod` `int4` `atttypmod` records type-specific data supplied at table
creation time (for example, the maximum length of a `varchar` column). It is
passed to type-specific input functions and length coercion functions. The
value will generally be -1 for types that do not need `atttypmod`.  
`attndims` `int2` Number of dimensions, if the column is an array type;
otherwise 0. (Presently, the number of dimensions of an array is not enforced,
so any nonzero value effectively means “it's an array”.)  
`attbyval` `bool` A copy of `pg_type.typbyval` of this column's type  
`attalign` `char` A copy of `pg_type.typalign` of this column's type  
`attstorage` `char` Normally a copy of `pg_type.typstorage` of this column's
type. For TOAST-able data types, this can be altered after column creation to
control storage policy.  
`attcompression` `char` The current compression method of the column.
Typically this is `'\0'` to specify use of the current default setting (see
[default_toast_compression](runtime-config-client.html#GUC-DEFAULT-TOAST-
COMPRESSION)). Otherwise, `'p'` selects pglz compression, while `'l'` selects
LZ4 compression. However, this field is ignored whenever `attstorage` does not
allow compression.  
`attnotnull` `bool` This represents a not-null constraint.  
`atthasdef` `bool` This column has a default expression or generation
expression, in which case there will be a corresponding entry in the
[`pg_attrdef`](catalog-pg-attrdef.html "53.6. pg_attrdef") catalog that
actually defines the expression. (Check `attgenerated` to determine whether
this is a default or a generation expression.)  
`atthasmissing` `bool` This column has a value which is used where the column
is entirely missing from the row, as happens when a column is added with a
non-volatile `DEFAULT` value after the row is created. The actual value used
is stored in the `attmissingval` column.  
`attidentity` `char` If a zero byte (`''`), then not an identity column.
Otherwise, `a` = generated always, `d` = generated by default.  
`attgenerated` `char` If a zero byte (`''`), then not a generated column.
Otherwise, `s` = stored. (Other values might be added in the future.)  
`attisdropped` `bool` This column has been dropped and is no longer valid. A
dropped column is still physically present in the table, but is ignored by the
parser and so cannot be accessed via SQL.  
`attislocal` `bool` This column is defined locally in the relation. Note that
a column can be locally defined and inherited simultaneously.  
`attinhcount` `int2` The number of direct ancestors this column has. A column
with a nonzero number of ancestors cannot be dropped nor renamed.  
`attstattarget` `int2` `attstattarget` controls the level of detail of
statistics accumulated for this column by [`ANALYZE`](sql-analyze.html
"ANALYZE"). A zero value indicates that no statistics should be collected. A
negative value says to use the system default statistics target. The exact
meaning of positive values is data type-dependent. For scalar data types,
`attstattarget` is both the target number of “most common values” to collect,
and the target number of histogram bins to create.  
`attcollation` `oid` (references [`pg_collation`](catalog-pg-collation.html
"53.12. pg_collation").`oid`) The defined collation of the column, or zero if
the column is not of a collatable data type  
`attacl` `aclitem[]` Column-level access privileges, if any have been granted
specifically on this column  
`attoptions` `text[]` Attribute-level options, as “keyword=value” strings  
`attfdwoptions` `text[]` Attribute-level foreign data wrapper options, as
“keyword=value” strings  
`attmissingval` `anyarray` This column has a one element array containing the
value used when the column is entirely missing from the row, as happens when
the column is added with a non-volatile `DEFAULT` value after the row is
created. The value is only used when `atthasmissing` is true. If there is no
value the column is null.  
  
  

In a dropped column's `pg_attribute` entry, `atttypid` is reset to zero, but
`attlen` and the other fields copied from [`pg_type`](catalog-pg-type.html
"53.64. pg_type") are still valid. This arrangement is needed to cope with the
situation where the dropped column's data type was later dropped, and so there
is no `pg_type` row anymore. `attlen` and the other fields can be used to
interpret the contents of a row of the table.

* * *

[Prev](catalog-pg-attrdef.html "53.6. pg_attrdef")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-authid.html "53.8. pg_authid")  
---|---|---  
53.6. `pg_attrdef`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.8. `pg_authid`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-attribute.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

