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

Supported Versions: [Current](/docs/current/catalog-pg-amop.html "PostgreSQL
17 - 53.4. pg_amop") ([17](/docs/17/catalog-pg-amop.html "PostgreSQL 17 -
53.4. pg_amop")) / [16](/docs/16/catalog-pg-amop.html "PostgreSQL 16 -
53.4. pg_amop") / [15](/docs/15/catalog-pg-amop.html "PostgreSQL 15 -
53.4. pg_amop") / [14](/docs/14/catalog-pg-amop.html "PostgreSQL 14 -
53.4. pg_amop") / [13](/docs/13/catalog-pg-amop.html "PostgreSQL 13 -
53.4. pg_amop")

Development Versions: [18](/docs/18/catalog-pg-amop.html "PostgreSQL 18 -
53.4. pg_amop") / [devel](/docs/devel/catalog-pg-amop.html "PostgreSQL devel -
53.4. pg_amop")

Unsupported versions: [12](/docs/12/catalog-pg-amop.html "PostgreSQL 12 -
53.4. pg_amop") / [11](/docs/11/catalog-pg-amop.html "PostgreSQL 11 -
53.4. pg_amop") / [10](/docs/10/catalog-pg-amop.html "PostgreSQL 10 -
53.4. pg_amop") / [9.6](/docs/9.6/catalog-pg-amop.html "PostgreSQL 9.6 -
53.4. pg_amop") / [9.5](/docs/9.5/catalog-pg-amop.html "PostgreSQL 9.5 -
53.4. pg_amop") / [9.4](/docs/9.4/catalog-pg-amop.html "PostgreSQL 9.4 -
53.4. pg_amop") / [9.3](/docs/9.3/catalog-pg-amop.html "PostgreSQL 9.3 -
53.4. pg_amop") / [9.2](/docs/9.2/catalog-pg-amop.html "PostgreSQL 9.2 -
53.4. pg_amop") / [9.1](/docs/9.1/catalog-pg-amop.html "PostgreSQL 9.1 -
53.4. pg_amop") / [9.0](/docs/9.0/catalog-pg-amop.html "PostgreSQL 9.0 -
53.4. pg_amop") / [8.4](/docs/8.4/catalog-pg-amop.html "PostgreSQL 8.4 -
53.4. pg_amop") / [8.3](/docs/8.3/catalog-pg-amop.html "PostgreSQL 8.3 -
53.4. pg_amop") / [8.2](/docs/8.2/catalog-pg-amop.html "PostgreSQL 8.2 -
53.4. pg_amop") / [8.1](/docs/8.1/catalog-pg-amop.html "PostgreSQL 8.1 -
53.4. pg_amop") / [8.0](/docs/8.0/catalog-pg-amop.html "PostgreSQL 8.0 -
53.4. pg_amop") / [7.4](/docs/7.4/catalog-pg-amop.html "PostgreSQL 7.4 -
53.4. pg_amop") / [7.3](/docs/7.3/catalog-pg-amop.html "PostgreSQL 7.3 -
53.4. pg_amop")

__

53.4. `pg_amop`  
---  
[Prev](catalog-pg-am.html "53.3. pg_am")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-amproc.html "53.5. pg_amproc")  
  
* * *

## 53.4. `pg_amop` #

The catalog `pg_amop` stores information about operators associated with
access method operator families. There is one row for each operator that is a
member of an operator family. A family member can be either a _search_
operator or an _ordering_ operator. An operator can appear in more than one
family, but cannot appear in more than one search position nor more than one
ordering position within a family. (It is allowed, though unlikely, for an
operator to be used for both search and ordering purposes.)

**Table  53.4. `pg_amop` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`amopfamily` `oid` (references [`pg_opfamily`](catalog-pg-opfamily.html
"53.35. pg_opfamily").`oid`) The operator family this entry is for  
`amoplefttype` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) Left-hand input data type of operator  
`amoprighttype` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) Right-hand input data type of operator  
`amopstrategy` `int2` Operator strategy number  
`amoppurpose` `char` Operator purpose, either `s` for search or `o` for
ordering  
`amopopr` `oid` (references [`pg_operator`](catalog-pg-operator.html
"53.34. pg_operator").`oid`) OID of the operator  
`amopmethod` `oid` (references [`pg_am`](catalog-pg-am.html
"53.3. pg_am").`oid`) Index access method operator family is for  
`amopsortfamily` `oid` (references [`pg_opfamily`](catalog-pg-opfamily.html
"53.35. pg_opfamily").`oid`) The B-tree operator family this entry sorts
according to, if an ordering operator; zero if a search operator  
  
  

A “search” operator entry indicates that an index of this operator family can
be searched to find all rows satisfying `WHERE` _`indexed_column`_
_`operator`_ _`constant`_. Obviously, such an operator must return `boolean`,
and its left-hand input type must match the index's column data type.

An “ordering” operator entry indicates that an index of this operator family
can be scanned to return rows in the order represented by `ORDER BY`
_`indexed_column`_ _`operator`_ _`constant`_. Such an operator could return
any sortable data type, though again its left-hand input type must match the
index's column data type. The exact semantics of the `ORDER BY` are specified
by the `amopsortfamily` column, which must reference a B-tree operator family
for the operator's result type.

### Note

At present, it's assumed that the sort order for an ordering operator is the
default for the referenced operator family, i.e., `ASC NULLS LAST`. This might
someday be relaxed by adding additional columns to specify sort options
explicitly.

An entry's `amopmethod` must match the `opfmethod` of its containing operator
family (including `amopmethod` here is an intentional denormalization of the
catalog structure for performance reasons). Also, `amoplefttype` and
`amoprighttype` must match the `oprleft` and `oprright` fields of the
referenced [`pg_operator`](catalog-pg-operator.html "53.34. pg_operator")
entry.

* * *

[Prev](catalog-pg-am.html "53.3. pg_am")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-amproc.html "53.5. pg_amproc")  
---|---|---  
53.3. `pg_am`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.5. `pg_amproc`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-amop.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

