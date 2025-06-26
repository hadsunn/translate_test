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

Supported Versions: [Current](/docs/current/catalog-pg-seclabel.html
"PostgreSQL 17 - 53.46. pg_seclabel") ([17](/docs/17/catalog-pg-seclabel.html
"PostgreSQL 17 - 53.46. pg_seclabel")) / [16](/docs/16/catalog-pg-
seclabel.html "PostgreSQL 16 - 53.46. pg_seclabel") / [15](/docs/15/catalog-
pg-seclabel.html "PostgreSQL 15 - 53.46. pg_seclabel") /
[14](/docs/14/catalog-pg-seclabel.html "PostgreSQL 14 - 53.46. pg_seclabel") /
[13](/docs/13/catalog-pg-seclabel.html "PostgreSQL 13 - 53.46. pg_seclabel")

Development Versions: [18](/docs/18/catalog-pg-seclabel.html "PostgreSQL 18 -
53.46. pg_seclabel") / [devel](/docs/devel/catalog-pg-seclabel.html
"PostgreSQL devel - 53.46. pg_seclabel")

Unsupported versions: [12](/docs/12/catalog-pg-seclabel.html "PostgreSQL 12 -
53.46. pg_seclabel") / [11](/docs/11/catalog-pg-seclabel.html "PostgreSQL 11 -
53.46. pg_seclabel") / [10](/docs/10/catalog-pg-seclabel.html "PostgreSQL 10 -
53.46. pg_seclabel") / [9.6](/docs/9.6/catalog-pg-seclabel.html "PostgreSQL
9.6 - 53.46. pg_seclabel") / [9.5](/docs/9.5/catalog-pg-seclabel.html
"PostgreSQL 9.5 - 53.46. pg_seclabel") / [9.4](/docs/9.4/catalog-pg-
seclabel.html "PostgreSQL 9.4 - 53.46. pg_seclabel") /
[9.3](/docs/9.3/catalog-pg-seclabel.html "PostgreSQL 9.3 -
53.46. pg_seclabel") / [9.2](/docs/9.2/catalog-pg-seclabel.html "PostgreSQL
9.2 - 53.46. pg_seclabel") / [9.1](/docs/9.1/catalog-pg-seclabel.html
"PostgreSQL 9.1 - 53.46. pg_seclabel")

__

53.46. `pg_seclabel`  
---  
[Prev](catalog-pg-rewrite.html "53.45. pg_rewrite")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-sequence.html "53.47. pg_sequence")  
  
* * *

## 53.46. `pg_seclabel` #

The catalog `pg_seclabel` stores security labels on database objects. Security
labels can be manipulated with the [`SECURITY LABEL`](sql-security-label.html
"SECURITY LABEL") command. For an easier way to view security labels, see
[Section 54.22](view-pg-seclabels.html "54.22. pg_seclabels").

See also [`pg_shseclabel`](catalog-pg-shseclabel.html "53.50. pg_shseclabel"),
which performs a similar function for security labels of database objects that
are shared across a database cluster.

**Table  53.46. `pg_seclabel` Columns**

Column Type Description  
---  
`objoid` `oid` (references any OID column) The OID of the object this security
label pertains to  
`classoid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The OID of the system catalog this object appears in  
`objsubid` `int4` For a security label on a table column, this is the column
number (the `objoid` and `classoid` refer to the table itself). For all other
object types, this column is zero.  
`provider` `text` The label provider associated with this label.  
`label` `text` The security label applied to this object.  
  
  

* * *

[Prev](catalog-pg-rewrite.html "53.45. pg_rewrite")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-sequence.html "53.47. pg_sequence")  
---|---|---  
53.45. `pg_rewrite`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.47. `pg_sequence`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-seclabel.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

