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

Supported Versions: [Current](/docs/current/infoschema-view-column-usage.html
"PostgreSQL 17 - 37.63. view_column_usage") ([17](/docs/17/infoschema-view-
column-usage.html "PostgreSQL 17 - 37.63. view_column_usage")) /
[16](/docs/16/infoschema-view-column-usage.html "PostgreSQL 16 -
37.63. view_column_usage") / [15](/docs/15/infoschema-view-column-usage.html
"PostgreSQL 15 - 37.63. view_column_usage") / [14](/docs/14/infoschema-view-
column-usage.html "PostgreSQL 14 - 37.63. view_column_usage") /
[13](/docs/13/infoschema-view-column-usage.html "PostgreSQL 13 -
37.63. view_column_usage")

Development Versions: [18](/docs/18/infoschema-view-column-usage.html
"PostgreSQL 18 - 37.63. view_column_usage") / [devel](/docs/devel/infoschema-
view-column-usage.html "PostgreSQL devel - 37.63. view_column_usage")

Unsupported versions: [12](/docs/12/infoschema-view-column-usage.html
"PostgreSQL 12 - 37.63. view_column_usage") / [11](/docs/11/infoschema-view-
column-usage.html "PostgreSQL 11 - 37.63. view_column_usage") /
[10](/docs/10/infoschema-view-column-usage.html "PostgreSQL 10 -
37.63. view_column_usage") / [9.6](/docs/9.6/infoschema-view-column-usage.html
"PostgreSQL 9.6 - 37.63. view_column_usage") / [9.5](/docs/9.5/infoschema-
view-column-usage.html "PostgreSQL 9.5 - 37.63. view_column_usage") /
[9.4](/docs/9.4/infoschema-view-column-usage.html "PostgreSQL 9.4 -
37.63. view_column_usage") / [9.3](/docs/9.3/infoschema-view-column-usage.html
"PostgreSQL 9.3 - 37.63. view_column_usage") / [9.2](/docs/9.2/infoschema-
view-column-usage.html "PostgreSQL 9.2 - 37.63. view_column_usage") /
[9.1](/docs/9.1/infoschema-view-column-usage.html "PostgreSQL 9.1 -
37.63. view_column_usage") / [9.0](/docs/9.0/infoschema-view-column-usage.html
"PostgreSQL 9.0 - 37.63. view_column_usage") / [8.4](/docs/8.4/infoschema-
view-column-usage.html "PostgreSQL 8.4 - 37.63. view_column_usage") /
[8.3](/docs/8.3/infoschema-view-column-usage.html "PostgreSQL 8.3 -
37.63. view_column_usage") / [8.2](/docs/8.2/infoschema-view-column-usage.html
"PostgreSQL 8.2 - 37.63. view_column_usage") / [8.1](/docs/8.1/infoschema-
view-column-usage.html "PostgreSQL 8.1 - 37.63. view_column_usage") /
[8.0](/docs/8.0/infoschema-view-column-usage.html "PostgreSQL 8.0 -
37.63. view_column_usage") / [7.4](/docs/7.4/infoschema-view-column-usage.html
"PostgreSQL 7.4 - 37.63. view_column_usage")

__

37.63. `view_column_usage`  
---  
[Prev](infoschema-user-mappings.html "37.62. user_mappings")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-view-routine-usage.html "37.64. view_routine_usage")  
  
* * *

## 37.63. `view_column_usage` #

The view `view_column_usage` identifies all columns that are used in the query
expression of a view (the `SELECT` statement that defines the view). A column
is only included if the table that contains the column is owned by a currently
enabled role.

### Note

Columns of system tables are not included. This should be fixed sometime.

**Table  37.61. `view_column_usage` Columns**

Column Type Description  
---  
`view_catalog` `sql_identifier` Name of the database that contains the view
(always the current database)  
`view_schema` `sql_identifier` Name of the schema that contains the view  
`view_name` `sql_identifier` Name of the view  
`table_catalog` `sql_identifier` Name of the database that contains the table
that contains the column that is used by the view (always the current
database)  
`table_schema` `sql_identifier` Name of the schema that contains the table
that contains the column that is used by the view  
`table_name` `sql_identifier` Name of the table that contains the column that
is used by the view  
`column_name` `sql_identifier` Name of the column that is used by the view  
  
  

* * *

[Prev](infoschema-user-mappings.html "37.62. user_mappings")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-view-routine-usage.html "37.64. view_routine_usage")  
---|---|---  
37.62. `user_mappings`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.64. `view_routine_usage`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-view-column-
usage.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

