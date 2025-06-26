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

Supported Versions: [Current](/docs/current/logical-replication.html
"PostgreSQL 17 - Chapter 31. Logical Replication") ([17](/docs/17/logical-
replication.html "PostgreSQL 17 - Chapter 31. Logical Replication")) /
[16](/docs/16/logical-replication.html "PostgreSQL 16 - Chapter 31. Logical
Replication") / [15](/docs/15/logical-replication.html "PostgreSQL 15 -
Chapter 31. Logical Replication") / [14](/docs/14/logical-replication.html
"PostgreSQL 14 - Chapter 31. Logical Replication") / [13](/docs/13/logical-
replication.html "PostgreSQL 13 - Chapter 31. Logical Replication")

Development Versions: [18](/docs/18/logical-replication.html "PostgreSQL 18 -
Chapter 31. Logical Replication") / [devel](/docs/devel/logical-
replication.html "PostgreSQL devel - Chapter 31. Logical Replication")

Unsupported versions: [12](/docs/12/logical-replication.html "PostgreSQL 12 -
Chapter 31. Logical Replication") / [11](/docs/11/logical-replication.html
"PostgreSQL 11 - Chapter 31. Logical Replication") / [10](/docs/10/logical-
replication.html "PostgreSQL 10 - Chapter 31. Logical Replication")

__

Chapter 31. Logical Replication  
---  
[Prev](wal-internals.html "30.6. WAL Internals")  | [Up](admin.html "Part III. Server Administration") | Part III. Server Administration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logical-replication-publication.html "31.1. Publication")  
  
* * *

## Chapter 31. Logical Replication

**Table of Contents**

[31.1. Publication](logical-replication-publication.html)

[31.2. Subscription](logical-replication-subscription.html)

    

[31.2.1. Replication Slot Management](logical-replication-
subscription.html#LOGICAL-REPLICATION-SUBSCRIPTION-SLOT)

[31.2.2. Examples: Set Up Logical Replication](logical-replication-
subscription.html#LOGICAL-REPLICATION-SUBSCRIPTION-EXAMPLES)

[31.2.3. Examples: Deferred Replication Slot Creation](logical-replication-
subscription.html#LOGICAL-REPLICATION-SUBSCRIPTION-EXAMPLES-DEFERRED-SLOT)

[31.3. Row Filters](logical-replication-row-filter.html)

    

[31.3.1. Row Filter Rules](logical-replication-row-filter.html#LOGICAL-
REPLICATION-ROW-FILTER-RULES)

[31.3.2. Expression Restrictions](logical-replication-row-filter.html#LOGICAL-
REPLICATION-ROW-FILTER-RESTRICTIONS)

[31.3.3. UPDATE Transformations](logical-replication-row-filter.html#LOGICAL-
REPLICATION-ROW-FILTER-TRANSFORMATIONS)

[31.3.4. Partitioned Tables](logical-replication-row-filter.html#LOGICAL-
REPLICATION-ROW-FILTER-PARTITIONED-TABLE)

[31.3.5. Initial Data Synchronization](logical-replication-row-
filter.html#LOGICAL-REPLICATION-ROW-FILTER-INITIAL-DATA-SYNC)

[31.3.6. Combining Multiple Row Filters](logical-replication-row-
filter.html#LOGICAL-REPLICATION-ROW-FILTER-COMBINING)

[31.3.7. Examples](logical-replication-row-filter.html#LOGICAL-REPLICATION-
ROW-FILTER-EXAMPLES)

[31.4. Column Lists](logical-replication-col-lists.html)

    

[31.4.1. Examples](logical-replication-col-lists.html#LOGICAL-REPLICATION-COL-
LIST-EXAMPLES)

[31.5. Conflicts](logical-replication-conflicts.html)

[31.6. Restrictions](logical-replication-restrictions.html)

[31.7. Architecture](logical-replication-architecture.html)

    

[31.7.1. Initial Snapshot](logical-replication-architecture.html#LOGICAL-
REPLICATION-SNAPSHOT)

[31.8. Monitoring](logical-replication-monitoring.html)

[31.9. Security](logical-replication-security.html)

[31.10. Configuration Settings](logical-replication-config.html)

    

[31.10.1. Publishers](logical-replication-config.html#LOGICAL-REPLICATION-
CONFIG-PUBLISHER)

[31.10.2. Subscribers](logical-replication-config.html#LOGICAL-REPLICATION-
CONFIG-SUBSCRIBER)

[31.11. Quick Setup](logical-replication-quick-setup.html)

Logical replication is a method of replicating data objects and their changes,
based upon their replication identity (usually a primary key). We use the term
logical in contrast to physical replication, which uses exact block addresses
and byte-by-byte replication. PostgreSQL supports both mechanisms
concurrently, see [Chapter 27](high-availability.html "Chapter 27. High
Availability, Load Balancing, and Replication"). Logical replication allows
fine-grained control over both data replication and security.

Logical replication uses a _publish_ and _subscribe_ model with one or more
_subscribers_ subscribing to one or more _publications_ on a _publisher_ node.
Subscribers pull data from the publications they subscribe to and may
subsequently re-publish data to allow cascading replication or more complex
configurations.

Logical replication of a table typically starts with taking a snapshot of the
data on the publisher database and copying that to the subscriber. Once that
is done, the changes on the publisher are sent to the subscriber as they occur
in real-time. The subscriber applies the data in the same order as the
publisher so that transactional consistency is guaranteed for publications
within a single subscription. This method of data replication is sometimes
referred to as transactional replication.

The typical use-cases for logical replication are:

  * Sending incremental changes in a single database or a subset of a database to subscribers as they occur.

  * Firing triggers for individual changes as they arrive on the subscriber.

  * Consolidating multiple databases into a single one (for example for analytical purposes).

  * Replicating between different major versions of PostgreSQL.

  * Replicating between PostgreSQL instances on different platforms (for example Linux to Windows)

  * Giving access to replicated data to different groups of users.

  * Sharing a subset of the database between multiple databases.

The subscriber database behaves in the same way as any other PostgreSQL
instance and can be used as a publisher for other databases by defining its
own publications. When the subscriber is treated as read-only by application,
there will be no conflicts from a single subscription. On the other hand, if
there are other writes done either by an application or by other subscribers
to the same set of tables, conflicts can arise.

* * *

[Prev](wal-internals.html "30.6. WAL Internals")  | [Up](admin.html "Part III. Server Administration") |  [Next](logical-replication-publication.html "31.1. Publication")  
---|---|---  
30.6. WAL Internals  | [Home](index.html "PostgreSQL 16.9 Documentation") |  31.1. Publication  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logical-replication.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

