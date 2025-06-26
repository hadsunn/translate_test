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

Supported Versions: [Current](/docs/current/infoschema-sql-implementation-
info.html "PostgreSQL 17 - 37.49. sql_implementation_info")
([17](/docs/17/infoschema-sql-implementation-info.html "PostgreSQL 17 -
37.49. sql_implementation_info")) / [16](/docs/16/infoschema-sql-
implementation-info.html "PostgreSQL 16 - 37.49. sql_implementation_info") /
[15](/docs/15/infoschema-sql-implementation-info.html "PostgreSQL 15 -
37.49. sql_implementation_info") / [14](/docs/14/infoschema-sql-
implementation-info.html "PostgreSQL 14 - 37.49. sql_implementation_info") /
[13](/docs/13/infoschema-sql-implementation-info.html "PostgreSQL 13 -
37.49. sql_implementation_info")

Development Versions: [18](/docs/18/infoschema-sql-implementation-info.html
"PostgreSQL 18 - 37.49. sql_implementation_info") /
[devel](/docs/devel/infoschema-sql-implementation-info.html "PostgreSQL devel
- 37.49. sql_implementation_info")

Unsupported versions: [12](/docs/12/infoschema-sql-implementation-info.html
"PostgreSQL 12 - 37.49. sql_implementation_info") / [11](/docs/11/infoschema-
sql-implementation-info.html "PostgreSQL 11 - 37.49. sql_implementation_info")
/ [10](/docs/10/infoschema-sql-implementation-info.html "PostgreSQL 10 -
37.49. sql_implementation_info") / [9.6](/docs/9.6/infoschema-sql-
implementation-info.html "PostgreSQL 9.6 - 37.49. sql_implementation_info") /
[9.5](/docs/9.5/infoschema-sql-implementation-info.html "PostgreSQL 9.5 -
37.49. sql_implementation_info") / [9.4](/docs/9.4/infoschema-sql-
implementation-info.html "PostgreSQL 9.4 - 37.49. sql_implementation_info") /
[9.3](/docs/9.3/infoschema-sql-implementation-info.html "PostgreSQL 9.3 -
37.49. sql_implementation_info") / [9.2](/docs/9.2/infoschema-sql-
implementation-info.html "PostgreSQL 9.2 - 37.49. sql_implementation_info") /
[9.1](/docs/9.1/infoschema-sql-implementation-info.html "PostgreSQL 9.1 -
37.49. sql_implementation_info") / [9.0](/docs/9.0/infoschema-sql-
implementation-info.html "PostgreSQL 9.0 - 37.49. sql_implementation_info") /
[8.4](/docs/8.4/infoschema-sql-implementation-info.html "PostgreSQL 8.4 -
37.49. sql_implementation_info") / [8.3](/docs/8.3/infoschema-sql-
implementation-info.html "PostgreSQL 8.3 - 37.49. sql_implementation_info") /
[8.2](/docs/8.2/infoschema-sql-implementation-info.html "PostgreSQL 8.2 -
37.49. sql_implementation_info") / [8.1](/docs/8.1/infoschema-sql-
implementation-info.html "PostgreSQL 8.1 - 37.49. sql_implementation_info") /
[8.0](/docs/8.0/infoschema-sql-implementation-info.html "PostgreSQL 8.0 -
37.49. sql_implementation_info") / [7.4](/docs/7.4/infoschema-sql-
implementation-info.html "PostgreSQL 7.4 - 37.49. sql_implementation_info")

__

37.49. `sql_implementation_info`  
---  
[Prev](infoschema-sql-features.html "37.48. sql_features")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-sql-parts.html "37.50. sql_parts")  
  
* * *

## 37.49. `sql_implementation_info` #

The table `sql_implementation_info` contains information about various aspects
that are left implementation-defined by the SQL standard. This information is
primarily intended for use in the context of the ODBC interface; users of
other interfaces will probably find this information to be of little use. For
this reason, the individual implementation information items are not described
here; you will find them in the description of the ODBC interface.

**Table  37.47. `sql_implementation_info` Columns**

Column Type Description  
---  
`implementation_info_id` `character_data` Identifier string of the
implementation information item  
`implementation_info_name` `character_data` Descriptive name of the
implementation information item  
`integer_value` `cardinal_number` Value of the implementation information
item, or null if the value is contained in the column `character_value`  
`character_value` `character_data` Value of the implementation information
item, or null if the value is contained in the column `integer_value`  
`comments` `character_data` Possibly a comment pertaining to the
implementation information item  
  
  

* * *

[Prev](infoschema-sql-features.html "37.48. sql_features")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-sql-parts.html "37.50. sql_parts")  
---|---|---  
37.48. `sql_features`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.50. `sql_parts`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-sql-implementation-
info.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

