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

Supported Versions: [Current](/docs/current/infoschema-column-udt-usage.html
"PostgreSQL 17 - 37.16. column_udt_usage") ([17](/docs/17/infoschema-column-
udt-usage.html "PostgreSQL 17 - 37.16. column_udt_usage")) /
[16](/docs/16/infoschema-column-udt-usage.html "PostgreSQL 16 -
37.16. column_udt_usage") / [15](/docs/15/infoschema-column-udt-usage.html
"PostgreSQL 15 - 37.16. column_udt_usage") / [14](/docs/14/infoschema-column-
udt-usage.html "PostgreSQL 14 - 37.16. column_udt_usage") /
[13](/docs/13/infoschema-column-udt-usage.html "PostgreSQL 13 -
37.16. column_udt_usage")

Development Versions: [18](/docs/18/infoschema-column-udt-usage.html
"PostgreSQL 18 - 37.16. column_udt_usage") / [devel](/docs/devel/infoschema-
column-udt-usage.html "PostgreSQL devel - 37.16. column_udt_usage")

Unsupported versions: [12](/docs/12/infoschema-column-udt-usage.html
"PostgreSQL 12 - 37.16. column_udt_usage") / [11](/docs/11/infoschema-column-
udt-usage.html "PostgreSQL 11 - 37.16. column_udt_usage") /
[10](/docs/10/infoschema-column-udt-usage.html "PostgreSQL 10 -
37.16. column_udt_usage") / [9.6](/docs/9.6/infoschema-column-udt-usage.html
"PostgreSQL 9.6 - 37.16. column_udt_usage") / [9.5](/docs/9.5/infoschema-
column-udt-usage.html "PostgreSQL 9.5 - 37.16. column_udt_usage") /
[9.4](/docs/9.4/infoschema-column-udt-usage.html "PostgreSQL 9.4 -
37.16. column_udt_usage") / [9.3](/docs/9.3/infoschema-column-udt-usage.html
"PostgreSQL 9.3 - 37.16. column_udt_usage") / [9.2](/docs/9.2/infoschema-
column-udt-usage.html "PostgreSQL 9.2 - 37.16. column_udt_usage") /
[9.1](/docs/9.1/infoschema-column-udt-usage.html "PostgreSQL 9.1 -
37.16. column_udt_usage") / [9.0](/docs/9.0/infoschema-column-udt-usage.html
"PostgreSQL 9.0 - 37.16. column_udt_usage") / [8.4](/docs/8.4/infoschema-
column-udt-usage.html "PostgreSQL 8.4 - 37.16. column_udt_usage") /
[8.3](/docs/8.3/infoschema-column-udt-usage.html "PostgreSQL 8.3 -
37.16. column_udt_usage") / [8.2](/docs/8.2/infoschema-column-udt-usage.html
"PostgreSQL 8.2 - 37.16. column_udt_usage") / [8.1](/docs/8.1/infoschema-
column-udt-usage.html "PostgreSQL 8.1 - 37.16. column_udt_usage") /
[8.0](/docs/8.0/infoschema-column-udt-usage.html "PostgreSQL 8.0 -
37.16. column_udt_usage") / [7.4](/docs/7.4/infoschema-column-udt-usage.html
"PostgreSQL 7.4 - 37.16. column_udt_usage")

__

37.16. `column_udt_usage`  
---  
[Prev](infoschema-column-privileges.html "37.15. column_privileges")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-columns.html "37.17. columns")  
  
* * *

## 37.16. `column_udt_usage` #

The view `column_udt_usage` identifies all columns that use data types owned
by a currently enabled role. Note that in PostgreSQL, built-in data types
behave like user-defined types, so they are included here as well. See also
[Section 37.17](infoschema-columns.html "37.17. columns") for details.

**Table  37.14. `column_udt_usage` Columns**

Column Type Description  
---  
`udt_catalog` `sql_identifier` Name of the database that the column data type
(the underlying type of the domain, if applicable) is defined in (always the
current database)  
`udt_schema` `sql_identifier` Name of the schema that the column data type
(the underlying type of the domain, if applicable) is defined in  
`udt_name` `sql_identifier` Name of the column data type (the underlying type
of the domain, if applicable)  
`table_catalog` `sql_identifier` Name of the database containing the table
(always the current database)  
`table_schema` `sql_identifier` Name of the schema containing the table  
`table_name` `sql_identifier` Name of the table  
`column_name` `sql_identifier` Name of the column  
  
  

* * *

[Prev](infoschema-column-privileges.html "37.15. column_privileges")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-columns.html "37.17. columns")  
---|---|---  
37.15. `column_privileges`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.17. `columns`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-column-udt-
usage.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

