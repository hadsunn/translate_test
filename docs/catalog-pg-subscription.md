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

Supported Versions: [Current](/docs/current/catalog-pg-subscription.html
"PostgreSQL 17 - 53.54. pg_subscription") ([17](/docs/17/catalog-pg-
subscription.html "PostgreSQL 17 - 53.54. pg_subscription")) /
[16](/docs/16/catalog-pg-subscription.html "PostgreSQL 16 -
53.54. pg_subscription") / [15](/docs/15/catalog-pg-subscription.html
"PostgreSQL 15 - 53.54. pg_subscription") / [14](/docs/14/catalog-pg-
subscription.html "PostgreSQL 14 - 53.54. pg_subscription") /
[13](/docs/13/catalog-pg-subscription.html "PostgreSQL 13 -
53.54. pg_subscription")

Development Versions: [18](/docs/18/catalog-pg-subscription.html "PostgreSQL
18 - 53.54. pg_subscription") / [devel](/docs/devel/catalog-pg-
subscription.html "PostgreSQL devel - 53.54. pg_subscription")

Unsupported versions: [12](/docs/12/catalog-pg-subscription.html "PostgreSQL
12 - 53.54. pg_subscription") / [11](/docs/11/catalog-pg-subscription.html
"PostgreSQL 11 - 53.54. pg_subscription") / [10](/docs/10/catalog-pg-
subscription.html "PostgreSQL 10 - 53.54. pg_subscription")

__

53.54. `pg_subscription`  
---  
[Prev](catalog-pg-statistic-ext-data.html "53.53. pg_statistic_ext_data")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-subscription-rel.html "53.55. pg_subscription_rel")  
  
* * *

## 53.54. `pg_subscription` #

The catalog `pg_subscription` contains all existing logical replication
subscriptions. For more information about logical replication see [Chapter
31](logical-replication.html "Chapter 31. Logical Replication").

Unlike most system catalogs, `pg_subscription` is shared across all databases
of a cluster: there is only one copy of `pg_subscription` per cluster, not one
per database.

Access to the column `subconninfo` is revoked from normal users, because it
could contain plain-text passwords.

**Table  53.54. `pg_subscription` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`subdbid` `oid` (references [`pg_database`](catalog-pg-database.html
"53.15. pg_database").`oid`) OID of the database that the subscription resides
in  
`subskiplsn` `pg_lsn` Finish LSN of the transaction whose changes are to be
skipped, if a valid LSN; otherwise `0/0`.  
`subname` `name` Name of the subscription  
`subowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the subscription  
`subenabled` `bool` If true, the subscription is enabled and should be
replicating  
`subbinary` `bool` If true, the subscription will request that the publisher
send data in binary format  
`substream` `char` Controls how to handle the streaming of in-progress
transactions: `f` = disallow streaming of in-progress transactions, `t` =
spill the changes of in-progress transactions to disk and apply at once after
the transaction is committed on the publisher and received by the subscriber,
`p` = apply changes directly using a parallel apply worker if available (same
as 't' if no worker is available)  
`subtwophasestate` `char` State codes for two-phase mode: `d` = disabled, `p`
= pending enablement, `e` = enabled  
`subdisableonerr` `bool` If true, the subscription will be disabled if one of
its workers detects an error  
`subpasswordrequired` `bool` If true, the subscription will be required to
specify a password for authentication  
`subrunasowner` `bool` If true, the subscription will be run with the
permissions of the subscription owner  
`subconninfo` `text` Connection string to the upstream database  
`subslotname` `name` Name of the replication slot in the upstream database
(also used for the local replication origin name); null represents `NONE`  
`subsynccommit` `text` The `synchronous_commit` setting for the subscription's
workers to use  
`subpublications` `text[]` Array of subscribed publication names. These
reference publications defined in the upstream database. For more on
publications see [Section 31.1](logical-replication-publication.html
"31.1. Publication").  
`suborigin` `text` The origin value must be either `none` or `any`. The
default is `any`. If `none`, the subscription will request the publisher to
only send changes that don't have an origin. If `any`, the publisher sends
changes regardless of their origin.  
  
  

* * *

[Prev](catalog-pg-statistic-ext-data.html "53.53. pg_statistic_ext_data")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-subscription-rel.html "53.55. pg_subscription_rel")  
---|---|---  
53.53. `pg_statistic_ext_data`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.55. `pg_subscription_rel`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-subscription.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

