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

Supported Versions: [Current](/docs/current/catalog-pg-inherits.html
"PostgreSQL 17 - 53.27. pg_inherits") ([17](/docs/17/catalog-pg-inherits.html
"PostgreSQL 17 - 53.27. pg_inherits")) / [16](/docs/16/catalog-pg-
inherits.html "PostgreSQL 16 - 53.27. pg_inherits") / [15](/docs/15/catalog-
pg-inherits.html "PostgreSQL 15 - 53.27. pg_inherits") /
[14](/docs/14/catalog-pg-inherits.html "PostgreSQL 14 - 53.27. pg_inherits") /
[13](/docs/13/catalog-pg-inherits.html "PostgreSQL 13 - 53.27. pg_inherits")

Development Versions: [18](/docs/18/catalog-pg-inherits.html "PostgreSQL 18 -
53.27. pg_inherits") / [devel](/docs/devel/catalog-pg-inherits.html
"PostgreSQL devel - 53.27. pg_inherits")

Unsupported versions: [12](/docs/12/catalog-pg-inherits.html "PostgreSQL 12 -
53.27. pg_inherits") / [11](/docs/11/catalog-pg-inherits.html "PostgreSQL 11 -
53.27. pg_inherits") / [10](/docs/10/catalog-pg-inherits.html "PostgreSQL 10 -
53.27. pg_inherits") / [9.6](/docs/9.6/catalog-pg-inherits.html "PostgreSQL
9.6 - 53.27. pg_inherits") / [9.5](/docs/9.5/catalog-pg-inherits.html
"PostgreSQL 9.5 - 53.27. pg_inherits") / [9.4](/docs/9.4/catalog-pg-
inherits.html "PostgreSQL 9.4 - 53.27. pg_inherits") /
[9.3](/docs/9.3/catalog-pg-inherits.html "PostgreSQL 9.3 -
53.27. pg_inherits") / [9.2](/docs/9.2/catalog-pg-inherits.html "PostgreSQL
9.2 - 53.27. pg_inherits") / [9.1](/docs/9.1/catalog-pg-inherits.html
"PostgreSQL 9.1 - 53.27. pg_inherits") / [9.0](/docs/9.0/catalog-pg-
inherits.html "PostgreSQL 9.0 - 53.27. pg_inherits") /
[8.4](/docs/8.4/catalog-pg-inherits.html "PostgreSQL 8.4 -
53.27. pg_inherits") / [8.3](/docs/8.3/catalog-pg-inherits.html "PostgreSQL
8.3 - 53.27. pg_inherits") / [8.2](/docs/8.2/catalog-pg-inherits.html
"PostgreSQL 8.2 - 53.27. pg_inherits") / [8.1](/docs/8.1/catalog-pg-
inherits.html "PostgreSQL 8.1 - 53.27. pg_inherits") /
[8.0](/docs/8.0/catalog-pg-inherits.html "PostgreSQL 8.0 -
53.27. pg_inherits") / [7.4](/docs/7.4/catalog-pg-inherits.html "PostgreSQL
7.4 - 53.27. pg_inherits") / [7.3](/docs/7.3/catalog-pg-inherits.html
"PostgreSQL 7.3 - 53.27. pg_inherits") / [7.2](/docs/7.2/catalog-pg-
inherits.html "PostgreSQL 7.2 - 53.27. pg_inherits") /
[7.1](/docs/7.1/catalog-pg-inherits.html "PostgreSQL 7.1 -
53.27. pg_inherits")

__

53.27. `pg_inherits`  
---  
[Prev](catalog-pg-index.html "53.26. pg_index")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-init-privs.html "53.28. pg_init_privs")  
  
* * *

## 53.27. `pg_inherits` #

The catalog `pg_inherits` records information about table and index
inheritance hierarchies. There is one entry for each direct parent-child table
or index relationship in the database. (Indirect inheritance can be determined
by following chains of entries.)

**Table  53.27. `pg_inherits` Columns**

Column Type Description  
---  
`inhrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The OID of the child table or index  
`inhparent` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The OID of the parent table or index  
`inhseqno` `int4` If there is more than one direct parent for a child table
(multiple inheritance), this number tells the order in which the inherited
columns are to be arranged. The count starts at 1. Indexes cannot have
multiple inheritance, since they can only inherit when using declarative
partitioning.  
`inhdetachpending` `bool` `true` for a partition that is in the process of
being detached; `false` otherwise.  
  
  

* * *

[Prev](catalog-pg-index.html "53.26. pg_index")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-init-privs.html "53.28. pg_init_privs")  
---|---|---  
53.26. `pg_index`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.28. `pg_init_privs`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-inherits.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

