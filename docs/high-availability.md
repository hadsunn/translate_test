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

Supported Versions: [Current](/docs/current/high-availability.html "PostgreSQL
17 - Chapter 27. High Availability, Load Balancing, and Replication")
([17](/docs/17/high-availability.html "PostgreSQL 17 - Chapter 27. High
Availability, Load Balancing, and Replication")) / [16](/docs/16/high-
availability.html "PostgreSQL 16 - Chapter 27. High Availability, Load
Balancing, and Replication") / [15](/docs/15/high-availability.html
"PostgreSQL 15 - Chapter 27. High Availability, Load Balancing, and
Replication") / [14](/docs/14/high-availability.html "PostgreSQL 14 -
Chapter 27. High Availability, Load Balancing, and Replication") /
[13](/docs/13/high-availability.html "PostgreSQL 13 - Chapter 27. High
Availability, Load Balancing, and Replication")

Development Versions: [18](/docs/18/high-availability.html "PostgreSQL 18 -
Chapter 27. High Availability, Load Balancing, and Replication") /
[devel](/docs/devel/high-availability.html "PostgreSQL devel -
Chapter 27. High Availability, Load Balancing, and Replication")

Unsupported versions: [12](/docs/12/high-availability.html "PostgreSQL 12 -
Chapter 27. High Availability, Load Balancing, and Replication") /
[11](/docs/11/high-availability.html "PostgreSQL 11 - Chapter 27. High
Availability, Load Balancing, and Replication") / [10](/docs/10/high-
availability.html "PostgreSQL 10 - Chapter 27. High Availability, Load
Balancing, and Replication") / [9.6](/docs/9.6/high-availability.html
"PostgreSQL 9.6 - Chapter 27. High Availability, Load Balancing, and
Replication") / [9.5](/docs/9.5/high-availability.html "PostgreSQL 9.5 -
Chapter 27. High Availability, Load Balancing, and Replication") /
[9.4](/docs/9.4/high-availability.html "PostgreSQL 9.4 - Chapter 27. High
Availability, Load Balancing, and Replication") / [9.3](/docs/9.3/high-
availability.html "PostgreSQL 9.3 - Chapter 27. High Availability, Load
Balancing, and Replication") / [9.2](/docs/9.2/high-availability.html
"PostgreSQL 9.2 - Chapter 27. High Availability, Load Balancing, and
Replication") / [9.1](/docs/9.1/high-availability.html "PostgreSQL 9.1 -
Chapter 27. High Availability, Load Balancing, and Replication") /
[9.0](/docs/9.0/high-availability.html "PostgreSQL 9.0 - Chapter 27. High
Availability, Load Balancing, and Replication") / [8.4](/docs/8.4/high-
availability.html "PostgreSQL 8.4 - Chapter 27. High Availability, Load
Balancing, and Replication") / [8.3](/docs/8.3/high-availability.html
"PostgreSQL 8.3 - Chapter 27. High Availability, Load Balancing, and
Replication") / [8.2](/docs/8.2/high-availability.html "PostgreSQL 8.2 -
Chapter 27. High Availability, Load Balancing, and Replication")

__

Chapter 27. High Availability, Load Balancing, and Replication  
---  
[Prev](continuous-archiving.html "26.3. Continuous Archiving and Point-in-Time Recovery \(PITR\)")  | [Up](admin.html "Part III. Server Administration") | Part III. Server Administration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](different-replication-solutions.html "27.1. Comparison of Different Solutions")  
  
* * *

## Chapter 27. High Availability, Load Balancing, and Replication

**Table of Contents**

[27.1. Comparison of Different Solutions](different-replication-
solutions.html)

[27.2. Log-Shipping Standby Servers](warm-standby.html)

    

[27.2.1. Planning](warm-standby.html#STANDBY-PLANNING)

[27.2.2. Standby Server Operation](warm-standby.html#STANDBY-SERVER-OPERATION)

[27.2.3. Preparing the Primary for Standby Servers](warm-
standby.html#PREPARING-PRIMARY-FOR-STANDBY)

[27.2.4. Setting Up a Standby Server](warm-standby.html#STANDBY-SERVER-SETUP)

[27.2.5. Streaming Replication](warm-standby.html#STREAMING-REPLICATION)

[27.2.6. Replication Slots](warm-standby.html#STREAMING-REPLICATION-SLOTS)

[27.2.7. Cascading Replication](warm-standby.html#CASCADING-REPLICATION)

[27.2.8. Synchronous Replication](warm-standby.html#SYNCHRONOUS-REPLICATION)

[27.2.9. Continuous Archiving in Standby](warm-standby.html#CONTINUOUS-
ARCHIVING-IN-STANDBY)

[27.3. Failover](warm-standby-failover.html)

[27.4. Hot Standby](hot-standby.html)

    

[27.4.1. User's Overview](hot-standby.html#HOT-STANDBY-USERS)

[27.4.2. Handling Query Conflicts](hot-standby.html#HOT-STANDBY-CONFLICT)

[27.4.3. Administrator's Overview](hot-standby.html#HOT-STANDBY-ADMIN)

[27.4.4. Hot Standby Parameter Reference](hot-standby.html#HOT-STANDBY-
PARAMETERS)

[27.4.5. Caveats](hot-standby.html#HOT-STANDBY-CAVEATS)

Database servers can work together to allow a second server to take over
quickly if the primary server fails (high availability), or to allow several
computers to serve the same data (load balancing). Ideally, database servers
could work together seamlessly. Web servers serving static web pages can be
combined quite easily by merely load-balancing web requests to multiple
machines. In fact, read-only database servers can be combined relatively
easily too. Unfortunately, most database servers have a read/write mix of
requests, and read/write servers are much harder to combine. This is because
though read-only data needs to be placed on each server only once, a write to
any server has to be propagated to all servers so that future read requests to
those servers return consistent results.

This synchronization problem is the fundamental difficulty for servers working
together. Because there is no single solution that eliminates the impact of
the sync problem for all use cases, there are multiple solutions. Each
solution addresses this problem in a different way, and minimizes its impact
for a specific workload.

Some solutions deal with synchronization by allowing only one server to modify
the data. Servers that can modify data are called read/write, _master_ or
_primary_ servers. Servers that track changes in the primary are called
_standby_ or _secondary_ servers. A standby server that cannot be connected to
until it is promoted to a primary server is called a _warm standby_ server,
and one that can accept connections and serves read-only queries is called a
_hot standby_ server.

Some solutions are synchronous, meaning that a data-modifying transaction is
not considered committed until all servers have committed the transaction.
This guarantees that a failover will not lose any data and that all load-
balanced servers will return consistent results no matter which server is
queried. In contrast, asynchronous solutions allow some delay between the time
of a commit and its propagation to the other servers, opening the possibility
that some transactions might be lost in the switch to a backup server, and
that load balanced servers might return slightly stale results. Asynchronous
communication is used when synchronous would be too slow.

Solutions can also be categorized by their granularity. Some solutions can
deal only with an entire database server, while others allow control at the
per-table or per-database level.

Performance must be considered in any choice. There is usually a trade-off
between functionality and performance. For example, a fully synchronous
solution over a slow network might cut performance by more than half, while an
asynchronous one might have a minimal performance impact.

The remainder of this section outlines various failover, replication, and load
balancing solutions.

* * *

[Prev](continuous-archiving.html "26.3. Continuous Archiving and Point-in-Time Recovery \(PITR\)")  | [Up](admin.html "Part III. Server Administration") |  [Next](different-replication-solutions.html "27.1. Comparison of Different Solutions")  
---|---|---  
26.3. Continuous Archiving and Point-in-Time Recovery (PITR)  | [Home](index.html "PostgreSQL 16.9 Documentation") |  27.1. Comparison of Different Solutions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/high-availability.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

