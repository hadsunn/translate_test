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

Supported Versions: [Current](/docs/current/catalog-pg-subscription-rel.html
"PostgreSQL 17 - 53.55. pg_subscription_rel") ([17](/docs/17/catalog-pg-
subscription-rel.html "PostgreSQL 17 - 53.55. pg_subscription_rel")) /
[16](/docs/16/catalog-pg-subscription-rel.html "PostgreSQL 16 -
53.55. pg_subscription_rel") / [15](/docs/15/catalog-pg-subscription-rel.html
"PostgreSQL 15 - 53.55. pg_subscription_rel") / [14](/docs/14/catalog-pg-
subscription-rel.html "PostgreSQL 14 - 53.55. pg_subscription_rel") /
[13](/docs/13/catalog-pg-subscription-rel.html "PostgreSQL 13 -
53.55. pg_subscription_rel")

Development Versions: [18](/docs/18/catalog-pg-subscription-rel.html
"PostgreSQL 18 - 53.55. pg_subscription_rel") / [devel](/docs/devel/catalog-
pg-subscription-rel.html "PostgreSQL devel - 53.55. pg_subscription_rel")

Unsupported versions: [12](/docs/12/catalog-pg-subscription-rel.html
"PostgreSQL 12 - 53.55. pg_subscription_rel") / [11](/docs/11/catalog-pg-
subscription-rel.html "PostgreSQL 11 - 53.55. pg_subscription_rel") /
[10](/docs/10/catalog-pg-subscription-rel.html "PostgreSQL 10 -
53.55. pg_subscription_rel")

__

53.55. `pg_subscription_rel`  
---  
[Prev](catalog-pg-subscription.html "53.54. pg_subscription")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-tablespace.html "53.56. pg_tablespace")  
  
* * *

## 53.55. `pg_subscription_rel` #

The catalog `pg_subscription_rel` contains the state for each replicated
relation in each subscription. This is a many-to-many mapping.

This catalog only contains tables known to the subscription after running
either [`CREATE SUBSCRIPTION`](sql-createsubscription.html "CREATE
SUBSCRIPTION") or [`ALTER SUBSCRIPTION ... REFRESH PUBLICATION`](sql-
altersubscription.html "ALTER SUBSCRIPTION").

**Table  53.55. `pg_subscription_rel` Columns**

Column Type Description  
---  
`srsubid` `oid` (references [`pg_subscription`](catalog-pg-subscription.html
"53.54. pg_subscription").`oid`) Reference to subscription  
`srrelid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) Reference to relation  
`srsubstate` `char` State code: `i` = initialize, `d` = data is being copied,
`f` = finished table copy, `s` = synchronized, `r` = ready (normal
replication)  
`srsublsn` `pg_lsn` Remote LSN of the state change used for synchronization
coordination when in `s` or `r` states, otherwise null  
  
  

* * *

[Prev](catalog-pg-subscription.html "53.54. pg_subscription")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-tablespace.html "53.56. pg_tablespace")  
---|---|---  
53.54. `pg_subscription`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.56. `pg_tablespace`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-subscription-
rel.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

