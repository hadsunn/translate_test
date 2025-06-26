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

Supported Versions: [Current](/docs/current/catalog-pg-operator.html
"PostgreSQL 17 - 53.34. pg_operator") ([17](/docs/17/catalog-pg-operator.html
"PostgreSQL 17 - 53.34. pg_operator")) / [16](/docs/16/catalog-pg-
operator.html "PostgreSQL 16 - 53.34. pg_operator") / [15](/docs/15/catalog-
pg-operator.html "PostgreSQL 15 - 53.34. pg_operator") /
[14](/docs/14/catalog-pg-operator.html "PostgreSQL 14 - 53.34. pg_operator") /
[13](/docs/13/catalog-pg-operator.html "PostgreSQL 13 - 53.34. pg_operator")

Development Versions: [18](/docs/18/catalog-pg-operator.html "PostgreSQL 18 -
53.34. pg_operator") / [devel](/docs/devel/catalog-pg-operator.html
"PostgreSQL devel - 53.34. pg_operator")

Unsupported versions: [12](/docs/12/catalog-pg-operator.html "PostgreSQL 12 -
53.34. pg_operator") / [11](/docs/11/catalog-pg-operator.html "PostgreSQL 11 -
53.34. pg_operator") / [10](/docs/10/catalog-pg-operator.html "PostgreSQL 10 -
53.34. pg_operator") / [9.6](/docs/9.6/catalog-pg-operator.html "PostgreSQL
9.6 - 53.34. pg_operator") / [9.5](/docs/9.5/catalog-pg-operator.html
"PostgreSQL 9.5 - 53.34. pg_operator") / [9.4](/docs/9.4/catalog-pg-
operator.html "PostgreSQL 9.4 - 53.34. pg_operator") /
[9.3](/docs/9.3/catalog-pg-operator.html "PostgreSQL 9.3 -
53.34. pg_operator") / [9.2](/docs/9.2/catalog-pg-operator.html "PostgreSQL
9.2 - 53.34. pg_operator") / [9.1](/docs/9.1/catalog-pg-operator.html
"PostgreSQL 9.1 - 53.34. pg_operator") / [9.0](/docs/9.0/catalog-pg-
operator.html "PostgreSQL 9.0 - 53.34. pg_operator") /
[8.4](/docs/8.4/catalog-pg-operator.html "PostgreSQL 8.4 -
53.34. pg_operator") / [8.3](/docs/8.3/catalog-pg-operator.html "PostgreSQL
8.3 - 53.34. pg_operator") / [8.2](/docs/8.2/catalog-pg-operator.html
"PostgreSQL 8.2 - 53.34. pg_operator") / [8.1](/docs/8.1/catalog-pg-
operator.html "PostgreSQL 8.1 - 53.34. pg_operator") /
[8.0](/docs/8.0/catalog-pg-operator.html "PostgreSQL 8.0 -
53.34. pg_operator") / [7.4](/docs/7.4/catalog-pg-operator.html "PostgreSQL
7.4 - 53.34. pg_operator") / [7.3](/docs/7.3/catalog-pg-operator.html
"PostgreSQL 7.3 - 53.34. pg_operator") / [7.2](/docs/7.2/catalog-pg-
operator.html "PostgreSQL 7.2 - 53.34. pg_operator") /
[7.1](/docs/7.1/catalog-pg-operator.html "PostgreSQL 7.1 -
53.34. pg_operator")

__

53.34. `pg_operator`  
---  
[Prev](catalog-pg-opclass.html "53.33. pg_opclass")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-opfamily.html "53.35. pg_opfamily")  
  
* * *

## 53.34. `pg_operator` #

The catalog `pg_operator` stores information about operators. See [CREATE
OPERATOR](sql-createoperator.html "CREATE OPERATOR") and [Section
38.14](xoper.html "38.14. User-Defined Operators") for more information.

**Table  53.34. `pg_operator` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`oprname` `name` Name of the operator  
`oprnamespace` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) The OID of the namespace that contains this
operator  
`oprowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the operator  
`oprkind` `char` `b` = infix operator (“both”), or `l` = prefix operator
(“left”)  
`oprcanmerge` `bool` This operator supports merge joins  
`oprcanhash` `bool` This operator supports hash joins  
`oprleft` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) Type of the left operand (zero for a prefix operator)  
`oprright` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) Type of the right operand  
`oprresult` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) Type of the result (zero for a not-yet-defined
“shell” operator)  
`oprcom` `oid` (references [`pg_operator`](catalog-pg-operator.html
"53.34. pg_operator").`oid`) Commutator of this operator (zero if none)  
`oprnegate` `oid` (references [`pg_operator`](catalog-pg-operator.html
"53.34. pg_operator").`oid`) Negator of this operator (zero if none)  
`oprcode` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Function that implements this operator (zero for a
not-yet-defined “shell” operator)  
`oprrest` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Restriction selectivity estimation function for this
operator (zero if none)  
`oprjoin` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Join selectivity estimation function for this
operator (zero if none)  
  
  

* * *

[Prev](catalog-pg-opclass.html "53.33. pg_opclass")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-opfamily.html "53.35. pg_opfamily")  
---|---|---  
53.33. `pg_opclass`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.35. `pg_opfamily`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-operator.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

