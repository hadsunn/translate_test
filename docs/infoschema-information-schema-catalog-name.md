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

Supported Versions: [Current](/docs/current/infoschema-information-schema-
catalog-name.html "PostgreSQL 17 - 37.3. information_schema_catalog_name")
([17](/docs/17/infoschema-information-schema-catalog-name.html "PostgreSQL 17
- 37.3. information_schema_catalog_name")) / [16](/docs/16/infoschema-
information-schema-catalog-name.html "PostgreSQL 16 -
37.3. information_schema_catalog_name") / [15](/docs/15/infoschema-
information-schema-catalog-name.html "PostgreSQL 15 -
37.3. information_schema_catalog_name") / [14](/docs/14/infoschema-
information-schema-catalog-name.html "PostgreSQL 14 -
37.3. information_schema_catalog_name") / [13](/docs/13/infoschema-
information-schema-catalog-name.html "PostgreSQL 13 -
37.3. information_schema_catalog_name")

Development Versions: [18](/docs/18/infoschema-information-schema-catalog-
name.html "PostgreSQL 18 - 37.3. information_schema_catalog_name") /
[devel](/docs/devel/infoschema-information-schema-catalog-name.html
"PostgreSQL devel - 37.3. information_schema_catalog_name")

Unsupported versions: [12](/docs/12/infoschema-information-schema-catalog-
name.html "PostgreSQL 12 - 37.3. information_schema_catalog_name") /
[11](/docs/11/infoschema-information-schema-catalog-name.html "PostgreSQL 11 -
37.3. information_schema_catalog_name") / [10](/docs/10/infoschema-
information-schema-catalog-name.html "PostgreSQL 10 -
37.3. information_schema_catalog_name") / [9.6](/docs/9.6/infoschema-
information-schema-catalog-name.html "PostgreSQL 9.6 -
37.3. information_schema_catalog_name") / [9.5](/docs/9.5/infoschema-
information-schema-catalog-name.html "PostgreSQL 9.5 -
37.3. information_schema_catalog_name") / [9.4](/docs/9.4/infoschema-
information-schema-catalog-name.html "PostgreSQL 9.4 -
37.3. information_schema_catalog_name") / [9.3](/docs/9.3/infoschema-
information-schema-catalog-name.html "PostgreSQL 9.3 -
37.3. information_schema_catalog_name") / [9.2](/docs/9.2/infoschema-
information-schema-catalog-name.html "PostgreSQL 9.2 -
37.3. information_schema_catalog_name") / [9.1](/docs/9.1/infoschema-
information-schema-catalog-name.html "PostgreSQL 9.1 -
37.3. information_schema_catalog_name") / [9.0](/docs/9.0/infoschema-
information-schema-catalog-name.html "PostgreSQL 9.0 -
37.3. information_schema_catalog_name") / [8.4](/docs/8.4/infoschema-
information-schema-catalog-name.html "PostgreSQL 8.4 -
37.3. information_schema_catalog_name") / [8.3](/docs/8.3/infoschema-
information-schema-catalog-name.html "PostgreSQL 8.3 -
37.3. information_schema_catalog_name") / [8.2](/docs/8.2/infoschema-
information-schema-catalog-name.html "PostgreSQL 8.2 -
37.3. information_schema_catalog_name") / [8.1](/docs/8.1/infoschema-
information-schema-catalog-name.html "PostgreSQL 8.1 -
37.3. information_schema_catalog_name") / [8.0](/docs/8.0/infoschema-
information-schema-catalog-name.html "PostgreSQL 8.0 -
37.3. information_schema_catalog_name") / [7.4](/docs/7.4/infoschema-
information-schema-catalog-name.html "PostgreSQL 7.4 -
37.3. information_schema_catalog_name")

__

37.3. `information_schema_catalog_name`  
---  
[Prev](infoschema-datatypes.html "37.2. Data Types")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-administrable-role-authorizations.html "37.4. administrable_role_​authorizations")  
  
* * *

## 37.3. `information_schema_catalog_name` #

`information_schema_catalog_name` is a table that always contains one row and
one column containing the name of the current database (current catalog, in
SQL terminology).

**Table  37.1. `information_schema_catalog_name` Columns**

Column Type Description  
---  
`catalog_name` `sql_identifier` Name of the database that contains this
information schema  
  
  

* * *

[Prev](infoschema-datatypes.html "37.2. Data Types")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-administrable-role-authorizations.html "37.4. administrable_role_​authorizations")  
---|---|---  
37.2. Data Types  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.4. `administrable_role_​authorizations`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-information-schema-
catalog-name.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

