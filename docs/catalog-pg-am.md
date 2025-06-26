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

Supported Versions: [Current](/docs/current/catalog-pg-am.html "PostgreSQL 17
- 53.3. pg_am") ([17](/docs/17/catalog-pg-am.html "PostgreSQL 17 -
53.3. pg_am")) / [16](/docs/16/catalog-pg-am.html "PostgreSQL 16 -
53.3. pg_am") / [15](/docs/15/catalog-pg-am.html "PostgreSQL 15 -
53.3. pg_am") / [14](/docs/14/catalog-pg-am.html "PostgreSQL 14 -
53.3. pg_am") / [13](/docs/13/catalog-pg-am.html "PostgreSQL 13 -
53.3. pg_am")

Development Versions: [18](/docs/18/catalog-pg-am.html "PostgreSQL 18 -
53.3. pg_am") / [devel](/docs/devel/catalog-pg-am.html "PostgreSQL devel -
53.3. pg_am")

Unsupported versions: [12](/docs/12/catalog-pg-am.html "PostgreSQL 12 -
53.3. pg_am") / [11](/docs/11/catalog-pg-am.html "PostgreSQL 11 -
53.3. pg_am") / [10](/docs/10/catalog-pg-am.html "PostgreSQL 10 -
53.3. pg_am") / [9.6](/docs/9.6/catalog-pg-am.html "PostgreSQL 9.6 -
53.3. pg_am") / [9.5](/docs/9.5/catalog-pg-am.html "PostgreSQL 9.5 -
53.3. pg_am") / [9.4](/docs/9.4/catalog-pg-am.html "PostgreSQL 9.4 -
53.3. pg_am") / [9.3](/docs/9.3/catalog-pg-am.html "PostgreSQL 9.3 -
53.3. pg_am") / [9.2](/docs/9.2/catalog-pg-am.html "PostgreSQL 9.2 -
53.3. pg_am") / [9.1](/docs/9.1/catalog-pg-am.html "PostgreSQL 9.1 -
53.3. pg_am") / [9.0](/docs/9.0/catalog-pg-am.html "PostgreSQL 9.0 -
53.3. pg_am") / [8.4](/docs/8.4/catalog-pg-am.html "PostgreSQL 8.4 -
53.3. pg_am") / [8.3](/docs/8.3/catalog-pg-am.html "PostgreSQL 8.3 -
53.3. pg_am") / [8.2](/docs/8.2/catalog-pg-am.html "PostgreSQL 8.2 -
53.3. pg_am") / [8.1](/docs/8.1/catalog-pg-am.html "PostgreSQL 8.1 -
53.3. pg_am") / [8.0](/docs/8.0/catalog-pg-am.html "PostgreSQL 8.0 -
53.3. pg_am") / [7.4](/docs/7.4/catalog-pg-am.html "PostgreSQL 7.4 -
53.3. pg_am") / [7.3](/docs/7.3/catalog-pg-am.html "PostgreSQL 7.3 -
53.3. pg_am")

__

53.3. `pg_am`  
---  
[Prev](catalog-pg-aggregate.html "53.2. pg_aggregate")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-amop.html "53.4. pg_amop")  
  
* * *

## 53.3. `pg_am` #

The catalog `pg_am` stores information about relation access methods. There is
one row for each access method supported by the system. Currently, only tables
and indexes have access methods. The requirements for table and index access
methods are discussed in detail in [Chapter 63](tableam.html
"Chapter 63. Table Access Method Interface Definition") and [Chapter
64](indexam.html "Chapter 64. Index Access Method Interface Definition")
respectively.

**Table  53.3. `pg_am` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`amname` `name` Name of the access method  
`amhandler` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) OID of a handler function that is responsible for
supplying information about the access method  
`amtype` `char` `t` = table (including materialized views), `i` = index.  
  
  

### Note

Before PostgreSQL 9.6, `pg_am` contained many additional columns representing
properties of index access methods. That data is now only directly visible at
the C code level. However, `pg_index_column_has_property()` and related
functions have been added to allow SQL queries to inspect index access method
properties; see [Table 9.72](functions-info.html#FUNCTIONS-INFO-CATALOG-TABLE
"Table 9.72. System Catalog Information Functions").

* * *

[Prev](catalog-pg-aggregate.html "53.2. pg_aggregate")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-amop.html "53.4. pg_amop")  
---|---|---  
53.2. `pg_aggregate`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.4. `pg_amop`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-am.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

