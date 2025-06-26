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

Supported Versions: [Current](/docs/current/infoschema-data-type-
privileges.html "PostgreSQL 17 - 37.20. data_type_privileges")
([17](/docs/17/infoschema-data-type-privileges.html "PostgreSQL 17 -
37.20. data_type_privileges")) / [16](/docs/16/infoschema-data-type-
privileges.html "PostgreSQL 16 - 37.20. data_type_privileges") /
[15](/docs/15/infoschema-data-type-privileges.html "PostgreSQL 15 -
37.20. data_type_privileges") / [14](/docs/14/infoschema-data-type-
privileges.html "PostgreSQL 14 - 37.20. data_type_privileges") /
[13](/docs/13/infoschema-data-type-privileges.html "PostgreSQL 13 -
37.20. data_type_privileges")

Development Versions: [18](/docs/18/infoschema-data-type-privileges.html
"PostgreSQL 18 - 37.20. data_type_privileges") /
[devel](/docs/devel/infoschema-data-type-privileges.html "PostgreSQL devel -
37.20. data_type_privileges")

Unsupported versions: [12](/docs/12/infoschema-data-type-privileges.html
"PostgreSQL 12 - 37.20. data_type_privileges") / [11](/docs/11/infoschema-
data-type-privileges.html "PostgreSQL 11 - 37.20. data_type_privileges") /
[10](/docs/10/infoschema-data-type-privileges.html "PostgreSQL 10 -
37.20. data_type_privileges") / [9.6](/docs/9.6/infoschema-data-type-
privileges.html "PostgreSQL 9.6 - 37.20. data_type_privileges") /
[9.5](/docs/9.5/infoschema-data-type-privileges.html "PostgreSQL 9.5 -
37.20. data_type_privileges") / [9.4](/docs/9.4/infoschema-data-type-
privileges.html "PostgreSQL 9.4 - 37.20. data_type_privileges") /
[9.3](/docs/9.3/infoschema-data-type-privileges.html "PostgreSQL 9.3 -
37.20. data_type_privileges") / [9.2](/docs/9.2/infoschema-data-type-
privileges.html "PostgreSQL 9.2 - 37.20. data_type_privileges") /
[9.1](/docs/9.1/infoschema-data-type-privileges.html "PostgreSQL 9.1 -
37.20. data_type_privileges") / [9.0](/docs/9.0/infoschema-data-type-
privileges.html "PostgreSQL 9.0 - 37.20. data_type_privileges") /
[8.4](/docs/8.4/infoschema-data-type-privileges.html "PostgreSQL 8.4 -
37.20. data_type_privileges") / [8.3](/docs/8.3/infoschema-data-type-
privileges.html "PostgreSQL 8.3 - 37.20. data_type_privileges") /
[8.2](/docs/8.2/infoschema-data-type-privileges.html "PostgreSQL 8.2 -
37.20. data_type_privileges") / [8.1](/docs/8.1/infoschema-data-type-
privileges.html "PostgreSQL 8.1 - 37.20. data_type_privileges") /
[8.0](/docs/8.0/infoschema-data-type-privileges.html "PostgreSQL 8.0 -
37.20. data_type_privileges") / [7.4](/docs/7.4/infoschema-data-type-
privileges.html "PostgreSQL 7.4 - 37.20. data_type_privileges")

__

37.20. `data_type_privileges`  
---  
[Prev](infoschema-constraint-table-usage.html "37.19. constraint_table_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") | Chapter 37. The Information Schema | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](infoschema-domain-constraints.html "37.21. domain_constraints")  
  
* * *

## 37.20. `data_type_privileges` #

The view `data_type_privileges` identifies all data type descriptors that the
current user has access to, by way of being the owner of the described object
or having some privilege for it. A data type descriptor is generated whenever
a data type is used in the definition of a table column, a domain, or a
function (as parameter or return type) and stores some information about how
the data type is used in that instance (for example, the declared maximum
length, if applicable). Each data type descriptor is assigned an arbitrary
identifier that is unique among the data type descriptor identifiers assigned
for one object (table, domain, function). This view is probably not useful for
applications, but it is used to define some other views in the information
schema.

**Table  37.18. `data_type_privileges` Columns**

Column Type Description  
---  
`object_catalog` `sql_identifier` Name of the database that contains the
described object (always the current database)  
`object_schema` `sql_identifier` Name of the schema that contains the
described object  
`object_name` `sql_identifier` Name of the described object  
`object_type` `character_data` The type of the described object: one of
`TABLE` (the data type descriptor pertains to a column of that table),
`DOMAIN` (the data type descriptors pertains to that domain), `ROUTINE` (the
data type descriptor pertains to a parameter or the return data type of that
function).  
`dtd_identifier` `sql_identifier` The identifier of the data type descriptor,
which is unique among the data type descriptors for that same object.  
  
  

* * *

[Prev](infoschema-constraint-table-usage.html "37.19. constraint_table_usage")  | [Up](information-schema.html "Chapter 37. The Information Schema") |  [Next](infoschema-domain-constraints.html "37.21. domain_constraints")  
---|---|---  
37.19. `constraint_table_usage`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  37.21. `domain_constraints`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/infoschema-data-type-
privileges.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

