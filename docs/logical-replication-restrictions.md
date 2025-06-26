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

Supported Versions: [Current](/docs/current/logical-replication-
restrictions.html "PostgreSQL 17 - 31.6. Restrictions")
([17](/docs/17/logical-replication-restrictions.html "PostgreSQL 17 -
31.6. Restrictions")) / [16](/docs/16/logical-replication-restrictions.html
"PostgreSQL 16 - 31.6. Restrictions") / [15](/docs/15/logical-replication-
restrictions.html "PostgreSQL 15 - 31.6. Restrictions") /
[14](/docs/14/logical-replication-restrictions.html "PostgreSQL 14 -
31.6. Restrictions") / [13](/docs/13/logical-replication-restrictions.html
"PostgreSQL 13 - 31.6. Restrictions")

Development Versions: [18](/docs/18/logical-replication-restrictions.html
"PostgreSQL 18 - 31.6. Restrictions") / [devel](/docs/devel/logical-
replication-restrictions.html "PostgreSQL devel - 31.6. Restrictions")

Unsupported versions: [12](/docs/12/logical-replication-restrictions.html
"PostgreSQL 12 - 31.6. Restrictions") / [11](/docs/11/logical-replication-
restrictions.html "PostgreSQL 11 - 31.6. Restrictions") /
[10](/docs/10/logical-replication-restrictions.html "PostgreSQL 10 -
31.6. Restrictions")

__

31.6. Restrictions  
---  
[Prev](logical-replication-conflicts.html "31.5. Conflicts")  | [Up](logical-replication.html "Chapter 31. Logical Replication") | Chapter 31. Logical Replication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logical-replication-architecture.html "31.7. Architecture")  
  
* * *

## 31.6. Restrictions #

Logical replication currently has the following restrictions or missing
functionality. These might be addressed in future releases.

  * The database schema and DDL commands are not replicated. The initial schema can be copied by hand using `pg_dump --schema-only`. Subsequent schema changes would need to be kept in sync manually. (Note, however, that there is no need for the schemas to be absolutely the same on both sides.) Logical replication is robust when schema definitions change in a live database: When the schema is changed on the publisher and replicated data starts arriving at the subscriber but does not fit into the table schema, replication will error until the schema is updated. In many cases, intermittent errors can be avoided by applying additive schema changes to the subscriber first.

  * Sequence data is not replicated. The data in serial or identity columns backed by sequences will of course be replicated as part of the table, but the sequence itself would still show the start value on the subscriber. If the subscriber is used as a read-only database, then this should typically not be a problem. If, however, some kind of switchover or failover to the subscriber database is intended, then the sequences would need to be updated to the latest values, either by copying the current data from the publisher (perhaps using `pg_dump`) or by determining a sufficiently high value from the tables themselves.

  * Replication of `TRUNCATE` commands is supported, but some care must be taken when truncating groups of tables connected by foreign keys. When replicating a truncate action, the subscriber will truncate the same group of tables that was truncated on the publisher, either explicitly specified or implicitly collected via `CASCADE`, minus tables that are not part of the subscription. This will work correctly if all affected tables are part of the same subscription. But if some tables to be truncated on the subscriber have foreign-key links to tables that are not part of the same (or any) subscription, then the application of the truncate action on the subscriber will fail.

  * Large objects (see [Chapter 35](largeobjects.html "Chapter 35. Large Objects")) are not replicated. There is no workaround for that, other than storing data in normal tables.

  * Replication is only supported by tables, including partitioned tables. Attempts to replicate other types of relations, such as views, materialized views, or foreign tables, will result in an error.

  * When replicating between partitioned tables, the actual replication originates, by default, from the leaf partitions on the publisher, so partitions on the publisher must also exist on the subscriber as valid target tables. (They could either be leaf partitions themselves, or they could be further subpartitioned, or they could even be independent tables.) Publications can also specify that changes are to be replicated using the identity and schema of the partitioned root table instead of that of the individual leaf partitions in which the changes actually originate (see [`publish_via_partition_root`](sql-createpublication.html#SQL-CREATEPUBLICATION-WITH-PUBLISH-VIA-PARTITION-ROOT) parameter of `CREATE PUBLICATION`).

* * *

[Prev](logical-replication-conflicts.html "31.5. Conflicts")  | [Up](logical-replication.html "Chapter 31. Logical Replication") |  [Next](logical-replication-architecture.html "31.7. Architecture")  
---|---|---  
31.5. Conflicts  | [Home](index.html "PostgreSQL 16.9 Documentation") |  31.7. Architecture  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logical-replication-
restrictions.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

