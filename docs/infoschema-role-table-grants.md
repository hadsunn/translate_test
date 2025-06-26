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

Supported Versions: [Current](/docs/current/infoschema-role-table-grants.html
"PostgreSQL 17 - 37.37. role_table_grants") ([17](/docs/17/infoschema-role-
table-grants.html "PostgreSQL 17 - 37.37. role_table_grants")) /
[16](/docs/16/infoschema-role-table-grants.html "PostgreSQL 16 -
37.37. role_table_grants") / [15](/docs/15/infoschema-role-table-grants.html
"PostgreSQL 15 - 37.37. role_table_grants") / [14](/docs/14/infoschema-role-
table-grants.html "PostgreSQL 14 - 37.37. role_table_grants") /
[13](/docs/13/infoschema-role-table-grants.html "PostgreSQL 13 -
37.37. role_table_grants")

Development Versions: [18](/docs/18/infoschema-role-table-grants.html
"PostgreSQL 18 - 37.37. role_table_grants") / [devel](/docs/devel/infoschema-
role-table-grants.html "PostgreSQL devel - 37.37. role_table_grants")

Unsupported versions: [12](/docs/12/infoschema-role-table-grants.html
"PostgreSQL 12 - 37.37. role_table_grants") / [11](/docs/11/infoschema-role-
table-grants.html "PostgreSQL 11 - 37.37. role_table_grants") /
[10](/docs/10/infoschema-role-table-grants.html "PostgreSQL 10 -
37.37. role_table_grants") / [9.6](/docs/9.6/infoschema-role-table-grants.html
"PostgreSQL 9.6 - 37.37. role_table_grants") / [9.5](/docs/9.5/infoschema-
role-table-grants.html "PostgreSQL 9.5 - 37.37. role_table_grants") /
[9.4](/docs/9.4/infoschema-role-table-grants.html "PostgreSQL 9.4 -
37.37. role_table_grants") / [9.3](/docs/9.3/infoschema-role-table-grants.html
"PostgreSQL 9.3 - 37.37. role_table_grants") / [9.2](/docs/9.2/infoschema-
role-table-grants.html "PostgreSQL 9.2 - 37.37. role_table_grants") /
[9.1](/docs/9.1/infoschema-role-table-grants.html "PostgreSQL 9.1 -
37.37. role_table_grants") / [9.0](/docs/9.0/infoschema-role-table-grants.html
"PostgreSQL 9.0 - 37.37. role_table_grants") / [8.4](/docs/8.4/infoschema-
role-table-grants.html "PostgreSQL 8.4 - 37.37. role_table_grants") /
[8.3](/docs/8.3/infoschema-role-table-grants.html "PostgreSQL 8.3 -
37.37. role_table_grants") / [8.2](/docs/8.2/infoschema-role-table-grants.html
"PostgreSQL 8.2 - 37.37. role_table_grants") / [8.1](/docs/8.1/infoschema-
role-table-grants.html "PostgreSQL 8.1 - 37.37. role_table_grants") /
[8.0](/docs/8.0/infoschema-role-table-grants.html "PostgreSQL 8.0 -
37.37. role_table_grants") / [7.4](/docs/7.4/infoschema-role-table-grants.html
"PostgreSQL 7.4 - 37.37. role_table_grants")

__

37.37. `role_table_grants`  
---  
[Prev](infoschema-role-routine-grants.html "37.36. role_routine_grants")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-role-udt-grants.html "37.38. role_udt_grants")  
  
* * *

## 37.37. `role_table_grants` #

The view `role_table_grants` identifies all privileges granted on tables or
views where the grantor or grantee is a currently enabled role. Further
information can be found under `table_privileges`. The only effective
difference between this view and `table_privileges` is that this view omits
tables that have been made accessible to the current user by way of a grant to
`PUBLIC`.

**Table  37.35. `role_table_grants` Columns**

Column Type Description  
---  
`grantor` `sql_identifier` Name of the role that granted the privilege  
`grantee` `sql_identifier` Name of the role that the privilege was granted to  
`table_catalog` `sql_identifier` Name of the database that contains the table
(always the current database)  
`table_schema` `sql_identifier` Name of the schema that contains the table  
`table_name` `sql_identifier` Name of the table  
`privilege_type` `character_data` Type of the privilege: `SELECT`, `INSERT`,
`UPDATE`, `DELETE`, `TRUNCATE`, `REFERENCES`, or `TRIGGER`  
`is_grantable` `yes_or_no` `YES` if the privilege is grantable, `NO` if not  
`with_hierarchy` `yes_or_no` In the SQL standard, `WITH HIERARCHY OPTION` is a
separate (sub-)privilege allowing certain operations on table inheritance
hierarchies. In PostgreSQL, this is included in the `SELECT` privilege, so
this column shows `YES` if the privilege is `SELECT`, else `NO`.  
  
  

* * *

[Prev](infoschema-role-routine-grants.html "37.36. role_routine_grants")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-role-udt-grants.html "37.38. role_udt_grants")  
---|---|---  
37.36. `role_routine_grants`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.38. `role_udt_grants`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-role-table-
grants.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

