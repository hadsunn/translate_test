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

Supported Versions: [Current](/docs/current/infoschema-views.html "PostgreSQL
17 - 37.66. views") ([17](/docs/17/infoschema-views.html "PostgreSQL 17 -
37.66. views")) / [16](/docs/16/infoschema-views.html "PostgreSQL 16 -
37.66. views") / [15](/docs/15/infoschema-views.html "PostgreSQL 15 -
37.66. views") / [14](/docs/14/infoschema-views.html "PostgreSQL 14 -
37.66. views") / [13](/docs/13/infoschema-views.html "PostgreSQL 13 -
37.66. views")

Development Versions: [18](/docs/18/infoschema-views.html "PostgreSQL 18 -
37.66. views") / [devel](/docs/devel/infoschema-views.html "PostgreSQL devel -
37.66. views")

Unsupported versions: [12](/docs/12/infoschema-views.html "PostgreSQL 12 -
37.66. views") / [11](/docs/11/infoschema-views.html "PostgreSQL 11 -
37.66. views") / [10](/docs/10/infoschema-views.html "PostgreSQL 10 -
37.66. views") / [9.6](/docs/9.6/infoschema-views.html "PostgreSQL 9.6 -
37.66. views") / [9.5](/docs/9.5/infoschema-views.html "PostgreSQL 9.5 -
37.66. views") / [9.4](/docs/9.4/infoschema-views.html "PostgreSQL 9.4 -
37.66. views") / [9.3](/docs/9.3/infoschema-views.html "PostgreSQL 9.3 -
37.66. views") / [9.2](/docs/9.2/infoschema-views.html "PostgreSQL 9.2 -
37.66. views") / [9.1](/docs/9.1/infoschema-views.html "PostgreSQL 9.1 -
37.66. views") / [9.0](/docs/9.0/infoschema-views.html "PostgreSQL 9.0 -
37.66. views") / [8.4](/docs/8.4/infoschema-views.html "PostgreSQL 8.4 -
37.66. views") / [8.3](/docs/8.3/infoschema-views.html "PostgreSQL 8.3 -
37.66. views") / [8.2](/docs/8.2/infoschema-views.html "PostgreSQL 8.2 -
37.66. views") / [8.1](/docs/8.1/infoschema-views.html "PostgreSQL 8.1 -
37.66. views") / [8.0](/docs/8.0/infoschema-views.html "PostgreSQL 8.0 -
37.66. views") / [7.4](/docs/7.4/infoschema-views.html "PostgreSQL 7.4 -
37.66. views")

__

37.66. `views`  
---  
[Prev](infoschema-view-table-usage.html "37.65. view_table_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](server-programming.html "Part V. Server Programming")  
  
* * *

## 37.66. `views` #

The view `views` contains all views defined in the current database. Only
those views are shown that the current user has access to (by way of being the
owner or having some privilege).

**Table  37.64. `views` Columns**

Column Type Description  
---  
`table_catalog` `sql_identifier` Name of the database that contains the view
(always the current database)  
`table_schema` `sql_identifier` Name of the schema that contains the view  
`table_name` `sql_identifier` Name of the view  
`view_definition` `character_data` Query expression defining the view (null if
the view is not owned by a currently enabled role)  
`check_option` `character_data` `CASCADED` or `LOCAL` if the view has a `CHECK
OPTION` defined on it, `NONE` if not  
`is_updatable` `yes_or_no` `YES` if the view is updatable (allows `UPDATE` and
`DELETE`), `NO` if not  
`is_insertable_into` `yes_or_no` `YES` if the view is insertable into (allows
`INSERT`), `NO` if not  
`is_trigger_updatable` `yes_or_no` `YES` if the view has an `INSTEAD OF`
`UPDATE` trigger defined on it, `NO` if not  
`is_trigger_deletable` `yes_or_no` `YES` if the view has an `INSTEAD OF`
`DELETE` trigger defined on it, `NO` if not  
`is_trigger_insertable_into` `yes_or_no` `YES` if the view has an `INSTEAD OF`
`INSERT` trigger defined on it, `NO` if not  
  
  

* * *

[Prev](infoschema-view-table-usage.html "37.65. view_table_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](server-programming.html "Part V. Server Programming")  
---|---|---  
37.65. `view_table_usage`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Part V. Server Programming  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-views.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

