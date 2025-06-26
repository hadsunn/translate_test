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

Supported Versions: [16](/docs/16/btree-intro.html "PostgreSQL 16 -
67.1. Introduction") / [15](/docs/15/btree-intro.html "PostgreSQL 15 -
67.1. Introduction") / [14](/docs/14/btree-intro.html "PostgreSQL 14 -
67.1. Introduction") / [13](/docs/13/btree-intro.html "PostgreSQL 13 -
67.1. Introduction")

Unsupported versions: [12](/docs/12/btree-intro.html "PostgreSQL 12 -
67.1. Introduction") / [11](/docs/11/btree-intro.html "PostgreSQL 11 -
67.1. Introduction")

__

67.1. Introduction  
---  
[Prev](btree.html "Chapter 67. B-Tree Indexes")  | [Up](btree.html "Chapter 67. B-Tree Indexes") | Chapter 67. B-Tree Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](btree-behavior.html "67.2. Behavior of B-Tree Operator Classes")  
  
* * *

## 67.1. Introduction #

PostgreSQL includes an implementation of the standard btree (multi-way
balanced tree) index data structure. Any data type that can be sorted into a
well-defined linear order can be indexed by a btree index. The only limitation
is that an index entry cannot exceed approximately one-third of a page (after
TOAST compression, if applicable).

Because each btree operator class imposes a sort order on its data type, btree
operator classes (or, really, operator families) have come to be used as
PostgreSQL's general representation and understanding of sorting semantics.
Therefore, they've acquired some features that go beyond what would be needed
just to support btree indexes, and parts of the system that are quite distant
from the btree AM make use of them.

* * *

[Prev](btree.html "Chapter 67. B-Tree Indexes")  | [Up](btree.html "Chapter 67. B-Tree Indexes") |  [Next](btree-behavior.html "67.2. Behavior of B-Tree Operator Classes")  
---|---|---  
Chapter 67. B-Tree Indexes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  67.2. Behavior of B-Tree Operator Classes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/btree-intro.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

