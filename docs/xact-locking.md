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

Supported Versions: [Current](/docs/current/xact-locking.html "PostgreSQL 17 -
74.2. Transactions and Locking") ([17](/docs/17/xact-locking.html "PostgreSQL
17 - 74.2. Transactions and Locking")) / [16](/docs/16/xact-locking.html
"PostgreSQL 16 - 74.2. Transactions and Locking")

Development Versions: [18](/docs/18/xact-locking.html "PostgreSQL 18 -
74.2. Transactions and Locking") / [devel](/docs/devel/xact-locking.html
"PostgreSQL devel - 74.2. Transactions and Locking")

__

74.2. Transactions and Locking  
---  
[Prev](transaction-id.html "74.1. Transactions and Identifiers")  | [Up](transactions.html "Chapter 74. Transaction Processing") | Chapter 74. Transaction Processing | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](subxacts.html "74.3. Subtransactions")  
  
* * *

## 74.2. Transactions and Locking #

The transaction IDs of currently executing transactions are shown in
[`pg_locks`](view-pg-locks.html "54.12. pg_locks") in columns `virtualxid` and
`transactionid`. Read-only transactions will have `virtualxid`s but NULL
`transactionid`s, while both columns will be set in read-write transactions.

Some lock types wait on `virtualxid`, while other types wait on
`transactionid`. Row-level read and write locks are recorded directly in the
locked rows and can be inspected using the [pgrowlocks](pgrowlocks.html
"F.31. pgrowlocks — show a table's row locking information") extension. Row-
level read locks might also require the assignment of multixact IDs (`mxid`;
see [Section 25.1.5.1](routine-vacuuming.html#VACUUM-FOR-MULTIXACT-WRAPAROUND
"25.1.5.1. Multixacts and Wraparound")).

* * *

[Prev](transaction-id.html "74.1. Transactions and Identifiers")  | [Up](transactions.html "Chapter 74. Transaction Processing") |  [Next](subxacts.html "74.3. Subtransactions")  
---|---|---  
74.1. Transactions and Identifiers  | [Home](index.html "PostgreSQL 16.9 Documentation") |  74.3. Subtransactions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/xact-locking.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

