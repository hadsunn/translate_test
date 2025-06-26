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

Supported Versions: [Current](/docs/current/catalog-pg-collation.html
"PostgreSQL 17 - 53.12. pg_collation") ([17](/docs/17/catalog-pg-
collation.html "PostgreSQL 17 - 53.12. pg_collation")) /
[16](/docs/16/catalog-pg-collation.html "PostgreSQL 16 - 53.12. pg_collation")
/ [15](/docs/15/catalog-pg-collation.html "PostgreSQL 15 -
53.12. pg_collation") / [14](/docs/14/catalog-pg-collation.html "PostgreSQL 14
- 53.12. pg_collation") / [13](/docs/13/catalog-pg-collation.html "PostgreSQL
13 - 53.12. pg_collation")

Development Versions: [18](/docs/18/catalog-pg-collation.html "PostgreSQL 18 -
53.12. pg_collation") / [devel](/docs/devel/catalog-pg-collation.html
"PostgreSQL devel - 53.12. pg_collation")

Unsupported versions: [12](/docs/12/catalog-pg-collation.html "PostgreSQL 12 -
53.12. pg_collation") / [11](/docs/11/catalog-pg-collation.html "PostgreSQL 11
- 53.12. pg_collation") / [10](/docs/10/catalog-pg-collation.html "PostgreSQL
10 - 53.12. pg_collation") / [9.6](/docs/9.6/catalog-pg-collation.html
"PostgreSQL 9.6 - 53.12. pg_collation") / [9.5](/docs/9.5/catalog-pg-
collation.html "PostgreSQL 9.5 - 53.12. pg_collation") /
[9.4](/docs/9.4/catalog-pg-collation.html "PostgreSQL 9.4 -
53.12. pg_collation") / [9.3](/docs/9.3/catalog-pg-collation.html "PostgreSQL
9.3 - 53.12. pg_collation") / [9.2](/docs/9.2/catalog-pg-collation.html
"PostgreSQL 9.2 - 53.12. pg_collation") / [9.1](/docs/9.1/catalog-pg-
collation.html "PostgreSQL 9.1 - 53.12. pg_collation")

__

53.12. `pg_collation`  
---  
[Prev](catalog-pg-class.html "53.11. pg_class")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-constraint.html "53.13. pg_constraint")  
  
* * *

## 53.12. `pg_collation` #

The catalog `pg_collation` describes the available collations, which are
essentially mappings from an SQL name to operating system locale categories.
See [Section 24.2](collation.html "24.2. Collation Support") for more
information.

**Table  53.12. `pg_collation` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`collname` `name` Collation name (unique per namespace and encoding)  
`collnamespace` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) The OID of the namespace that contains this
collation  
`collowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the collation  
`collprovider` `char` Provider of the collation: `d` = database default, `c` =
libc, `i` = icu  
`collisdeterministic` `bool` Is the collation deterministic?  
`collencoding` `int4` Encoding in which the collation is applicable, or -1 if
it works for any encoding  
`collcollate` `text` `LC_COLLATE` for this collation object  
`collctype` `text` `LC_CTYPE` for this collation object  
`colliculocale` `text` ICU locale ID for this collation object  
`collicurules` `text` ICU collation rules for this collation object  
`collversion` `text` Provider-specific version of the collation. This is
recorded when the collation is created and then checked when it is used, to
detect changes in the collation definition that could lead to data corruption.  
  
  

Note that the unique key on this catalog is (`collname`, `collencoding`,
`collnamespace`) not just (`collname`, `collnamespace`). PostgreSQL generally
ignores all collations that do not have `collencoding` equal to either the
current database's encoding or -1, and creation of new entries with the same
name as an entry with `collencoding` = -1 is forbidden. Therefore it is
sufficient to use a qualified SQL name (_`schema`_._`name`_) to identify a
collation, even though this is not unique according to the catalog definition.
The reason for defining the catalog this way is that initdb fills it in at
cluster initialization time with entries for all locales available on the
system, so it must be able to hold entries for all encodings that might ever
be used in the cluster.

In the `template0` database, it could be useful to create collations whose
encoding does not match the database encoding, since they could match the
encodings of databases later cloned from `template0`. This would currently
have to be done manually.

* * *

[Prev](catalog-pg-class.html "53.11. pg_class")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-constraint.html "53.13. pg_constraint")  
---|---|---  
53.11. `pg_class`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.13. `pg_constraint`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-collation.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

