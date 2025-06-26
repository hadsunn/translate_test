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

Supported Versions: [Current](/docs/current/logicaldecoding-two-phase-
commits.html "PostgreSQL 17 - 49.10. Two-phase Commit Support for Logical
Decoding") ([17](/docs/17/logicaldecoding-two-phase-commits.html "PostgreSQL
17 - 49.10. Two-phase Commit Support for Logical Decoding")) /
[16](/docs/16/logicaldecoding-two-phase-commits.html "PostgreSQL 16 -
49.10. Two-phase Commit Support for Logical Decoding") /
[15](/docs/15/logicaldecoding-two-phase-commits.html "PostgreSQL 15 -
49.10. Two-phase Commit Support for Logical Decoding") /
[14](/docs/14/logicaldecoding-two-phase-commits.html "PostgreSQL 14 -
49.10. Two-phase Commit Support for Logical Decoding")

Development Versions: [18](/docs/18/logicaldecoding-two-phase-commits.html
"PostgreSQL 18 - 49.10. Two-phase Commit Support for Logical Decoding") /
[devel](/docs/devel/logicaldecoding-two-phase-commits.html "PostgreSQL devel -
49.10. Two-phase Commit Support for Logical Decoding")

__

49.10. Two-phase Commit Support for Logical Decoding  
---  
[Prev](logicaldecoding-streaming.html "49.9. Streaming of Large Transactions for Logical Decoding")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") | Chapter 49. Logical Decoding | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](replication-origins.html "Chapter 50. Replication Progress Tracking")  
  
* * *

## 49.10. Two-phase Commit Support for Logical Decoding #

With the basic output plugin callbacks (eg., `begin_cb`, `change_cb`,
`commit_cb` and `message_cb`) two-phase commit commands like `PREPARE
TRANSACTION`, `COMMIT PREPARED` and `ROLLBACK PREPARED` are not decoded. While
the `PREPARE TRANSACTION` is ignored, `COMMIT PREPARED` is decoded as a
`COMMIT` and `ROLLBACK PREPARED` is decoded as a `ROLLBACK`.

To support the streaming of two-phase commands, an output plugin needs to
provide additional callbacks. There are multiple two-phase commit callbacks
that are required, (`begin_prepare_cb`, `prepare_cb`, `commit_prepared_cb`,
`rollback_prepared_cb` and `stream_prepare_cb`) and an optional callback
(`filter_prepare_cb`).

If the output plugin callbacks for decoding two-phase commit commands are
provided, then on `PREPARE TRANSACTION`, the changes of that transaction are
decoded, passed to the output plugin, and the `prepare_cb` callback is
invoked. This differs from the basic decoding setup where changes are only
passed to the output plugin when a transaction is committed. The start of a
prepared transaction is indicated by the `begin_prepare_cb` callback.

When a prepared transaction is rolled back using the `ROLLBACK PREPARED`, then
the `rollback_prepared_cb` callback is invoked and when the prepared
transaction is committed using `COMMIT PREPARED`, then the
`commit_prepared_cb` callback is invoked.

Optionally the output plugin can define filtering rules via
`filter_prepare_cb` to decode only specific transaction in two phases. This
can be achieved by pattern matching on the _`gid`_ or via lookups using the
_`xid`_.

The users that want to decode prepared transactions need to be careful about
below mentioned points:

  * If the prepared transaction has locked [user] catalog tables exclusively then decoding prepare can block till the main transaction is committed.

  * The logical replication solution that builds distributed two phase commit using this feature can deadlock if the prepared transaction has locked [user] catalog tables exclusively. To avoid this users must refrain from having locks on catalog tables (e.g. explicit `LOCK` command) in such transactions. See [Section 49.8.2](logicaldecoding-synchronous.html#LOGICALDECODING-SYNCHRONOUS-CAVEATS "49.8.2. Caveats") for the details.

* * *

[Prev](logicaldecoding-streaming.html "49.9. Streaming of Large Transactions for Logical Decoding")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") |  [Next](replication-origins.html "Chapter 50. Replication Progress Tracking")  
---|---|---  
49.9. Streaming of Large Transactions for Logical Decoding  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 50. Replication Progress Tracking  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logicaldecoding-two-phase-
commits.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

