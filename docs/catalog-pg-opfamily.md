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

Supported Versions: [Current](/docs/current/catalog-pg-opfamily.html
"PostgreSQL 17 - 53.35. pg_opfamily") ([17](/docs/17/catalog-pg-opfamily.html
"PostgreSQL 17 - 53.35. pg_opfamily")) / [16](/docs/16/catalog-pg-
opfamily.html "PostgreSQL 16 - 53.35. pg_opfamily") / [15](/docs/15/catalog-
pg-opfamily.html "PostgreSQL 15 - 53.35. pg_opfamily") /
[14](/docs/14/catalog-pg-opfamily.html "PostgreSQL 14 - 53.35. pg_opfamily") /
[13](/docs/13/catalog-pg-opfamily.html "PostgreSQL 13 - 53.35. pg_opfamily")

Development Versions: [18](/docs/18/catalog-pg-opfamily.html "PostgreSQL 18 -
53.35. pg_opfamily") / [devel](/docs/devel/catalog-pg-opfamily.html
"PostgreSQL devel - 53.35. pg_opfamily")

Unsupported versions: [12](/docs/12/catalog-pg-opfamily.html "PostgreSQL 12 -
53.35. pg_opfamily") / [11](/docs/11/catalog-pg-opfamily.html "PostgreSQL 11 -
53.35. pg_opfamily") / [10](/docs/10/catalog-pg-opfamily.html "PostgreSQL 10 -
53.35. pg_opfamily") / [9.6](/docs/9.6/catalog-pg-opfamily.html "PostgreSQL
9.6 - 53.35. pg_opfamily") / [9.5](/docs/9.5/catalog-pg-opfamily.html
"PostgreSQL 9.5 - 53.35. pg_opfamily") / [9.4](/docs/9.4/catalog-pg-
opfamily.html "PostgreSQL 9.4 - 53.35. pg_opfamily") /
[9.3](/docs/9.3/catalog-pg-opfamily.html "PostgreSQL 9.3 -
53.35. pg_opfamily") / [9.2](/docs/9.2/catalog-pg-opfamily.html "PostgreSQL
9.2 - 53.35. pg_opfamily") / [9.1](/docs/9.1/catalog-pg-opfamily.html
"PostgreSQL 9.1 - 53.35. pg_opfamily") / [9.0](/docs/9.0/catalog-pg-
opfamily.html "PostgreSQL 9.0 - 53.35. pg_opfamily") /
[8.4](/docs/8.4/catalog-pg-opfamily.html "PostgreSQL 8.4 -
53.35. pg_opfamily") / [8.3](/docs/8.3/catalog-pg-opfamily.html "PostgreSQL
8.3 - 53.35. pg_opfamily")

__

53.35. `pg_opfamily`  
---  
[Prev](catalog-pg-operator.html "53.34. pg_operator")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-parameter-acl.html "53.36. pg_parameter_acl")  
  
* * *

## 53.35. `pg_opfamily` #

The catalog `pg_opfamily` defines operator families. Each operator family is a
collection of operators and associated support routines that implement the
semantics specified for a particular index access method. Furthermore, the
operators in a family are all “compatible”, in a way that is specified by the
access method. The operator family concept allows cross-data-type operators to
be used with indexes and to be reasoned about using knowledge of access method
semantics.

Operator families are described at length in [Section 38.16](xindex.html
"38.16. Interfacing Extensions to Indexes").

**Table  53.35. `pg_opfamily` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`opfmethod` `oid` (references [`pg_am`](catalog-pg-am.html
"53.3. pg_am").`oid`) Index access method operator family is for  
`opfname` `name` Name of this operator family  
`opfnamespace` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) Namespace of this operator family  
`opfowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the operator family  
  
  

The majority of the information defining an operator family is not in its
`pg_opfamily` row, but in the associated rows in [`pg_amop`](catalog-pg-
amop.html "53.4. pg_amop"), [`pg_amproc`](catalog-pg-amproc.html
"53.5. pg_amproc"), and [`pg_opclass`](catalog-pg-opclass.html
"53.33. pg_opclass").

* * *

[Prev](catalog-pg-operator.html "53.34. pg_operator")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-parameter-acl.html "53.36. pg_parameter_acl")  
---|---|---  
53.34. `pg_operator`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.36. `pg_parameter_acl`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-opfamily.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

