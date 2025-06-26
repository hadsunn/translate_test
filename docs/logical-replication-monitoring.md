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
monitoring.html "PostgreSQL 17 - 31.8. Monitoring") ([17](/docs/17/logical-
replication-monitoring.html "PostgreSQL 17 - 31.8. Monitoring")) /
[16](/docs/16/logical-replication-monitoring.html "PostgreSQL 16 -
31.8. Monitoring") / [15](/docs/15/logical-replication-monitoring.html
"PostgreSQL 15 - 31.8. Monitoring") / [14](/docs/14/logical-replication-
monitoring.html "PostgreSQL 14 - 31.8. Monitoring") / [13](/docs/13/logical-
replication-monitoring.html "PostgreSQL 13 - 31.8. Monitoring")

Development Versions: [18](/docs/18/logical-replication-monitoring.html
"PostgreSQL 18 - 31.8. Monitoring") / [devel](/docs/devel/logical-replication-
monitoring.html "PostgreSQL devel - 31.8. Monitoring")

Unsupported versions: [12](/docs/12/logical-replication-monitoring.html
"PostgreSQL 12 - 31.8. Monitoring") / [11](/docs/11/logical-replication-
monitoring.html "PostgreSQL 11 - 31.8. Monitoring") / [10](/docs/10/logical-
replication-monitoring.html "PostgreSQL 10 - 31.8. Monitoring")

__

31.8. Monitoring  
---  
[Prev](logical-replication-architecture.html "31.7. Architecture")  | [Up](logical-replication.html "Chapter 31. Logical Replication") | Chapter 31. Logical Replication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logical-replication-security.html "31.9. Security")  
  
* * *

## 31.8. Monitoring #

Because logical replication is based on a similar architecture as [physical
streaming replication](warm-standby.html#STREAMING-REPLICATION
"27.2.5. Streaming Replication"), the monitoring on a publication node is
similar to monitoring of a physical replication primary (see [Section
27.2.5.2](warm-standby.html#STREAMING-REPLICATION-MONITORING
"27.2.5.2. Monitoring")).

The monitoring information about subscription is visible in
[`pg_stat_subscription`](monitoring-stats.html#MONITORING-PG-STAT-SUBSCRIPTION
"28.2.8. pg_stat_subscription"). This view contains one row for every
subscription worker. A subscription can have zero or more active subscription
workers depending on its state.

Normally, there is a single apply process running for an enabled subscription.
A disabled subscription or a crashed subscription will have zero rows in this
view. If the initial data synchronization of any table is in progress, there
will be additional workers for the tables being synchronized. Moreover, if the
[`streaming`](sql-createsubscription.html#SQL-CREATESUBSCRIPTION-WITH-
STREAMING) transaction is applied in parallel, there may be additional
parallel apply workers.

* * *

[Prev](logical-replication-architecture.html "31.7. Architecture")  | [Up](logical-replication.html "Chapter 31. Logical Replication") |  [Next](logical-replication-security.html "31.9. Security")  
---|---|---  
31.7. Architecture  | [Home](index.html "PostgreSQL 16.9 Documentation") |  31.9. Security  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logical-replication-
monitoring.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

