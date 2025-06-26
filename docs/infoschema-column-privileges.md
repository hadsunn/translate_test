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

Supported Versions: [Current](/docs/current/infoschema-column-privileges.html
"PostgreSQL 17 - 37.15. column_privileges") ([17](/docs/17/infoschema-column-
privileges.html "PostgreSQL 17 - 37.15. column_privileges")) /
[16](/docs/16/infoschema-column-privileges.html "PostgreSQL 16 -
37.15. column_privileges") / [15](/docs/15/infoschema-column-privileges.html
"PostgreSQL 15 - 37.15. column_privileges") / [14](/docs/14/infoschema-column-
privileges.html "PostgreSQL 14 - 37.15. column_privileges") /
[13](/docs/13/infoschema-column-privileges.html "PostgreSQL 13 -
37.15. column_privileges")

Development Versions: [18](/docs/18/infoschema-column-privileges.html
"PostgreSQL 18 - 37.15. column_privileges") / [devel](/docs/devel/infoschema-
column-privileges.html "PostgreSQL devel - 37.15. column_privileges")

Unsupported versions: [12](/docs/12/infoschema-column-privileges.html
"PostgreSQL 12 - 37.15. column_privileges") / [11](/docs/11/infoschema-column-
privileges.html "PostgreSQL 11 - 37.15. column_privileges") /
[10](/docs/10/infoschema-column-privileges.html "PostgreSQL 10 -
37.15. column_privileges") / [9.6](/docs/9.6/infoschema-column-privileges.html
"PostgreSQL 9.6 - 37.15. column_privileges") / [9.5](/docs/9.5/infoschema-
column-privileges.html "PostgreSQL 9.5 - 37.15. column_privileges") /
[9.4](/docs/9.4/infoschema-column-privileges.html "PostgreSQL 9.4 -
37.15. column_privileges") / [9.3](/docs/9.3/infoschema-column-privileges.html
"PostgreSQL 9.3 - 37.15. column_privileges") / [9.2](/docs/9.2/infoschema-
column-privileges.html "PostgreSQL 9.2 - 37.15. column_privileges") /
[9.1](/docs/9.1/infoschema-column-privileges.html "PostgreSQL 9.1 -
37.15. column_privileges") / [9.0](/docs/9.0/infoschema-column-privileges.html
"PostgreSQL 9.0 - 37.15. column_privileges") / [8.4](/docs/8.4/infoschema-
column-privileges.html "PostgreSQL 8.4 - 37.15. column_privileges") /
[8.3](/docs/8.3/infoschema-column-privileges.html "PostgreSQL 8.3 -
37.15. column_privileges") / [8.2](/docs/8.2/infoschema-column-privileges.html
"PostgreSQL 8.2 - 37.15. column_privileges") / [8.1](/docs/8.1/infoschema-
column-privileges.html "PostgreSQL 8.1 - 37.15. column_privileges") /
[8.0](/docs/8.0/infoschema-column-privileges.html "PostgreSQL 8.0 -
37.15. column_privileges") / [7.4](/docs/7.4/infoschema-column-privileges.html
"PostgreSQL 7.4 - 37.15. column_privileges")

__

37.15. `column_privileges`  
---  
[Prev](infoschema-column-options.html "37.14. column_options")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-column-udt-usage.html "37.16. column_udt_usage")  
  
* * *

## 37.15. `column_privileges` #

The view `column_privileges` identifies all privileges granted on columns to a
currently enabled role or by a currently enabled role. There is one row for
each combination of column, grantor, and grantee.

If a privilege has been granted on an entire table, it will show up in this
view as a grant for each column, but only for the privilege types where column
granularity is possible: `SELECT`, `INSERT`, `UPDATE`, `REFERENCES`.

**Table  37.13. `column_privileges` Columns**

Column Type Description  
---  
`grantor` `sql_identifier` Name of the role that granted the privilege  
`grantee` `sql_identifier` Name of the role that the privilege was granted to  
`table_catalog` `sql_identifier` Name of the database that contains the table
that contains the column (always the current database)  
`table_schema` `sql_identifier` Name of the schema that contains the table
that contains the column  
`table_name` `sql_identifier` Name of the table that contains the column  
`column_name` `sql_identifier` Name of the column  
`privilege_type` `character_data` Type of the privilege: `SELECT`, `INSERT`,
`UPDATE`, or `REFERENCES`  
`is_grantable` `yes_or_no` `YES` if the privilege is grantable, `NO` if not  
  
  

* * *

[Prev](infoschema-column-options.html "37.14. column_options")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-column-udt-usage.html "37.16. column_udt_usage")  
---|---|---  
37.14. `column_options`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.16. `column_udt_usage`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-column-
privileges.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

