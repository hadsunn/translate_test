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

Supported Versions: [16](/docs/16/brin-intro.html "PostgreSQL 16 -
71.1. Introduction") / [15](/docs/15/brin-intro.html "PostgreSQL 15 -
71.1. Introduction") / [14](/docs/14/brin-intro.html "PostgreSQL 14 -
71.1. Introduction") / [13](/docs/13/brin-intro.html "PostgreSQL 13 -
71.1. Introduction")

Unsupported versions: [12](/docs/12/brin-intro.html "PostgreSQL 12 -
71.1. Introduction") / [11](/docs/11/brin-intro.html "PostgreSQL 11 -
71.1. Introduction") / [10](/docs/10/brin-intro.html "PostgreSQL 10 -
71.1. Introduction") / [9.6](/docs/9.6/brin-intro.html "PostgreSQL 9.6 -
71.1. Introduction") / [9.5](/docs/9.5/brin-intro.html "PostgreSQL 9.5 -
71.1. Introduction")

__

71.1. Introduction  
---  
[Prev](brin.html "Chapter 71. BRIN Indexes")  | [Up](brin.html "Chapter 71. BRIN Indexes") | Chapter 71. BRIN Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](brin-builtin-opclasses.html "71.2. Built-in Operator Classes")  
  
* * *

## 71.1. Introduction #

[71.1.1. Index Maintenance](brin-intro.html#BRIN-OPERATION)

BRIN stands for Block Range Index. BRIN is designed for handling very large
tables in which certain columns have some natural correlation with their
physical location within the table.

BRIN works in terms of _block ranges_ (or “page ranges”). A block range is a
group of pages that are physically adjacent in the table; for each block
range, some summary info is stored by the index. For example, a table storing
a store's sale orders might have a date column on which each order was placed,
and most of the time the entries for earlier orders will appear earlier in the
table as well; a table storing a ZIP code column might have all codes for a
city grouped together naturally.

BRIN indexes can satisfy queries via regular bitmap index scans, and will
return all tuples in all pages within each range if the summary info stored by
the index is _consistent_ with the query conditions. The query executor is in
charge of rechecking these tuples and discarding those that do not match the
query conditions — in other words, these indexes are lossy. Because a BRIN
index is very small, scanning the index adds little overhead compared to a
sequential scan, but may avoid scanning large parts of the table that are
known not to contain matching tuples.

The specific data that a BRIN index will store, as well as the specific
queries that the index will be able to satisfy, depend on the operator class
selected for each column of the index. Data types having a linear sort order
can have operator classes that store the minimum and maximum value within each
block range, for instance; geometrical types might store the bounding box for
all the objects in the block range.

The size of the block range is determined at index creation time by the
`pages_per_range` storage parameter. The number of index entries will be equal
to the size of the relation in pages divided by the selected value for
`pages_per_range`. Therefore, the smaller the number, the larger the index
becomes (because of the need to store more index entries), but at the same
time the summary data stored can be more precise and more data blocks can be
skipped during an index scan.

### 71.1.1. Index Maintenance #

At the time of creation, all existing heap pages are scanned and a summary
index tuple is created for each range, including the possibly-incomplete range
at the end. As new pages are filled with data, page ranges that are already
summarized will cause the summary information to be updated with data from the
new tuples. When a new page is created that does not fall within the last
summarized range, the range that the new page belongs to does not
automatically acquire a summary tuple; those tuples remain unsummarized until
a summarization run is invoked later, creating the initial summary for that
range.

There are several ways to trigger the initial summarization of a page range.
If the table is vacuumed, either manually or by [autovacuum](routine-
vacuuming.html#AUTOVACUUM "25.1.6. The Autovacuum Daemon"), all existing
unsummarized page ranges are summarized. Also, if the index's
[autosummarize](sql-createindex.html#INDEX-RELOPTION-AUTOSUMMARIZE) parameter
is enabled, which it isn't by default, whenever autovacuum runs in that
database, summarization will occur for all unsummarized page ranges that have
been filled, regardless of whether the table itself is processed by
autovacuum; see below.

Lastly, the following functions can be used:

`brin_summarize_new_values(regclass)` which summarizes all unsummarized
ranges;  
---  
`brin_summarize_range(regclass, bigint)` which summarizes only the range
containing the given page, if it is unsummarized.  
  
When autosummarization is enabled, a request is sent to `autovacuum` to
execute a targeted summarization for a block range when an insertion is
detected for the first item of the first page of the next block range, to be
fulfilled the next time an autovacuum worker finishes running in the same
database. If the request queue is full, the request is not recorded and a
message is sent to the server log:

    
    
    LOG:  request for BRIN range summarization for index "brin_wi_idx" page 128 was not recorded
    

When this happens, the range will remain unsummarized until the next regular
vacuum run on the table, or one of the functions mentioned above are invoked.

Conversely, a range can be de-summarized using the
`brin_desummarize_range(regclass, bigint)` function, which is useful when the
index tuple is no longer a very good representation because the existing
values have changed. See [Section 9.27.8](functions-admin.html#FUNCTIONS-
ADMIN-INDEX "9.27.8. Index Maintenance Functions") for details.

* * *

[Prev](brin.html "Chapter 71. BRIN Indexes")  | [Up](brin.html "Chapter 71. BRIN Indexes") |  [Next](brin-builtin-opclasses.html "71.2. Built-in Operator Classes")  
---|---|---  
Chapter 71. BRIN Indexes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  71.2. Built-in Operator Classes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/brin-intro.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

