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

Supported Versions: [16](/docs/16/gin-implementation.html "PostgreSQL 16 -
70.4. Implementation") / [15](/docs/15/gin-implementation.html "PostgreSQL 15
- 70.4. Implementation") / [14](/docs/14/gin-implementation.html "PostgreSQL
14 - 70.4. Implementation") / [13](/docs/13/gin-implementation.html
"PostgreSQL 13 - 70.4. Implementation")

Unsupported versions: [12](/docs/12/gin-implementation.html "PostgreSQL 12 -
70.4. Implementation") / [11](/docs/11/gin-implementation.html "PostgreSQL 11
- 70.4. Implementation") / [10](/docs/10/gin-implementation.html "PostgreSQL
10 - 70.4. Implementation") / [9.6](/docs/9.6/gin-implementation.html
"PostgreSQL 9.6 - 70.4. Implementation") / [9.5](/docs/9.5/gin-
implementation.html "PostgreSQL 9.5 - 70.4. Implementation") /
[9.4](/docs/9.4/gin-implementation.html "PostgreSQL 9.4 -
70.4. Implementation") / [9.3](/docs/9.3/gin-implementation.html "PostgreSQL
9.3 - 70.4. Implementation") / [9.2](/docs/9.2/gin-implementation.html
"PostgreSQL 9.2 - 70.4. Implementation") / [9.1](/docs/9.1/gin-
implementation.html "PostgreSQL 9.1 - 70.4. Implementation") /
[9.0](/docs/9.0/gin-implementation.html "PostgreSQL 9.0 -
70.4. Implementation") / [8.4](/docs/8.4/gin-implementation.html "PostgreSQL
8.4 - 70.4. Implementation") / [8.3](/docs/8.3/gin-implementation.html
"PostgreSQL 8.3 - 70.4. Implementation") / [8.2](/docs/8.2/gin-
implementation.html "PostgreSQL 8.2 - 70.4. Implementation")

__

70.4. Implementation  
---  
[Prev](gin-extensibility.html "70.3. Extensibility")  | [Up](gin.html "Chapter 70. GIN Indexes") | Chapter 70. GIN Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](gin-tips.html "70.5. GIN Tips and Tricks")  
  
* * *

## 70.4. Implementation #

[70.4.1. GIN Fast Update Technique](gin-implementation.html#GIN-FAST-UPDATE)

[70.4.2. Partial Match Algorithm](gin-implementation.html#GIN-PARTIAL-MATCH)

Internally, a GIN index contains a B-tree index constructed over keys, where
each key is an element of one or more indexed items (a member of an array, for
example) and where each tuple in a leaf page contains either a pointer to a
B-tree of heap pointers (a “posting tree”), or a simple list of heap pointers
(a “posting list”) when the list is small enough to fit into a single index
tuple along with the key value. [Figure 70.1](gin-implementation.html#GIN-
INTERNALS-FIGURE "Figure 70.1. GIN Internals") illustrates these components of
a GIN index.

As of PostgreSQL 9.1, null key values can be included in the index. Also,
placeholder nulls are included in the index for indexed items that are null or
contain no keys according to `extractValue`. This allows searches that should
find empty items to do so.

Multicolumn GIN indexes are implemented by building a single B-tree over
composite values (column number, key value). The key values for different
columns can be of different types.

**Figure  70.1. GIN Internals**

  

### 70.4.1. GIN Fast Update Technique #

Updating a GIN index tends to be slow because of the intrinsic nature of
inverted indexes: inserting or updating one heap row can cause many inserts
into the index (one for each key extracted from the indexed item). GIN is
capable of postponing much of this work by inserting new tuples into a
temporary, unsorted list of pending entries. When the table is vacuumed or
autoanalyzed, or when `gin_clean_pending_list` function is called, or if the
pending list becomes larger than [gin_pending_list_limit](runtime-config-
client.html#GUC-GIN-PENDING-LIST-LIMIT), the entries are moved to the main GIN
data structure using the same bulk insert techniques used during initial index
creation. This greatly improves GIN index update speed, even counting the
additional vacuum overhead. Moreover the overhead work can be done by a
background process instead of in foreground query processing.

The main disadvantage of this approach is that searches must scan the list of
pending entries in addition to searching the regular index, and so a large
list of pending entries will slow searches significantly. Another disadvantage
is that, while most updates are fast, an update that causes the pending list
to become “too large” will incur an immediate cleanup cycle and thus be much
slower than other updates. Proper use of autovacuum can minimize both of these
problems.

If consistent response time is more important than update speed, use of
pending entries can be disabled by turning off the `fastupdate` storage
parameter for a GIN index. See [CREATE INDEX](sql-createindex.html "CREATE
INDEX") for details.

### 70.4.2. Partial Match Algorithm #

GIN can support “partial match” queries, in which the query does not determine
an exact match for one or more keys, but the possible matches fall within a
reasonably narrow range of key values (within the key sorting order determined
by the `compare` support method). The `extractQuery` method, instead of
returning a key value to be matched exactly, returns a key value that is the
lower bound of the range to be searched, and sets the `pmatch` flag true. The
key range is then scanned using the `comparePartial` method. `comparePartial`
must return zero for a matching index key, less than zero for a non-match that
is still within the range to be searched, or greater than zero if the index
key is past the range that could match.

* * *

[Prev](gin-extensibility.html "70.3. Extensibility")  | [Up](gin.html "Chapter 70. GIN Indexes") |  [Next](gin-tips.html "70.5. GIN Tips and Tricks")  
---|---|---  
70.3. Extensibility  | [Home](index.html "PostgreSQL 16.9 Documentation") |  70.5. GIN Tips and Tricks  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/gin-implementation.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

