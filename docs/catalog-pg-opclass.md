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

Supported Versions: [Current](/docs/current/catalog-pg-opclass.html
"PostgreSQL 17 - 53.33. pg_opclass") ([17](/docs/17/catalog-pg-opclass.html
"PostgreSQL 17 - 53.33. pg_opclass")) / [16](/docs/16/catalog-pg-opclass.html
"PostgreSQL 16 - 53.33. pg_opclass") / [15](/docs/15/catalog-pg-opclass.html
"PostgreSQL 15 - 53.33. pg_opclass") / [14](/docs/14/catalog-pg-opclass.html
"PostgreSQL 14 - 53.33. pg_opclass") / [13](/docs/13/catalog-pg-opclass.html
"PostgreSQL 13 - 53.33. pg_opclass")

Development Versions: [18](/docs/18/catalog-pg-opclass.html "PostgreSQL 18 -
53.33. pg_opclass") / [devel](/docs/devel/catalog-pg-opclass.html "PostgreSQL
devel - 53.33. pg_opclass")

Unsupported versions: [12](/docs/12/catalog-pg-opclass.html "PostgreSQL 12 -
53.33. pg_opclass") / [11](/docs/11/catalog-pg-opclass.html "PostgreSQL 11 -
53.33. pg_opclass") / [10](/docs/10/catalog-pg-opclass.html "PostgreSQL 10 -
53.33. pg_opclass") / [9.6](/docs/9.6/catalog-pg-opclass.html "PostgreSQL 9.6
- 53.33. pg_opclass") / [9.5](/docs/9.5/catalog-pg-opclass.html "PostgreSQL
9.5 - 53.33. pg_opclass") / [9.4](/docs/9.4/catalog-pg-opclass.html
"PostgreSQL 9.4 - 53.33. pg_opclass") / [9.3](/docs/9.3/catalog-pg-
opclass.html "PostgreSQL 9.3 - 53.33. pg_opclass") / [9.2](/docs/9.2/catalog-
pg-opclass.html "PostgreSQL 9.2 - 53.33. pg_opclass") /
[9.1](/docs/9.1/catalog-pg-opclass.html "PostgreSQL 9.1 - 53.33. pg_opclass")
/ [9.0](/docs/9.0/catalog-pg-opclass.html "PostgreSQL 9.0 -
53.33. pg_opclass") / [8.4](/docs/8.4/catalog-pg-opclass.html "PostgreSQL 8.4
- 53.33. pg_opclass") / [8.3](/docs/8.3/catalog-pg-opclass.html "PostgreSQL
8.3 - 53.33. pg_opclass") / [8.2](/docs/8.2/catalog-pg-opclass.html
"PostgreSQL 8.2 - 53.33. pg_opclass") / [8.1](/docs/8.1/catalog-pg-
opclass.html "PostgreSQL 8.1 - 53.33. pg_opclass") / [8.0](/docs/8.0/catalog-
pg-opclass.html "PostgreSQL 8.0 - 53.33. pg_opclass") /
[7.4](/docs/7.4/catalog-pg-opclass.html "PostgreSQL 7.4 - 53.33. pg_opclass")
/ [7.3](/docs/7.3/catalog-pg-opclass.html "PostgreSQL 7.3 -
53.33. pg_opclass")

__

53.33. `pg_opclass`  
---  
[Prev](catalog-pg-namespace.html "53.32. pg_namespace")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-operator.html "53.34. pg_operator")  
  
* * *

## 53.33. `pg_opclass` #

The catalog `pg_opclass` defines index access method operator classes. Each
operator class defines semantics for index columns of a particular data type
and a particular index access method. An operator class essentially specifies
that a particular operator family is applicable to a particular indexable
column data type. The set of operators from the family that are actually
usable with the indexed column are whichever ones accept the column's data
type as their left-hand input.

Operator classes are described at length in [Section 38.16](xindex.html
"38.16. Interfacing Extensions to Indexes").

**Table  53.33. `pg_opclass` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`opcmethod` `oid` (references [`pg_am`](catalog-pg-am.html
"53.3. pg_am").`oid`) Index access method operator class is for  
`opcname` `name` Name of this operator class  
`opcnamespace` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) Namespace of this operator class  
`opcowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the operator class  
`opcfamily` `oid` (references [`pg_opfamily`](catalog-pg-opfamily.html
"53.35. pg_opfamily").`oid`) Operator family containing the operator class  
`opcintype` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) Data type that the operator class indexes  
`opcdefault` `bool` True if this operator class is the default for `opcintype`  
`opckeytype` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) Type of data stored in index, or zero if same as
`opcintype`  
  
  

An operator class's `opcmethod` must match the `opfmethod` of its containing
operator family. Also, there must be no more than one `pg_opclass` row having
`opcdefault` true for any given combination of `opcmethod` and `opcintype`.

* * *

[Prev](catalog-pg-namespace.html "53.32. pg_namespace")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-operator.html "53.34. pg_operator")  
---|---|---  
53.32. `pg_namespace`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.34. `pg_operator`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-opclass.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

