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

Supported Versions: [Current](/docs/current/infoschema-user-defined-types.html
"PostgreSQL 17 - 37.60. user_defined_types") ([17](/docs/17/infoschema-user-
defined-types.html "PostgreSQL 17 - 37.60. user_defined_types")) /
[16](/docs/16/infoschema-user-defined-types.html "PostgreSQL 16 -
37.60. user_defined_types") / [15](/docs/15/infoschema-user-defined-types.html
"PostgreSQL 15 - 37.60. user_defined_types") / [14](/docs/14/infoschema-user-
defined-types.html "PostgreSQL 14 - 37.60. user_defined_types") /
[13](/docs/13/infoschema-user-defined-types.html "PostgreSQL 13 -
37.60. user_defined_types")

Development Versions: [18](/docs/18/infoschema-user-defined-types.html
"PostgreSQL 18 - 37.60. user_defined_types") / [devel](/docs/devel/infoschema-
user-defined-types.html "PostgreSQL devel - 37.60. user_defined_types")

Unsupported versions: [12](/docs/12/infoschema-user-defined-types.html
"PostgreSQL 12 - 37.60. user_defined_types") / [11](/docs/11/infoschema-user-
defined-types.html "PostgreSQL 11 - 37.60. user_defined_types") /
[10](/docs/10/infoschema-user-defined-types.html "PostgreSQL 10 -
37.60. user_defined_types") / [9.6](/docs/9.6/infoschema-user-defined-
types.html "PostgreSQL 9.6 - 37.60. user_defined_types") /
[9.5](/docs/9.5/infoschema-user-defined-types.html "PostgreSQL 9.5 -
37.60. user_defined_types") / [9.4](/docs/9.4/infoschema-user-defined-
types.html "PostgreSQL 9.4 - 37.60. user_defined_types") /
[9.3](/docs/9.3/infoschema-user-defined-types.html "PostgreSQL 9.3 -
37.60. user_defined_types") / [9.2](/docs/9.2/infoschema-user-defined-
types.html "PostgreSQL 9.2 - 37.60. user_defined_types")

__

37.60. `user_defined_types`  
---  
[Prev](infoschema-usage-privileges.html "37.59. usage_privileges")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-user-mapping-options.html "37.61. user_mapping_options")  
  
* * *

## 37.60. `user_defined_types` #

The view `user_defined_types` currently contains all composite types defined
in the current database. Only those types are shown that the current user has
access to (by way of being the owner or having some privilege).

SQL knows about two kinds of user-defined types: structured types (also known
as composite types in PostgreSQL) and distinct types (not implemented in
PostgreSQL). To be future-proof, use the column `user_defined_type_category`
to differentiate between these. Other user-defined types such as base types
and enums, which are PostgreSQL extensions, are not shown here. For domains,
see [Section 37.23](infoschema-domains.html "37.23. domains") instead.

**Table  37.58. `user_defined_types` Columns**

Column Type Description  
---  
`user_defined_type_catalog` `sql_identifier` Name of the database that
contains the type (always the current database)  
`user_defined_type_schema` `sql_identifier` Name of the schema that contains
the type  
`user_defined_type_name` `sql_identifier` Name of the type  
`user_defined_type_category` `character_data` Currently always `STRUCTURED`  
`is_instantiable` `yes_or_no` Applies to a feature not available in PostgreSQL  
`is_final` `yes_or_no` Applies to a feature not available in PostgreSQL  
`ordering_form` `character_data` Applies to a feature not available in
PostgreSQL  
`ordering_category` `character_data` Applies to a feature not available in
PostgreSQL  
`ordering_routine_catalog` `sql_identifier` Applies to a feature not available
in PostgreSQL  
`ordering_routine_schema` `sql_identifier` Applies to a feature not available
in PostgreSQL  
`ordering_routine_name` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`reference_type` `character_data` Applies to a feature not available in
PostgreSQL  
`data_type` `character_data` Applies to a feature not available in PostgreSQL  
`character_maximum_length` `cardinal_number` Applies to a feature not
available in PostgreSQL  
`character_octet_length` `cardinal_number` Applies to a feature not available
in PostgreSQL  
`character_set_catalog` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`character_set_schema` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`character_set_name` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`collation_catalog` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`collation_schema` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`collation_name` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`numeric_precision` `cardinal_number` Applies to a feature not available in
PostgreSQL  
`numeric_precision_radix` `cardinal_number` Applies to a feature not available
in PostgreSQL  
`numeric_scale` `cardinal_number` Applies to a feature not available in
PostgreSQL  
`datetime_precision` `cardinal_number` Applies to a feature not available in
PostgreSQL  
`interval_type` `character_data` Applies to a feature not available in
PostgreSQL  
`interval_precision` `cardinal_number` Applies to a feature not available in
PostgreSQL  
`source_dtd_identifier` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`ref_dtd_identifier` `sql_identifier` Applies to a feature not available in
PostgreSQL  
  
  

* * *

[Prev](infoschema-usage-privileges.html "37.59. usage_privileges")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-user-mapping-options.html "37.61. user_mapping_options")  
---|---|---  
37.59. `usage_privileges`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.61. `user_mapping_options`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-user-defined-
types.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

