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

Supported Versions: [Current](/docs/current/infoschema-triggered-update-
columns.html "PostgreSQL 17 - 37.56. triggered_update_columns")
([17](/docs/17/infoschema-triggered-update-columns.html "PostgreSQL 17 -
37.56. triggered_update_columns")) / [16](/docs/16/infoschema-triggered-
update-columns.html "PostgreSQL 16 - 37.56. triggered_update_columns") /
[15](/docs/15/infoschema-triggered-update-columns.html "PostgreSQL 15 -
37.56. triggered_update_columns") / [14](/docs/14/infoschema-triggered-update-
columns.html "PostgreSQL 14 - 37.56. triggered_update_columns") /
[13](/docs/13/infoschema-triggered-update-columns.html "PostgreSQL 13 -
37.56. triggered_update_columns")

Development Versions: [18](/docs/18/infoschema-triggered-update-columns.html
"PostgreSQL 18 - 37.56. triggered_update_columns") /
[devel](/docs/devel/infoschema-triggered-update-columns.html "PostgreSQL devel
- 37.56. triggered_update_columns")

Unsupported versions: [12](/docs/12/infoschema-triggered-update-columns.html
"PostgreSQL 12 - 37.56. triggered_update_columns") / [11](/docs/11/infoschema-
triggered-update-columns.html "PostgreSQL 11 -
37.56. triggered_update_columns") / [10](/docs/10/infoschema-triggered-update-
columns.html "PostgreSQL 10 - 37.56. triggered_update_columns") /
[9.6](/docs/9.6/infoschema-triggered-update-columns.html "PostgreSQL 9.6 -
37.56. triggered_update_columns") / [9.5](/docs/9.5/infoschema-triggered-
update-columns.html "PostgreSQL 9.5 - 37.56. triggered_update_columns") /
[9.4](/docs/9.4/infoschema-triggered-update-columns.html "PostgreSQL 9.4 -
37.56. triggered_update_columns") / [9.3](/docs/9.3/infoschema-triggered-
update-columns.html "PostgreSQL 9.3 - 37.56. triggered_update_columns") /
[9.2](/docs/9.2/infoschema-triggered-update-columns.html "PostgreSQL 9.2 -
37.56. triggered_update_columns") / [9.1](/docs/9.1/infoschema-triggered-
update-columns.html "PostgreSQL 9.1 - 37.56. triggered_update_columns") /
[9.0](/docs/9.0/infoschema-triggered-update-columns.html "PostgreSQL 9.0 -
37.56. triggered_update_columns")

__

37.56. `triggered_update_columns`  
---  
[Prev](infoschema-transforms.html "37.55. transforms")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-triggers.html "37.57. triggers")  
  
* * *

## 37.56. `triggered_update_columns` #

For triggers in the current database that specify a column list (like `UPDATE
OF column1, column2`), the view `triggered_update_columns` identifies these
columns. Triggers that do not specify a column list are not included in this
view. Only those columns are shown that the current user owns or has some
privilege other than `SELECT` on.

**Table  37.54. `triggered_update_columns` Columns**

Column Type Description  
---  
`trigger_catalog` `sql_identifier` Name of the database that contains the
trigger (always the current database)  
`trigger_schema` `sql_identifier` Name of the schema that contains the trigger  
`trigger_name` `sql_identifier` Name of the trigger  
`event_object_catalog` `sql_identifier` Name of the database that contains the
table that the trigger is defined on (always the current database)  
`event_object_schema` `sql_identifier` Name of the schema that contains the
table that the trigger is defined on  
`event_object_table` `sql_identifier` Name of the table that the trigger is
defined on  
`event_object_column` `sql_identifier` Name of the column that the trigger is
defined on  
  
  

* * *

[Prev](infoschema-transforms.html "37.55. transforms")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-triggers.html "37.57. triggers")  
---|---|---  
37.55. `transforms`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.57. `triggers`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-triggered-update-
columns.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

