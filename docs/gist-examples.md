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

Supported Versions: [16](/docs/16/gist-examples.html "PostgreSQL 16 -
68.5. Examples") / [15](/docs/15/gist-examples.html "PostgreSQL 15 -
68.5. Examples") / [14](/docs/14/gist-examples.html "PostgreSQL 14 -
68.5. Examples") / [13](/docs/13/gist-examples.html "PostgreSQL 13 -
68.5. Examples")

Unsupported versions: [12](/docs/12/gist-examples.html "PostgreSQL 12 -
68.5. Examples") / [11](/docs/11/gist-examples.html "PostgreSQL 11 -
68.5. Examples") / [10](/docs/10/gist-examples.html "PostgreSQL 10 -
68.5. Examples") / [9.6](/docs/9.6/gist-examples.html "PostgreSQL 9.6 -
68.5. Examples") / [9.5](/docs/9.5/gist-examples.html "PostgreSQL 9.5 -
68.5. Examples") / [9.4](/docs/9.4/gist-examples.html "PostgreSQL 9.4 -
68.5. Examples") / [9.3](/docs/9.3/gist-examples.html "PostgreSQL 9.3 -
68.5. Examples") / [9.2](/docs/9.2/gist-examples.html "PostgreSQL 9.2 -
68.5. Examples") / [9.1](/docs/9.1/gist-examples.html "PostgreSQL 9.1 -
68.5. Examples") / [9.0](/docs/9.0/gist-examples.html "PostgreSQL 9.0 -
68.5. Examples") / [8.4](/docs/8.4/gist-examples.html "PostgreSQL 8.4 -
68.5. Examples") / [8.3](/docs/8.3/gist-examples.html "PostgreSQL 8.3 -
68.5. Examples") / [8.2](/docs/8.2/gist-examples.html "PostgreSQL 8.2 -
68.5. Examples") / [8.1](/docs/8.1/gist-examples.html "PostgreSQL 8.1 -
68.5. Examples")

__

68.5. Examples  
---  
[Prev](gist-implementation.html "68.4. Implementation")  | [Up](gist.html "Chapter 68. GiST Indexes") | Chapter 68. GiST Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spgist.html "Chapter 69. SP-GiST Indexes")  
  
* * *

## 68.5. Examples #

The PostgreSQL source distribution includes several examples of index methods
implemented using GiST. The core system currently provides text search support
(indexing for `tsvector` and `tsquery`) as well as R-Tree equivalent
functionality for some of the built-in geometric data types (see
`src/backend/access/gist/gistproc.c`). The following `contrib` modules also
contain GiST operator classes:

`btree_gist`

    

B-tree equivalent functionality for several data types

`cube`

    

Indexing for multidimensional cubes

`hstore`

    

Module for storing (key, value) pairs

`intarray`

    

RD-Tree for one-dimensional array of int4 values

`ltree`

    

Indexing for tree-like structures

`pg_trgm`

    

Text similarity using trigram matching

`seg`

    

Indexing for “float ranges”

* * *

[Prev](gist-implementation.html "68.4. Implementation")  | [Up](gist.html "Chapter 68. GiST Indexes") |  [Next](spgist.html "Chapter 69. SP-GiST Indexes")  
---|---|---  
68.4. Implementation  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 69. SP-GiST Indexes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/gist-examples.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

