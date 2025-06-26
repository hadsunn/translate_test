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

Supported Versions: [Current](/docs/current/infoschema-columns.html
"PostgreSQL 17 - 37.17. columns") ([17](/docs/17/infoschema-columns.html
"PostgreSQL 17 - 37.17. columns")) / [16](/docs/16/infoschema-columns.html
"PostgreSQL 16 - 37.17. columns") / [15](/docs/15/infoschema-columns.html
"PostgreSQL 15 - 37.17. columns") / [14](/docs/14/infoschema-columns.html
"PostgreSQL 14 - 37.17. columns") / [13](/docs/13/infoschema-columns.html
"PostgreSQL 13 - 37.17. columns")

Development Versions: [18](/docs/18/infoschema-columns.html "PostgreSQL 18 -
37.17. columns") / [devel](/docs/devel/infoschema-columns.html "PostgreSQL
devel - 37.17. columns")

Unsupported versions: [12](/docs/12/infoschema-columns.html "PostgreSQL 12 -
37.17. columns") / [11](/docs/11/infoschema-columns.html "PostgreSQL 11 -
37.17. columns") / [10](/docs/10/infoschema-columns.html "PostgreSQL 10 -
37.17. columns") / [9.6](/docs/9.6/infoschema-columns.html "PostgreSQL 9.6 -
37.17. columns") / [9.5](/docs/9.5/infoschema-columns.html "PostgreSQL 9.5 -
37.17. columns") / [9.4](/docs/9.4/infoschema-columns.html "PostgreSQL 9.4 -
37.17. columns") / [9.3](/docs/9.3/infoschema-columns.html "PostgreSQL 9.3 -
37.17. columns") / [9.2](/docs/9.2/infoschema-columns.html "PostgreSQL 9.2 -
37.17. columns") / [9.1](/docs/9.1/infoschema-columns.html "PostgreSQL 9.1 -
37.17. columns") / [9.0](/docs/9.0/infoschema-columns.html "PostgreSQL 9.0 -
37.17. columns") / [8.4](/docs/8.4/infoschema-columns.html "PostgreSQL 8.4 -
37.17. columns") / [8.3](/docs/8.3/infoschema-columns.html "PostgreSQL 8.3 -
37.17. columns") / [8.2](/docs/8.2/infoschema-columns.html "PostgreSQL 8.2 -
37.17. columns") / [8.1](/docs/8.1/infoschema-columns.html "PostgreSQL 8.1 -
37.17. columns") / [8.0](/docs/8.0/infoschema-columns.html "PostgreSQL 8.0 -
37.17. columns") / [7.4](/docs/7.4/infoschema-columns.html "PostgreSQL 7.4 -
37.17. columns")

__

37.17. `columns`  
---  
[Prev](infoschema-column-udt-usage.html "37.16. column_udt_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-constraint-column-usage.html "37.18. constraint_column_usage")  
  
* * *

## 37.17. `columns` #

The view `columns` contains information about all table columns (or view
columns) in the database. System columns (`ctid`, etc.) are not included. Only
those columns are shown that the current user has access to (by way of being
the owner or having some privilege).

**Table  37.15. `columns` Columns**

Column Type Description  
---  
`table_catalog` `sql_identifier` Name of the database containing the table
(always the current database)  
`table_schema` `sql_identifier` Name of the schema containing the table  
`table_name` `sql_identifier` Name of the table  
`column_name` `sql_identifier` Name of the column  
`ordinal_position` `cardinal_number` Ordinal position of the column within the
table (count starts at 1)  
`column_default` `character_data` Default expression of the column  
`is_nullable` `yes_or_no` `YES` if the column is possibly nullable, `NO` if it
is known not nullable. A not-null constraint is one way a column can be known
not nullable, but there can be others.  
`data_type` `character_data` Data type of the column, if it is a built-in
type, or `ARRAY` if it is some array (in that case, see the view
`element_types`), else `USER-DEFINED` (in that case, the type is identified in
`udt_name` and associated columns). If the column is based on a domain, this
column refers to the type underlying the domain (and the domain is identified
in `domain_name` and associated columns).  
`character_maximum_length` `cardinal_number` If `data_type` identifies a
character or bit string type, the declared maximum length; null for all other
data types or if no maximum length was declared.  
`character_octet_length` `cardinal_number` If `data_type` identifies a
character type, the maximum possible length in octets (bytes) of a datum; null
for all other data types. The maximum octet length depends on the declared
character maximum length (see above) and the server encoding.  
`numeric_precision` `cardinal_number` If `data_type` identifies a numeric
type, this column contains the (declared or implicit) precision of the type
for this column. The precision indicates the number of significant digits. It
can be expressed in decimal (base 10) or binary (base 2) terms, as specified
in the column `numeric_precision_radix`. For all other data types, this column
is null.  
`numeric_precision_radix` `cardinal_number` If `data_type` identifies a
numeric type, this column indicates in which base the values in the columns
`numeric_precision` and `numeric_scale` are expressed. The value is either 2
or 10. For all other data types, this column is null.  
`numeric_scale` `cardinal_number` If `data_type` identifies an exact numeric
type, this column contains the (declared or implicit) scale of the type for
this column. The scale indicates the number of significant digits to the right
of the decimal point. It can be expressed in decimal (base 10) or binary (base
2) terms, as specified in the column `numeric_precision_radix`. For all other
data types, this column is null.  
`datetime_precision` `cardinal_number` If `data_type` identifies a date, time,
timestamp, or interval type, this column contains the (declared or implicit)
fractional seconds precision of the type for this column, that is, the number
of decimal digits maintained following the decimal point in the seconds value.
For all other data types, this column is null.  
`interval_type` `character_data` If `data_type` identifies an interval type,
this column contains the specification which fields the intervals include for
this column, e.g., `YEAR TO MONTH`, `DAY TO SECOND`, etc. If no field
restrictions were specified (that is, the interval accepts all fields), and
for all other data types, this field is null.  
`interval_precision` `cardinal_number` Applies to a feature not available in
PostgreSQL (see `datetime_precision` for the fractional seconds precision of
interval type columns)  
`character_set_catalog` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`character_set_schema` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`character_set_name` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`collation_catalog` `sql_identifier` Name of the database containing the
collation of the column (always the current database), null if default or the
data type of the column is not collatable  
`collation_schema` `sql_identifier` Name of the schema containing the
collation of the column, null if default or the data type of the column is not
collatable  
`collation_name` `sql_identifier` Name of the collation of the column, null if
default or the data type of the column is not collatable  
`domain_catalog` `sql_identifier` If the column has a domain type, the name of
the database that the domain is defined in (always the current database), else
null.  
`domain_schema` `sql_identifier` If the column has a domain type, the name of
the schema that the domain is defined in, else null.  
`domain_name` `sql_identifier` If the column has a domain type, the name of
the domain, else null.  
`udt_catalog` `sql_identifier` Name of the database that the column data type
(the underlying type of the domain, if applicable) is defined in (always the
current database)  
`udt_schema` `sql_identifier` Name of the schema that the column data type
(the underlying type of the domain, if applicable) is defined in  
`udt_name` `sql_identifier` Name of the column data type (the underlying type
of the domain, if applicable)  
`scope_catalog` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`scope_schema` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`scope_name` `sql_identifier` Applies to a feature not available in PostgreSQL  
`maximum_cardinality` `cardinal_number` Always null, because arrays always
have unlimited maximum cardinality in PostgreSQL  
`dtd_identifier` `sql_identifier` An identifier of the data type descriptor of
the column, unique among the data type descriptors pertaining to the table.
This is mainly useful for joining with other instances of such identifiers.
(The specific format of the identifier is not defined and not guaranteed to
remain the same in future versions.)  
`is_self_referencing` `yes_or_no` Applies to a feature not available in
PostgreSQL  
`is_identity` `yes_or_no` If the column is an identity column, then `YES`,
else `NO`.  
`identity_generation` `character_data` If the column is an identity column,
then `ALWAYS` or `BY DEFAULT`, reflecting the definition of the column.  
`identity_start` `character_data` If the column is an identity column, then
the start value of the internal sequence, else null.  
`identity_increment` `character_data` If the column is an identity column,
then the increment of the internal sequence, else null.  
`identity_maximum` `character_data` If the column is an identity column, then
the maximum value of the internal sequence, else null.  
`identity_minimum` `character_data` If the column is an identity column, then
the minimum value of the internal sequence, else null.  
`identity_cycle` `yes_or_no` If the column is an identity column, then `YES`
if the internal sequence cycles or `NO` if it does not; otherwise null.  
`is_generated` `character_data` If the column is a generated column, then
`ALWAYS`, else `NEVER`.  
`generation_expression` `character_data` If the column is a generated column,
then the generation expression, else null.  
`is_updatable` `yes_or_no` `YES` if the column is updatable, `NO` if not
(Columns in base tables are always updatable, columns in views not
necessarily)  
  
  

Since data types can be defined in a variety of ways in SQL, and PostgreSQL
contains additional ways to define data types, their representation in the
information schema can be somewhat difficult. The column `data_type` is
supposed to identify the underlying built-in type of the column. In
PostgreSQL, this means that the type is defined in the system catalog schema
`pg_catalog`. This column might be useful if the application can handle the
well-known built-in types specially (for example, format the numeric types
differently or use the data in the precision columns). The columns `udt_name`,
`udt_schema`, and `udt_catalog` always identify the underlying data type of
the column, even if the column is based on a domain. (Since PostgreSQL treats
built-in types like user-defined types, built-in types appear here as well.
This is an extension of the SQL standard.) These columns should be used if an
application wants to process data differently according to the type, because
in that case it wouldn't matter if the column is really based on a domain. If
the column is based on a domain, the identity of the domain is stored in the
columns `domain_name`, `domain_schema`, and `domain_catalog`. If you want to
pair up columns with their associated data types and treat domains as separate
types, you could write `coalesce(domain_name, udt_name)`, etc.

* * *

[Prev](infoschema-column-udt-usage.html "37.16. column_udt_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-constraint-column-usage.html "37.18. constraint_column_usage")  
---|---|---  
37.16. `column_udt_usage`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.18. `constraint_column_usage`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-columns.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

