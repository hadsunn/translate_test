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

Supported Versions: [Current](/docs/current/infoschema-udt-privileges.html
"PostgreSQL 17 - 37.58. udt_privileges") ([17](/docs/17/infoschema-udt-
privileges.html "PostgreSQL 17 - 37.58. udt_privileges")) /
[16](/docs/16/infoschema-udt-privileges.html "PostgreSQL 16 -
37.58. udt_privileges") / [15](/docs/15/infoschema-udt-privileges.html
"PostgreSQL 15 - 37.58. udt_privileges") / [14](/docs/14/infoschema-udt-
privileges.html "PostgreSQL 14 - 37.58. udt_privileges") /
[13](/docs/13/infoschema-udt-privileges.html "PostgreSQL 13 -
37.58. udt_privileges")

Development Versions: [18](/docs/18/infoschema-udt-privileges.html "PostgreSQL
18 - 37.58. udt_privileges") / [devel](/docs/devel/infoschema-udt-
privileges.html "PostgreSQL devel - 37.58. udt_privileges")

Unsupported versions: [12](/docs/12/infoschema-udt-privileges.html "PostgreSQL
12 - 37.58. udt_privileges") / [11](/docs/11/infoschema-udt-privileges.html
"PostgreSQL 11 - 37.58. udt_privileges") / [10](/docs/10/infoschema-udt-
privileges.html "PostgreSQL 10 - 37.58. udt_privileges") /
[9.6](/docs/9.6/infoschema-udt-privileges.html "PostgreSQL 9.6 -
37.58. udt_privileges") / [9.5](/docs/9.5/infoschema-udt-privileges.html
"PostgreSQL 9.5 - 37.58. udt_privileges") / [9.4](/docs/9.4/infoschema-udt-
privileges.html "PostgreSQL 9.4 - 37.58. udt_privileges") /
[9.3](/docs/9.3/infoschema-udt-privileges.html "PostgreSQL 9.3 -
37.58. udt_privileges") / [9.2](/docs/9.2/infoschema-udt-privileges.html
"PostgreSQL 9.2 - 37.58. udt_privileges")

__

37.58. `udt_privileges`  
---  
[Prev](infoschema-triggers.html "37.57. triggers")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-usage-privileges.html "37.59. usage_privileges")  
  
* * *

## 37.58. `udt_privileges` #

The view `udt_privileges` identifies `USAGE` privileges granted on user-
defined types to a currently enabled role or by a currently enabled role.
There is one row for each combination of type, grantor, and grantee. This view
shows only composite types (see under [Section 37.60](infoschema-user-defined-
types.html "37.60. user_defined_types") for why); see [Section
37.59](infoschema-usage-privileges.html "37.59. usage_privileges") for domain
privileges.

**Table  37.56. `udt_privileges` Columns**

Column Type Description  
---  
`grantor` `sql_identifier` Name of the role that granted the privilege  
`grantee` `sql_identifier` Name of the role that the privilege was granted to  
`udt_catalog` `sql_identifier` Name of the database containing the type
(always the current database)  
`udt_schema` `sql_identifier` Name of the schema containing the type  
`udt_name` `sql_identifier` Name of the type  
`privilege_type` `character_data` Always `TYPE USAGE`  
`is_grantable` `yes_or_no` `YES` if the privilege is grantable, `NO` if not  
  
  

* * *

[Prev](infoschema-triggers.html "37.57. triggers")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-usage-privileges.html "37.59. usage_privileges")  
---|---|---  
37.57. `triggers`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.59. `usage_privileges`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-udt-
privileges.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

