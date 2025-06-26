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

Supported Versions: [Current](/docs/current/infoschema-routine-sequence-
usage.html "PostgreSQL 17 - 37.43. routine_sequence_usage")
([17](/docs/17/infoschema-routine-sequence-usage.html "PostgreSQL 17 -
37.43. routine_sequence_usage")) / [16](/docs/16/infoschema-routine-sequence-
usage.html "PostgreSQL 16 - 37.43. routine_sequence_usage") /
[15](/docs/15/infoschema-routine-sequence-usage.html "PostgreSQL 15 -
37.43. routine_sequence_usage") / [14](/docs/14/infoschema-routine-sequence-
usage.html "PostgreSQL 14 - 37.43. routine_sequence_usage")

Development Versions: [18](/docs/18/infoschema-routine-sequence-usage.html
"PostgreSQL 18 - 37.43. routine_sequence_usage") /
[devel](/docs/devel/infoschema-routine-sequence-usage.html "PostgreSQL devel -
37.43. routine_sequence_usage")

__

37.43. `routine_sequence_usage`  
---  
[Prev](infoschema-routine-routine-usage.html "37.42. routine_routine_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-routine-table-usage.html "37.44. routine_table_usage")  
  
* * *

## 37.43. `routine_sequence_usage` #

The view `routine_sequence_usage` identifies all sequences that are used by a
function or procedure, either in the SQL body or in parameter default
expressions. (This only works for unquoted SQL bodies, not quoted bodies or
functions in other languages.) A sequence is only included if that sequence is
owned by a currently enabled role.

**Table  37.41. `routine_sequence_usage` Columns**

Column Type Description  
---  
`specific_catalog` `sql_identifier` Name of the database containing the
function (always the current database)  
`specific_schema` `sql_identifier` Name of the schema containing the function  
`specific_name` `sql_identifier` The “specific name” of the function. See
[Section 37.45](infoschema-routines.html "37.45. routines") for more
information.  
`routine_catalog` `sql_identifier` Name of the database containing the
function (always the current database)  
`routine_schema` `sql_identifier` Name of the schema containing the function  
`routine_name` `sql_identifier` Name of the function (might be duplicated in
case of overloading)  
`schema_catalog` `sql_identifier` Name of the database that contains the
sequence that is used by the function (always the current database)  
`sequence_schema` `sql_identifier` Name of the schema that contains the
sequence that is used by the function  
`sequence_name` `sql_identifier` Name of the sequence that is used by the
function  
  
  

* * *

[Prev](infoschema-routine-routine-usage.html "37.42. routine_routine_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-routine-table-usage.html "37.44. routine_table_usage")  
---|---|---  
37.42. `routine_routine_usage`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.44. `routine_table_usage`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-routine-sequence-
usage.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

