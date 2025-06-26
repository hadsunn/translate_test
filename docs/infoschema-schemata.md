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

Supported Versions: [Current](/docs/current/infoschema-schemata.html
"PostgreSQL 17 - 37.46. schemata") ([17](/docs/17/infoschema-schemata.html
"PostgreSQL 17 - 37.46. schemata")) / [16](/docs/16/infoschema-schemata.html
"PostgreSQL 16 - 37.46. schemata") / [15](/docs/15/infoschema-schemata.html
"PostgreSQL 15 - 37.46. schemata") / [14](/docs/14/infoschema-schemata.html
"PostgreSQL 14 - 37.46. schemata") / [13](/docs/13/infoschema-schemata.html
"PostgreSQL 13 - 37.46. schemata")

Development Versions: [18](/docs/18/infoschema-schemata.html "PostgreSQL 18 -
37.46. schemata") / [devel](/docs/devel/infoschema-schemata.html "PostgreSQL
devel - 37.46. schemata")

Unsupported versions: [12](/docs/12/infoschema-schemata.html "PostgreSQL 12 -
37.46. schemata") / [11](/docs/11/infoschema-schemata.html "PostgreSQL 11 -
37.46. schemata") / [10](/docs/10/infoschema-schemata.html "PostgreSQL 10 -
37.46. schemata") / [9.6](/docs/9.6/infoschema-schemata.html "PostgreSQL 9.6 -
37.46. schemata") / [9.5](/docs/9.5/infoschema-schemata.html "PostgreSQL 9.5 -
37.46. schemata") / [9.4](/docs/9.4/infoschema-schemata.html "PostgreSQL 9.4 -
37.46. schemata") / [9.3](/docs/9.3/infoschema-schemata.html "PostgreSQL 9.3 -
37.46. schemata") / [9.2](/docs/9.2/infoschema-schemata.html "PostgreSQL 9.2 -
37.46. schemata") / [9.1](/docs/9.1/infoschema-schemata.html "PostgreSQL 9.1 -
37.46. schemata") / [9.0](/docs/9.0/infoschema-schemata.html "PostgreSQL 9.0 -
37.46. schemata") / [8.4](/docs/8.4/infoschema-schemata.html "PostgreSQL 8.4 -
37.46. schemata") / [8.3](/docs/8.3/infoschema-schemata.html "PostgreSQL 8.3 -
37.46. schemata") / [8.2](/docs/8.2/infoschema-schemata.html "PostgreSQL 8.2 -
37.46. schemata") / [8.1](/docs/8.1/infoschema-schemata.html "PostgreSQL 8.1 -
37.46. schemata") / [8.0](/docs/8.0/infoschema-schemata.html "PostgreSQL 8.0 -
37.46. schemata") / [7.4](/docs/7.4/infoschema-schemata.html "PostgreSQL 7.4 -
37.46. schemata")

__

37.46. `schemata`  
---  
[Prev](infoschema-routines.html "37.45. routines")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-sequences.html "37.47. sequences")  
  
* * *

## 37.46. `schemata` #

The view `schemata` contains all schemas in the current database that the
current user has access to (by way of being the owner or having some
privilege).

**Table  37.44. `schemata` Columns**

Column Type Description  
---  
`catalog_name` `sql_identifier` Name of the database that the schema is
contained in (always the current database)  
`schema_name` `sql_identifier` Name of the schema  
`schema_owner` `sql_identifier` Name of the owner of the schema  
`default_character_set_catalog` `sql_identifier` Applies to a feature not
available in PostgreSQL  
`default_character_set_schema` `sql_identifier` Applies to a feature not
available in PostgreSQL  
`default_character_set_name` `sql_identifier` Applies to a feature not
available in PostgreSQL  
`sql_path` `character_data` Applies to a feature not available in PostgreSQL  
  
  

* * *

[Prev](infoschema-routines.html "37.45. routines")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-sequences.html "37.47. sequences")  
---|---|---  
37.45. `routines`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.47. `sequences`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-schemata.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

