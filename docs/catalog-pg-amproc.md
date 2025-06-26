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

Supported Versions: [Current](/docs/current/catalog-pg-amproc.html "PostgreSQL
17 - 53.5. pg_amproc") ([17](/docs/17/catalog-pg-amproc.html "PostgreSQL 17 -
53.5. pg_amproc")) / [16](/docs/16/catalog-pg-amproc.html "PostgreSQL 16 -
53.5. pg_amproc") / [15](/docs/15/catalog-pg-amproc.html "PostgreSQL 15 -
53.5. pg_amproc") / [14](/docs/14/catalog-pg-amproc.html "PostgreSQL 14 -
53.5. pg_amproc") / [13](/docs/13/catalog-pg-amproc.html "PostgreSQL 13 -
53.5. pg_amproc")

Development Versions: [18](/docs/18/catalog-pg-amproc.html "PostgreSQL 18 -
53.5. pg_amproc") / [devel](/docs/devel/catalog-pg-amproc.html "PostgreSQL
devel - 53.5. pg_amproc")

Unsupported versions: [12](/docs/12/catalog-pg-amproc.html "PostgreSQL 12 -
53.5. pg_amproc") / [11](/docs/11/catalog-pg-amproc.html "PostgreSQL 11 -
53.5. pg_amproc") / [10](/docs/10/catalog-pg-amproc.html "PostgreSQL 10 -
53.5. pg_amproc") / [9.6](/docs/9.6/catalog-pg-amproc.html "PostgreSQL 9.6 -
53.5. pg_amproc") / [9.5](/docs/9.5/catalog-pg-amproc.html "PostgreSQL 9.5 -
53.5. pg_amproc") / [9.4](/docs/9.4/catalog-pg-amproc.html "PostgreSQL 9.4 -
53.5. pg_amproc") / [9.3](/docs/9.3/catalog-pg-amproc.html "PostgreSQL 9.3 -
53.5. pg_amproc") / [9.2](/docs/9.2/catalog-pg-amproc.html "PostgreSQL 9.2 -
53.5. pg_amproc") / [9.1](/docs/9.1/catalog-pg-amproc.html "PostgreSQL 9.1 -
53.5. pg_amproc") / [9.0](/docs/9.0/catalog-pg-amproc.html "PostgreSQL 9.0 -
53.5. pg_amproc") / [8.4](/docs/8.4/catalog-pg-amproc.html "PostgreSQL 8.4 -
53.5. pg_amproc") / [8.3](/docs/8.3/catalog-pg-amproc.html "PostgreSQL 8.3 -
53.5. pg_amproc") / [8.2](/docs/8.2/catalog-pg-amproc.html "PostgreSQL 8.2 -
53.5. pg_amproc") / [8.1](/docs/8.1/catalog-pg-amproc.html "PostgreSQL 8.1 -
53.5. pg_amproc") / [8.0](/docs/8.0/catalog-pg-amproc.html "PostgreSQL 8.0 -
53.5. pg_amproc") / [7.4](/docs/7.4/catalog-pg-amproc.html "PostgreSQL 7.4 -
53.5. pg_amproc") / [7.3](/docs/7.3/catalog-pg-amproc.html "PostgreSQL 7.3 -
53.5. pg_amproc")

__

53.5. `pg_amproc`  
---  
[Prev](catalog-pg-amop.html "53.4. pg_amop")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-attrdef.html "53.6. pg_attrdef")  
  
* * *

## 53.5. `pg_amproc` #

The catalog `pg_amproc` stores information about support functions associated
with access method operator families. There is one row for each support
function belonging to an operator family.

**Table  53.5. `pg_amproc` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`amprocfamily` `oid` (references [`pg_opfamily`](catalog-pg-opfamily.html
"53.35. pg_opfamily").`oid`) The operator family this entry is for  
`amproclefttype` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) Left-hand input data type of associated operator  
`amprocrighttype` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) Right-hand input data type of associated operator  
`amprocnum` `int2` Support function number  
`amproc` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) OID of the function  
  
  

The usual interpretation of the `amproclefttype` and `amprocrighttype` fields
is that they identify the left and right input types of the operator(s) that a
particular support function supports. For some access methods these match the
input data type(s) of the support function itself, for others not. There is a
notion of “default” support functions for an index, which are those with
`amproclefttype` and `amprocrighttype` both equal to the index operator
class's `opcintype`.

* * *

[Prev](catalog-pg-amop.html "53.4. pg_amop")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-attrdef.html "53.6. pg_attrdef")  
---|---|---  
53.4. `pg_amop`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.6. `pg_attrdef`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-amproc.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

