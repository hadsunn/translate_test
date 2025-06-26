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

Supported Versions: [Current](/docs/current/infoschema-routine-privileges.html
"PostgreSQL 17 - 37.41. routine_privileges") ([17](/docs/17/infoschema-
routine-privileges.html "PostgreSQL 17 - 37.41. routine_privileges")) /
[16](/docs/16/infoschema-routine-privileges.html "PostgreSQL 16 -
37.41. routine_privileges") / [15](/docs/15/infoschema-routine-privileges.html
"PostgreSQL 15 - 37.41. routine_privileges") / [14](/docs/14/infoschema-
routine-privileges.html "PostgreSQL 14 - 37.41. routine_privileges") /
[13](/docs/13/infoschema-routine-privileges.html "PostgreSQL 13 -
37.41. routine_privileges")

Development Versions: [18](/docs/18/infoschema-routine-privileges.html
"PostgreSQL 18 - 37.41. routine_privileges") / [devel](/docs/devel/infoschema-
routine-privileges.html "PostgreSQL devel - 37.41. routine_privileges")

Unsupported versions: [12](/docs/12/infoschema-routine-privileges.html
"PostgreSQL 12 - 37.41. routine_privileges") / [11](/docs/11/infoschema-
routine-privileges.html "PostgreSQL 11 - 37.41. routine_privileges") /
[10](/docs/10/infoschema-routine-privileges.html "PostgreSQL 10 -
37.41. routine_privileges") / [9.6](/docs/9.6/infoschema-routine-
privileges.html "PostgreSQL 9.6 - 37.41. routine_privileges") /
[9.5](/docs/9.5/infoschema-routine-privileges.html "PostgreSQL 9.5 -
37.41. routine_privileges") / [9.4](/docs/9.4/infoschema-routine-
privileges.html "PostgreSQL 9.4 - 37.41. routine_privileges") /
[9.3](/docs/9.3/infoschema-routine-privileges.html "PostgreSQL 9.3 -
37.41. routine_privileges") / [9.2](/docs/9.2/infoschema-routine-
privileges.html "PostgreSQL 9.2 - 37.41. routine_privileges") /
[9.1](/docs/9.1/infoschema-routine-privileges.html "PostgreSQL 9.1 -
37.41. routine_privileges") / [9.0](/docs/9.0/infoschema-routine-
privileges.html "PostgreSQL 9.0 - 37.41. routine_privileges") /
[8.4](/docs/8.4/infoschema-routine-privileges.html "PostgreSQL 8.4 -
37.41. routine_privileges") / [8.3](/docs/8.3/infoschema-routine-
privileges.html "PostgreSQL 8.3 - 37.41. routine_privileges") /
[8.2](/docs/8.2/infoschema-routine-privileges.html "PostgreSQL 8.2 -
37.41. routine_privileges") / [8.1](/docs/8.1/infoschema-routine-
privileges.html "PostgreSQL 8.1 - 37.41. routine_privileges") /
[8.0](/docs/8.0/infoschema-routine-privileges.html "PostgreSQL 8.0 -
37.41. routine_privileges") / [7.4](/docs/7.4/infoschema-routine-
privileges.html "PostgreSQL 7.4 - 37.41. routine_privileges")

__

37.41. `routine_privileges`  
---  
[Prev](infoschema-routine-column-usage.html "37.40. routine_column_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-routine-routine-usage.html "37.42. routine_routine_usage")  
  
* * *

## 37.41. `routine_privileges` #

The view `routine_privileges` identifies all privileges granted on functions
to a currently enabled role or by a currently enabled role. There is one row
for each combination of function, grantor, and grantee.

**Table  37.39. `routine_privileges` Columns**

Column Type Description  
---  
`grantor` `sql_identifier` Name of the role that granted the privilege  
`grantee` `sql_identifier` Name of the role that the privilege was granted to  
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
`privilege_type` `character_data` Always `EXECUTE` (the only privilege type
for functions)  
`is_grantable` `yes_or_no` `YES` if the privilege is grantable, `NO` if not  
  
  

* * *

[Prev](infoschema-routine-column-usage.html "37.40. routine_column_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-routine-routine-usage.html "37.42. routine_routine_usage")  
---|---|---  
37.40. `routine_column_usage`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.42. `routine_routine_usage`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-routine-
privileges.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

