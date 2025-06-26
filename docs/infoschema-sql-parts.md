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

Supported Versions: [Current](/docs/current/infoschema-sql-parts.html
"PostgreSQL 17 - 37.50. sql_parts") ([17](/docs/17/infoschema-sql-parts.html
"PostgreSQL 17 - 37.50. sql_parts")) / [16](/docs/16/infoschema-sql-parts.html
"PostgreSQL 16 - 37.50. sql_parts") / [15](/docs/15/infoschema-sql-parts.html
"PostgreSQL 15 - 37.50. sql_parts") / [14](/docs/14/infoschema-sql-parts.html
"PostgreSQL 14 - 37.50. sql_parts") / [13](/docs/13/infoschema-sql-parts.html
"PostgreSQL 13 - 37.50. sql_parts")

Development Versions: [18](/docs/18/infoschema-sql-parts.html "PostgreSQL 18 -
37.50. sql_parts") / [devel](/docs/devel/infoschema-sql-parts.html "PostgreSQL
devel - 37.50. sql_parts")

Unsupported versions: [12](/docs/12/infoschema-sql-parts.html "PostgreSQL 12 -
37.50. sql_parts") / [11](/docs/11/infoschema-sql-parts.html "PostgreSQL 11 -
37.50. sql_parts") / [10](/docs/10/infoschema-sql-parts.html "PostgreSQL 10 -
37.50. sql_parts") / [9.6](/docs/9.6/infoschema-sql-parts.html "PostgreSQL 9.6
- 37.50. sql_parts") / [9.5](/docs/9.5/infoschema-sql-parts.html "PostgreSQL
9.5 - 37.50. sql_parts") / [9.4](/docs/9.4/infoschema-sql-parts.html
"PostgreSQL 9.4 - 37.50. sql_parts") / [9.3](/docs/9.3/infoschema-sql-
parts.html "PostgreSQL 9.3 - 37.50. sql_parts") / [9.2](/docs/9.2/infoschema-
sql-parts.html "PostgreSQL 9.2 - 37.50. sql_parts") /
[9.1](/docs/9.1/infoschema-sql-parts.html "PostgreSQL 9.1 - 37.50. sql_parts")
/ [9.0](/docs/9.0/infoschema-sql-parts.html "PostgreSQL 9.0 -
37.50. sql_parts") / [8.4](/docs/8.4/infoschema-sql-parts.html "PostgreSQL 8.4
- 37.50. sql_parts") / [8.3](/docs/8.3/infoschema-sql-parts.html "PostgreSQL
8.3 - 37.50. sql_parts") / [8.2](/docs/8.2/infoschema-sql-parts.html
"PostgreSQL 8.2 - 37.50. sql_parts")

__

37.50. `sql_parts`  
---  
[Prev](infoschema-sql-implementation-info.html "37.49. sql_implementation_info")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-sql-sizing.html "37.51. sql_sizing")  
  
* * *

## 37.50. `sql_parts` #

The table `sql_parts` contains information about which of the several parts of
the SQL standard are supported by PostgreSQL.

**Table  37.48. `sql_parts` Columns**

Column Type Description  
---  
`feature_id` `character_data` An identifier string containing the number of
the part  
`feature_name` `character_data` Descriptive name of the part  
`is_supported` `yes_or_no` `YES` if the part is fully supported by the current
version of PostgreSQL, `NO` if not  
`is_verified_by` `character_data` Always null, since the PostgreSQL
development group does not perform formal testing of feature conformance  
`comments` `character_data` Possibly a comment about the supported status of
the part  
  
  

* * *

[Prev](infoschema-sql-implementation-info.html "37.49. sql_implementation_info")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-sql-sizing.html "37.51. sql_sizing")  
---|---|---  
37.49. `sql_implementation_info`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.51. `sql_sizing`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-sql-parts.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

