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

Supported Versions: [Current](/docs/current/catalog-pg-publication-rel.html
"PostgreSQL 17 - 53.42. pg_publication_rel") ([17](/docs/17/catalog-pg-
publication-rel.html "PostgreSQL 17 - 53.42. pg_publication_rel")) /
[16](/docs/16/catalog-pg-publication-rel.html "PostgreSQL 16 -
53.42. pg_publication_rel") / [15](/docs/15/catalog-pg-publication-rel.html
"PostgreSQL 15 - 53.42. pg_publication_rel") / [14](/docs/14/catalog-pg-
publication-rel.html "PostgreSQL 14 - 53.42. pg_publication_rel") /
[13](/docs/13/catalog-pg-publication-rel.html "PostgreSQL 13 -
53.42. pg_publication_rel")

Development Versions: [18](/docs/18/catalog-pg-publication-rel.html
"PostgreSQL 18 - 53.42. pg_publication_rel") / [devel](/docs/devel/catalog-pg-
publication-rel.html "PostgreSQL devel - 53.42. pg_publication_rel")

Unsupported versions: [12](/docs/12/catalog-pg-publication-rel.html
"PostgreSQL 12 - 53.42. pg_publication_rel") / [11](/docs/11/catalog-pg-
publication-rel.html "PostgreSQL 11 - 53.42. pg_publication_rel") /
[10](/docs/10/catalog-pg-publication-rel.html "PostgreSQL 10 -
53.42. pg_publication_rel")

__

53.42. `pg_publication_rel`  
---  
[Prev](catalog-pg-publication-namespace.html "53.41. pg_publication_namespace")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-range.html "53.43. pg_range")  
  
* * *

## 53.42. `pg_publication_rel` #

The catalog `pg_publication_rel` contains the mapping between relations and
publications in the database. This is a many-to-many mapping. See also
[Section 54.17](view-pg-publication-tables.html
"54.17. pg_publication_tables") for a more user-friendly view of this
information.

**Table  53.42. `pg_publication_rel` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`prpubid` `oid` (references [`pg_publication`](catalog-pg-publication.html
"53.40. pg_publication").`oid`) Reference to publication  
`prrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) Reference to relation  
`prqual` `pg_node_tree` Expression tree (in `nodeToString()` representation)
for the relation's publication qualifying condition. Null if there is no
publication qualifying condition.  
`prattrs` `int2vector` (references [`pg_attribute`](catalog-pg-attribute.html
"53.7. pg_attribute").`attnum`) This is an array of values that indicates
which table columns are part of the publication. For example, a value of `1 3`
would mean that the first and the third table columns are published. A null
value indicates that all columns are published.  
  
  

* * *

[Prev](catalog-pg-publication-namespace.html "53.41. pg_publication_namespace")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-range.html "53.43. pg_range")  
---|---|---  
53.41. `pg_publication_namespace`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.43. `pg_range`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-publication-
rel.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

