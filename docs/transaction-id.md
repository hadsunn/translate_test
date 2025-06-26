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

Supported Versions: [Current](/docs/current/transaction-id.html "PostgreSQL 17
- 74.1. Transactions and Identifiers") ([17](/docs/17/transaction-id.html
"PostgreSQL 17 - 74.1. Transactions and Identifiers")) /
[16](/docs/16/transaction-id.html "PostgreSQL 16 - 74.1. Transactions and
Identifiers")

Development Versions: [18](/docs/18/transaction-id.html "PostgreSQL 18 -
74.1. Transactions and Identifiers") / [devel](/docs/devel/transaction-id.html
"PostgreSQL devel - 74.1. Transactions and Identifiers")

__

74.1. Transactions and Identifiers  
---  
[Prev](transactions.html "Chapter 74. Transaction Processing")  | [Up](transactions.html "Chapter 74. Transaction Processing") | Chapter 74. Transaction Processing | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](xact-locking.html "74.2. Transactions and Locking")  
  
* * *

## 74.1. Transactions and Identifiers #

Transactions can be created explicitly using `BEGIN` or `START TRANSACTION`
and ended using `COMMIT` or `ROLLBACK`. SQL statements outside of explicit
transactions automatically use single-statement transactions.

Every transaction is identified by a unique `VirtualTransactionId` (also
called `virtualXID` or `vxid`), which is comprised of a backend ID (or
`backendID`) and a sequentially-assigned number local to each backend, known
as `localXID`. For example, the virtual transaction ID `4/12532` has a
`backendID` of `4` and a `localXID` of `12532`.

Non-virtual `TransactionId`s (or `xid`), e.g., `278394`, are assigned
sequentially to transactions from a global counter used by all databases
within the PostgreSQL cluster. This assignment happens when a transaction
first writes to the database. This means lower-numbered xids started writing
before higher-numbered xids. Note that the order in which transactions perform
their first database write might be different from the order in which the
transactions started, particularly if the transaction started with statements
that only performed database reads.

The internal transaction ID type `xid` is 32 bits wide and [wraps
around](routine-vacuuming.html#VACUUM-FOR-WRAPAROUND "25.1.5. Preventing
Transaction ID Wraparound Failures") every 4 billion transactions. A 32-bit
epoch is incremented during each wraparound. There is also a 64-bit type
`xid8` which includes this epoch and therefore does not wrap around during the
life of an installation; it can be converted to xid by casting. The functions
in [Table 9.80](functions-info.html#FUNCTIONS-PG-SNAPSHOT
"Table 9.80. Transaction ID and Snapshot Information Functions") return `xid8`
values. Xids are used as the basis for PostgreSQL's [MVCC](mvcc.html
"Chapter 13. Concurrency Control") concurrency mechanism and streaming
replication.

When a top-level transaction with a (non-virtual) xid commits, it is marked as
committed in the `pg_xact` directory. Additional information is recorded in
the `pg_commit_ts` directory if [track_commit_timestamp](runtime-config-
replication.html#GUC-TRACK-COMMIT-TIMESTAMP) is enabled.

In addition to `vxid` and `xid`, prepared transactions are also assigned
Global Transaction Identifiers (GID). GIDs are string literals up to 200 bytes
long, which must be unique amongst other currently prepared transactions. The
mapping of GID to xid is shown in [`pg_prepared_xacts`](view-pg-prepared-
xacts.html "54.16. pg_prepared_xacts").

* * *

[Prev](transactions.html "Chapter 74. Transaction Processing")  | [Up](transactions.html "Chapter 74. Transaction Processing") |  [Next](xact-locking.html "74.2. Transactions and Locking")  
---|---|---  
Chapter 74. Transaction Processing  | [Home](index.html "PostgreSQL 16.9 Documentation") |  74.2. Transactions and Locking  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/transaction-id.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

