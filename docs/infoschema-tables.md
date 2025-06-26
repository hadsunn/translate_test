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

Supported Versions: [Current](/docs/current/infoschema-tables.html "PostgreSQL
17 - 37.54. tables") ([17](/docs/17/infoschema-tables.html "PostgreSQL 17 -
37.54. tables")) / [16](/docs/16/infoschema-tables.html "PostgreSQL 16 -
37.54. tables") / [15](/docs/15/infoschema-tables.html "PostgreSQL 15 -
37.54. tables") / [14](/docs/14/infoschema-tables.html "PostgreSQL 14 -
37.54. tables") / [13](/docs/13/infoschema-tables.html "PostgreSQL 13 -
37.54. tables")

Development Versions: [18](/docs/18/infoschema-tables.html "PostgreSQL 18 -
37.54. tables") / [devel](/docs/devel/infoschema-tables.html "PostgreSQL devel
- 37.54. tables")

Unsupported versions: [12](/docs/12/infoschema-tables.html "PostgreSQL 12 -
37.54. tables") / [11](/docs/11/infoschema-tables.html "PostgreSQL 11 -
37.54. tables") / [10](/docs/10/infoschema-tables.html "PostgreSQL 10 -
37.54. tables") / [9.6](/docs/9.6/infoschema-tables.html "PostgreSQL 9.6 -
37.54. tables") / [9.5](/docs/9.5/infoschema-tables.html "PostgreSQL 9.5 -
37.54. tables") / [9.4](/docs/9.4/infoschema-tables.html "PostgreSQL 9.4 -
37.54. tables") / [9.3](/docs/9.3/infoschema-tables.html "PostgreSQL 9.3 -
37.54. tables") / [9.2](/docs/9.2/infoschema-tables.html "PostgreSQL 9.2 -
37.54. tables") / [9.1](/docs/9.1/infoschema-tables.html "PostgreSQL 9.1 -
37.54. tables") / [9.0](/docs/9.0/infoschema-tables.html "PostgreSQL 9.0 -
37.54. tables") / [8.4](/docs/8.4/infoschema-tables.html "PostgreSQL 8.4 -
37.54. tables") / [8.3](/docs/8.3/infoschema-tables.html "PostgreSQL 8.3 -
37.54. tables") / [8.2](/docs/8.2/infoschema-tables.html "PostgreSQL 8.2 -
37.54. tables") / [8.1](/docs/8.1/infoschema-tables.html "PostgreSQL 8.1 -
37.54. tables") / [8.0](/docs/8.0/infoschema-tables.html "PostgreSQL 8.0 -
37.54. tables") / [7.4](/docs/7.4/infoschema-tables.html "PostgreSQL 7.4 -
37.54. tables")

__

37.54. `tables`  
---  
[Prev](infoschema-table-privileges.html "37.53. table_privileges")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-transforms.html "37.55. transforms")  
  
* * *

## 37.54. `tables` #

The view `tables` contains all tables and views defined in the current
database. Only those tables and views are shown that the current user has
access to (by way of being the owner or having some privilege).

**Table  37.52. `tables` Columns**

Column Type Description  
---  
`table_catalog` `sql_identifier` Name of the database that contains the table
(always the current database)  
`table_schema` `sql_identifier` Name of the schema that contains the table  
`table_name` `sql_identifier` Name of the table  
`table_type` `character_data` Type of the table: `BASE TABLE` for a persistent
base table (the normal table type), `VIEW` for a view, `FOREIGN` for a foreign
table, or `LOCAL TEMPORARY` for a temporary table  
`self_referencing_column_name` `sql_identifier` Applies to a feature not
available in PostgreSQL  
`reference_generation` `character_data` Applies to a feature not available in
PostgreSQL  
`user_defined_type_catalog` `sql_identifier` If the table is a typed table,
the name of the database that contains the underlying data type (always the
current database), else null.  
`user_defined_type_schema` `sql_identifier` If the table is a typed table, the
name of the schema that contains the underlying data type, else null.  
`user_defined_type_name` `sql_identifier` If the table is a typed table, the
name of the underlying data type, else null.  
`is_insertable_into` `yes_or_no` `YES` if the table is insertable into, `NO`
if not (Base tables are always insertable into, views not necessarily.)  
`is_typed` `yes_or_no` `YES` if the table is a typed table, `NO` if not  
`commit_action` `character_data` Not yet implemented  
  
  

* * *

[Prev](infoschema-table-privileges.html "37.53. table_privileges")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-transforms.html "37.55. transforms")  
---|---|---  
37.53. `table_privileges`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.55. `transforms`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-tables.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

