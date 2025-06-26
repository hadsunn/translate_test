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

Supported Versions: [Current](/docs/current/mvcc-intro.html "PostgreSQL 17 -
13.1. Introduction") ([17](/docs/17/mvcc-intro.html "PostgreSQL 17 -
13.1. Introduction")) / [16](/docs/16/mvcc-intro.html "PostgreSQL 16 -
13.1. Introduction") / [15](/docs/15/mvcc-intro.html "PostgreSQL 15 -
13.1. Introduction") / [14](/docs/14/mvcc-intro.html "PostgreSQL 14 -
13.1. Introduction") / [13](/docs/13/mvcc-intro.html "PostgreSQL 13 -
13.1. Introduction")

Development Versions: [18](/docs/18/mvcc-intro.html "PostgreSQL 18 -
13.1. Introduction") / [devel](/docs/devel/mvcc-intro.html "PostgreSQL devel -
13.1. Introduction")

Unsupported versions: [12](/docs/12/mvcc-intro.html "PostgreSQL 12 -
13.1. Introduction") / [11](/docs/11/mvcc-intro.html "PostgreSQL 11 -
13.1. Introduction") / [10](/docs/10/mvcc-intro.html "PostgreSQL 10 -
13.1. Introduction") / [9.6](/docs/9.6/mvcc-intro.html "PostgreSQL 9.6 -
13.1. Introduction") / [9.5](/docs/9.5/mvcc-intro.html "PostgreSQL 9.5 -
13.1. Introduction") / [9.4](/docs/9.4/mvcc-intro.html "PostgreSQL 9.4 -
13.1. Introduction") / [9.3](/docs/9.3/mvcc-intro.html "PostgreSQL 9.3 -
13.1. Introduction") / [9.2](/docs/9.2/mvcc-intro.html "PostgreSQL 9.2 -
13.1. Introduction") / [9.1](/docs/9.1/mvcc-intro.html "PostgreSQL 9.1 -
13.1. Introduction") / [9.0](/docs/9.0/mvcc-intro.html "PostgreSQL 9.0 -
13.1. Introduction") / [8.4](/docs/8.4/mvcc-intro.html "PostgreSQL 8.4 -
13.1. Introduction") / [8.3](/docs/8.3/mvcc-intro.html "PostgreSQL 8.3 -
13.1. Introduction") / [8.2](/docs/8.2/mvcc-intro.html "PostgreSQL 8.2 -
13.1. Introduction")

__

13.1. Introduction  
---  
[Prev](mvcc.html "Chapter 13. Concurrency Control")  | [Up](mvcc.html "Chapter 13. Concurrency Control") | Chapter 13. Concurrency Control | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](transaction-iso.html "13.2. Transaction Isolation")  
  
* * *

## 13.1. Introduction #

PostgreSQL provides a rich set of tools for developers to manage concurrent
access to data. Internally, data consistency is maintained by using a
multiversion model (Multiversion Concurrency Control, MVCC). This means that
each SQL statement sees a snapshot of data (a _database version_) as it was
some time ago, regardless of the current state of the underlying data. This
prevents statements from viewing inconsistent data produced by concurrent
transactions performing updates on the same data rows, providing _transaction
isolation_ for each database session. MVCC, by eschewing the locking
methodologies of traditional database systems, minimizes lock contention in
order to allow for reasonable performance in multiuser environments.

The main advantage of using the MVCC model of concurrency control rather than
locking is that in MVCC locks acquired for querying (reading) data do not
conflict with locks acquired for writing data, and so reading never blocks
writing and writing never blocks reading. PostgreSQL maintains this guarantee
even when providing the strictest level of transaction isolation through the
use of an innovative _Serializable Snapshot Isolation_ (SSI) level.

Table- and row-level locking facilities are also available in PostgreSQL for
applications which don't generally need full transaction isolation and prefer
to explicitly manage particular points of conflict. However, proper use of
MVCC will generally provide better performance than locks. In addition,
application-defined advisory locks provide a mechanism for acquiring locks
that are not tied to a single transaction.

* * *

[Prev](mvcc.html "Chapter 13. Concurrency Control")  | [Up](mvcc.html "Chapter 13. Concurrency Control") |  [Next](transaction-iso.html "13.2. Transaction Isolation")  
---|---|---  
Chapter 13. Concurrency Control  | [Home](index.html "PostgreSQL 16.9 Documentation") |  13.2. Transaction Isolation  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/mvcc-intro.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

