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

Supported Versions: [Current](/docs/current/infoschema-foreign-data-wrapper-
options.html "PostgreSQL 17 - 37.26. foreign_data_wrapper_options")
([17](/docs/17/infoschema-foreign-data-wrapper-options.html "PostgreSQL 17 -
37.26. foreign_data_wrapper_options")) / [16](/docs/16/infoschema-foreign-
data-wrapper-options.html "PostgreSQL 16 -
37.26. foreign_data_wrapper_options") / [15](/docs/15/infoschema-foreign-data-
wrapper-options.html "PostgreSQL 15 - 37.26. foreign_data_wrapper_options") /
[14](/docs/14/infoschema-foreign-data-wrapper-options.html "PostgreSQL 14 -
37.26. foreign_data_wrapper_options") / [13](/docs/13/infoschema-foreign-data-
wrapper-options.html "PostgreSQL 13 - 37.26. foreign_data_wrapper_options")

Development Versions: [18](/docs/18/infoschema-foreign-data-wrapper-
options.html "PostgreSQL 18 - 37.26. foreign_data_wrapper_options") /
[devel](/docs/devel/infoschema-foreign-data-wrapper-options.html "PostgreSQL
devel - 37.26. foreign_data_wrapper_options")

Unsupported versions: [12](/docs/12/infoschema-foreign-data-wrapper-
options.html "PostgreSQL 12 - 37.26. foreign_data_wrapper_options") /
[11](/docs/11/infoschema-foreign-data-wrapper-options.html "PostgreSQL 11 -
37.26. foreign_data_wrapper_options") / [10](/docs/10/infoschema-foreign-data-
wrapper-options.html "PostgreSQL 10 - 37.26. foreign_data_wrapper_options") /
[9.6](/docs/9.6/infoschema-foreign-data-wrapper-options.html "PostgreSQL 9.6 -
37.26. foreign_data_wrapper_options") / [9.5](/docs/9.5/infoschema-foreign-
data-wrapper-options.html "PostgreSQL 9.5 -
37.26. foreign_data_wrapper_options") / [9.4](/docs/9.4/infoschema-foreign-
data-wrapper-options.html "PostgreSQL 9.4 -
37.26. foreign_data_wrapper_options") / [9.3](/docs/9.3/infoschema-foreign-
data-wrapper-options.html "PostgreSQL 9.3 -
37.26. foreign_data_wrapper_options") / [9.2](/docs/9.2/infoschema-foreign-
data-wrapper-options.html "PostgreSQL 9.2 -
37.26. foreign_data_wrapper_options") / [9.1](/docs/9.1/infoschema-foreign-
data-wrapper-options.html "PostgreSQL 9.1 -
37.26. foreign_data_wrapper_options") / [9.0](/docs/9.0/infoschema-foreign-
data-wrapper-options.html "PostgreSQL 9.0 -
37.26. foreign_data_wrapper_options") / [8.4](/docs/8.4/infoschema-foreign-
data-wrapper-options.html "PostgreSQL 8.4 -
37.26. foreign_data_wrapper_options")

__

37.26. `foreign_data_wrapper_options`  
---  
[Prev](infoschema-enabled-roles.html "37.25. enabled_roles")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-foreign-data-wrappers.html "37.27. foreign_data_wrappers")  
  
* * *

## 37.26. `foreign_data_wrapper_options` #

The view `foreign_data_wrapper_options` contains all the options defined for
foreign-data wrappers in the current database. Only those foreign-data
wrappers are shown that the current user has access to (by way of being the
owner or having some privilege).

**Table  37.24. `foreign_data_wrapper_options` Columns**

Column Type Description  
---  
`foreign_data_wrapper_catalog` `sql_identifier` Name of the database that the
foreign-data wrapper is defined in (always the current database)  
`foreign_data_wrapper_name` `sql_identifier` Name of the foreign-data wrapper  
`option_name` `sql_identifier` Name of an option  
`option_value` `character_data` Value of the option  
  
  

* * *

[Prev](infoschema-enabled-roles.html "37.25. enabled_roles")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-foreign-data-wrappers.html "37.27. foreign_data_wrappers")  
---|---|---  
37.25. `enabled_roles`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.27. `foreign_data_wrappers`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-foreign-data-
wrapper-options.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

