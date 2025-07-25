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

Supported Versions: [Current](/docs/current/infoschema-constraint-table-
usage.html "PostgreSQL 17 - 37.19. constraint_table_usage")
([17](/docs/17/infoschema-constraint-table-usage.html "PostgreSQL 17 -
37.19. constraint_table_usage")) / [16](/docs/16/infoschema-constraint-table-
usage.html "PostgreSQL 16 - 37.19. constraint_table_usage") /
[15](/docs/15/infoschema-constraint-table-usage.html "PostgreSQL 15 -
37.19. constraint_table_usage") / [14](/docs/14/infoschema-constraint-table-
usage.html "PostgreSQL 14 - 37.19. constraint_table_usage") /
[13](/docs/13/infoschema-constraint-table-usage.html "PostgreSQL 13 -
37.19. constraint_table_usage")

Development Versions: [18](/docs/18/infoschema-constraint-table-usage.html
"PostgreSQL 18 - 37.19. constraint_table_usage") /
[devel](/docs/devel/infoschema-constraint-table-usage.html "PostgreSQL devel -
37.19. constraint_table_usage")

Unsupported versions: [12](/docs/12/infoschema-constraint-table-usage.html
"PostgreSQL 12 - 37.19. constraint_table_usage") / [11](/docs/11/infoschema-
constraint-table-usage.html "PostgreSQL 11 - 37.19. constraint_table_usage") /
[10](/docs/10/infoschema-constraint-table-usage.html "PostgreSQL 10 -
37.19. constraint_table_usage") / [9.6](/docs/9.6/infoschema-constraint-table-
usage.html "PostgreSQL 9.6 - 37.19. constraint_table_usage") /
[9.5](/docs/9.5/infoschema-constraint-table-usage.html "PostgreSQL 9.5 -
37.19. constraint_table_usage") / [9.4](/docs/9.4/infoschema-constraint-table-
usage.html "PostgreSQL 9.4 - 37.19. constraint_table_usage") /
[9.3](/docs/9.3/infoschema-constraint-table-usage.html "PostgreSQL 9.3 -
37.19. constraint_table_usage") / [9.2](/docs/9.2/infoschema-constraint-table-
usage.html "PostgreSQL 9.2 - 37.19. constraint_table_usage") /
[9.1](/docs/9.1/infoschema-constraint-table-usage.html "PostgreSQL 9.1 -
37.19. constraint_table_usage") / [9.0](/docs/9.0/infoschema-constraint-table-
usage.html "PostgreSQL 9.0 - 37.19. constraint_table_usage") /
[8.4](/docs/8.4/infoschema-constraint-table-usage.html "PostgreSQL 8.4 -
37.19. constraint_table_usage") / [8.3](/docs/8.3/infoschema-constraint-table-
usage.html "PostgreSQL 8.3 - 37.19. constraint_table_usage") /
[8.2](/docs/8.2/infoschema-constraint-table-usage.html "PostgreSQL 8.2 -
37.19. constraint_table_usage") / [8.1](/docs/8.1/infoschema-constraint-table-
usage.html "PostgreSQL 8.1 - 37.19. constraint_table_usage") /
[8.0](/docs/8.0/infoschema-constraint-table-usage.html "PostgreSQL 8.0 -
37.19. constraint_table_usage") / [7.4](/docs/7.4/infoschema-constraint-table-
usage.html "PostgreSQL 7.4 - 37.19. constraint_table_usage")

__

37.19. `constraint_table_usage`  
---  
[Prev](infoschema-constraint-column-usage.html "37.18. constraint_column_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-data-type-privileges.html "37.20. data_type_privileges")  
  
* * *

## 37.19. `constraint_table_usage` #

The view `constraint_table_usage` identifies all tables in the current
database that are used by some constraint and are owned by a currently enabled
role. (This is different from the view `table_constraints`, which identifies
all table constraints along with the table they are defined on.) For a foreign
key constraint, this view identifies the table that the foreign key
references. For a unique or primary key constraint, this view simply
identifies the table the constraint belongs to. Check constraints and not-null
constraints are not included in this view.

**Table  37.17. `constraint_table_usage` Columns**

Column Type Description  
---  
`table_catalog` `sql_identifier` Name of the database that contains the table
that is used by some constraint (always the current database)  
`table_schema` `sql_identifier` Name of the schema that contains the table
that is used by some constraint  
`table_name` `sql_identifier` Name of the table that is used by some
constraint  
`constraint_catalog` `sql_identifier` Name of the database that contains the
constraint (always the current database)  
`constraint_schema` `sql_identifier` Name of the schema that contains the
constraint  
`constraint_name` `sql_identifier` Name of the constraint  
  
  

* * *

[Prev](infoschema-constraint-column-usage.html "37.18. constraint_column_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-data-type-privileges.html "37.20. data_type_privileges")  
---|---|---  
37.18. `constraint_column_usage`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.20. `data_type_privileges`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-constraint-table-
usage.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

