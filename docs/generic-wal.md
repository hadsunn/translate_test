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

Supported Versions: [Current](/docs/current/generic-wal.html "PostgreSQL 17 -
Chapter 65. Generic WAL Records") ([17](/docs/17/generic-wal.html "PostgreSQL
17 - Chapter 65. Generic WAL Records")) / [16](/docs/16/generic-wal.html
"PostgreSQL 16 - Chapter 65. Generic WAL Records") / [15](/docs/15/generic-
wal.html "PostgreSQL 15 - Chapter 65. Generic WAL Records") /
[14](/docs/14/generic-wal.html "PostgreSQL 14 - Chapter 65. Generic WAL
Records") / [13](/docs/13/generic-wal.html "PostgreSQL 13 -
Chapter 65. Generic WAL Records")

Development Versions: [18](/docs/18/generic-wal.html "PostgreSQL 18 -
Chapter 65. Generic WAL Records") / [devel](/docs/devel/generic-wal.html
"PostgreSQL devel - Chapter 65. Generic WAL Records")

Unsupported versions: [12](/docs/12/generic-wal.html "PostgreSQL 12 -
Chapter 65. Generic WAL Records") / [11](/docs/11/generic-wal.html "PostgreSQL
11 - Chapter 65. Generic WAL Records") / [10](/docs/10/generic-wal.html
"PostgreSQL 10 - Chapter 65. Generic WAL Records") / [9.6](/docs/9.6/generic-
wal.html "PostgreSQL 9.6 - Chapter 65. Generic WAL Records")

__

Chapter 65. Generic WAL Records  
---  
[Prev](index-cost-estimation.html "64.6. Index Cost Estimation Functions")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](custom-rmgr.html "Chapter 66. Custom WAL Resource Managers")  
  
* * *

## Chapter 65. Generic WAL Records

Although all built-in WAL-logged modules have their own types of WAL records,
there is also a generic WAL record type, which describes changes to pages in a
generic way. This is useful for extensions that provide custom access methods.

In comparison with [Custom WAL Resource Managers](custom-rmgr.html
"Chapter 66. Custom WAL Resource Managers"), Generic WAL is simpler for an
extension to implement and does not require the extension library to be loaded
in order to apply the records.

### Note

Generic WAL records are ignored during [Logical Decoding](logicaldecoding.html
"Chapter 49. Logical Decoding"). If logical decoding is required for your
extension, consider a Custom WAL Resource Manager.

The API for constructing generic WAL records is defined in
`access/generic_xlog.h` and implemented in `access/transam/generic_xlog.c`.

To perform a WAL-logged data update using the generic WAL record facility,
follow these steps:

  1. `state = GenericXLogStart(relation)` — start construction of a generic WAL record for the given relation.

  2. `page = GenericXLogRegisterBuffer(state, buffer, flags)` — register a buffer to be modified within the current generic WAL record. This function returns a pointer to a temporary copy of the buffer's page, where modifications should be made. (Do not modify the buffer's contents directly.) The third argument is a bit mask of flags applicable to the operation. Currently the only such flag is `GENERIC_XLOG_FULL_IMAGE`, which indicates that a full-page image rather than a delta update should be included in the WAL record. Typically this flag would be set if the page is new or has been rewritten completely. `GenericXLogRegisterBuffer` can be repeated if the WAL-logged action needs to modify multiple pages.

  3. Apply modifications to the page images obtained in the previous step.

  4. `GenericXLogFinish(state)` — apply the changes to the buffers and emit the generic WAL record.

WAL record construction can be canceled between any of the above steps by
calling `GenericXLogAbort(state)`. This will discard all changes to the page
image copies.

Please note the following points when using the generic WAL record facility:

  * No direct modifications of buffers are allowed! All modifications must be done in copies acquired from `GenericXLogRegisterBuffer()`. In other words, code that makes generic WAL records should never call `BufferGetPage()` for itself. However, it remains the caller's responsibility to pin/unpin and lock/unlock the buffers at appropriate times. Exclusive lock must be held on each target buffer from before `GenericXLogRegisterBuffer()` until after `GenericXLogFinish()`.

  * Registrations of buffers (step 2) and modifications of page images (step 3) can be mixed freely, i.e., both steps may be repeated in any sequence. Keep in mind that buffers should be registered in the same order in which locks are to be obtained on them during replay.

  * The maximum number of buffers that can be registered for a generic WAL record is `MAX_GENERIC_XLOG_PAGES`. An error will be thrown if this limit is exceeded.

  * Generic WAL assumes that the pages to be modified have standard layout, and in particular that there is no useful data between `pd_lower` and `pd_upper`.

  * Since you are modifying copies of buffer pages, `GenericXLogStart()` does not start a critical section. Thus, you can safely do memory allocation, error throwing, etc. between `GenericXLogStart()` and `GenericXLogFinish()`. The only actual critical section is present inside `GenericXLogFinish()`. There is no need to worry about calling `GenericXLogAbort()` during an error exit, either.

  * `GenericXLogFinish()` takes care of marking buffers dirty and setting their LSNs. You do not need to do this explicitly.

  * For unlogged relations, everything works the same except that no actual WAL record is emitted. Thus, you typically do not need to do any explicit checks for unlogged relations.

  * The generic WAL redo function will acquire exclusive locks to buffers in the same order as they were registered. After redoing all changes, the locks will be released in the same order.

  * If `GENERIC_XLOG_FULL_IMAGE` is not specified for a registered buffer, the generic WAL record contains a delta between the old and the new page images. This delta is based on byte-by-byte comparison. This is not very compact for the case of moving data within a page, and might be improved in the future.

* * *

[Prev](index-cost-estimation.html "64.6. Index Cost Estimation Functions")  | [Up](internals.html "Part VII. Internals") |  [Next](custom-rmgr.html "Chapter 66. Custom WAL Resource Managers")  
---|---|---  
64.6. Index Cost Estimation Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 66. Custom WAL Resource Managers  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/generic-wal.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

