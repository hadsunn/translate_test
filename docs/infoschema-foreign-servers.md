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

Supported Versions: [Current](/docs/current/infoschema-foreign-servers.html
"PostgreSQL 17 - 37.29. foreign_servers") ([17](/docs/17/infoschema-foreign-
servers.html "PostgreSQL 17 - 37.29. foreign_servers")) /
[16](/docs/16/infoschema-foreign-servers.html "PostgreSQL 16 -
37.29. foreign_servers") / [15](/docs/15/infoschema-foreign-servers.html
"PostgreSQL 15 - 37.29. foreign_servers") / [14](/docs/14/infoschema-foreign-
servers.html "PostgreSQL 14 - 37.29. foreign_servers") /
[13](/docs/13/infoschema-foreign-servers.html "PostgreSQL 13 -
37.29. foreign_servers")

Development Versions: [18](/docs/18/infoschema-foreign-servers.html
"PostgreSQL 18 - 37.29. foreign_servers") / [devel](/docs/devel/infoschema-
foreign-servers.html "PostgreSQL devel - 37.29. foreign_servers")

Unsupported versions: [12](/docs/12/infoschema-foreign-servers.html
"PostgreSQL 12 - 37.29. foreign_servers") / [11](/docs/11/infoschema-foreign-
servers.html "PostgreSQL 11 - 37.29. foreign_servers") /
[10](/docs/10/infoschema-foreign-servers.html "PostgreSQL 10 -
37.29. foreign_servers") / [9.6](/docs/9.6/infoschema-foreign-servers.html
"PostgreSQL 9.6 - 37.29. foreign_servers") / [9.5](/docs/9.5/infoschema-
foreign-servers.html "PostgreSQL 9.5 - 37.29. foreign_servers") /
[9.4](/docs/9.4/infoschema-foreign-servers.html "PostgreSQL 9.4 -
37.29. foreign_servers") / [9.3](/docs/9.3/infoschema-foreign-servers.html
"PostgreSQL 9.3 - 37.29. foreign_servers") / [9.2](/docs/9.2/infoschema-
foreign-servers.html "PostgreSQL 9.2 - 37.29. foreign_servers") /
[9.1](/docs/9.1/infoschema-foreign-servers.html "PostgreSQL 9.1 -
37.29. foreign_servers") / [9.0](/docs/9.0/infoschema-foreign-servers.html
"PostgreSQL 9.0 - 37.29. foreign_servers") / [8.4](/docs/8.4/infoschema-
foreign-servers.html "PostgreSQL 8.4 - 37.29. foreign_servers")

__

37.29. `foreign_servers`  
---  
[Prev](infoschema-foreign-server-options.html "37.28. foreign_server_options")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-foreign-table-options.html "37.30. foreign_table_options")  
  
* * *

## 37.29. `foreign_servers` #

The view `foreign_servers` contains all foreign servers defined in the current
database. Only those foreign servers are shown that the current user has
access to (by way of being the owner or having some privilege).

**Table  37.27. `foreign_servers` Columns**

Column Type Description  
---  
`foreign_server_catalog` `sql_identifier` Name of the database that the
foreign server is defined in (always the current database)  
`foreign_server_name` `sql_identifier` Name of the foreign server  
`foreign_data_wrapper_catalog` `sql_identifier` Name of the database that
contains the foreign-data wrapper used by the foreign server (always the
current database)  
`foreign_data_wrapper_name` `sql_identifier` Name of the foreign-data wrapper
used by the foreign server  
`foreign_server_type` `character_data` Foreign server type information, if
specified upon creation  
`foreign_server_version` `character_data` Foreign server version information,
if specified upon creation  
`authorization_identifier` `sql_identifier` Name of the owner of the foreign
server  
  
  

* * *

[Prev](infoschema-foreign-server-options.html "37.28. foreign_server_options")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-foreign-table-options.html "37.30. foreign_table_options")  
---|---|---  
37.28. `foreign_server_options`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.30. `foreign_table_options`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-foreign-
servers.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

