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

Supported Versions: [Current](/docs/current/infoschema-foreign-table-
options.html "PostgreSQL 17 - 37.30. foreign_table_options")
([17](/docs/17/infoschema-foreign-table-options.html "PostgreSQL 17 -
37.30. foreign_table_options")) / [16](/docs/16/infoschema-foreign-table-
options.html "PostgreSQL 16 - 37.30. foreign_table_options") /
[15](/docs/15/infoschema-foreign-table-options.html "PostgreSQL 15 -
37.30. foreign_table_options") / [14](/docs/14/infoschema-foreign-table-
options.html "PostgreSQL 14 - 37.30. foreign_table_options") /
[13](/docs/13/infoschema-foreign-table-options.html "PostgreSQL 13 -
37.30. foreign_table_options")

Development Versions: [18](/docs/18/infoschema-foreign-table-options.html
"PostgreSQL 18 - 37.30. foreign_table_options") /
[devel](/docs/devel/infoschema-foreign-table-options.html "PostgreSQL devel -
37.30. foreign_table_options")

Unsupported versions: [12](/docs/12/infoschema-foreign-table-options.html
"PostgreSQL 12 - 37.30. foreign_table_options") / [11](/docs/11/infoschema-
foreign-table-options.html "PostgreSQL 11 - 37.30. foreign_table_options") /
[10](/docs/10/infoschema-foreign-table-options.html "PostgreSQL 10 -
37.30. foreign_table_options") / [9.6](/docs/9.6/infoschema-foreign-table-
options.html "PostgreSQL 9.6 - 37.30. foreign_table_options") /
[9.5](/docs/9.5/infoschema-foreign-table-options.html "PostgreSQL 9.5 -
37.30. foreign_table_options") / [9.4](/docs/9.4/infoschema-foreign-table-
options.html "PostgreSQL 9.4 - 37.30. foreign_table_options") /
[9.3](/docs/9.3/infoschema-foreign-table-options.html "PostgreSQL 9.3 -
37.30. foreign_table_options") / [9.2](/docs/9.2/infoschema-foreign-table-
options.html "PostgreSQL 9.2 - 37.30. foreign_table_options") /
[9.1](/docs/9.1/infoschema-foreign-table-options.html "PostgreSQL 9.1 -
37.30. foreign_table_options")

__

37.30. `foreign_table_options`  
---  
[Prev](infoschema-foreign-servers.html "37.29. foreign_servers")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-foreign-tables.html "37.31. foreign_tables")  
  
* * *

## 37.30. `foreign_table_options` #

The view `foreign_table_options` contains all the options defined for foreign
tables in the current database. Only those foreign tables are shown that the
current user has access to (by way of being the owner or having some
privilege).

**Table  37.28. `foreign_table_options` Columns**

Column Type Description  
---  
`foreign_table_catalog` `sql_identifier` Name of the database that contains
the foreign table (always the current database)  
`foreign_table_schema` `sql_identifier` Name of the schema that contains the
foreign table  
`foreign_table_name` `sql_identifier` Name of the foreign table  
`option_name` `sql_identifier` Name of an option  
`option_value` `character_data` Value of the option  
  
  

* * *

[Prev](infoschema-foreign-servers.html "37.29. foreign_servers")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-foreign-tables.html "37.31. foreign_tables")  
---|---|---  
37.29. `foreign_servers`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.31. `foreign_tables`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-foreign-table-
options.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

