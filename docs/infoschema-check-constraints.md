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

Supported Versions: [Current](/docs/current/infoschema-check-constraints.html
"PostgreSQL 17 - 37.9. check_constraints") ([17](/docs/17/infoschema-check-
constraints.html "PostgreSQL 17 - 37.9. check_constraints")) /
[16](/docs/16/infoschema-check-constraints.html "PostgreSQL 16 -
37.9. check_constraints") / [15](/docs/15/infoschema-check-constraints.html
"PostgreSQL 15 - 37.9. check_constraints") / [14](/docs/14/infoschema-check-
constraints.html "PostgreSQL 14 - 37.9. check_constraints") /
[13](/docs/13/infoschema-check-constraints.html "PostgreSQL 13 -
37.9. check_constraints")

Development Versions: [18](/docs/18/infoschema-check-constraints.html
"PostgreSQL 18 - 37.9. check_constraints") / [devel](/docs/devel/infoschema-
check-constraints.html "PostgreSQL devel - 37.9. check_constraints")

Unsupported versions: [12](/docs/12/infoschema-check-constraints.html
"PostgreSQL 12 - 37.9. check_constraints") / [11](/docs/11/infoschema-check-
constraints.html "PostgreSQL 11 - 37.9. check_constraints") /
[10](/docs/10/infoschema-check-constraints.html "PostgreSQL 10 -
37.9. check_constraints") / [9.6](/docs/9.6/infoschema-check-constraints.html
"PostgreSQL 9.6 - 37.9. check_constraints") / [9.5](/docs/9.5/infoschema-
check-constraints.html "PostgreSQL 9.5 - 37.9. check_constraints") /
[9.4](/docs/9.4/infoschema-check-constraints.html "PostgreSQL 9.4 -
37.9. check_constraints") / [9.3](/docs/9.3/infoschema-check-constraints.html
"PostgreSQL 9.3 - 37.9. check_constraints") / [9.2](/docs/9.2/infoschema-
check-constraints.html "PostgreSQL 9.2 - 37.9. check_constraints") /
[9.1](/docs/9.1/infoschema-check-constraints.html "PostgreSQL 9.1 -
37.9. check_constraints") / [9.0](/docs/9.0/infoschema-check-constraints.html
"PostgreSQL 9.0 - 37.9. check_constraints") / [8.4](/docs/8.4/infoschema-
check-constraints.html "PostgreSQL 8.4 - 37.9. check_constraints") /
[8.3](/docs/8.3/infoschema-check-constraints.html "PostgreSQL 8.3 -
37.9. check_constraints") / [8.2](/docs/8.2/infoschema-check-constraints.html
"PostgreSQL 8.2 - 37.9. check_constraints") / [8.1](/docs/8.1/infoschema-
check-constraints.html "PostgreSQL 8.1 - 37.9. check_constraints") /
[8.0](/docs/8.0/infoschema-check-constraints.html "PostgreSQL 8.0 -
37.9. check_constraints") / [7.4](/docs/7.4/infoschema-check-constraints.html
"PostgreSQL 7.4 - 37.9. check_constraints")

__

37.9. `check_constraints`  
---  
[Prev](infoschema-check-constraint-routine-usage.html "37.8. check_constraint_routine_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-collations.html "37.10. collations")  
  
* * *

## 37.9. `check_constraints` #

The view `check_constraints` contains all check constraints, either defined on
a table or on a domain, that are owned by a currently enabled role. (The owner
of the table or domain is the owner of the constraint.)

**Table  37.7. `check_constraints` Columns**

Column Type Description  
---  
`constraint_catalog` `sql_identifier` Name of the database containing the
constraint (always the current database)  
`constraint_schema` `sql_identifier` Name of the schema containing the
constraint  
`constraint_name` `sql_identifier` Name of the constraint  
`check_clause` `character_data` The check expression of the check constraint  
  
  

* * *

[Prev](infoschema-check-constraint-routine-usage.html "37.8. check_constraint_routine_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-collations.html "37.10. collations")  
---|---|---  
37.8. `check_constraint_routine_usage`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.10. `collations`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-check-
constraints.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

