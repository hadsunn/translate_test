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

Supported Versions: [Current](/docs/current/infoschema-column-options.html
"PostgreSQL 17 - 37.14. column_options") ([17](/docs/17/infoschema-column-
options.html "PostgreSQL 17 - 37.14. column_options")) /
[16](/docs/16/infoschema-column-options.html "PostgreSQL 16 -
37.14. column_options") / [15](/docs/15/infoschema-column-options.html
"PostgreSQL 15 - 37.14. column_options") / [14](/docs/14/infoschema-column-
options.html "PostgreSQL 14 - 37.14. column_options") /
[13](/docs/13/infoschema-column-options.html "PostgreSQL 13 -
37.14. column_options")

Development Versions: [18](/docs/18/infoschema-column-options.html "PostgreSQL
18 - 37.14. column_options") / [devel](/docs/devel/infoschema-column-
options.html "PostgreSQL devel - 37.14. column_options")

Unsupported versions: [12](/docs/12/infoschema-column-options.html "PostgreSQL
12 - 37.14. column_options") / [11](/docs/11/infoschema-column-options.html
"PostgreSQL 11 - 37.14. column_options") / [10](/docs/10/infoschema-column-
options.html "PostgreSQL 10 - 37.14. column_options") /
[9.6](/docs/9.6/infoschema-column-options.html "PostgreSQL 9.6 -
37.14. column_options") / [9.5](/docs/9.5/infoschema-column-options.html
"PostgreSQL 9.5 - 37.14. column_options") / [9.4](/docs/9.4/infoschema-column-
options.html "PostgreSQL 9.4 - 37.14. column_options") /
[9.3](/docs/9.3/infoschema-column-options.html "PostgreSQL 9.3 -
37.14. column_options") / [9.2](/docs/9.2/infoschema-column-options.html
"PostgreSQL 9.2 - 37.14. column_options")

__

37.14. `column_options`  
---  
[Prev](infoschema-column-domain-usage.html "37.13. column_domain_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-column-privileges.html "37.15. column_privileges")  
  
* * *

## 37.14. `column_options` #

The view `column_options` contains all the options defined for foreign table
columns in the current database. Only those foreign table columns are shown
that the current user has access to (by way of being the owner or having some
privilege).

**Table  37.12. `column_options` Columns**

Column Type Description  
---  
`table_catalog` `sql_identifier` Name of the database that contains the
foreign table (always the current database)  
`table_schema` `sql_identifier` Name of the schema that contains the foreign
table  
`table_name` `sql_identifier` Name of the foreign table  
`column_name` `sql_identifier` Name of the column  
`option_name` `sql_identifier` Name of an option  
`option_value` `character_data` Value of the option  
  
  

* * *

[Prev](infoschema-column-domain-usage.html "37.13. column_domain_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-column-privileges.html "37.15. column_privileges")  
---|---|---  
37.13. `column_domain_usage`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.15. `column_privileges`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-column-
options.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

