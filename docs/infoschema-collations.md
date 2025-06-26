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

Supported Versions: [Current](/docs/current/infoschema-collations.html
"PostgreSQL 17 - 37.10. collations") ([17](/docs/17/infoschema-collations.html
"PostgreSQL 17 - 37.10. collations")) / [16](/docs/16/infoschema-
collations.html "PostgreSQL 16 - 37.10. collations") /
[15](/docs/15/infoschema-collations.html "PostgreSQL 15 - 37.10. collations")
/ [14](/docs/14/infoschema-collations.html "PostgreSQL 14 -
37.10. collations") / [13](/docs/13/infoschema-collations.html "PostgreSQL 13
- 37.10. collations")

Development Versions: [18](/docs/18/infoschema-collations.html "PostgreSQL 18
- 37.10. collations") / [devel](/docs/devel/infoschema-collations.html
"PostgreSQL devel - 37.10. collations")

Unsupported versions: [12](/docs/12/infoschema-collations.html "PostgreSQL 12
- 37.10. collations") / [11](/docs/11/infoschema-collations.html "PostgreSQL
11 - 37.10. collations") / [10](/docs/10/infoschema-collations.html
"PostgreSQL 10 - 37.10. collations") / [9.6](/docs/9.6/infoschema-
collations.html "PostgreSQL 9.6 - 37.10. collations") /
[9.5](/docs/9.5/infoschema-collations.html "PostgreSQL 9.5 -
37.10. collations") / [9.4](/docs/9.4/infoschema-collations.html "PostgreSQL
9.4 - 37.10. collations") / [9.3](/docs/9.3/infoschema-collations.html
"PostgreSQL 9.3 - 37.10. collations") / [9.2](/docs/9.2/infoschema-
collations.html "PostgreSQL 9.2 - 37.10. collations") /
[9.1](/docs/9.1/infoschema-collations.html "PostgreSQL 9.1 -
37.10. collations")

__

37.10. `collations`  
---  
[Prev](infoschema-check-constraints.html "37.9. check_constraints")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-collation-character-set-applicab.html "37.11. collation_character_set_​applicability")  
  
* * *

## 37.10. `collations` #

The view `collations` contains the collations available in the current
database.

**Table  37.8. `collations` Columns**

Column Type Description  
---  
`collation_catalog` `sql_identifier` Name of the database containing the
collation (always the current database)  
`collation_schema` `sql_identifier` Name of the schema containing the
collation  
`collation_name` `sql_identifier` Name of the default collation  
`pad_attribute` `character_data` Always `NO PAD` (The alternative `PAD SPACE`
is not supported by PostgreSQL.)  
  
  

* * *

[Prev](infoschema-check-constraints.html "37.9. check_constraints")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-collation-character-set-applicab.html "37.11. collation_character_set_​applicability")  
---|---|---  
37.9. `check_constraints`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.11. `collation_character_set_​applicability`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-collations.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

