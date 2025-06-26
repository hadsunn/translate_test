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

Supported Versions: [Current](/docs/current/infoschema-table-constraints.html
"PostgreSQL 17 - 37.52. table_constraints") ([17](/docs/17/infoschema-table-
constraints.html "PostgreSQL 17 - 37.52. table_constraints")) /
[16](/docs/16/infoschema-table-constraints.html "PostgreSQL 16 -
37.52. table_constraints") / [15](/docs/15/infoschema-table-constraints.html
"PostgreSQL 15 - 37.52. table_constraints") / [14](/docs/14/infoschema-table-
constraints.html "PostgreSQL 14 - 37.52. table_constraints") /
[13](/docs/13/infoschema-table-constraints.html "PostgreSQL 13 -
37.52. table_constraints")

Development Versions: [18](/docs/18/infoschema-table-constraints.html
"PostgreSQL 18 - 37.52. table_constraints") / [devel](/docs/devel/infoschema-
table-constraints.html "PostgreSQL devel - 37.52. table_constraints")

Unsupported versions: [12](/docs/12/infoschema-table-constraints.html
"PostgreSQL 12 - 37.52. table_constraints") / [11](/docs/11/infoschema-table-
constraints.html "PostgreSQL 11 - 37.52. table_constraints") /
[10](/docs/10/infoschema-table-constraints.html "PostgreSQL 10 -
37.52. table_constraints") / [9.6](/docs/9.6/infoschema-table-constraints.html
"PostgreSQL 9.6 - 37.52. table_constraints") / [9.5](/docs/9.5/infoschema-
table-constraints.html "PostgreSQL 9.5 - 37.52. table_constraints") /
[9.4](/docs/9.4/infoschema-table-constraints.html "PostgreSQL 9.4 -
37.52. table_constraints") / [9.3](/docs/9.3/infoschema-table-constraints.html
"PostgreSQL 9.3 - 37.52. table_constraints") / [9.2](/docs/9.2/infoschema-
table-constraints.html "PostgreSQL 9.2 - 37.52. table_constraints") /
[9.1](/docs/9.1/infoschema-table-constraints.html "PostgreSQL 9.1 -
37.52. table_constraints") / [9.0](/docs/9.0/infoschema-table-constraints.html
"PostgreSQL 9.0 - 37.52. table_constraints") / [8.4](/docs/8.4/infoschema-
table-constraints.html "PostgreSQL 8.4 - 37.52. table_constraints") /
[8.3](/docs/8.3/infoschema-table-constraints.html "PostgreSQL 8.3 -
37.52. table_constraints") / [8.2](/docs/8.2/infoschema-table-constraints.html
"PostgreSQL 8.2 - 37.52. table_constraints") / [8.1](/docs/8.1/infoschema-
table-constraints.html "PostgreSQL 8.1 - 37.52. table_constraints") /
[8.0](/docs/8.0/infoschema-table-constraints.html "PostgreSQL 8.0 -
37.52. table_constraints") / [7.4](/docs/7.4/infoschema-table-constraints.html
"PostgreSQL 7.4 - 37.52. table_constraints")

__

37.52. `table_constraints`  
---  
[Prev](infoschema-sql-sizing.html "37.51. sql_sizing")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-table-privileges.html "37.53. table_privileges")  
  
* * *

## 37.52. `table_constraints` #

The view `table_constraints` contains all constraints belonging to tables that
the current user owns or has some privilege other than `SELECT` on.

**Table  37.50. `table_constraints` Columns**

Column Type Description  
---  
`constraint_catalog` `sql_identifier` Name of the database that contains the
constraint (always the current database)  
`constraint_schema` `sql_identifier` Name of the schema that contains the
constraint  
`constraint_name` `sql_identifier` Name of the constraint  
`table_catalog` `sql_identifier` Name of the database that contains the table
(always the current database)  
`table_schema` `sql_identifier` Name of the schema that contains the table  
`table_name` `sql_identifier` Name of the table  
`constraint_type` `character_data` Type of the constraint: `CHECK`, `FOREIGN
KEY`, `PRIMARY KEY`, or `UNIQUE`  
`is_deferrable` `yes_or_no` `YES` if the constraint is deferrable, `NO` if not  
`initially_deferred` `yes_or_no` `YES` if the constraint is deferrable and
initially deferred, `NO` if not  
`enforced` `yes_or_no` Applies to a feature not available in PostgreSQL
(currently always `YES`)  
`nulls_distinct` `yes_or_no` If the constraint is a unique constraint, then
`YES` if the constraint treats nulls as distinct or `NO` if it treats nulls as
not distinct, otherwise null for other types of constraints.  
  
  

* * *

[Prev](infoschema-sql-sizing.html "37.51. sql_sizing")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-table-privileges.html "37.53. table_privileges")  
---|---|---  
37.51. `sql_sizing`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.53. `table_privileges`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-table-
constraints.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

