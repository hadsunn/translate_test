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

Supported Versions: [Current](/docs/current/catalog-pg-attrdef.html
"PostgreSQL 17 - 53.6. pg_attrdef") ([17](/docs/17/catalog-pg-attrdef.html
"PostgreSQL 17 - 53.6. pg_attrdef")) / [16](/docs/16/catalog-pg-attrdef.html
"PostgreSQL 16 - 53.6. pg_attrdef") / [15](/docs/15/catalog-pg-attrdef.html
"PostgreSQL 15 - 53.6. pg_attrdef") / [14](/docs/14/catalog-pg-attrdef.html
"PostgreSQL 14 - 53.6. pg_attrdef") / [13](/docs/13/catalog-pg-attrdef.html
"PostgreSQL 13 - 53.6. pg_attrdef")

Development Versions: [18](/docs/18/catalog-pg-attrdef.html "PostgreSQL 18 -
53.6. pg_attrdef") / [devel](/docs/devel/catalog-pg-attrdef.html "PostgreSQL
devel - 53.6. pg_attrdef")

Unsupported versions: [12](/docs/12/catalog-pg-attrdef.html "PostgreSQL 12 -
53.6. pg_attrdef") / [11](/docs/11/catalog-pg-attrdef.html "PostgreSQL 11 -
53.6. pg_attrdef") / [10](/docs/10/catalog-pg-attrdef.html "PostgreSQL 10 -
53.6. pg_attrdef") / [9.6](/docs/9.6/catalog-pg-attrdef.html "PostgreSQL 9.6 -
53.6. pg_attrdef") / [9.5](/docs/9.5/catalog-pg-attrdef.html "PostgreSQL 9.5 -
53.6. pg_attrdef") / [9.4](/docs/9.4/catalog-pg-attrdef.html "PostgreSQL 9.4 -
53.6. pg_attrdef") / [9.3](/docs/9.3/catalog-pg-attrdef.html "PostgreSQL 9.3 -
53.6. pg_attrdef") / [9.2](/docs/9.2/catalog-pg-attrdef.html "PostgreSQL 9.2 -
53.6. pg_attrdef") / [9.1](/docs/9.1/catalog-pg-attrdef.html "PostgreSQL 9.1 -
53.6. pg_attrdef") / [9.0](/docs/9.0/catalog-pg-attrdef.html "PostgreSQL 9.0 -
53.6. pg_attrdef") / [8.4](/docs/8.4/catalog-pg-attrdef.html "PostgreSQL 8.4 -
53.6. pg_attrdef") / [8.3](/docs/8.3/catalog-pg-attrdef.html "PostgreSQL 8.3 -
53.6. pg_attrdef") / [8.2](/docs/8.2/catalog-pg-attrdef.html "PostgreSQL 8.2 -
53.6. pg_attrdef") / [8.1](/docs/8.1/catalog-pg-attrdef.html "PostgreSQL 8.1 -
53.6. pg_attrdef") / [8.0](/docs/8.0/catalog-pg-attrdef.html "PostgreSQL 8.0 -
53.6. pg_attrdef") / [7.4](/docs/7.4/catalog-pg-attrdef.html "PostgreSQL 7.4 -
53.6. pg_attrdef") / [7.3](/docs/7.3/catalog-pg-attrdef.html "PostgreSQL 7.3 -
53.6. pg_attrdef") / [7.2](/docs/7.2/catalog-pg-attrdef.html "PostgreSQL 7.2 -
53.6. pg_attrdef") / [7.1](/docs/7.1/catalog-pg-attrdef.html "PostgreSQL 7.1 -
53.6. pg_attrdef")

__

53.6. `pg_attrdef`  
---  
[Prev](catalog-pg-amproc.html "53.5. pg_amproc")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-attribute.html "53.7. pg_attribute")  
  
* * *

## 53.6. `pg_attrdef` #

The catalog `pg_attrdef` stores column default values. The main information
about columns is stored in [`pg_attribute`](catalog-pg-attribute.html
"53.7. pg_attribute"). Only columns for which a default value has been
explicitly set will have an entry here.

**Table  53.6. `pg_attrdef` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`adrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The table this column belongs to  
`adnum` `int2` (references [`pg_attribute`](catalog-pg-attribute.html
"53.7. pg_attribute").`attnum`) The number of the column  
`adbin` `pg_node_tree` The column default value, in `nodeToString()`
representation. Use `pg_get_expr(adbin, adrelid)` to convert it to an SQL
expression.  
  
  

* * *

[Prev](catalog-pg-amproc.html "53.5. pg_amproc")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-attribute.html "53.7. pg_attribute")  
---|---|---  
53.5. `pg_amproc`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.7. `pg_attribute`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-attrdef.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

