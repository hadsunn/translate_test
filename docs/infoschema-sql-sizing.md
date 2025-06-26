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

Supported Versions: [Current](/docs/current/infoschema-sql-sizing.html
"PostgreSQL 17 - 37.51. sql_sizing") ([17](/docs/17/infoschema-sql-sizing.html
"PostgreSQL 17 - 37.51. sql_sizing")) / [16](/docs/16/infoschema-sql-
sizing.html "PostgreSQL 16 - 37.51. sql_sizing") / [15](/docs/15/infoschema-
sql-sizing.html "PostgreSQL 15 - 37.51. sql_sizing") /
[14](/docs/14/infoschema-sql-sizing.html "PostgreSQL 14 - 37.51. sql_sizing")
/ [13](/docs/13/infoschema-sql-sizing.html "PostgreSQL 13 -
37.51. sql_sizing")

Development Versions: [18](/docs/18/infoschema-sql-sizing.html "PostgreSQL 18
- 37.51. sql_sizing") / [devel](/docs/devel/infoschema-sql-sizing.html
"PostgreSQL devel - 37.51. sql_sizing")

Unsupported versions: [12](/docs/12/infoschema-sql-sizing.html "PostgreSQL 12
- 37.51. sql_sizing") / [11](/docs/11/infoschema-sql-sizing.html "PostgreSQL
11 - 37.51. sql_sizing") / [10](/docs/10/infoschema-sql-sizing.html
"PostgreSQL 10 - 37.51. sql_sizing") / [9.6](/docs/9.6/infoschema-sql-
sizing.html "PostgreSQL 9.6 - 37.51. sql_sizing") /
[9.5](/docs/9.5/infoschema-sql-sizing.html "PostgreSQL 9.5 -
37.51. sql_sizing") / [9.4](/docs/9.4/infoschema-sql-sizing.html "PostgreSQL
9.4 - 37.51. sql_sizing") / [9.3](/docs/9.3/infoschema-sql-sizing.html
"PostgreSQL 9.3 - 37.51. sql_sizing") / [9.2](/docs/9.2/infoschema-sql-
sizing.html "PostgreSQL 9.2 - 37.51. sql_sizing") /
[9.1](/docs/9.1/infoschema-sql-sizing.html "PostgreSQL 9.1 -
37.51. sql_sizing") / [9.0](/docs/9.0/infoschema-sql-sizing.html "PostgreSQL
9.0 - 37.51. sql_sizing") / [8.4](/docs/8.4/infoschema-sql-sizing.html
"PostgreSQL 8.4 - 37.51. sql_sizing") / [8.3](/docs/8.3/infoschema-sql-
sizing.html "PostgreSQL 8.3 - 37.51. sql_sizing") /
[8.2](/docs/8.2/infoschema-sql-sizing.html "PostgreSQL 8.2 -
37.51. sql_sizing") / [8.1](/docs/8.1/infoschema-sql-sizing.html "PostgreSQL
8.1 - 37.51. sql_sizing") / [8.0](/docs/8.0/infoschema-sql-sizing.html
"PostgreSQL 8.0 - 37.51. sql_sizing") / [7.4](/docs/7.4/infoschema-sql-
sizing.html "PostgreSQL 7.4 - 37.51. sql_sizing")

__

37.51. `sql_sizing`  
---  
[Prev](infoschema-sql-parts.html "37.50. sql_parts")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-table-constraints.html "37.52. table_constraints")  
  
* * *

## 37.51. `sql_sizing` #

The table `sql_sizing` contains information about various size limits and
maximum values in PostgreSQL. This information is primarily intended for use
in the context of the ODBC interface; users of other interfaces will probably
find this information to be of little use. For this reason, the individual
sizing items are not described here; you will find them in the description of
the ODBC interface.

**Table  37.49. `sql_sizing` Columns**

Column Type Description  
---  
`sizing_id` `cardinal_number` Identifier of the sizing item  
`sizing_name` `character_data` Descriptive name of the sizing item  
`supported_value` `cardinal_number` Value of the sizing item, or 0 if the size
is unlimited or cannot be determined, or null if the features for which the
sizing item is applicable are not supported  
`comments` `character_data` Possibly a comment pertaining to the sizing item  
  
  

* * *

[Prev](infoschema-sql-parts.html "37.50. sql_parts")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-table-constraints.html "37.52. table_constraints")  
---|---|---  
37.50. `sql_parts`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.52. `table_constraints`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-sql-sizing.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

