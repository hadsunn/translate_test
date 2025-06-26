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

Supported Versions: [Current](/docs/current/infoschema-datatypes.html
"PostgreSQL 17 - 37.2. Data Types") ([17](/docs/17/infoschema-datatypes.html
"PostgreSQL 17 - 37.2. Data Types")) / [16](/docs/16/infoschema-datatypes.html
"PostgreSQL 16 - 37.2. Data Types") / [15](/docs/15/infoschema-datatypes.html
"PostgreSQL 15 - 37.2. Data Types") / [14](/docs/14/infoschema-datatypes.html
"PostgreSQL 14 - 37.2. Data Types") / [13](/docs/13/infoschema-datatypes.html
"PostgreSQL 13 - 37.2. Data Types")

Development Versions: [18](/docs/18/infoschema-datatypes.html "PostgreSQL 18 -
37.2. Data Types") / [devel](/docs/devel/infoschema-datatypes.html "PostgreSQL
devel - 37.2. Data Types")

Unsupported versions: [12](/docs/12/infoschema-datatypes.html "PostgreSQL 12 -
37.2. Data Types") / [11](/docs/11/infoschema-datatypes.html "PostgreSQL 11 -
37.2. Data Types") / [10](/docs/10/infoschema-datatypes.html "PostgreSQL 10 -
37.2. Data Types") / [9.6](/docs/9.6/infoschema-datatypes.html "PostgreSQL 9.6
- 37.2. Data Types") / [9.5](/docs/9.5/infoschema-datatypes.html "PostgreSQL
9.5 - 37.2. Data Types") / [9.4](/docs/9.4/infoschema-datatypes.html
"PostgreSQL 9.4 - 37.2. Data Types") / [9.3](/docs/9.3/infoschema-
datatypes.html "PostgreSQL 9.3 - 37.2. Data Types") /
[9.2](/docs/9.2/infoschema-datatypes.html "PostgreSQL 9.2 - 37.2. Data Types")
/ [9.1](/docs/9.1/infoschema-datatypes.html "PostgreSQL 9.1 - 37.2. Data
Types") / [9.0](/docs/9.0/infoschema-datatypes.html "PostgreSQL 9.0 -
37.2. Data Types") / [8.4](/docs/8.4/infoschema-datatypes.html "PostgreSQL 8.4
- 37.2. Data Types") / [8.3](/docs/8.3/infoschema-datatypes.html "PostgreSQL
8.3 - 37.2. Data Types") / [8.2](/docs/8.2/infoschema-datatypes.html
"PostgreSQL 8.2 - 37.2. Data Types") / [8.1](/docs/8.1/infoschema-
datatypes.html "PostgreSQL 8.1 - 37.2. Data Types") /
[8.0](/docs/8.0/infoschema-datatypes.html "PostgreSQL 8.0 - 37.2. Data Types")
/ [7.4](/docs/7.4/infoschema-datatypes.html "PostgreSQL 7.4 - 37.2. Data
Types")

__

37.2. Data Types  
---  
[Prev](infoschema-schema.html "37.1. The Schema")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-information-schema-catalog-name.html "37.3. information_schema_catalog_name")  
  
* * *

## 37.2. Data Types #

The columns of the information schema views use special data types that are
defined in the information schema. These are defined as simple domains over
ordinary built-in types. You should not use these types for work outside the
information schema, but your applications must be prepared for them if they
select from the information schema.

These types are:

`cardinal_number`

    

A nonnegative integer.

`character_data`

    

A character string (without specific maximum length).

`sql_identifier`

    

A character string. This type is used for SQL identifiers, the type
`character_data` is used for any other kind of text data.

`time_stamp`

    

A domain over the type `timestamp with time zone`

`yes_or_no`

    

A character string domain that contains either `YES` or `NO`. This is used to
represent Boolean (true/false) data in the information schema. (The
information schema was invented before the type `boolean` was added to the SQL
standard, so this convention is necessary to keep the information schema
backward compatible.)

Every column in the information schema has one of these five types.

* * *

[Prev](infoschema-schema.html "37.1. The Schema")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-information-schema-catalog-name.html "37.3. information_schema_catalog_name")  
---|---|---  
37.1. The Schema  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.3. `information_schema_catalog_name`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-datatypes.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

