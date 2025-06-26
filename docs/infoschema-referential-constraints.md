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

Supported Versions: [Current](/docs/current/infoschema-referential-
constraints.html "PostgreSQL 17 - 37.34. referential_constraints")
([17](/docs/17/infoschema-referential-constraints.html "PostgreSQL 17 -
37.34. referential_constraints")) / [16](/docs/16/infoschema-referential-
constraints.html "PostgreSQL 16 - 37.34. referential_constraints") /
[15](/docs/15/infoschema-referential-constraints.html "PostgreSQL 15 -
37.34. referential_constraints") / [14](/docs/14/infoschema-referential-
constraints.html "PostgreSQL 14 - 37.34. referential_constraints") /
[13](/docs/13/infoschema-referential-constraints.html "PostgreSQL 13 -
37.34. referential_constraints")

Development Versions: [18](/docs/18/infoschema-referential-constraints.html
"PostgreSQL 18 - 37.34. referential_constraints") /
[devel](/docs/devel/infoschema-referential-constraints.html "PostgreSQL devel
- 37.34. referential_constraints")

Unsupported versions: [12](/docs/12/infoschema-referential-constraints.html
"PostgreSQL 12 - 37.34. referential_constraints") / [11](/docs/11/infoschema-
referential-constraints.html "PostgreSQL 11 - 37.34. referential_constraints")
/ [10](/docs/10/infoschema-referential-constraints.html "PostgreSQL 10 -
37.34. referential_constraints") / [9.6](/docs/9.6/infoschema-referential-
constraints.html "PostgreSQL 9.6 - 37.34. referential_constraints") /
[9.5](/docs/9.5/infoschema-referential-constraints.html "PostgreSQL 9.5 -
37.34. referential_constraints") / [9.4](/docs/9.4/infoschema-referential-
constraints.html "PostgreSQL 9.4 - 37.34. referential_constraints") /
[9.3](/docs/9.3/infoschema-referential-constraints.html "PostgreSQL 9.3 -
37.34. referential_constraints") / [9.2](/docs/9.2/infoschema-referential-
constraints.html "PostgreSQL 9.2 - 37.34. referential_constraints") /
[9.1](/docs/9.1/infoschema-referential-constraints.html "PostgreSQL 9.1 -
37.34. referential_constraints") / [9.0](/docs/9.0/infoschema-referential-
constraints.html "PostgreSQL 9.0 - 37.34. referential_constraints") /
[8.4](/docs/8.4/infoschema-referential-constraints.html "PostgreSQL 8.4 -
37.34. referential_constraints") / [8.3](/docs/8.3/infoschema-referential-
constraints.html "PostgreSQL 8.3 - 37.34. referential_constraints") /
[8.2](/docs/8.2/infoschema-referential-constraints.html "PostgreSQL 8.2 -
37.34. referential_constraints") / [8.1](/docs/8.1/infoschema-referential-
constraints.html "PostgreSQL 8.1 - 37.34. referential_constraints") /
[8.0](/docs/8.0/infoschema-referential-constraints.html "PostgreSQL 8.0 -
37.34. referential_constraints") / [7.4](/docs/7.4/infoschema-referential-
constraints.html "PostgreSQL 7.4 - 37.34. referential_constraints")

__

37.34. `referential_constraints`  
---  
[Prev](infoschema-parameters.html "37.33. parameters")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-role-column-grants.html "37.35. role_column_grants")  
  
* * *

## 37.34. `referential_constraints` #

The view `referential_constraints` contains all referential (foreign key)
constraints in the current database. Only those constraints are shown for
which the current user has write access to the referencing table (by way of
being the owner or having some privilege other than `SELECT`).

**Table  37.32. `referential_constraints` Columns**

Column Type Description  
---  
`constraint_catalog` `sql_identifier` Name of the database containing the
constraint (always the current database)  
`constraint_schema` `sql_identifier` Name of the schema containing the
constraint  
`constraint_name` `sql_identifier` Name of the constraint  
`unique_constraint_catalog` `sql_identifier` Name of the database that
contains the unique or primary key constraint that the foreign key constraint
references (always the current database)  
`unique_constraint_schema` `sql_identifier` Name of the schema that contains
the unique or primary key constraint that the foreign key constraint
references  
`unique_constraint_name` `sql_identifier` Name of the unique or primary key
constraint that the foreign key constraint references  
`match_option` `character_data` Match option of the foreign key constraint:
`FULL`, `PARTIAL`, or `NONE`.  
`update_rule` `character_data` Update rule of the foreign key constraint:
`CASCADE`, `SET NULL`, `SET DEFAULT`, `RESTRICT`, or `NO ACTION`.  
`delete_rule` `character_data` Delete rule of the foreign key constraint:
`CASCADE`, `SET NULL`, `SET DEFAULT`, `RESTRICT`, or `NO ACTION`.  
  
  

* * *

[Prev](infoschema-parameters.html "37.33. parameters")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-role-column-grants.html "37.35. role_column_grants")  
---|---|---  
37.33. `parameters`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.35. `role_column_grants`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-referential-
constraints.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

