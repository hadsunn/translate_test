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

Supported Versions: [Current](/docs/current/infoschema-foreign-tables.html
"PostgreSQL 17 - 37.31. foreign_tables") ([17](/docs/17/infoschema-foreign-
tables.html "PostgreSQL 17 - 37.31. foreign_tables")) /
[16](/docs/16/infoschema-foreign-tables.html "PostgreSQL 16 -
37.31. foreign_tables") / [15](/docs/15/infoschema-foreign-tables.html
"PostgreSQL 15 - 37.31. foreign_tables") / [14](/docs/14/infoschema-foreign-
tables.html "PostgreSQL 14 - 37.31. foreign_tables") /
[13](/docs/13/infoschema-foreign-tables.html "PostgreSQL 13 -
37.31. foreign_tables")

Development Versions: [18](/docs/18/infoschema-foreign-tables.html "PostgreSQL
18 - 37.31. foreign_tables") / [devel](/docs/devel/infoschema-foreign-
tables.html "PostgreSQL devel - 37.31. foreign_tables")

Unsupported versions: [12](/docs/12/infoschema-foreign-tables.html "PostgreSQL
12 - 37.31. foreign_tables") / [11](/docs/11/infoschema-foreign-tables.html
"PostgreSQL 11 - 37.31. foreign_tables") / [10](/docs/10/infoschema-foreign-
tables.html "PostgreSQL 10 - 37.31. foreign_tables") /
[9.6](/docs/9.6/infoschema-foreign-tables.html "PostgreSQL 9.6 -
37.31. foreign_tables") / [9.5](/docs/9.5/infoschema-foreign-tables.html
"PostgreSQL 9.5 - 37.31. foreign_tables") / [9.4](/docs/9.4/infoschema-
foreign-tables.html "PostgreSQL 9.4 - 37.31. foreign_tables") /
[9.3](/docs/9.3/infoschema-foreign-tables.html "PostgreSQL 9.3 -
37.31. foreign_tables") / [9.2](/docs/9.2/infoschema-foreign-tables.html
"PostgreSQL 9.2 - 37.31. foreign_tables") / [9.1](/docs/9.1/infoschema-
foreign-tables.html "PostgreSQL 9.1 - 37.31. foreign_tables")

__

37.31. `foreign_tables`  
---  
[Prev](infoschema-foreign-table-options.html "37.30. foreign_table_options")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-key-column-usage.html "37.32. key_column_usage")  
  
* * *

## 37.31. `foreign_tables` #

The view `foreign_tables` contains all foreign tables defined in the current
database. Only those foreign tables are shown that the current user has access
to (by way of being the owner or having some privilege).

**Table  37.29. `foreign_tables` Columns**

Column Type Description  
---  
`foreign_table_catalog` `sql_identifier` Name of the database that the foreign
table is defined in (always the current database)  
`foreign_table_schema` `sql_identifier` Name of the schema that contains the
foreign table  
`foreign_table_name` `sql_identifier` Name of the foreign table  
`foreign_server_catalog` `sql_identifier` Name of the database that the
foreign server is defined in (always the current database)  
`foreign_server_name` `sql_identifier` Name of the foreign server  
  
  

* * *

[Prev](infoschema-foreign-table-options.html "37.30. foreign_table_options")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-key-column-usage.html "37.32. key_column_usage")  
---|---|---  
37.30. `foreign_table_options`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.32. `key_column_usage`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-foreign-
tables.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

