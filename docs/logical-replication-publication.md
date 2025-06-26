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
publication.html "PostgreSQL 17 - 31.1. Publication") ([17](/docs/17/logical-
replication-publication.html "PostgreSQL 17 - 31.1. Publication")) /
[16](/docs/16/logical-replication-publication.html "PostgreSQL 16 -
31.1. Publication") / [15](/docs/15/logical-replication-publication.html
"PostgreSQL 15 - 31.1. Publication") / [14](/docs/14/logical-replication-
publication.html "PostgreSQL 14 - 31.1. Publication") / [13](/docs/13/logical-
replication-publication.html "PostgreSQL 13 - 31.1. Publication")

Development Versions: [18](/docs/18/logical-replication-publication.html
"PostgreSQL 18 - 31.1. Publication") / [devel](/docs/devel/logical-
replication-publication.html "PostgreSQL devel - 31.1. Publication")

Unsupported versions: [12](/docs/12/logical-replication-publication.html
"PostgreSQL 12 - 31.1. Publication") / [11](/docs/11/logical-replication-
publication.html "PostgreSQL 11 - 31.1. Publication") / [10](/docs/10/logical-
replication-publication.html "PostgreSQL 10 - 31.1. Publication")

__

31.1. Publication  
---  
[Prev](logical-replication.html "Chapter 31. Logical Replication")  | [Up](logical-replication.html "Chapter 31. Logical Replication") | Chapter 31. Logical Replication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logical-replication-subscription.html "31.2. Subscription")  
  
* * *

## 31.1. Publication #

A _publication_ can be defined on any physical replication primary. The node
where a publication is defined is referred to as _publisher_. A publication is
a set of changes generated from a table or a group of tables, and might also
be described as a change set or replication set. Each publication exists in
only one database.

Publications are different from schemas and do not affect how the table is
accessed. Each table can be added to multiple publications if needed.
Publications may currently only contain tables and all tables in schema.
Objects must be added explicitly, except when a publication is created for
`ALL TABLES`.

Publications can choose to limit the changes they produce to any combination
of `INSERT`, `UPDATE`, `DELETE`, and `TRUNCATE`, similar to how triggers are
fired by particular event types. By default, all operation types are
replicated. These publication specifications apply only for DML operations;
they do not affect the initial data synchronization copy. (Row filters have no
effect for `TRUNCATE`. See [Section 31.3](logical-replication-row-filter.html
"31.3. Row Filters")).

A published table must have a _replica identity_ configured in order to be
able to replicate `UPDATE` and `DELETE` operations, so that appropriate rows
to update or delete can be identified on the subscriber side. By default, this
is the primary key, if there is one. Another unique index (with certain
additional requirements) can also be set to be the replica identity. If the
table does not have any suitable key, then it can be set to replica identity
`FULL`, which means the entire row becomes the key. When replica identity
`FULL` is specified, indexes can be used on the subscriber side for searching
the rows. Candidate indexes must be btree, non-partial, and the leftmost index
field must be a column (not an expression) that references the published table
column. These restrictions on the non-unique index properties adhere to some
of the restrictions that are enforced for primary keys. If there are no such
suitable indexes, the search on the subscriber side can be very inefficient,
therefore replica identity `FULL` should only be used as a fallback if no
other solution is possible. If a replica identity other than `FULL` is set on
the publisher side, a replica identity comprising the same or fewer columns
must also be set on the subscriber side. See [`REPLICA IDENTITY`](sql-
altertable.html#SQL-ALTERTABLE-REPLICA-IDENTITY) for details on how to set the
replica identity. If a table without a replica identity is added to a
publication that replicates `UPDATE` or `DELETE` operations then subsequent
`UPDATE` or `DELETE` operations will cause an error on the publisher. `INSERT`
operations can proceed regardless of any replica identity.

Every publication can have multiple subscribers.

A publication is created using the [`CREATE PUBLICATION`](sql-
createpublication.html "CREATE PUBLICATION") command and may later be altered
or dropped using corresponding commands.

The individual tables can be added and removed dynamically using [`ALTER
PUBLICATION`](sql-alterpublication.html "ALTER PUBLICATION"). Both the `ADD
TABLE` and `DROP TABLE` operations are transactional; so the table will start
or stop replicating at the correct snapshot once the transaction has
committed.

* * *

[Prev](logical-replication.html "Chapter 31. Logical Replication")  | [Up](logical-replication.html "Chapter 31. Logical Replication") |  [Next](logical-replication-subscription.html "31.2. Subscription")  
---|---|---  
Chapter 31. Logical Replication  | [Home](index.html "PostgreSQL 16.9 Documentation") |  31.2. Subscription  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logical-replication-
publication.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

