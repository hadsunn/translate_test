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

Supported Versions: [Current](/docs/current/infoschema-foreign-data-
wrappers.html "PostgreSQL 17 - 37.27. foreign_data_wrappers")
([17](/docs/17/infoschema-foreign-data-wrappers.html "PostgreSQL 17 -
37.27. foreign_data_wrappers")) / [16](/docs/16/infoschema-foreign-data-
wrappers.html "PostgreSQL 16 - 37.27. foreign_data_wrappers") /
[15](/docs/15/infoschema-foreign-data-wrappers.html "PostgreSQL 15 -
37.27. foreign_data_wrappers") / [14](/docs/14/infoschema-foreign-data-
wrappers.html "PostgreSQL 14 - 37.27. foreign_data_wrappers") /
[13](/docs/13/infoschema-foreign-data-wrappers.html "PostgreSQL 13 -
37.27. foreign_data_wrappers")

Development Versions: [18](/docs/18/infoschema-foreign-data-wrappers.html
"PostgreSQL 18 - 37.27. foreign_data_wrappers") /
[devel](/docs/devel/infoschema-foreign-data-wrappers.html "PostgreSQL devel -
37.27. foreign_data_wrappers")

Unsupported versions: [12](/docs/12/infoschema-foreign-data-wrappers.html
"PostgreSQL 12 - 37.27. foreign_data_wrappers") / [11](/docs/11/infoschema-
foreign-data-wrappers.html "PostgreSQL 11 - 37.27. foreign_data_wrappers") /
[10](/docs/10/infoschema-foreign-data-wrappers.html "PostgreSQL 10 -
37.27. foreign_data_wrappers") / [9.6](/docs/9.6/infoschema-foreign-data-
wrappers.html "PostgreSQL 9.6 - 37.27. foreign_data_wrappers") /
[9.5](/docs/9.5/infoschema-foreign-data-wrappers.html "PostgreSQL 9.5 -
37.27. foreign_data_wrappers") / [9.4](/docs/9.4/infoschema-foreign-data-
wrappers.html "PostgreSQL 9.4 - 37.27. foreign_data_wrappers") /
[9.3](/docs/9.3/infoschema-foreign-data-wrappers.html "PostgreSQL 9.3 -
37.27. foreign_data_wrappers") / [9.2](/docs/9.2/infoschema-foreign-data-
wrappers.html "PostgreSQL 9.2 - 37.27. foreign_data_wrappers") /
[9.1](/docs/9.1/infoschema-foreign-data-wrappers.html "PostgreSQL 9.1 -
37.27. foreign_data_wrappers") / [9.0](/docs/9.0/infoschema-foreign-data-
wrappers.html "PostgreSQL 9.0 - 37.27. foreign_data_wrappers") /
[8.4](/docs/8.4/infoschema-foreign-data-wrappers.html "PostgreSQL 8.4 -
37.27. foreign_data_wrappers")

__

37.27. `foreign_data_wrappers`  
---  
[Prev](infoschema-foreign-data-wrapper-options.html "37.26. foreign_data_wrapper_options")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-foreign-server-options.html "37.28. foreign_server_options")  
  
* * *

## 37.27. `foreign_data_wrappers` #

The view `foreign_data_wrappers` contains all foreign-data wrappers defined in
the current database. Only those foreign-data wrappers are shown that the
current user has access to (by way of being the owner or having some
privilege).

**Table  37.25. `foreign_data_wrappers` Columns**

Column Type Description  
---  
`foreign_data_wrapper_catalog` `sql_identifier` Name of the database that
contains the foreign-data wrapper (always the current database)  
`foreign_data_wrapper_name` `sql_identifier` Name of the foreign-data wrapper  
`authorization_identifier` `sql_identifier` Name of the owner of the foreign
server  
`library_name` `character_data` File name of the library that implementing
this foreign-data wrapper  
`foreign_data_wrapper_language` `character_data` Language used to implement
this foreign-data wrapper  
  
  

* * *

[Prev](infoschema-foreign-data-wrapper-options.html "37.26. foreign_data_wrapper_options")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-foreign-server-options.html "37.28. foreign_server_options")  
---|---|---  
37.26. `foreign_data_wrapper_options`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.28. `foreign_server_options`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-foreign-data-
wrappers.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

