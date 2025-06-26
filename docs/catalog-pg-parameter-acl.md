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

Supported Versions: [Current](/docs/current/catalog-pg-parameter-acl.html
"PostgreSQL 17 - 53.36. pg_parameter_acl") ([17](/docs/17/catalog-pg-
parameter-acl.html "PostgreSQL 17 - 53.36. pg_parameter_acl")) /
[16](/docs/16/catalog-pg-parameter-acl.html "PostgreSQL 16 -
53.36. pg_parameter_acl") / [15](/docs/15/catalog-pg-parameter-acl.html
"PostgreSQL 15 - 53.36. pg_parameter_acl")

Development Versions: [18](/docs/18/catalog-pg-parameter-acl.html "PostgreSQL
18 - 53.36. pg_parameter_acl") / [devel](/docs/devel/catalog-pg-parameter-
acl.html "PostgreSQL devel - 53.36. pg_parameter_acl")

__

53.36. `pg_parameter_acl`  
---  
[Prev](catalog-pg-opfamily.html "53.35. pg_opfamily")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-partitioned-table.html "53.37. pg_partitioned_table")  
  
* * *

## 53.36. `pg_parameter_acl` #

The catalog `pg_parameter_acl` records configuration parameters for which
privileges have been granted to one or more roles. No entry is made for
parameters that have default privileges.

Unlike most system catalogs, `pg_parameter_acl` is shared across all databases
of a cluster: there is only one copy of `pg_parameter_acl` per cluster, not
one per database.

**Table  53.36. `pg_parameter_acl` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`parname` `text` The name of a configuration parameter for which privileges
are granted  
`paracl` `aclitem[]` Access privileges; see [Section 5.7](ddl-priv.html
"5.7. Privileges") for details  
  
  

* * *

[Prev](catalog-pg-opfamily.html "53.35. pg_opfamily")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-partitioned-table.html "53.37. pg_partitioned_table")  
---|---|---  
53.35. `pg_opfamily`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.37. `pg_partitioned_table`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-parameter-
acl.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

