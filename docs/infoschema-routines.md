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

Supported Versions: [Current](/docs/current/infoschema-routines.html
"PostgreSQL 17 - 37.45. routines") ([17](/docs/17/infoschema-routines.html
"PostgreSQL 17 - 37.45. routines")) / [16](/docs/16/infoschema-routines.html
"PostgreSQL 16 - 37.45. routines") / [15](/docs/15/infoschema-routines.html
"PostgreSQL 15 - 37.45. routines") / [14](/docs/14/infoschema-routines.html
"PostgreSQL 14 - 37.45. routines") / [13](/docs/13/infoschema-routines.html
"PostgreSQL 13 - 37.45. routines")

Development Versions: [18](/docs/18/infoschema-routines.html "PostgreSQL 18 -
37.45. routines") / [devel](/docs/devel/infoschema-routines.html "PostgreSQL
devel - 37.45. routines")

Unsupported versions: [12](/docs/12/infoschema-routines.html "PostgreSQL 12 -
37.45. routines") / [11](/docs/11/infoschema-routines.html "PostgreSQL 11 -
37.45. routines") / [10](/docs/10/infoschema-routines.html "PostgreSQL 10 -
37.45. routines") / [9.6](/docs/9.6/infoschema-routines.html "PostgreSQL 9.6 -
37.45. routines") / [9.5](/docs/9.5/infoschema-routines.html "PostgreSQL 9.5 -
37.45. routines") / [9.4](/docs/9.4/infoschema-routines.html "PostgreSQL 9.4 -
37.45. routines") / [9.3](/docs/9.3/infoschema-routines.html "PostgreSQL 9.3 -
37.45. routines") / [9.2](/docs/9.2/infoschema-routines.html "PostgreSQL 9.2 -
37.45. routines") / [9.1](/docs/9.1/infoschema-routines.html "PostgreSQL 9.1 -
37.45. routines") / [9.0](/docs/9.0/infoschema-routines.html "PostgreSQL 9.0 -
37.45. routines") / [8.4](/docs/8.4/infoschema-routines.html "PostgreSQL 8.4 -
37.45. routines") / [8.3](/docs/8.3/infoschema-routines.html "PostgreSQL 8.3 -
37.45. routines") / [8.2](/docs/8.2/infoschema-routines.html "PostgreSQL 8.2 -
37.45. routines") / [8.1](/docs/8.1/infoschema-routines.html "PostgreSQL 8.1 -
37.45. routines") / [8.0](/docs/8.0/infoschema-routines.html "PostgreSQL 8.0 -
37.45. routines") / [7.4](/docs/7.4/infoschema-routines.html "PostgreSQL 7.4 -
37.45. routines")

__

37.45. `routines`  
---  
[Prev](infoschema-routine-table-usage.html "37.44. routine_table_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-schemata.html "37.46. schemata")  
  
* * *

## 37.45. `routines` #

The view `routines` contains all functions and procedures in the current
database. Only those functions and procedures are shown that the current user
has access to (by way of being the owner or having some privilege).

**Table  37.43. `routines` Columns**

Column Type Description  
---  
`specific_catalog` `sql_identifier` Name of the database containing the
function (always the current database)  
`specific_schema` `sql_identifier` Name of the schema containing the function  
`specific_name` `sql_identifier` The “specific name” of the function. This is
a name that uniquely identifies the function in the schema, even if the real
name of the function is overloaded. The format of the specific name is not
defined, it should only be used to compare it to other instances of specific
routine names.  
`routine_catalog` `sql_identifier` Name of the database containing the
function (always the current database)  
`routine_schema` `sql_identifier` Name of the schema containing the function  
`routine_name` `sql_identifier` Name of the function (might be duplicated in
case of overloading)  
`routine_type` `character_data` `FUNCTION` for a function, `PROCEDURE` for a
procedure  
`module_catalog` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`module_schema` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`module_name` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`udt_catalog` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`udt_schema` `sql_identifier` Applies to a feature not available in PostgreSQL  
`udt_name` `sql_identifier` Applies to a feature not available in PostgreSQL  
`data_type` `character_data` Return data type of the function, if it is a
built-in type, or `ARRAY` if it is some array (in that case, see the view
`element_types`), else `USER-DEFINED` (in that case, the type is identified in
`type_udt_name` and associated columns). Null for a procedure.  
`character_maximum_length` `cardinal_number` Always null, since this
information is not applied to return data types in PostgreSQL  
`character_octet_length` `cardinal_number` Always null, since this information
is not applied to return data types in PostgreSQL  
`character_set_catalog` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`character_set_schema` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`character_set_name` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`collation_catalog` `sql_identifier` Always null, since this information is
not applied to return data types in PostgreSQL  
`collation_schema` `sql_identifier` Always null, since this information is not
applied to return data types in PostgreSQL  
`collation_name` `sql_identifier` Always null, since this information is not
applied to return data types in PostgreSQL  
`numeric_precision` `cardinal_number` Always null, since this information is
not applied to return data types in PostgreSQL  
`numeric_precision_radix` `cardinal_number` Always null, since this
information is not applied to return data types in PostgreSQL  
`numeric_scale` `cardinal_number` Always null, since this information is not
applied to return data types in PostgreSQL  
`datetime_precision` `cardinal_number` Always null, since this information is
not applied to return data types in PostgreSQL  
`interval_type` `character_data` Always null, since this information is not
applied to return data types in PostgreSQL  
`interval_precision` `cardinal_number` Always null, since this information is
not applied to return data types in PostgreSQL  
`type_udt_catalog` `sql_identifier` Name of the database that the return data
type of the function is defined in (always the current database). Null for a
procedure.  
`type_udt_schema` `sql_identifier` Name of the schema that the return data
type of the function is defined in. Null for a procedure.  
`type_udt_name` `sql_identifier` Name of the return data type of the function.
Null for a procedure.  
`scope_catalog` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`scope_schema` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`scope_name` `sql_identifier` Applies to a feature not available in PostgreSQL  
`maximum_cardinality` `cardinal_number` Always null, because arrays always
have unlimited maximum cardinality in PostgreSQL  
`dtd_identifier` `sql_identifier` An identifier of the data type descriptor of
the return data type of this function, unique among the data type descriptors
pertaining to the function. This is mainly useful for joining with other
instances of such identifiers. (The specific format of the identifier is not
defined and not guaranteed to remain the same in future versions.)  
`routine_body` `character_data` If the function is an SQL function, then
`SQL`, else `EXTERNAL`.  
`routine_definition` `character_data` The source text of the function (null if
the function is not owned by a currently enabled role). (According to the SQL
standard, this column is only applicable if `routine_body` is `SQL`, but in
PostgreSQL it will contain whatever source text was specified when the
function was created.)  
`external_name` `character_data` If this function is a C function, then the
external name (link symbol) of the function; else null. (This works out to be
the same value that is shown in `routine_definition`.)  
`external_language` `character_data` The language the function is written in  
`parameter_style` `character_data` Always `GENERAL` (The SQL standard defines
other parameter styles, which are not available in PostgreSQL.)  
`is_deterministic` `yes_or_no` If the function is declared immutable (called
deterministic in the SQL standard), then `YES`, else `NO`. (You cannot query
the other volatility levels available in PostgreSQL through the information
schema.)  
`sql_data_access` `character_data` Always `MODIFIES`, meaning that the
function possibly modifies SQL data. This information is not useful for
PostgreSQL.  
`is_null_call` `yes_or_no` If the function automatically returns null if any
of its arguments are null, then `YES`, else `NO`. Null for a procedure.  
`sql_path` `character_data` Applies to a feature not available in PostgreSQL  
`schema_level_routine` `yes_or_no` Always `YES` (The opposite would be a
method of a user-defined type, which is a feature not available in
PostgreSQL.)  
`max_dynamic_result_sets` `cardinal_number` Applies to a feature not available
in PostgreSQL  
`is_user_defined_cast` `yes_or_no` Applies to a feature not available in
PostgreSQL  
`is_implicitly_invocable` `yes_or_no` Applies to a feature not available in
PostgreSQL  
`security_type` `character_data` If the function runs with the privileges of
the current user, then `INVOKER`, if the function runs with the privileges of
the user who defined it, then `DEFINER`.  
`to_sql_specific_catalog` `sql_identifier` Applies to a feature not available
in PostgreSQL  
`to_sql_specific_schema` `sql_identifier` Applies to a feature not available
in PostgreSQL  
`to_sql_specific_name` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`as_locator` `yes_or_no` Applies to a feature not available in PostgreSQL  
`created` `time_stamp` Applies to a feature not available in PostgreSQL  
`last_altered` `time_stamp` Applies to a feature not available in PostgreSQL  
`new_savepoint_level` `yes_or_no` Applies to a feature not available in
PostgreSQL  
`is_udt_dependent` `yes_or_no` Currently always `NO`. The alternative `YES`
applies to a feature not available in PostgreSQL.  
`result_cast_from_data_type` `character_data` Applies to a feature not
available in PostgreSQL  
`result_cast_as_locator` `yes_or_no` Applies to a feature not available in
PostgreSQL  
`result_cast_char_max_length` `cardinal_number` Applies to a feature not
available in PostgreSQL  
`result_cast_char_octet_length` `cardinal_number` Applies to a feature not
available in PostgreSQL  
`result_cast_char_set_catalog` `sql_identifier` Applies to a feature not
available in PostgreSQL  
`result_cast_char_set_schema` `sql_identifier` Applies to a feature not
available in PostgreSQL  
`result_cast_char_set_name` `sql_identifier` Applies to a feature not
available in PostgreSQL  
`result_cast_collation_catalog` `sql_identifier` Applies to a feature not
available in PostgreSQL  
`result_cast_collation_schema` `sql_identifier` Applies to a feature not
available in PostgreSQL  
`result_cast_collation_name` `sql_identifier` Applies to a feature not
available in PostgreSQL  
`result_cast_numeric_precision` `cardinal_number` Applies to a feature not
available in PostgreSQL  
`result_cast_numeric_precision_radix` `cardinal_number` Applies to a feature
not available in PostgreSQL  
`result_cast_numeric_scale` `cardinal_number` Applies to a feature not
available in PostgreSQL  
`result_cast_datetime_precision` `cardinal_number` Applies to a feature not
available in PostgreSQL  
`result_cast_interval_type` `character_data` Applies to a feature not
available in PostgreSQL  
`result_cast_interval_precision` `cardinal_number` Applies to a feature not
available in PostgreSQL  
`result_cast_type_udt_catalog` `sql_identifier` Applies to a feature not
available in PostgreSQL  
`result_cast_type_udt_schema` `sql_identifier` Applies to a feature not
available in PostgreSQL  
`result_cast_type_udt_name` `sql_identifier` Applies to a feature not
available in PostgreSQL  
`result_cast_scope_catalog` `sql_identifier` Applies to a feature not
available in PostgreSQL  
`result_cast_scope_schema` `sql_identifier` Applies to a feature not available
in PostgreSQL  
`result_cast_scope_name` `sql_identifier` Applies to a feature not available
in PostgreSQL  
`result_cast_maximum_cardinality` `cardinal_number` Applies to a feature not
available in PostgreSQL  
`result_cast_dtd_identifier` `sql_identifier` Applies to a feature not
available in PostgreSQL  
  
  

* * *

[Prev](infoschema-routine-table-usage.html "37.44. routine_table_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-schemata.html "37.46. schemata")  
---|---|---  
37.44. `routine_table_usage`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.46. `schemata`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-routines.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

