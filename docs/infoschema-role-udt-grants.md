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

Supported Versions: [Current](/docs/current/infoschema-role-udt-grants.html
"PostgreSQL 17 - 37.38. role_udt_grants") ([17](/docs/17/infoschema-role-udt-
grants.html "PostgreSQL 17 - 37.38. role_udt_grants")) /
[16](/docs/16/infoschema-role-udt-grants.html "PostgreSQL 16 -
37.38. role_udt_grants") / [15](/docs/15/infoschema-role-udt-grants.html
"PostgreSQL 15 - 37.38. role_udt_grants") / [14](/docs/14/infoschema-role-udt-
grants.html "PostgreSQL 14 - 37.38. role_udt_grants") /
[13](/docs/13/infoschema-role-udt-grants.html "PostgreSQL 13 -
37.38. role_udt_grants")

Development Versions: [18](/docs/18/infoschema-role-udt-grants.html
"PostgreSQL 18 - 37.38. role_udt_grants") / [devel](/docs/devel/infoschema-
role-udt-grants.html "PostgreSQL devel - 37.38. role_udt_grants")

Unsupported versions: [12](/docs/12/infoschema-role-udt-grants.html
"PostgreSQL 12 - 37.38. role_udt_grants") / [11](/docs/11/infoschema-role-udt-
grants.html "PostgreSQL 11 - 37.38. role_udt_grants") /
[10](/docs/10/infoschema-role-udt-grants.html "PostgreSQL 10 -
37.38. role_udt_grants") / [9.6](/docs/9.6/infoschema-role-udt-grants.html
"PostgreSQL 9.6 - 37.38. role_udt_grants") / [9.5](/docs/9.5/infoschema-role-
udt-grants.html "PostgreSQL 9.5 - 37.38. role_udt_grants") /
[9.4](/docs/9.4/infoschema-role-udt-grants.html "PostgreSQL 9.4 -
37.38. role_udt_grants") / [9.3](/docs/9.3/infoschema-role-udt-grants.html
"PostgreSQL 9.3 - 37.38. role_udt_grants") / [9.2](/docs/9.2/infoschema-role-
udt-grants.html "PostgreSQL 9.2 - 37.38. role_udt_grants")

__

37.38. `role_udt_grants`  
---  
[Prev](infoschema-role-table-grants.html "37.37. role_table_grants")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-role-usage-grants.html "37.39. role_usage_grants")  
  
* * *

## 37.38. `role_udt_grants` #

The view `role_udt_grants` is intended to identify `USAGE` privileges granted
on user-defined types where the grantor or grantee is a currently enabled
role. Further information can be found under `udt_privileges`. The only
effective difference between this view and `udt_privileges` is that this view
omits objects that have been made accessible to the current user by way of a
grant to `PUBLIC`. Since data types do not have real privileges in PostgreSQL,
but only an implicit grant to `PUBLIC`, this view is empty.

**Table  37.36. `role_udt_grants` Columns**

Column Type Description  
---  
`grantor` `sql_identifier` The name of the role that granted the privilege  
`grantee` `sql_identifier` The name of the role that the privilege was granted
to  
`udt_catalog` `sql_identifier` Name of the database containing the type
(always the current database)  
`udt_schema` `sql_identifier` Name of the schema containing the type  
`udt_name` `sql_identifier` Name of the type  
`privilege_type` `character_data` Always `TYPE USAGE`  
`is_grantable` `yes_or_no` `YES` if the privilege is grantable, `NO` if not  
  
  

* * *

[Prev](infoschema-role-table-grants.html "37.37. role_table_grants")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-role-usage-grants.html "37.39. role_usage_grants")  
---|---|---  
37.37. `role_table_grants`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.39. `role_usage_grants`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-role-udt-
grants.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

