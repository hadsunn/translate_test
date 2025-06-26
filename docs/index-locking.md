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

Supported Versions: [Current](/docs/current/index-locking.html "PostgreSQL 17
- 64.4. Index Locking Considerations") ([17](/docs/17/index-locking.html
"PostgreSQL 17 - 64.4. Index Locking Considerations")) / [16](/docs/16/index-
locking.html "PostgreSQL 16 - 64.4. Index Locking Considerations") /
[15](/docs/15/index-locking.html "PostgreSQL 15 - 64.4. Index Locking
Considerations") / [14](/docs/14/index-locking.html "PostgreSQL 14 -
64.4. Index Locking Considerations") / [13](/docs/13/index-locking.html
"PostgreSQL 13 - 64.4. Index Locking Considerations")

Development Versions: [18](/docs/18/index-locking.html "PostgreSQL 18 -
64.4. Index Locking Considerations") / [devel](/docs/devel/index-locking.html
"PostgreSQL devel - 64.4. Index Locking Considerations")

Unsupported versions: [12](/docs/12/index-locking.html "PostgreSQL 12 -
64.4. Index Locking Considerations") / [11](/docs/11/index-locking.html
"PostgreSQL 11 - 64.4. Index Locking Considerations") / [10](/docs/10/index-
locking.html "PostgreSQL 10 - 64.4. Index Locking Considerations") /
[9.6](/docs/9.6/index-locking.html "PostgreSQL 9.6 - 64.4. Index Locking
Considerations") / [9.5](/docs/9.5/index-locking.html "PostgreSQL 9.5 -
64.4. Index Locking Considerations") / [9.4](/docs/9.4/index-locking.html
"PostgreSQL 9.4 - 64.4. Index Locking Considerations") /
[9.3](/docs/9.3/index-locking.html "PostgreSQL 9.3 - 64.4. Index Locking
Considerations") / [9.2](/docs/9.2/index-locking.html "PostgreSQL 9.2 -
64.4. Index Locking Considerations") / [9.1](/docs/9.1/index-locking.html
"PostgreSQL 9.1 - 64.4. Index Locking Considerations") /
[9.0](/docs/9.0/index-locking.html "PostgreSQL 9.0 - 64.4. Index Locking
Considerations") / [8.4](/docs/8.4/index-locking.html "PostgreSQL 8.4 -
64.4. Index Locking Considerations") / [8.3](/docs/8.3/index-locking.html
"PostgreSQL 8.3 - 64.4. Index Locking Considerations") /
[8.2](/docs/8.2/index-locking.html "PostgreSQL 8.2 - 64.4. Index Locking
Considerations") / [8.1](/docs/8.1/index-locking.html "PostgreSQL 8.1 -
64.4. Index Locking Considerations")

__

64.4. Index Locking Considerations  
---  
[Prev](index-scanning.html "64.3. Index Scanning")  | [Up](indexam.html "Chapter 64. Index Access Method Interface Definition") | Chapter 64. Index Access Method Interface Definition | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](index-unique-checks.html "64.5. Index Uniqueness Checks")  
  
* * *

## 64.4. Index Locking Considerations #

Index access methods must handle concurrent updates of the index by multiple
processes. The core PostgreSQL system obtains `AccessShareLock` on the index
during an index scan, and `RowExclusiveLock` when updating the index
(including plain `VACUUM`). Since these lock types do not conflict, the access
method is responsible for handling any fine-grained locking it might need. An
`ACCESS EXCLUSIVE` lock on the index as a whole will be taken only during
index creation, destruction, or `REINDEX` (`SHARE UPDATE EXCLUSIVE` is taken
instead with `CONCURRENTLY`).

Building an index type that supports concurrent updates usually requires
extensive and subtle analysis of the required behavior. For the b-tree and
hash index types, you can read about the design decisions involved in
`src/backend/access/nbtree/README` and `src/backend/access/hash/README`.

Aside from the index's own internal consistency requirements, concurrent
updates create issues about consistency between the parent table (the _heap_)
and the index. Because PostgreSQL separates accesses and updates of the heap
from those of the index, there are windows in which the index might be
inconsistent with the heap. We handle this problem with the following rules:

  * A new heap entry is made before making its index entries. (Therefore a concurrent index scan is likely to fail to see the heap entry. This is okay because the index reader would be uninterested in an uncommitted row anyway. But see [Section 64.5](index-unique-checks.html "64.5. Index Uniqueness Checks").)

  * When a heap entry is to be deleted (by `VACUUM`), all its index entries must be removed first.

  * An index scan must maintain a pin on the index page holding the item last returned by `amgettuple`, and `ambulkdelete` cannot delete entries from pages that are pinned by other backends. The need for this rule is explained below.

Without the third rule, it is possible for an index reader to see an index
entry just before it is removed by `VACUUM`, and then to arrive at the
corresponding heap entry after that was removed by `VACUUM`. This creates no
serious problems if that item number is still unused when the reader reaches
it, since an empty item slot will be ignored by `heap_fetch()`. But what if a
third backend has already re-used the item slot for something else? When using
an MVCC-compliant snapshot, there is no problem because the new occupant of
the slot is certain to be too new to pass the snapshot test. However, with a
non-MVCC-compliant snapshot (such as `SnapshotAny`), it would be possible to
accept and return a row that does not in fact match the scan keys. We could
defend against this scenario by requiring the scan keys to be rechecked
against the heap row in all cases, but that is too expensive. Instead, we use
a pin on an index page as a proxy to indicate that the reader might still be
“in flight” from the index entry to the matching heap entry. Making
`ambulkdelete` block on such a pin ensures that `VACUUM` cannot delete the
heap entry before the reader is done with it. This solution costs little in
run time, and adds blocking overhead only in the rare cases where there
actually is a conflict.

This solution requires that index scans be “synchronous”: we have to fetch
each heap tuple immediately after scanning the corresponding index entry. This
is expensive for a number of reasons. An “asynchronous” scan in which we
collect many TIDs from the index, and only visit the heap tuples sometime
later, requires much less index locking overhead and can allow a more
efficient heap access pattern. Per the above analysis, we must use the
synchronous approach for non-MVCC-compliant snapshots, but an asynchronous
scan is workable for a query using an MVCC snapshot.

In an `amgetbitmap` index scan, the access method does not keep an index pin
on any of the returned tuples. Therefore it is only safe to use such scans
with MVCC-compliant snapshots.

When the `ampredlocks` flag is not set, any scan using that index access
method within a serializable transaction will acquire a nonblocking predicate
lock on the full index. This will generate a read-write conflict with the
insert of any tuple into that index by a concurrent serializable transaction.
If certain patterns of read-write conflicts are detected among a set of
concurrent serializable transactions, one of those transactions may be
canceled to protect data integrity. When the flag is set, it indicates that
the index access method implements finer-grained predicate locking, which will
tend to reduce the frequency of such transaction cancellations.

* * *

[Prev](index-scanning.html "64.3. Index Scanning")  | [Up](indexam.html "Chapter 64. Index Access Method Interface Definition") |  [Next](index-unique-checks.html "64.5. Index Uniqueness Checks")  
---|---|---  
64.3. Index Scanning  | [Home](index.html "PostgreSQL 16.9 Documentation") |  64.5. Index Uniqueness Checks  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/index-locking.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

