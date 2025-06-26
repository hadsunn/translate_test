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

Supported Versions: [Current](/docs/current/infoschema-key-column-usage.html
"PostgreSQL 17 - 37.32. key_column_usage") ([17](/docs/17/infoschema-key-
column-usage.html "PostgreSQL 17 - 37.32. key_column_usage")) /
[16](/docs/16/infoschema-key-column-usage.html "PostgreSQL 16 -
37.32. key_column_usage") / [15](/docs/15/infoschema-key-column-usage.html
"PostgreSQL 15 - 37.32. key_column_usage") / [14](/docs/14/infoschema-key-
column-usage.html "PostgreSQL 14 - 37.32. key_column_usage") /
[13](/docs/13/infoschema-key-column-usage.html "PostgreSQL 13 -
37.32. key_column_usage")

Development Versions: [18](/docs/18/infoschema-key-column-usage.html
"PostgreSQL 18 - 37.32. key_column_usage") / [devel](/docs/devel/infoschema-
key-column-usage.html "PostgreSQL devel - 37.32. key_column_usage")

Unsupported versions: [12](/docs/12/infoschema-key-column-usage.html
"PostgreSQL 12 - 37.32. key_column_usage") / [11](/docs/11/infoschema-key-
column-usage.html "PostgreSQL 11 - 37.32. key_column_usage") /
[10](/docs/10/infoschema-key-column-usage.html "PostgreSQL 10 -
37.32. key_column_usage") / [9.6](/docs/9.6/infoschema-key-column-usage.html
"PostgreSQL 9.6 - 37.32. key_column_usage") / [9.5](/docs/9.5/infoschema-key-
column-usage.html "PostgreSQL 9.5 - 37.32. key_column_usage") /
[9.4](/docs/9.4/infoschema-key-column-usage.html "PostgreSQL 9.4 -
37.32. key_column_usage") / [9.3](/docs/9.3/infoschema-key-column-usage.html
"PostgreSQL 9.3 - 37.32. key_column_usage") / [9.2](/docs/9.2/infoschema-key-
column-usage.html "PostgreSQL 9.2 - 37.32. key_column_usage") /
[9.1](/docs/9.1/infoschema-key-column-usage.html "PostgreSQL 9.1 -
37.32. key_column_usage") / [9.0](/docs/9.0/infoschema-key-column-usage.html
"PostgreSQL 9.0 - 37.32. key_column_usage") / [8.4](/docs/8.4/infoschema-key-
column-usage.html "PostgreSQL 8.4 - 37.32. key_column_usage") /
[8.3](/docs/8.3/infoschema-key-column-usage.html "PostgreSQL 8.3 -
37.32. key_column_usage") / [8.2](/docs/8.2/infoschema-key-column-usage.html
"PostgreSQL 8.2 - 37.32. key_column_usage") / [8.1](/docs/8.1/infoschema-key-
column-usage.html "PostgreSQL 8.1 - 37.32. key_column_usage") /
[8.0](/docs/8.0/infoschema-key-column-usage.html "PostgreSQL 8.0 -
37.32. key_column_usage") / [7.4](/docs/7.4/infoschema-key-column-usage.html
"PostgreSQL 7.4 - 37.32. key_column_usage")

__

37.32. `key_column_usage`  
---  
[Prev](infoschema-foreign-tables.html "37.31. foreign_tables")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-parameters.html "37.33. parameters")  
  
* * *

## 37.32. `key_column_usage` #

The view `key_column_usage` identifies all columns in the current database
that are restricted by some unique, primary key, or foreign key constraint.
Check constraints are not included in this view. Only those columns are shown
that the current user has access to, by way of being the owner or having some
privilege.

**Table  37.30. `key_column_usage` Columns**

Column Type Description  
---  
`constraint_catalog` `sql_identifier` Name of the database that contains the
constraint (always the current database)  
`constraint_schema` `sql_identifier` Name of the schema that contains the
constraint  
`constraint_name` `sql_identifier` Name of the constraint  
`table_catalog` `sql_identifier` Name of the database that contains the table
that contains the column that is restricted by this constraint (always the
current database)  
`table_schema` `sql_identifier` Name of the schema that contains the table
that contains the column that is restricted by this constraint  
`table_name` `sql_identifier` Name of the table that contains the column that
is restricted by this constraint  
`column_name` `sql_identifier` Name of the column that is restricted by this
constraint  
`ordinal_position` `cardinal_number` Ordinal position of the column within the
constraint key (count starts at 1)  
`position_in_unique_constraint` `cardinal_number` For a foreign-key
constraint, ordinal position of the referenced column within its unique
constraint (count starts at 1); otherwise null  
  
  

* * *

[Prev](infoschema-foreign-tables.html "37.31. foreign_tables")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-parameters.html "37.33. parameters")  
---|---|---  
37.31. `foreign_tables`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.33. `parameters`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-key-column-
usage.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

