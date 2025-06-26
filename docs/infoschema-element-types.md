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

Supported Versions: [Current](/docs/current/infoschema-element-types.html
"PostgreSQL 17 - 37.24. element_types") ([17](/docs/17/infoschema-element-
types.html "PostgreSQL 17 - 37.24. element_types")) /
[16](/docs/16/infoschema-element-types.html "PostgreSQL 16 -
37.24. element_types") / [15](/docs/15/infoschema-element-types.html
"PostgreSQL 15 - 37.24. element_types") / [14](/docs/14/infoschema-element-
types.html "PostgreSQL 14 - 37.24. element_types") / [13](/docs/13/infoschema-
element-types.html "PostgreSQL 13 - 37.24. element_types")

Development Versions: [18](/docs/18/infoschema-element-types.html "PostgreSQL
18 - 37.24. element_types") / [devel](/docs/devel/infoschema-element-
types.html "PostgreSQL devel - 37.24. element_types")

Unsupported versions: [12](/docs/12/infoschema-element-types.html "PostgreSQL
12 - 37.24. element_types") / [11](/docs/11/infoschema-element-types.html
"PostgreSQL 11 - 37.24. element_types") / [10](/docs/10/infoschema-element-
types.html "PostgreSQL 10 - 37.24. element_types") /
[9.6](/docs/9.6/infoschema-element-types.html "PostgreSQL 9.6 -
37.24. element_types") / [9.5](/docs/9.5/infoschema-element-types.html
"PostgreSQL 9.5 - 37.24. element_types") / [9.4](/docs/9.4/infoschema-element-
types.html "PostgreSQL 9.4 - 37.24. element_types") /
[9.3](/docs/9.3/infoschema-element-types.html "PostgreSQL 9.3 -
37.24. element_types") / [9.2](/docs/9.2/infoschema-element-types.html
"PostgreSQL 9.2 - 37.24. element_types") / [9.1](/docs/9.1/infoschema-element-
types.html "PostgreSQL 9.1 - 37.24. element_types") /
[9.0](/docs/9.0/infoschema-element-types.html "PostgreSQL 9.0 -
37.24. element_types") / [8.4](/docs/8.4/infoschema-element-types.html
"PostgreSQL 8.4 - 37.24. element_types") / [8.3](/docs/8.3/infoschema-element-
types.html "PostgreSQL 8.3 - 37.24. element_types") /
[8.2](/docs/8.2/infoschema-element-types.html "PostgreSQL 8.2 -
37.24. element_types") / [8.1](/docs/8.1/infoschema-element-types.html
"PostgreSQL 8.1 - 37.24. element_types") / [8.0](/docs/8.0/infoschema-element-
types.html "PostgreSQL 8.0 - 37.24. element_types") /
[7.4](/docs/7.4/infoschema-element-types.html "PostgreSQL 7.4 -
37.24. element_types")

__

37.24. `element_types`  
---  
[Prev](infoschema-domains.html "37.23. domains")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-enabled-roles.html "37.25. enabled_roles")  
  
* * *

## 37.24. `element_types` #

The view `element_types` contains the data type descriptors of the elements of
arrays. When a table column, composite-type attribute, domain, function
parameter, or function return value is defined to be of an array type, the
respective information schema view only contains `ARRAY` in the column
`data_type`. To obtain information on the element type of the array, you can
join the respective view with this view. For example, to show the columns of a
table with data types and array element types, if applicable, you could do:

    
    
    SELECT c.column_name, c.data_type, e.data_type AS element_type
    FROM information_schema.columns c LEFT JOIN information_schema.element_types e
         ON ((c.table_catalog, c.table_schema, c.table_name, 'TABLE', c.dtd_identifier)
           = (e.object_catalog, e.object_schema, e.object_name, e.object_type, e.collection_type_identifier))
    WHERE c.table_schema = '...' AND c.table_name = '...'
    ORDER BY c.ordinal_position;
    

This view only includes objects that the current user has access to, by way of
being the owner or having some privilege.

**Table  37.22. `element_types` Columns**

Column Type Description  
---  
`object_catalog` `sql_identifier` Name of the database that contains the
object that uses the array being described (always the current database)  
`object_schema` `sql_identifier` Name of the schema that contains the object
that uses the array being described  
`object_name` `sql_identifier` Name of the object that uses the array being
described  
`object_type` `character_data` The type of the object that uses the array
being described: one of `TABLE` (the array is used by a column of that table),
`USER-DEFINED TYPE` (the array is used by an attribute of that composite
type), `DOMAIN` (the array is used by that domain), `ROUTINE` (the array is
used by a parameter or the return data type of that function).  
`collection_type_identifier` `sql_identifier` The identifier of the data type
descriptor of the array being described. Use this to join with the
`dtd_identifier` columns of other information schema views.  
`data_type` `character_data` Data type of the array elements, if it is a
built-in type, else `USER-DEFINED` (in that case, the type is identified in
`udt_name` and associated columns).  
`character_maximum_length` `cardinal_number` Always null, since this
information is not applied to array element data types in PostgreSQL  
`character_octet_length` `cardinal_number` Always null, since this information
is not applied to array element data types in PostgreSQL  
`character_set_catalog` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`character_set_schema` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`character_set_name` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`collation_catalog` `sql_identifier` Name of the database containing the
collation of the element type (always the current database), null if default
or the data type of the element is not collatable  
`collation_schema` `sql_identifier` Name of the schema containing the
collation of the element type, null if default or the data type of the element
is not collatable  
`collation_name` `sql_identifier` Name of the collation of the element type,
null if default or the data type of the element is not collatable  
`numeric_precision` `cardinal_number` Always null, since this information is
not applied to array element data types in PostgreSQL  
`numeric_precision_radix` `cardinal_number` Always null, since this
information is not applied to array element data types in PostgreSQL  
`numeric_scale` `cardinal_number` Always null, since this information is not
applied to array element data types in PostgreSQL  
`datetime_precision` `cardinal_number` Always null, since this information is
not applied to array element data types in PostgreSQL  
`interval_type` `character_data` Always null, since this information is not
applied to array element data types in PostgreSQL  
`interval_precision` `cardinal_number` Always null, since this information is
not applied to array element data types in PostgreSQL  
`domain_default` `character_data` Not yet implemented  
`udt_catalog` `sql_identifier` Name of the database that the data type of the
elements is defined in (always the current database)  
`udt_schema` `sql_identifier` Name of the schema that the data type of the
elements is defined in  
`udt_name` `sql_identifier` Name of the data type of the elements  
`scope_catalog` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`scope_schema` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`scope_name` `sql_identifier` Applies to a feature not available in PostgreSQL  
`maximum_cardinality` `cardinal_number` Always null, because arrays always
have unlimited maximum cardinality in PostgreSQL  
`dtd_identifier` `sql_identifier` An identifier of the data type descriptor of
the element. This is currently not useful.  
  
  

* * *

[Prev](infoschema-domains.html "37.23. domains")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-enabled-roles.html "37.25. enabled_roles")  
---|---|---  
37.23. `domains`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.25. `enabled_roles`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-element-
types.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

