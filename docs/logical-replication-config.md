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

Supported Versions: [Current](/docs/current/logical-replication-config.html
"PostgreSQL 17 - 31.10. Configuration Settings") ([17](/docs/17/logical-
replication-config.html "PostgreSQL 17 - 31.10. Configuration Settings")) /
[16](/docs/16/logical-replication-config.html "PostgreSQL 16 -
31.10. Configuration Settings") / [15](/docs/15/logical-replication-
config.html "PostgreSQL 15 - 31.10. Configuration Settings") /
[14](/docs/14/logical-replication-config.html "PostgreSQL 14 -
31.10. Configuration Settings") / [13](/docs/13/logical-replication-
config.html "PostgreSQL 13 - 31.10. Configuration Settings")

Development Versions: [18](/docs/18/logical-replication-config.html
"PostgreSQL 18 - 31.10. Configuration Settings") /
[devel](/docs/devel/logical-replication-config.html "PostgreSQL devel -
31.10. Configuration Settings")

Unsupported versions: [12](/docs/12/logical-replication-config.html
"PostgreSQL 12 - 31.10. Configuration Settings") / [11](/docs/11/logical-
replication-config.html "PostgreSQL 11 - 31.10. Configuration Settings") /
[10](/docs/10/logical-replication-config.html "PostgreSQL 10 -
31.10. Configuration Settings")

__

31.10. Configuration Settings  
---  
[Prev](logical-replication-security.html "31.9. Security")  | [Up](logical-replication.html "Chapter 31. Logical Replication") | Chapter 31. Logical Replication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logical-replication-quick-setup.html "31.11. Quick Setup")  
  
* * *

## 31.10. Configuration Settings #

[31.10.1. Publishers](logical-replication-config.html#LOGICAL-REPLICATION-
CONFIG-PUBLISHER)

[31.10.2. Subscribers](logical-replication-config.html#LOGICAL-REPLICATION-
CONFIG-SUBSCRIBER)

Logical replication requires several configuration options to be set. Most
options are relevant only on one side of the replication. However,
`max_replication_slots` is used on both the publisher and the subscriber, but
it has a different meaning for each.

### 31.10.1. Publishers #

[`wal_level`](runtime-config-wal.html#GUC-WAL-LEVEL) must be set to `logical`.

[`max_replication_slots`](runtime-config-replication.html#GUC-MAX-REPLICATION-
SLOTS) must be set to at least the number of subscriptions expected to
connect, plus some reserve for table synchronization.

[`max_wal_senders`](runtime-config-replication.html#GUC-MAX-WAL-SENDERS)
should be set to at least the same as `max_replication_slots`, plus the number
of physical replicas that are connected at the same time.

Logical replication walsender is also affected by
[`wal_sender_timeout`](runtime-config-replication.html#GUC-WAL-SENDER-
TIMEOUT).

### 31.10.2. Subscribers #

[`max_replication_slots`](runtime-config-replication.html#GUC-MAX-REPLICATION-
SLOTS-SUBSCRIBER) must be set to at least the number of subscriptions that
will be added to the subscriber, plus some reserve for table synchronization.

[`max_logical_replication_workers`](runtime-config-replication.html#GUC-MAX-
LOGICAL-REPLICATION-WORKERS) must be set to at least the number of
subscriptions (for leader apply workers), plus some reserve for the table
synchronization workers and parallel apply workers.

[`max_worker_processes`](runtime-config-resource.html#GUC-MAX-WORKER-
PROCESSES) may need to be adjusted to accommodate for replication workers, at
least ([`max_logical_replication_workers`](runtime-config-
replication.html#GUC-MAX-LOGICAL-REPLICATION-WORKERS) \+ `1`). Note, some
extensions and parallel queries also take worker slots from
`max_worker_processes`.

[`max_sync_workers_per_subscription`](runtime-config-replication.html#GUC-MAX-
SYNC-WORKERS-PER-SUBSCRIPTION) controls the amount of parallelism of the
initial data copy during the subscription initialization or when new tables
are added.

[`max_parallel_apply_workers_per_subscription`](runtime-config-
replication.html#GUC-MAX-PARALLEL-APPLY-WORKERS-PER-SUBSCRIPTION) controls the
amount of parallelism for streaming of in-progress transactions with
subscription parameter `streaming = parallel`.

Logical replication workers are also affected by
[`wal_receiver_timeout`](runtime-config-replication.html#GUC-WAL-RECEIVER-
TIMEOUT), [`wal_receiver_status_interval`](runtime-config-
replication.html#GUC-WAL-RECEIVER-STATUS-INTERVAL) and
[`wal_retrieve_retry_interval`](runtime-config-replication.html#GUC-WAL-
RETRIEVE-RETRY-INTERVAL).

* * *

[Prev](logical-replication-security.html "31.9. Security")  | [Up](logical-replication.html "Chapter 31. Logical Replication") |  [Next](logical-replication-quick-setup.html "31.11. Quick Setup")  
---|---|---  
31.9. Security  | [Home](index.html "PostgreSQL 16.9 Documentation") |  31.11. Quick Setup  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logical-replication-
config.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

