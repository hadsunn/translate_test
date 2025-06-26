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

Supported Versions: [Current](/docs/current/infoschema-domains.html
"PostgreSQL 17 - 37.23. domains") ([17](/docs/17/infoschema-domains.html
"PostgreSQL 17 - 37.23. domains")) / [16](/docs/16/infoschema-domains.html
"PostgreSQL 16 - 37.23. domains") / [15](/docs/15/infoschema-domains.html
"PostgreSQL 15 - 37.23. domains") / [14](/docs/14/infoschema-domains.html
"PostgreSQL 14 - 37.23. domains") / [13](/docs/13/infoschema-domains.html
"PostgreSQL 13 - 37.23. domains")

Development Versions: [18](/docs/18/infoschema-domains.html "PostgreSQL 18 -
37.23. domains") / [devel](/docs/devel/infoschema-domains.html "PostgreSQL
devel - 37.23. domains")

Unsupported versions: [12](/docs/12/infoschema-domains.html "PostgreSQL 12 -
37.23. domains") / [11](/docs/11/infoschema-domains.html "PostgreSQL 11 -
37.23. domains") / [10](/docs/10/infoschema-domains.html "PostgreSQL 10 -
37.23. domains") / [9.6](/docs/9.6/infoschema-domains.html "PostgreSQL 9.6 -
37.23. domains") / [9.5](/docs/9.5/infoschema-domains.html "PostgreSQL 9.5 -
37.23. domains") / [9.4](/docs/9.4/infoschema-domains.html "PostgreSQL 9.4 -
37.23. domains") / [9.3](/docs/9.3/infoschema-domains.html "PostgreSQL 9.3 -
37.23. domains") / [9.2](/docs/9.2/infoschema-domains.html "PostgreSQL 9.2 -
37.23. domains") / [9.1](/docs/9.1/infoschema-domains.html "PostgreSQL 9.1 -
37.23. domains") / [9.0](/docs/9.0/infoschema-domains.html "PostgreSQL 9.0 -
37.23. domains") / [8.4](/docs/8.4/infoschema-domains.html "PostgreSQL 8.4 -
37.23. domains") / [8.3](/docs/8.3/infoschema-domains.html "PostgreSQL 8.3 -
37.23. domains") / [8.2](/docs/8.2/infoschema-domains.html "PostgreSQL 8.2 -
37.23. domains") / [8.1](/docs/8.1/infoschema-domains.html "PostgreSQL 8.1 -
37.23. domains") / [8.0](/docs/8.0/infoschema-domains.html "PostgreSQL 8.0 -
37.23. domains") / [7.4](/docs/7.4/infoschema-domains.html "PostgreSQL 7.4 -
37.23. domains")

__

37.23. `domains`  
---  
[Prev](infoschema-domain-udt-usage.html "37.22. domain_udt_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-element-types.html "37.24. element_types")  
  
* * *

## 37.23. `domains` #

The view `domains` contains all [](glossary.html#GLOSSARY-
DOMAIN)[domains](glossary.html#GLOSSARY-DOMAIN "Domain") defined in the
current database. Only those domains are shown that the current user has
access to (by way of being the owner or having some privilege).

**Table  37.21. `domains` Columns**

Column Type Description  
---  
`domain_catalog` `sql_identifier` Name of the database that contains the
domain (always the current database)  
`domain_schema` `sql_identifier` Name of the schema that contains the domain  
`domain_name` `sql_identifier` Name of the domain  
`data_type` `character_data` Data type of the domain, if it is a built-in
type, or `ARRAY` if it is some array (in that case, see the view
`element_types`), else `USER-DEFINED` (in that case, the type is identified in
`udt_name` and associated columns).  
`character_maximum_length` `cardinal_number` If the domain has a character or
bit string type, the declared maximum length; null for all other data types or
if no maximum length was declared.  
`character_octet_length` `cardinal_number` If the domain has a character type,
the maximum possible length in octets (bytes) of a datum; null for all other
data types. The maximum octet length depends on the declared character maximum
length (see above) and the server encoding.  
`character_set_catalog` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`character_set_schema` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`character_set_name` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`collation_catalog` `sql_identifier` Name of the database containing the
collation of the domain (always the current database), null if default or the
data type of the domain is not collatable  
`collation_schema` `sql_identifier` Name of the schema containing the
collation of the domain, null if default or the data type of the domain is not
collatable  
`collation_name` `sql_identifier` Name of the collation of the domain, null if
default or the data type of the domain is not collatable  
`numeric_precision` `cardinal_number` If the domain has a numeric type, this
column contains the (declared or implicit) precision of the type for this
domain. The precision indicates the number of significant digits. It can be
expressed in decimal (base 10) or binary (base 2) terms, as specified in the
column `numeric_precision_radix`. For all other data types, this column is
null.  
`numeric_precision_radix` `cardinal_number` If the domain has a numeric type,
this column indicates in which base the values in the columns
`numeric_precision` and `numeric_scale` are expressed. The value is either 2
or 10. For all other data types, this column is null.  
`numeric_scale` `cardinal_number` If the domain has an exact numeric type,
this column contains the (declared or implicit) scale of the type for this
domain. The scale indicates the number of significant digits to the right of
the decimal point. It can be expressed in decimal (base 10) or binary (base 2)
terms, as specified in the column `numeric_precision_radix`. For all other
data types, this column is null.  
`datetime_precision` `cardinal_number` If `data_type` identifies a date, time,
timestamp, or interval type, this column contains the (declared or implicit)
fractional seconds precision of the type for this domain, that is, the number
of decimal digits maintained following the decimal point in the seconds value.
For all other data types, this column is null.  
`interval_type` `character_data` If `data_type` identifies an interval type,
this column contains the specification which fields the intervals include for
this domain, e.g., `YEAR TO MONTH`, `DAY TO SECOND`, etc. If no field
restrictions were specified (that is, the interval accepts all fields), and
for all other data types, this field is null.  
`interval_precision` `cardinal_number` Applies to a feature not available in
PostgreSQL (see `datetime_precision` for the fractional seconds precision of
interval type domains)  
`domain_default` `character_data` Default expression of the domain  
`udt_catalog` `sql_identifier` Name of the database that the domain data type
is defined in (always the current database)  
`udt_schema` `sql_identifier` Name of the schema that the domain data type is
defined in  
`udt_name` `sql_identifier` Name of the domain data type  
`scope_catalog` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`scope_schema` `sql_identifier` Applies to a feature not available in
PostgreSQL  
`scope_name` `sql_identifier` Applies to a feature not available in PostgreSQL  
`maximum_cardinality` `cardinal_number` Always null, because arrays always
have unlimited maximum cardinality in PostgreSQL  
`dtd_identifier` `sql_identifier` An identifier of the data type descriptor of
the domain, unique among the data type descriptors pertaining to the domain
(which is trivial, because a domain only contains one data type descriptor).
This is mainly useful for joining with other instances of such identifiers.
(The specific format of the identifier is not defined and not guaranteed to
remain the same in future versions.)  
  
  

* * *

[Prev](infoschema-domain-udt-usage.html "37.22. domain_udt_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-element-types.html "37.24. element_types")  
---|---|---  
37.22. `domain_udt_usage`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.24. `element_types`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-domains.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

