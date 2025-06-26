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

Supported Versions: [Current](/docs/current/infoschema-collation-character-
set-applicab.html "PostgreSQL 17 -
37.11. collation_character_set_​applicability") ([17](/docs/17/infoschema-
collation-character-set-applicab.html "PostgreSQL 17 -
37.11. collation_character_set_​applicability")) / [16](/docs/16/infoschema-
collation-character-set-applicab.html "PostgreSQL 16 -
37.11. collation_character_set_​applicability") / [15](/docs/15/infoschema-
collation-character-set-applicab.html "PostgreSQL 15 -
37.11. collation_character_set_​applicability") / [14](/docs/14/infoschema-
collation-character-set-applicab.html "PostgreSQL 14 -
37.11. collation_character_set_​applicability") / [13](/docs/13/infoschema-
collation-character-set-applicab.html "PostgreSQL 13 -
37.11. collation_character_set_​applicability")

Development Versions: [18](/docs/18/infoschema-collation-character-set-
applicab.html "PostgreSQL 18 - 37.11. collation_character_set_​applicability")
/ [devel](/docs/devel/infoschema-collation-character-set-applicab.html
"PostgreSQL devel - 37.11. collation_character_set_​applicability")

Unsupported versions: [12](/docs/12/infoschema-collation-character-set-
applicab.html "PostgreSQL 12 - 37.11. collation_character_set_​applicability")
/ [11](/docs/11/infoschema-collation-character-set-applicab.html "PostgreSQL
11 - 37.11. collation_character_set_​applicability") /
[10](/docs/10/infoschema-collation-character-set-applicab.html "PostgreSQL 10
- 37.11. collation_character_set_​applicability") /
[9.6](/docs/9.6/infoschema-collation-character-set-applicab.html "PostgreSQL
9.6 - 37.11. collation_character_set_​applicability") /
[9.5](/docs/9.5/infoschema-collation-character-set-applicab.html "PostgreSQL
9.5 - 37.11. collation_character_set_​applicability") /
[9.4](/docs/9.4/infoschema-collation-character-set-applicab.html "PostgreSQL
9.4 - 37.11. collation_character_set_​applicability") /
[9.3](/docs/9.3/infoschema-collation-character-set-applicab.html "PostgreSQL
9.3 - 37.11. collation_character_set_​applicability") /
[9.2](/docs/9.2/infoschema-collation-character-set-applicab.html "PostgreSQL
9.2 - 37.11. collation_character_set_​applicability") /
[9.1](/docs/9.1/infoschema-collation-character-set-applicab.html "PostgreSQL
9.1 - 37.11. collation_character_set_​applicability")

__

37.11. `collation_character_set_​applicability`  
---  
[Prev](infoschema-collations.html "37.10. collations")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-column-column-usage.html "37.12. column_column_usage")  
  
* * *

## 37.11. `collation_character_set_​applicability` #

The view `collation_character_set_applicability` identifies which character
set the available collations are applicable to. In PostgreSQL, there is only
one character set per database (see explanation in [Section 37.7](infoschema-
character-sets.html "37.7. character_sets")), so this view does not provide
much useful information.

**Table  37.9. `collation_character_set_applicability` Columns**

Column Type Description  
---  
`collation_catalog` `sql_identifier` Name of the database containing the
collation (always the current database)  
`collation_schema` `sql_identifier` Name of the schema containing the
collation  
`collation_name` `sql_identifier` Name of the default collation  
`character_set_catalog` `sql_identifier` Character sets are currently not
implemented as schema objects, so this column is null  
`character_set_schema` `sql_identifier` Character sets are currently not
implemented as schema objects, so this column is null  
`character_set_name` `sql_identifier` Name of the character set  
  
  

* * *

[Prev](infoschema-collations.html "37.10. collations")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-column-column-usage.html "37.12. column_column_usage")  
---|---|---  
37.10. `collations`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.12. `column_column_usage`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-collation-
character-set-applicab.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

