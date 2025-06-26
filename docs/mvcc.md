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

Supported Versions: [Current](/docs/current/mvcc.html "PostgreSQL 17 -
Chapter 13. Concurrency Control") ([17](/docs/17/mvcc.html "PostgreSQL 17 -
Chapter 13. Concurrency Control")) / [16](/docs/16/mvcc.html "PostgreSQL 16 -
Chapter 13. Concurrency Control") / [15](/docs/15/mvcc.html "PostgreSQL 15 -
Chapter 13. Concurrency Control") / [14](/docs/14/mvcc.html "PostgreSQL 14 -
Chapter 13. Concurrency Control") / [13](/docs/13/mvcc.html "PostgreSQL 13 -
Chapter 13. Concurrency Control")

Development Versions: [18](/docs/18/mvcc.html "PostgreSQL 18 -
Chapter 13. Concurrency Control") / [devel](/docs/devel/mvcc.html "PostgreSQL
devel - Chapter 13. Concurrency Control")

Unsupported versions: [12](/docs/12/mvcc.html "PostgreSQL 12 -
Chapter 13. Concurrency Control") / [11](/docs/11/mvcc.html "PostgreSQL 11 -
Chapter 13. Concurrency Control") / [10](/docs/10/mvcc.html "PostgreSQL 10 -
Chapter 13. Concurrency Control") / [9.6](/docs/9.6/mvcc.html "PostgreSQL 9.6
- Chapter 13. Concurrency Control") / [9.5](/docs/9.5/mvcc.html "PostgreSQL
9.5 - Chapter 13. Concurrency Control") / [9.4](/docs/9.4/mvcc.html
"PostgreSQL 9.4 - Chapter 13. Concurrency Control") /
[9.3](/docs/9.3/mvcc.html "PostgreSQL 9.3 - Chapter 13. Concurrency Control")
/ [9.2](/docs/9.2/mvcc.html "PostgreSQL 9.2 - Chapter 13. Concurrency
Control") / [9.1](/docs/9.1/mvcc.html "PostgreSQL 9.1 -
Chapter 13. Concurrency Control") / [9.0](/docs/9.0/mvcc.html "PostgreSQL 9.0
- Chapter 13. Concurrency Control") / [8.4](/docs/8.4/mvcc.html "PostgreSQL
8.4 - Chapter 13. Concurrency Control") / [8.3](/docs/8.3/mvcc.html
"PostgreSQL 8.3 - Chapter 13. Concurrency Control") /
[8.2](/docs/8.2/mvcc.html "PostgreSQL 8.2 - Chapter 13. Concurrency Control")
/ [8.1](/docs/8.1/mvcc.html "PostgreSQL 8.1 - Chapter 13. Concurrency
Control") / [8.0](/docs/8.0/mvcc.html "PostgreSQL 8.0 -
Chapter 13. Concurrency Control") / [7.4](/docs/7.4/mvcc.html "PostgreSQL 7.4
- Chapter 13. Concurrency Control") / [7.3](/docs/7.3/mvcc.html "PostgreSQL
7.3 - Chapter 13. Concurrency Control") / [7.2](/docs/7.2/mvcc.html
"PostgreSQL 7.2 - Chapter 13. Concurrency Control") /
[7.1](/docs/7.1/mvcc.html "PostgreSQL 7.1 - Chapter 13. Concurrency Control")

__

Chapter 13. Concurrency Control  
---  
[Prev](textsearch-limitations.html "12.11. Limitations")  | [Up](sql.html "Part II. The SQL Language") | Part II. The SQL Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](mvcc-intro.html "13.1. Introduction")  
  
* * *

## Chapter 13. Concurrency Control

**Table of Contents**

[13.1. Introduction](mvcc-intro.html)

[13.2. Transaction Isolation](transaction-iso.html)

    

[13.2.1. Read Committed Isolation Level](transaction-iso.html#XACT-READ-
COMMITTED)

[13.2.2. Repeatable Read Isolation Level](transaction-iso.html#XACT-
REPEATABLE-READ)

[13.2.3. Serializable Isolation Level](transaction-iso.html#XACT-SERIALIZABLE)

[13.3. Explicit Locking](explicit-locking.html)

    

[13.3.1. Table-Level Locks](explicit-locking.html#LOCKING-TABLES)

[13.3.2. Row-Level Locks](explicit-locking.html#LOCKING-ROWS)

[13.3.3. Page-Level Locks](explicit-locking.html#LOCKING-PAGES)

[13.3.4. Deadlocks](explicit-locking.html#LOCKING-DEADLOCKS)

[13.3.5. Advisory Locks](explicit-locking.html#ADVISORY-LOCKS)

[13.4. Data Consistency Checks at the Application Level](applevel-
consistency.html)

    

[13.4.1. Enforcing Consistency with Serializable Transactions](applevel-
consistency.html#SERIALIZABLE-CONSISTENCY)

[13.4.2. Enforcing Consistency with Explicit Blocking Locks](applevel-
consistency.html#NON-SERIALIZABLE-CONSISTENCY)

[13.5. Serialization Failure Handling](mvcc-serialization-failure-
handling.html)

[13.6. Caveats](mvcc-caveats.html)

[13.7. Locking and Indexes](locking-indexes.html)

This chapter describes the behavior of the PostgreSQL database system when two
or more sessions try to access the same data at the same time. The goals in
that situation are to allow efficient access for all sessions while
maintaining strict data integrity. Every developer of database applications
should be familiar with the topics covered in this chapter.

* * *

[Prev](textsearch-limitations.html "12.11. Limitations")  | [Up](sql.html "Part II. The SQL Language") |  [Next](mvcc-intro.html "13.1. Introduction")  
---|---|---  
12.11. Limitations  | [Home](index.html "PostgreSQL 16.9 Documentation") |  13.1. Introduction  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/mvcc.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

