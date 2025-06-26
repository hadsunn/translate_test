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

Supported Versions: [Current](/docs/current/infoschema-transforms.html
"PostgreSQL 17 - 37.55. transforms") ([17](/docs/17/infoschema-transforms.html
"PostgreSQL 17 - 37.55. transforms")) / [16](/docs/16/infoschema-
transforms.html "PostgreSQL 16 - 37.55. transforms") /
[15](/docs/15/infoschema-transforms.html "PostgreSQL 15 - 37.55. transforms")
/ [14](/docs/14/infoschema-transforms.html "PostgreSQL 14 -
37.55. transforms") / [13](/docs/13/infoschema-transforms.html "PostgreSQL 13
- 37.55. transforms")

Development Versions: [18](/docs/18/infoschema-transforms.html "PostgreSQL 18
- 37.55. transforms") / [devel](/docs/devel/infoschema-transforms.html
"PostgreSQL devel - 37.55. transforms")

Unsupported versions: [12](/docs/12/infoschema-transforms.html "PostgreSQL 12
- 37.55. transforms") / [11](/docs/11/infoschema-transforms.html "PostgreSQL
11 - 37.55. transforms") / [10](/docs/10/infoschema-transforms.html
"PostgreSQL 10 - 37.55. transforms") / [9.6](/docs/9.6/infoschema-
transforms.html "PostgreSQL 9.6 - 37.55. transforms") /
[9.5](/docs/9.5/infoschema-transforms.html "PostgreSQL 9.5 -
37.55. transforms")

__

37.55. `transforms`  
---  
[Prev](infoschema-tables.html "37.54. tables")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-triggered-update-columns.html "37.56. triggered_update_columns")  
  
* * *

## 37.55. `transforms` #

The view `transforms` contains information about the transforms defined in the
current database. More precisely, it contains a row for each function
contained in a transform (the “from SQL” or “to SQL” function).

**Table  37.53. `transforms` Columns**

Column Type Description  
---  
`udt_catalog` `sql_identifier` Name of the database that contains the type the
transform is for (always the current database)  
`udt_schema` `sql_identifier` Name of the schema that contains the type the
transform is for  
`udt_name` `sql_identifier` Name of the type the transform is for  
`specific_catalog` `sql_identifier` Name of the database containing the
function (always the current database)  
`specific_schema` `sql_identifier` Name of the schema containing the function  
`specific_name` `sql_identifier` The “specific name” of the function. See
[Section 37.45](infoschema-routines.html "37.45. routines") for more
information.  
`group_name` `sql_identifier` The SQL standard allows defining transforms in
“groups”, and selecting a group at run time. PostgreSQL does not support this.
Instead, transforms are specific to a language. As a compromise, this field
contains the language the transform is for.  
`transform_type` `character_data` `FROM SQL` or `TO SQL`  
  
  

* * *

[Prev](infoschema-tables.html "37.54. tables")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-triggered-update-columns.html "37.56. triggered_update_columns")  
---|---|---  
37.54. `tables`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.56. `triggered_update_columns`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-transforms.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

