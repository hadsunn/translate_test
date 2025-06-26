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

Supported Versions: [Current](/docs/current/infoschema-triggers.html
"PostgreSQL 17 - 37.57. triggers") ([17](/docs/17/infoschema-triggers.html
"PostgreSQL 17 - 37.57. triggers")) / [16](/docs/16/infoschema-triggers.html
"PostgreSQL 16 - 37.57. triggers") / [15](/docs/15/infoschema-triggers.html
"PostgreSQL 15 - 37.57. triggers") / [14](/docs/14/infoschema-triggers.html
"PostgreSQL 14 - 37.57. triggers") / [13](/docs/13/infoschema-triggers.html
"PostgreSQL 13 - 37.57. triggers")

Development Versions: [18](/docs/18/infoschema-triggers.html "PostgreSQL 18 -
37.57. triggers") / [devel](/docs/devel/infoschema-triggers.html "PostgreSQL
devel - 37.57. triggers")

Unsupported versions: [12](/docs/12/infoschema-triggers.html "PostgreSQL 12 -
37.57. triggers") / [11](/docs/11/infoschema-triggers.html "PostgreSQL 11 -
37.57. triggers") / [10](/docs/10/infoschema-triggers.html "PostgreSQL 10 -
37.57. triggers") / [9.6](/docs/9.6/infoschema-triggers.html "PostgreSQL 9.6 -
37.57. triggers") / [9.5](/docs/9.5/infoschema-triggers.html "PostgreSQL 9.5 -
37.57. triggers") / [9.4](/docs/9.4/infoschema-triggers.html "PostgreSQL 9.4 -
37.57. triggers") / [9.3](/docs/9.3/infoschema-triggers.html "PostgreSQL 9.3 -
37.57. triggers") / [9.2](/docs/9.2/infoschema-triggers.html "PostgreSQL 9.2 -
37.57. triggers") / [9.1](/docs/9.1/infoschema-triggers.html "PostgreSQL 9.1 -
37.57. triggers") / [9.0](/docs/9.0/infoschema-triggers.html "PostgreSQL 9.0 -
37.57. triggers") / [8.4](/docs/8.4/infoschema-triggers.html "PostgreSQL 8.4 -
37.57. triggers") / [8.3](/docs/8.3/infoschema-triggers.html "PostgreSQL 8.3 -
37.57. triggers") / [8.2](/docs/8.2/infoschema-triggers.html "PostgreSQL 8.2 -
37.57. triggers") / [8.1](/docs/8.1/infoschema-triggers.html "PostgreSQL 8.1 -
37.57. triggers") / [8.0](/docs/8.0/infoschema-triggers.html "PostgreSQL 8.0 -
37.57. triggers") / [7.4](/docs/7.4/infoschema-triggers.html "PostgreSQL 7.4 -
37.57. triggers")

__

37.57. `triggers`  
---  
[Prev](infoschema-triggered-update-columns.html "37.56. triggered_update_columns")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-udt-privileges.html "37.58. udt_privileges")  
  
* * *

## 37.57. `triggers` #

The view `triggers` contains all triggers defined in the current database on
tables and views that the current user owns or has some privilege other than
`SELECT` on.

**Table  37.55. `triggers` Columns**

Column Type Description  
---  
`trigger_catalog` `sql_identifier` Name of the database that contains the
trigger (always the current database)  
`trigger_schema` `sql_identifier` Name of the schema that contains the trigger  
`trigger_name` `sql_identifier` Name of the trigger  
`event_manipulation` `character_data` Event that fires the trigger (`INSERT`,
`UPDATE`, or `DELETE`)  
`event_object_catalog` `sql_identifier` Name of the database that contains the
table that the trigger is defined on (always the current database)  
`event_object_schema` `sql_identifier` Name of the schema that contains the
table that the trigger is defined on  
`event_object_table` `sql_identifier` Name of the table that the trigger is
defined on  
`action_order` `cardinal_number` Firing order among triggers on the same table
having the same `event_manipulation`, `action_timing`, and
`action_orientation`. In PostgreSQL, triggers are fired in name order, so this
column reflects that.  
`action_condition` `character_data` `WHEN` condition of the trigger, null if
none (also null if the table is not owned by a currently enabled role)  
`action_statement` `character_data` Statement that is executed by the trigger
(currently always `EXECUTE FUNCTION _`function`_(...)`)  
`action_orientation` `character_data` Identifies whether the trigger fires
once for each processed row or once for each statement (`ROW` or `STATEMENT`)  
`action_timing` `character_data` Time at which the trigger fires (`BEFORE`,
`AFTER`, or `INSTEAD OF`)  
`action_reference_old_table` `sql_identifier` Name of the “old” transition
table, or null if none  
`action_reference_new_table` `sql_identifier` Name of the “new” transition
table, or null if none  
`action_reference_old_row` `sql_identifier` Applies to a feature not available
in PostgreSQL  
`action_reference_new_row` `sql_identifier` Applies to a feature not available
in PostgreSQL  
`created` `time_stamp` Applies to a feature not available in PostgreSQL  
  
  

Triggers in PostgreSQL have two incompatibilities with the SQL standard that
affect the representation in the information schema. First, trigger names are
local to each table in PostgreSQL, rather than being independent schema
objects. Therefore there can be duplicate trigger names defined in one schema,
so long as they belong to different tables. (`trigger_catalog` and
`trigger_schema` are really the values pertaining to the table that the
trigger is defined on.) Second, triggers can be defined to fire on multiple
events in PostgreSQL (e.g., `ON INSERT OR UPDATE`), whereas the SQL standard
only allows one. If a trigger is defined to fire on multiple events, it is
represented as multiple rows in the information schema, one for each type of
event. As a consequence of these two issues, the primary key of the view
`triggers` is really `(trigger_catalog, trigger_schema, event_object_table,
trigger_name, event_manipulation)` instead of `(trigger_catalog,
trigger_schema, trigger_name)`, which is what the SQL standard specifies.
Nonetheless, if you define your triggers in a manner that conforms with the
SQL standard (trigger names unique in the schema and only one event type per
trigger), this will not affect you.

### Note

Prior to PostgreSQL 9.1, this view's columns `action_timing`,
`action_reference_old_table`, `action_reference_new_table`,
`action_reference_old_row`, and `action_reference_new_row` were named
`condition_timing`, `condition_reference_old_table`,
`condition_reference_new_table`, `condition_reference_old_row`, and
`condition_reference_new_row` respectively. That was how they were named in
the SQL:1999 standard. The new naming conforms to SQL:2003 and later.

* * *

[Prev](infoschema-triggered-update-columns.html "37.56. triggered_update_columns")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-udt-privileges.html "37.58. udt_privileges")  
---|---|---  
37.56. `triggered_update_columns`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.58. `udt_privileges`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-triggers.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

