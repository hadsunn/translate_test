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

Supported Versions: [Current](/docs/current/infoschema-check-constraint-
routine-usage.html "PostgreSQL 17 - 37.8. check_constraint_routine_usage")
([17](/docs/17/infoschema-check-constraint-routine-usage.html "PostgreSQL 17 -
37.8. check_constraint_routine_usage")) / [16](/docs/16/infoschema-check-
constraint-routine-usage.html "PostgreSQL 16 -
37.8. check_constraint_routine_usage") / [15](/docs/15/infoschema-check-
constraint-routine-usage.html "PostgreSQL 15 -
37.8. check_constraint_routine_usage") / [14](/docs/14/infoschema-check-
constraint-routine-usage.html "PostgreSQL 14 -
37.8. check_constraint_routine_usage") / [13](/docs/13/infoschema-check-
constraint-routine-usage.html "PostgreSQL 13 -
37.8. check_constraint_routine_usage")

Development Versions: [18](/docs/18/infoschema-check-constraint-routine-
usage.html "PostgreSQL 18 - 37.8. check_constraint_routine_usage") /
[devel](/docs/devel/infoschema-check-constraint-routine-usage.html "PostgreSQL
devel - 37.8. check_constraint_routine_usage")

Unsupported versions: [12](/docs/12/infoschema-check-constraint-routine-
usage.html "PostgreSQL 12 - 37.8. check_constraint_routine_usage") /
[11](/docs/11/infoschema-check-constraint-routine-usage.html "PostgreSQL 11 -
37.8. check_constraint_routine_usage") / [10](/docs/10/infoschema-check-
constraint-routine-usage.html "PostgreSQL 10 -
37.8. check_constraint_routine_usage") / [9.6](/docs/9.6/infoschema-check-
constraint-routine-usage.html "PostgreSQL 9.6 -
37.8. check_constraint_routine_usage") / [9.5](/docs/9.5/infoschema-check-
constraint-routine-usage.html "PostgreSQL 9.5 -
37.8. check_constraint_routine_usage") / [9.4](/docs/9.4/infoschema-check-
constraint-routine-usage.html "PostgreSQL 9.4 -
37.8. check_constraint_routine_usage") / [9.3](/docs/9.3/infoschema-check-
constraint-routine-usage.html "PostgreSQL 9.3 -
37.8. check_constraint_routine_usage") / [9.2](/docs/9.2/infoschema-check-
constraint-routine-usage.html "PostgreSQL 9.2 -
37.8. check_constraint_routine_usage") / [9.1](/docs/9.1/infoschema-check-
constraint-routine-usage.html "PostgreSQL 9.1 -
37.8. check_constraint_routine_usage") / [9.0](/docs/9.0/infoschema-check-
constraint-routine-usage.html "PostgreSQL 9.0 -
37.8. check_constraint_routine_usage") / [8.4](/docs/8.4/infoschema-check-
constraint-routine-usage.html "PostgreSQL 8.4 -
37.8. check_constraint_routine_usage") / [8.3](/docs/8.3/infoschema-check-
constraint-routine-usage.html "PostgreSQL 8.3 -
37.8. check_constraint_routine_usage") / [8.2](/docs/8.2/infoschema-check-
constraint-routine-usage.html "PostgreSQL 8.2 -
37.8. check_constraint_routine_usage")

__

37.8. `check_constraint_routine_usage`  
---  
[Prev](infoschema-character-sets.html "37.7. character_sets")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-check-constraints.html "37.9. check_constraints")  
  
* * *

## 37.8. `check_constraint_routine_usage` #

The view `check_constraint_routine_usage` identifies routines (functions and
procedures) that are used by a check constraint. Only those routines are shown
that are owned by a currently enabled role.

**Table  37.6. `check_constraint_routine_usage` Columns**

Column Type Description  
---  
`constraint_catalog` `sql_identifier` Name of the database containing the
constraint (always the current database)  
`constraint_schema` `sql_identifier` Name of the schema containing the
constraint  
`constraint_name` `sql_identifier` Name of the constraint  
`specific_catalog` `sql_identifier` Name of the database containing the
function (always the current database)  
`specific_schema` `sql_identifier` Name of the schema containing the function  
`specific_name` `sql_identifier` The “specific name” of the function. See
[Section 37.45](infoschema-routines.html "37.45. routines") for more
information.  
  
  

* * *

[Prev](infoschema-character-sets.html "37.7. character_sets")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-check-constraints.html "37.9. check_constraints")  
---|---|---  
37.7. `character_sets`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.9. `check_constraints`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-check-constraint-
routine-usage.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

