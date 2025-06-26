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

Supported Versions: [Current](/docs/current/infoschema-usage-privileges.html
"PostgreSQL 17 - 37.59. usage_privileges") ([17](/docs/17/infoschema-usage-
privileges.html "PostgreSQL 17 - 37.59. usage_privileges")) /
[16](/docs/16/infoschema-usage-privileges.html "PostgreSQL 16 -
37.59. usage_privileges") / [15](/docs/15/infoschema-usage-privileges.html
"PostgreSQL 15 - 37.59. usage_privileges") / [14](/docs/14/infoschema-usage-
privileges.html "PostgreSQL 14 - 37.59. usage_privileges") /
[13](/docs/13/infoschema-usage-privileges.html "PostgreSQL 13 -
37.59. usage_privileges")

Development Versions: [18](/docs/18/infoschema-usage-privileges.html
"PostgreSQL 18 - 37.59. usage_privileges") / [devel](/docs/devel/infoschema-
usage-privileges.html "PostgreSQL devel - 37.59. usage_privileges")

Unsupported versions: [12](/docs/12/infoschema-usage-privileges.html
"PostgreSQL 12 - 37.59. usage_privileges") / [11](/docs/11/infoschema-usage-
privileges.html "PostgreSQL 11 - 37.59. usage_privileges") /
[10](/docs/10/infoschema-usage-privileges.html "PostgreSQL 10 -
37.59. usage_privileges") / [9.6](/docs/9.6/infoschema-usage-privileges.html
"PostgreSQL 9.6 - 37.59. usage_privileges") / [9.5](/docs/9.5/infoschema-
usage-privileges.html "PostgreSQL 9.5 - 37.59. usage_privileges") /
[9.4](/docs/9.4/infoschema-usage-privileges.html "PostgreSQL 9.4 -
37.59. usage_privileges") / [9.3](/docs/9.3/infoschema-usage-privileges.html
"PostgreSQL 9.3 - 37.59. usage_privileges") / [9.2](/docs/9.2/infoschema-
usage-privileges.html "PostgreSQL 9.2 - 37.59. usage_privileges") /
[9.1](/docs/9.1/infoschema-usage-privileges.html "PostgreSQL 9.1 -
37.59. usage_privileges") / [9.0](/docs/9.0/infoschema-usage-privileges.html
"PostgreSQL 9.0 - 37.59. usage_privileges") / [8.4](/docs/8.4/infoschema-
usage-privileges.html "PostgreSQL 8.4 - 37.59. usage_privileges") /
[8.3](/docs/8.3/infoschema-usage-privileges.html "PostgreSQL 8.3 -
37.59. usage_privileges") / [8.2](/docs/8.2/infoschema-usage-privileges.html
"PostgreSQL 8.2 - 37.59. usage_privileges") / [8.1](/docs/8.1/infoschema-
usage-privileges.html "PostgreSQL 8.1 - 37.59. usage_privileges") /
[8.0](/docs/8.0/infoschema-usage-privileges.html "PostgreSQL 8.0 -
37.59. usage_privileges") / [7.4](/docs/7.4/infoschema-usage-privileges.html
"PostgreSQL 7.4 - 37.59. usage_privileges")

__

37.59. `usage_privileges`  
---  
[Prev](infoschema-udt-privileges.html "37.58. udt_privileges")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-user-defined-types.html "37.60. user_defined_types")  
  
* * *

## 37.59. `usage_privileges` #

The view `usage_privileges` identifies `USAGE` privileges granted on various
kinds of objects to a currently enabled role or by a currently enabled role.
In PostgreSQL, this currently applies to collations, domains, foreign-data
wrappers, foreign servers, and sequences. There is one row for each
combination of object, grantor, and grantee.

Since collations do not have real privileges in PostgreSQL, this view shows
implicit non-grantable `USAGE` privileges granted by the owner to `PUBLIC` for
all collations. The other object types, however, show real privileges.

In PostgreSQL, sequences also support `SELECT` and `UPDATE` privileges in
addition to the `USAGE` privilege. These are nonstandard and therefore not
visible in the information schema.

**Table  37.57. `usage_privileges` Columns**

Column Type Description  
---  
`grantor` `sql_identifier` Name of the role that granted the privilege  
`grantee` `sql_identifier` Name of the role that the privilege was granted to  
`object_catalog` `sql_identifier` Name of the database containing the object
(always the current database)  
`object_schema` `sql_identifier` Name of the schema containing the object, if
applicable, else an empty string  
`object_name` `sql_identifier` Name of the object  
`object_type` `character_data` `COLLATION` or `DOMAIN` or `FOREIGN DATA
WRAPPER` or `FOREIGN SERVER` or `SEQUENCE`  
`privilege_type` `character_data` Always `USAGE`  
`is_grantable` `yes_or_no` `YES` if the privilege is grantable, `NO` if not  
  
  

* * *

[Prev](infoschema-udt-privileges.html "37.58. udt_privileges")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-user-defined-types.html "37.60. user_defined_types")  
---|---|---  
37.58. `udt_privileges`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.60. `user_defined_types`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-usage-
privileges.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

