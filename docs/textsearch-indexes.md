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

Supported Versions: [Current](/docs/current/textsearch-indexes.html
"PostgreSQL 17 - 12.9. Preferred Index Types for Text Search")
([17](/docs/17/textsearch-indexes.html "PostgreSQL 17 - 12.9. Preferred Index
Types for Text Search")) / [16](/docs/16/textsearch-indexes.html "PostgreSQL
16 - 12.9. Preferred Index Types for Text Search") / [15](/docs/15/textsearch-
indexes.html "PostgreSQL 15 - 12.9. Preferred Index Types for Text Search") /
[14](/docs/14/textsearch-indexes.html "PostgreSQL 14 - 12.9. Preferred Index
Types for Text Search") / [13](/docs/13/textsearch-indexes.html "PostgreSQL 13
- 12.9. Preferred Index Types for Text Search")

Development Versions: [18](/docs/18/textsearch-indexes.html "PostgreSQL 18 -
12.9. Preferred Index Types for Text Search") /
[devel](/docs/devel/textsearch-indexes.html "PostgreSQL devel -
12.9. Preferred Index Types for Text Search")

Unsupported versions: [12](/docs/12/textsearch-indexes.html "PostgreSQL 12 -
12.9. Preferred Index Types for Text Search") / [11](/docs/11/textsearch-
indexes.html "PostgreSQL 11 - 12.9. Preferred Index Types for Text Search") /
[10](/docs/10/textsearch-indexes.html "PostgreSQL 10 - 12.9. Preferred Index
Types for Text Search") / [9.6](/docs/9.6/textsearch-indexes.html "PostgreSQL
9.6 - 12.9. Preferred Index Types for Text Search") /
[9.5](/docs/9.5/textsearch-indexes.html "PostgreSQL 9.5 - 12.9. Preferred
Index Types for Text Search") / [9.4](/docs/9.4/textsearch-indexes.html
"PostgreSQL 9.4 - 12.9. Preferred Index Types for Text Search") /
[9.3](/docs/9.3/textsearch-indexes.html "PostgreSQL 9.3 - 12.9. Preferred
Index Types for Text Search") / [9.2](/docs/9.2/textsearch-indexes.html
"PostgreSQL 9.2 - 12.9. Preferred Index Types for Text Search") /
[9.1](/docs/9.1/textsearch-indexes.html "PostgreSQL 9.1 - 12.9. Preferred
Index Types for Text Search") / [9.0](/docs/9.0/textsearch-indexes.html
"PostgreSQL 9.0 - 12.9. Preferred Index Types for Text Search") /
[8.4](/docs/8.4/textsearch-indexes.html "PostgreSQL 8.4 - 12.9. Preferred
Index Types for Text Search") / [8.3](/docs/8.3/textsearch-indexes.html
"PostgreSQL 8.3 - 12.9. Preferred Index Types for Text Search")

__

12.9. Preferred Index Types for Text Search  
---  
[Prev](textsearch-debugging.html "12.8. Testing and Debugging Text Search")  | [Up](textsearch.html "Chapter 12. Full Text Search") | Chapter 12. Full Text Search | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](textsearch-psql.html "12.10. psql Support")  
  
* * *

## 12.9. Preferred Index Types for Text Search #

There are two kinds of indexes that can be used to speed up full text
searches: [GIN](gin.html "Chapter 70. GIN Indexes") and [GiST](gist.html
"Chapter 68. GiST Indexes"). Note that indexes are not mandatory for full text
searching, but in cases where a column is searched on a regular basis, an
index is usually desirable.

To create such an index, do one of:

`CREATE INDEX _`name`_ ON _`table`_ USING GIN (_`column`_);`

    

Creates a GIN (Generalized Inverted Index)-based index. The _`column`_ must be
of `tsvector` type.

`CREATE INDEX _`name`_ ON _`table`_ USING GIST (_`column`_ [ { DEFAULT | tsvector_ops } (siglen = _`number`_) ] );`
    

Creates a GiST (Generalized Search Tree)-based index. The _`column`_ can be of
`tsvector` or `tsquery` type. Optional integer parameter `siglen` determines
signature length in bytes (see below for details).

GIN indexes are the preferred text search index type. As inverted indexes,
they contain an index entry for each word (lexeme), with a compressed list of
matching locations. Multi-word searches can find the first match, then use the
index to remove rows that are lacking additional words. GIN indexes store only
the words (lexemes) of `tsvector` values, and not their weight labels. Thus a
table row recheck is needed when using a query that involves weights.

A GiST index is _lossy_ , meaning that the index might produce false matches,
and it is necessary to check the actual table row to eliminate such false
matches. (PostgreSQL does this automatically when needed.) GiST indexes are
lossy because each document is represented in the index by a fixed-length
signature. The signature length in bytes is determined by the value of the
optional integer parameter `siglen`. The default signature length (when
`siglen` is not specified) is 124 bytes, the maximum signature length is 2024
bytes. The signature is generated by hashing each word into a single bit in an
n-bit string, with all these bits OR-ed together to produce an n-bit document
signature. When two words hash to the same bit position there will be a false
match. If all words in the query have matches (real or false) then the table
row must be retrieved to see if the match is correct. Longer signatures lead
to a more precise search (scanning a smaller fraction of the index and fewer
heap pages), at the cost of a larger index.

A GiST index can be covering, i.e., use the `INCLUDE` clause. Included columns
can have data types without any GiST operator class. Included attributes will
be stored uncompressed.

Lossiness causes performance degradation due to unnecessary fetches of table
records that turn out to be false matches. Since random access to table
records is slow, this limits the usefulness of GiST indexes. The likelihood of
false matches depends on several factors, in particular the number of unique
words, so using dictionaries to reduce this number is recommended.

Note that GIN index build time can often be improved by increasing
[maintenance_work_mem](runtime-config-resource.html#GUC-MAINTENANCE-WORK-MEM),
while GiST index build time is not sensitive to that parameter.

Partitioning of big collections and the proper use of GIN and GiST indexes
allows the implementation of very fast searches with online update.
Partitioning can be done at the database level using table inheritance, or by
distributing documents over servers and collecting external search results,
e.g., via [Foreign Data](ddl-foreign-data.html "5.12. Foreign Data") access.
The latter is possible because ranking functions use only local information.

* * *

[Prev](textsearch-debugging.html "12.8. Testing and Debugging Text Search")  | [Up](textsearch.html "Chapter 12. Full Text Search") |  [Next](textsearch-psql.html "12.10. psql Support")  
---|---|---  
12.8. Testing and Debugging Text Search  | [Home](index.html "PostgreSQL 16.9 Documentation") |  12.10. psql Support  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/textsearch-indexes.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

