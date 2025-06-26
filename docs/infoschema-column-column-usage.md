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

Supported Versions: [Current](/docs/current/infoschema-column-column-
usage.html "PostgreSQL 17 - 37.12. column_column_usage")
([17](/docs/17/infoschema-column-column-usage.html "PostgreSQL 17 -
37.12. column_column_usage")) / [16](/docs/16/infoschema-column-column-
usage.html "PostgreSQL 16 - 37.12. column_column_usage") /
[15](/docs/15/infoschema-column-column-usage.html "PostgreSQL 15 -
37.12. column_column_usage") / [14](/docs/14/infoschema-column-column-
usage.html "PostgreSQL 14 - 37.12. column_column_usage") /
[13](/docs/13/infoschema-column-column-usage.html "PostgreSQL 13 -
37.12. column_column_usage")

Development Versions: [18](/docs/18/infoschema-column-column-usage.html
"PostgreSQL 18 - 37.12. column_column_usage") /
[devel](/docs/devel/infoschema-column-column-usage.html "PostgreSQL devel -
37.12. column_column_usage")

Unsupported versions: [12](/docs/12/infoschema-column-column-usage.html
"PostgreSQL 12 - 37.12. column_column_usage")

__

37.12. `column_column_usage`  
---  
[Prev](infoschema-collation-character-set-applicab.html "37.11. collation_character_set_​applicability")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-column-domain-usage.html "37.13. column_domain_usage")  
  
* * *

## 37.12. `column_column_usage` #

The view `column_column_usage` identifies all generated columns that depend on
another base column in the same table. Only tables owned by a currently
enabled role are included.

**Table  37.10. `column_column_usage` Columns**

Column Type Description  
---  
`table_catalog` `sql_identifier` Name of the database containing the table
(always the current database)  
`table_schema` `sql_identifier` Name of the schema containing the table  
`table_name` `sql_identifier` Name of the table  
`column_name` `sql_identifier` Name of the base column that a generated column
depends on  
`dependent_column` `sql_identifier` Name of the generated column  
  
  

* * *

[Prev](infoschema-collation-character-set-applicab.html "37.11. collation_character_set_​applicability")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-column-domain-usage.html "37.13. column_domain_usage")  
---|---|---  
37.11. `collation_character_set_​applicability`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.13. `column_domain_usage`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-column-column-
usage.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

