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

Supported Versions: [Current](/docs/current/catalog-pg-publication.html
"PostgreSQL 17 - 53.40. pg_publication") ([17](/docs/17/catalog-pg-
publication.html "PostgreSQL 17 - 53.40. pg_publication")) /
[16](/docs/16/catalog-pg-publication.html "PostgreSQL 16 -
53.40. pg_publication") / [15](/docs/15/catalog-pg-publication.html
"PostgreSQL 15 - 53.40. pg_publication") / [14](/docs/14/catalog-pg-
publication.html "PostgreSQL 14 - 53.40. pg_publication") /
[13](/docs/13/catalog-pg-publication.html "PostgreSQL 13 -
53.40. pg_publication")

Development Versions: [18](/docs/18/catalog-pg-publication.html "PostgreSQL 18
- 53.40. pg_publication") / [devel](/docs/devel/catalog-pg-publication.html
"PostgreSQL devel - 53.40. pg_publication")

Unsupported versions: [12](/docs/12/catalog-pg-publication.html "PostgreSQL 12
- 53.40. pg_publication") / [11](/docs/11/catalog-pg-publication.html
"PostgreSQL 11 - 53.40. pg_publication") / [10](/docs/10/catalog-pg-
publication.html "PostgreSQL 10 - 53.40. pg_publication")

__

53.40. `pg_publication`  
---  
[Prev](catalog-pg-proc.html "53.39. pg_proc")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-publication-namespace.html "53.41. pg_publication_namespace")  
  
* * *

## 53.40. `pg_publication` #

The catalog `pg_publication` contains all publications created in the
database. For more on publications see [Section 31.1](logical-replication-
publication.html "31.1. Publication").

**Table  53.40. `pg_publication` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`pubname` `name` Name of the publication  
`pubowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the publication  
`puballtables` `bool` If true, this publication automatically includes all
tables in the database, including any that will be created in the future.  
`pubinsert` `bool` If true, [INSERT](sql-insert.html "INSERT") operations are
replicated for tables in the publication.  
`pubupdate` `bool` If true, [UPDATE](sql-update.html "UPDATE") operations are
replicated for tables in the publication.  
`pubdelete` `bool` If true, [DELETE](sql-delete.html "DELETE") operations are
replicated for tables in the publication.  
`pubtruncate` `bool` If true, [TRUNCATE](sql-truncate.html "TRUNCATE")
operations are replicated for tables in the publication.  
`pubviaroot` `bool` If true, operations on a leaf partition are replicated
using the identity and schema of its topmost partitioned ancestor mentioned in
the publication instead of its own.  
  
  

* * *

[Prev](catalog-pg-proc.html "53.39. pg_proc")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-publication-namespace.html "53.41. pg_publication_namespace")  
---|---|---  
53.39. `pg_proc`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.41. `pg_publication_namespace`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-publication.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

