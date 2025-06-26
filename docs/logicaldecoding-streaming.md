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

Supported Versions: [Current](/docs/current/logicaldecoding-streaming.html
"PostgreSQL 17 - 49.9. Streaming of Large Transactions for Logical Decoding")
([17](/docs/17/logicaldecoding-streaming.html "PostgreSQL 17 - 49.9. Streaming
of Large Transactions for Logical Decoding")) / [16](/docs/16/logicaldecoding-
streaming.html "PostgreSQL 16 - 49.9. Streaming of Large Transactions for
Logical Decoding") / [15](/docs/15/logicaldecoding-streaming.html "PostgreSQL
15 - 49.9. Streaming of Large Transactions for Logical Decoding") /
[14](/docs/14/logicaldecoding-streaming.html "PostgreSQL 14 - 49.9. Streaming
of Large Transactions for Logical Decoding")

Development Versions: [18](/docs/18/logicaldecoding-streaming.html "PostgreSQL
18 - 49.9. Streaming of Large Transactions for Logical Decoding") /
[devel](/docs/devel/logicaldecoding-streaming.html "PostgreSQL devel -
49.9. Streaming of Large Transactions for Logical Decoding")

__

49.9. Streaming of Large Transactions for Logical Decoding  
---  
[Prev](logicaldecoding-synchronous.html "49.8. Synchronous Replication Support for Logical Decoding")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") | Chapter 49. Logical Decoding | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logicaldecoding-two-phase-commits.html "49.10. Two-phase Commit Support for Logical Decoding")  
  
* * *

## 49.9. Streaming of Large Transactions for Logical Decoding #

The basic output plugin callbacks (e.g., `begin_cb`, `change_cb`, `commit_cb`
and `message_cb`) are only invoked when the transaction actually commits. The
changes are still decoded from the transaction log, but are only passed to the
output plugin at commit (and discarded if the transaction aborts).

This means that while the decoding happens incrementally, and may spill to
disk to keep memory usage under control, all the decoded changes have to be
transmitted when the transaction finally commits (or more precisely, when the
commit is decoded from the transaction log). Depending on the size of the
transaction and network bandwidth, the transfer time may significantly
increase the apply lag.

To reduce the apply lag caused by large transactions, an output plugin may
provide additional callback to support incremental streaming of in-progress
transactions. There are multiple required streaming callbacks
(`stream_start_cb`, `stream_stop_cb`, `stream_abort_cb`, `stream_commit_cb`
and `stream_change_cb`) and two optional callbacks (`stream_message_cb` and
`stream_truncate_cb`). Also, if streaming of two-phase commands is to be
supported, then additional callbacks must be provided. (See [Section
49.10](logicaldecoding-two-phase-commits.html "49.10. Two-phase Commit Support
for Logical Decoding") for details).

When streaming an in-progress transaction, the changes (and messages) are
streamed in blocks demarcated by `stream_start_cb` and `stream_stop_cb`
callbacks. Once all the decoded changes are transmitted, the transaction can
be committed using the `stream_commit_cb` callback (or possibly aborted using
the `stream_abort_cb` callback). If two-phase commits are supported, the
transaction can be prepared using the `stream_prepare_cb` callback, `COMMIT
PREPARED` using the `commit_prepared_cb` callback or aborted using the
`rollback_prepared_cb`.

One example sequence of streaming callback calls for one transaction may look
like this:

    
    
    stream_start_cb(...);   <-- start of first block of changes
      stream_change_cb(...);
      stream_change_cb(...);
      stream_message_cb(...);
      stream_change_cb(...);
      ...
      stream_change_cb(...);
    stream_stop_cb(...);    <-- end of first block of changes
    
    stream_start_cb(...);   <-- start of second block of changes
      stream_change_cb(...);
      stream_change_cb(...);
      stream_change_cb(...);
      ...
      stream_message_cb(...);
      stream_change_cb(...);
    stream_stop_cb(...);    <-- end of second block of changes
    
    
    [a. when using normal commit]
    stream_commit_cb(...);    <-- commit of the streamed transaction
    
    [b. when using two-phase commit]
    stream_prepare_cb(...);   <-- prepare the streamed transaction
    commit_prepared_cb(...);  <-- commit of the prepared transaction
    

The actual sequence of callback calls may be more complicated, of course.
There may be blocks for multiple streamed transactions, some of the
transactions may get aborted, etc.

Similar to spill-to-disk behavior, streaming is triggered when the total
amount of changes decoded from the WAL (for all in-progress transactions)
exceeds the limit defined by `logical_decoding_work_mem` setting. At that
point, the largest top-level transaction (measured by the amount of memory
currently used for decoded changes) is selected and streamed. However, in some
cases we still have to spill to disk even if streaming is enabled because we
exceed the memory threshold but still have not decoded the complete tuple
e.g., only decoded toast table insert but not the main table insert.

Even when streaming large transactions, the changes are still applied in
commit order, preserving the same guarantees as the non-streaming mode.

* * *

[Prev](logicaldecoding-synchronous.html "49.8. Synchronous Replication Support for Logical Decoding")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") |  [Next](logicaldecoding-two-phase-commits.html "49.10. Two-phase Commit Support for Logical Decoding")  
---|---|---  
49.8. Synchronous Replication Support for Logical Decoding  | [Home](index.html "PostgreSQL 16.9 Documentation") |  49.10. Two-phase Commit Support for Logical Decoding  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logicaldecoding-
streaming.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

