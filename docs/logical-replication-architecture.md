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
architecture.html "PostgreSQL 17 - 31.7. Architecture")
([17](/docs/17/logical-replication-architecture.html "PostgreSQL 17 -
31.7. Architecture")) / [16](/docs/16/logical-replication-architecture.html
"PostgreSQL 16 - 31.7. Architecture") / [15](/docs/15/logical-replication-
architecture.html "PostgreSQL 15 - 31.7. Architecture") /
[14](/docs/14/logical-replication-architecture.html "PostgreSQL 14 -
31.7. Architecture") / [13](/docs/13/logical-replication-architecture.html
"PostgreSQL 13 - 31.7. Architecture")

Development Versions: [18](/docs/18/logical-replication-architecture.html
"PostgreSQL 18 - 31.7. Architecture") / [devel](/docs/devel/logical-
replication-architecture.html "PostgreSQL devel - 31.7. Architecture")

Unsupported versions: [12](/docs/12/logical-replication-architecture.html
"PostgreSQL 12 - 31.7. Architecture") / [11](/docs/11/logical-replication-
architecture.html "PostgreSQL 11 - 31.7. Architecture") /
[10](/docs/10/logical-replication-architecture.html "PostgreSQL 10 -
31.7. Architecture")

__

31.7. Architecture  
---  
[Prev](logical-replication-restrictions.html "31.6. Restrictions")  | [Up](logical-replication.html "Chapter 31. Logical Replication") | Chapter 31. Logical Replication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logical-replication-monitoring.html "31.8. Monitoring")  
  
* * *

## 31.7. Architecture #

[31.7.1. Initial Snapshot](logical-replication-architecture.html#LOGICAL-
REPLICATION-SNAPSHOT)

Logical replication starts by copying a snapshot of the data on the publisher
database. Once that is done, changes on the publisher are sent to the
subscriber as they occur in real time. The subscriber applies data in the
order in which commits were made on the publisher so that transactional
consistency is guaranteed for the publications within any single subscription.

Logical replication is built with an architecture similar to physical
streaming replication (see [Section 27.2.5](warm-standby.html#STREAMING-
REPLICATION "27.2.5. Streaming Replication")). It is implemented by
`walsender` and `apply` processes. The walsender process starts logical
decoding (described in [Chapter 49](logicaldecoding.html "Chapter 49. Logical
Decoding")) of the WAL and loads the standard logical decoding output plugin
(`pgoutput`). The plugin transforms the changes read from WAL to the logical
replication protocol (see [Section 55.5](protocol-logical-replication.html
"55.5. Logical Streaming Replication Protocol")) and filters the data
according to the publication specification. The data is then continuously
transferred using the streaming replication protocol to the apply worker,
which maps the data to local tables and applies the individual changes as they
are received, in correct transactional order.

The apply process on the subscriber database always runs with
[`session_replication_role`](runtime-config-client.html#GUC-SESSION-
REPLICATION-ROLE) set to `replica`. This means that, by default, triggers and
rules will not fire on a subscriber. Users can optionally choose to enable
triggers and rules on a table using the [`ALTER TABLE`](sql-altertable.html
"ALTER TABLE") command and the `ENABLE TRIGGER` and `ENABLE RULE` clauses.

The logical replication apply process currently only fires row triggers, not
statement triggers. The initial table synchronization, however, is implemented
like a `COPY` command and thus fires both row and statement triggers for
`INSERT`.

### 31.7.1. Initial Snapshot #

The initial data in existing subscribed tables are snapshotted and copied in a
parallel instance of a special kind of apply process. This process will create
its own replication slot and copy the existing data. As soon as the copy is
finished the table contents will become visible to other backends. Once
existing data is copied, the worker enters synchronization mode, which ensures
that the table is brought up to a synchronized state with the main apply
process by streaming any changes that happened during the initial data copy
using standard logical replication. During this synchronization phase, the
changes are applied and committed in the same order as they happened on the
publisher. Once synchronization is done, control of the replication of the
table is given back to the main apply process where replication continues as
normal.

### Note

The publication [`publish`](sql-createpublication.html#SQL-CREATEPUBLICATION-
WITH-PUBLISH) parameter only affects what DML operations will be replicated.
The initial data synchronization does not take this parameter into account
when copying the existing table data.

* * *

[Prev](logical-replication-restrictions.html "31.6. Restrictions")  | [Up](logical-replication.html "Chapter 31. Logical Replication") |  [Next](logical-replication-monitoring.html "31.8. Monitoring")  
---|---|---  
31.6. Restrictions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  31.8. Monitoring  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logical-replication-
architecture.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

