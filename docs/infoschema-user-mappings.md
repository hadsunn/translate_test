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

Supported Versions: [Current](/docs/current/infoschema-user-mappings.html
"PostgreSQL 17 - 37.62. user_mappings") ([17](/docs/17/infoschema-user-
mappings.html "PostgreSQL 17 - 37.62. user_mappings")) /
[16](/docs/16/infoschema-user-mappings.html "PostgreSQL 16 -
37.62. user_mappings") / [15](/docs/15/infoschema-user-mappings.html
"PostgreSQL 15 - 37.62. user_mappings") / [14](/docs/14/infoschema-user-
mappings.html "PostgreSQL 14 - 37.62. user_mappings") /
[13](/docs/13/infoschema-user-mappings.html "PostgreSQL 13 -
37.62. user_mappings")

Development Versions: [18](/docs/18/infoschema-user-mappings.html "PostgreSQL
18 - 37.62. user_mappings") / [devel](/docs/devel/infoschema-user-
mappings.html "PostgreSQL devel - 37.62. user_mappings")

Unsupported versions: [12](/docs/12/infoschema-user-mappings.html "PostgreSQL
12 - 37.62. user_mappings") / [11](/docs/11/infoschema-user-mappings.html
"PostgreSQL 11 - 37.62. user_mappings") / [10](/docs/10/infoschema-user-
mappings.html "PostgreSQL 10 - 37.62. user_mappings") /
[9.6](/docs/9.6/infoschema-user-mappings.html "PostgreSQL 9.6 -
37.62. user_mappings") / [9.5](/docs/9.5/infoschema-user-mappings.html
"PostgreSQL 9.5 - 37.62. user_mappings") / [9.4](/docs/9.4/infoschema-user-
mappings.html "PostgreSQL 9.4 - 37.62. user_mappings") /
[9.3](/docs/9.3/infoschema-user-mappings.html "PostgreSQL 9.3 -
37.62. user_mappings") / [9.2](/docs/9.2/infoschema-user-mappings.html
"PostgreSQL 9.2 - 37.62. user_mappings") / [9.1](/docs/9.1/infoschema-user-
mappings.html "PostgreSQL 9.1 - 37.62. user_mappings") /
[9.0](/docs/9.0/infoschema-user-mappings.html "PostgreSQL 9.0 -
37.62. user_mappings") / [8.4](/docs/8.4/infoschema-user-mappings.html
"PostgreSQL 8.4 - 37.62. user_mappings")

__

37.62. `user_mappings`  
---  
[Prev](infoschema-user-mapping-options.html "37.61. user_mapping_options")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-view-column-usage.html "37.63. view_column_usage")  
  
* * *

## 37.62. `user_mappings` #

The view `user_mappings` contains all user mappings defined in the current
database. Only those user mappings are shown where the current user has access
to the corresponding foreign server (by way of being the owner or having some
privilege).

**Table  37.60. `user_mappings` Columns**

Column Type Description  
---  
`authorization_identifier` `sql_identifier` Name of the user being mapped, or
`PUBLIC` if the mapping is public  
`foreign_server_catalog` `sql_identifier` Name of the database that the
foreign server used by this mapping is defined in (always the current
database)  
`foreign_server_name` `sql_identifier` Name of the foreign server used by this
mapping  
  
  

* * *

[Prev](infoschema-user-mapping-options.html "37.61. user_mapping_options")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-view-column-usage.html "37.63. view_column_usage")  
---|---|---  
37.61. `user_mapping_options`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.63. `view_column_usage`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-user-
mappings.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

