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

Supported Versions: [Current](/docs/current/infoschema-sequences.html
"PostgreSQL 17 - 37.47. sequences") ([17](/docs/17/infoschema-sequences.html
"PostgreSQL 17 - 37.47. sequences")) / [16](/docs/16/infoschema-sequences.html
"PostgreSQL 16 - 37.47. sequences") / [15](/docs/15/infoschema-sequences.html
"PostgreSQL 15 - 37.47. sequences") / [14](/docs/14/infoschema-sequences.html
"PostgreSQL 14 - 37.47. sequences") / [13](/docs/13/infoschema-sequences.html
"PostgreSQL 13 - 37.47. sequences")

Development Versions: [18](/docs/18/infoschema-sequences.html "PostgreSQL 18 -
37.47. sequences") / [devel](/docs/devel/infoschema-sequences.html "PostgreSQL
devel - 37.47. sequences")

Unsupported versions: [12](/docs/12/infoschema-sequences.html "PostgreSQL 12 -
37.47. sequences") / [11](/docs/11/infoschema-sequences.html "PostgreSQL 11 -
37.47. sequences") / [10](/docs/10/infoschema-sequences.html "PostgreSQL 10 -
37.47. sequences") / [9.6](/docs/9.6/infoschema-sequences.html "PostgreSQL 9.6
- 37.47. sequences") / [9.5](/docs/9.5/infoschema-sequences.html "PostgreSQL
9.5 - 37.47. sequences") / [9.4](/docs/9.4/infoschema-sequences.html
"PostgreSQL 9.4 - 37.47. sequences") / [9.3](/docs/9.3/infoschema-
sequences.html "PostgreSQL 9.3 - 37.47. sequences") /
[9.2](/docs/9.2/infoschema-sequences.html "PostgreSQL 9.2 - 37.47. sequences")
/ [9.1](/docs/9.1/infoschema-sequences.html "PostgreSQL 9.1 -
37.47. sequences") / [9.0](/docs/9.0/infoschema-sequences.html "PostgreSQL 9.0
- 37.47. sequences") / [8.4](/docs/8.4/infoschema-sequences.html "PostgreSQL
8.4 - 37.47. sequences") / [8.3](/docs/8.3/infoschema-sequences.html
"PostgreSQL 8.3 - 37.47. sequences") / [8.2](/docs/8.2/infoschema-
sequences.html "PostgreSQL 8.2 - 37.47. sequences")

__

37.47. `sequences`  
---  
[Prev](infoschema-schemata.html "37.46. schemata")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-sql-features.html "37.48. sql_features")  
  
* * *

## 37.47. `sequences` #

The view `sequences` contains all sequences defined in the current database.
Only those sequences are shown that the current user has access to (by way of
being the owner or having some privilege).

**Table  37.45. `sequences` Columns**

Column Type Description  
---  
`sequence_catalog` `sql_identifier` Name of the database that contains the
sequence (always the current database)  
`sequence_schema` `sql_identifier` Name of the schema that contains the
sequence  
`sequence_name` `sql_identifier` Name of the sequence  
`data_type` `character_data` The data type of the sequence.  
`numeric_precision` `cardinal_number` This column contains the (declared or
implicit) precision of the sequence data type (see above). The precision
indicates the number of significant digits. It can be expressed in decimal
(base 10) or binary (base 2) terms, as specified in the column
`numeric_precision_radix`.  
`numeric_precision_radix` `cardinal_number` This column indicates in which
base the values in the columns `numeric_precision` and `numeric_scale` are
expressed. The value is either 2 or 10.  
`numeric_scale` `cardinal_number` This column contains the (declared or
implicit) scale of the sequence data type (see above). The scale indicates the
number of significant digits to the right of the decimal point. It can be
expressed in decimal (base 10) or binary (base 2) terms, as specified in the
column `numeric_precision_radix`.  
`start_value` `character_data` The start value of the sequence  
`minimum_value` `character_data` The minimum value of the sequence  
`maximum_value` `character_data` The maximum value of the sequence  
`increment` `character_data` The increment of the sequence  
`cycle_option` `yes_or_no` `YES` if the sequence cycles, else `NO`  
  
  

Note that in accordance with the SQL standard, the start, minimum, maximum,
and increment values are returned as character strings.

* * *

[Prev](infoschema-schemata.html "37.46. schemata")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-sql-features.html "37.48. sql_features")  
---|---|---  
37.46. `schemata`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.48. `sql_features`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-sequences.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

