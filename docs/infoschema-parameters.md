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

Supported Versions: [Current](/docs/current/infoschema-parameters.html
"PostgreSQL 17 - 37.33. parameters") ([17](/docs/17/infoschema-parameters.html
"PostgreSQL 17 - 37.33. parameters")) / [16](/docs/16/infoschema-
parameters.html "PostgreSQL 16 - 37.33. parameters") /
[15](/docs/15/infoschema-parameters.html "PostgreSQL 15 - 37.33. parameters")
/ [14](/docs/14/infoschema-parameters.html "PostgreSQL 14 -
37.33. parameters") / [13](/docs/13/infoschema-parameters.html "PostgreSQL 13
- 37.33. parameters")

Development Versions: [18](/docs/18/infoschema-parameters.html "PostgreSQL 18
- 37.33. parameters") / [devel](/docs/devel/infoschema-parameters.html
"PostgreSQL devel - 37.33. parameters")

Unsupported versions: [12](/docs/12/infoschema-parameters.html "PostgreSQL 12
- 37.33. parameters") / [11](/docs/11/infoschema-parameters.html "PostgreSQL
11 - 37.33. parameters") / [10](/docs/10/infoschema-parameters.html
"PostgreSQL 10 - 37.33. parameters") / [9.6](/docs/9.6/infoschema-
parameters.html "PostgreSQL 9.6 - 37.33. parameters") /
[9.5](/docs/9.5/infoschema-parameters.html "PostgreSQL 9.5 -
37.33. parameters") / [9.4](/docs/9.4/infoschema-parameters.html "PostgreSQL
9.4 - 37.33. parameters") / [9.3](/docs/9.3/infoschema-parameters.html
"PostgreSQL 9.3 - 37.33. parameters") / [9.2](/docs/9.2/infoschema-
parameters.html "PostgreSQL 9.2 - 37.33. parameters") /
[9.1](/docs/9.1/infoschema-parameters.html "PostgreSQL 9.1 -
37.33. parameters") / [9.0](/docs/9.0/infoschema-parameters.html "PostgreSQL
9.0 - 37.33. parameters") / [8.4](/docs/8.4/infoschema-parameters.html
"PostgreSQL 8.4 - 37.33. parameters") / [8.3](/docs/8.3/infoschema-
parameters.html "PostgreSQL 8.3 - 37.33. parameters") /
[8.2](/docs/8.2/infoschema-parameters.html "PostgreSQL 8.2 -
37.33. parameters") / [8.1](/docs/8.1/infoschema-parameters.html "PostgreSQL
8.1 - 37.33. parameters") / [8.0](/docs/8.0/infoschema-parameters.html
"PostgreSQL 8.0 - 37.33. parameters") / [7.4](/docs/7.4/infoschema-
parameters.html "PostgreSQL 7.4 - 37.33. parameters")

__

37.33. `parameters`  
---  
[Prev](infoschema-key-column-usage.html "37.32. key_column_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-referential-constraints.html "37.34. referential_constraints")  
  
* * *

## 37.33. `parameters` #

The view `parameters` contains information about the parameters (arguments) of
all functions in the current database. Only those functions are shown that the
current user has access to (by way of being the owner or having some
privilege).

**Table  37.31. `parameters` Columns**

Column Type Description  
---  
`specific_catalog` `sql_identifier` Name of the database containing the
function (always the current database)  
`specific_schema` `sql_identifier` Name of the schema containing the function  
`specific_name` `sql_identifier` The “specific name” of the function. See
[Section 37.45](infoschema-routines.html "37.45. routines") for more
information.  
`ordinal_position` `cardinal_number` Ordinal position of the parameter in the
argument list of the function (count starts at 1)  
`parameter_mode` `character_data` `IN` for input parameter, `OUT` for output
parameter, and `INOUT` for input/output parameter.  
`is_result` `yes_or_no` Applies to a feature not available in PostgreSQL  
`as_locator` `yes_or_no` Applies to a feature not available in PostgreSQL  
`parameter_name` `sql_identifier` Name of the parameter, or null if the
parameter has no name  
`data_type` `character_data` Data type of the parameter, if it is a built-in
type, or `ARRAY` if it is some array (in that case, see the view
`element_types`), else `USER-DEFINED` (in that case, the type is identified in
`udt_name` and associated columns).  
`character_maximum_length` `cardinal_number` Always null, since this
information is not applied to parameter data types in PostgreSQL  
`character_octet_length` `cardinal_number` Always null, since this information
is not applied to parameter data types in PostgreSQL  
`character_set_catalog` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`character_set_schema` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`character_set_name` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`collation_catalog` `sql_identifier` Always null, since this information is
not applied to parameter data types in PostgreSQL  
`collation_schema` `sql_identifier` Always null, since this information is not
applied to parameter data types in PostgreSQL  
`collation_name` `sql_identifier` Always null, since this information is not
applied to parameter data types in PostgreSQL  
`numeric_precision` `cardinal_number` Always null, since this information is
not applied to parameter data types in PostgreSQL  
`numeric_precision_radix` `cardinal_number` Always null, since this
information is not applied to parameter data types in PostgreSQL  
`numeric_scale` `cardinal_number` Always null, since this information is not
applied to parameter data types in PostgreSQL  
`datetime_precision` `cardinal_number` Always null, since this information is
not applied to parameter data types in PostgreSQL  
`interval_type` `character_data` Always null, since this information is not
applied to parameter data types in PostgreSQL  
`interval_precision` `cardinal_number` Always null, since this information is
not applied to parameter data types in PostgreSQL  
`udt_catalog` `sql_identifier` Name of the database that the data type of the
parameter is defined in (always the current database)  
`udt_schema` `sql_identifier` Name of the schema that the data type of the
parameter is defined in  
`udt_name` `sql_identifier` Name of the data type of the parameter  
`scope_catalog` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`scope_schema` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`scope_name` `sql_identifier` Applies to a feature not available in PostgreSQL  
`maximum_cardinality` `cardinal_number` Always null, because arrays always
have unlimited maximum cardinality in PostgreSQL  
`dtd_identifier` `sql_identifier` An identifier of the data type descriptor of
the parameter, unique among the data type descriptors pertaining to the
function. This is mainly useful for joining with other instances of such
identifiers. (The specific format of the identifier is not defined and not
guaranteed to remain the same in future versions.)  
`parameter_default` `character_data` The default expression of the parameter,
or null if none or if the function is not owned by a currently enabled role.  
  
  

* * *

[Prev](infoschema-key-column-usage.html "37.32. key_column_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-referential-constraints.html "37.34. referential_constraints")  
---|---|---  
37.32. `key_column_usage`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.34. `referential_constraints`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-parameters.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

