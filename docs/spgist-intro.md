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

Supported Versions: [16](/docs/16/spgist-intro.html "PostgreSQL 16 -
69.1. Introduction") / [15](/docs/15/spgist-intro.html "PostgreSQL 15 -
69.1. Introduction") / [14](/docs/14/spgist-intro.html "PostgreSQL 14 -
69.1. Introduction") / [13](/docs/13/spgist-intro.html "PostgreSQL 13 -
69.1. Introduction")

Unsupported versions: [12](/docs/12/spgist-intro.html "PostgreSQL 12 -
69.1. Introduction") / [11](/docs/11/spgist-intro.html "PostgreSQL 11 -
69.1. Introduction") / [10](/docs/10/spgist-intro.html "PostgreSQL 10 -
69.1. Introduction") / [9.6](/docs/9.6/spgist-intro.html "PostgreSQL 9.6 -
69.1. Introduction") / [9.5](/docs/9.5/spgist-intro.html "PostgreSQL 9.5 -
69.1. Introduction") / [9.4](/docs/9.4/spgist-intro.html "PostgreSQL 9.4 -
69.1. Introduction") / [9.3](/docs/9.3/spgist-intro.html "PostgreSQL 9.3 -
69.1. Introduction") / [9.2](/docs/9.2/spgist-intro.html "PostgreSQL 9.2 -
69.1. Introduction")

__

69.1. Introduction  
---  
[Prev](spgist.html "Chapter 69. SP-GiST Indexes")  | [Up](spgist.html "Chapter 69. SP-GiST Indexes") | Chapter 69. SP-GiST Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spgist-builtin-opclasses.html "69.2. Built-in Operator Classes")  
  
* * *

## 69.1. Introduction #

SP-GiST is an abbreviation for space-partitioned GiST. SP-GiST supports
partitioned search trees, which facilitate development of a wide range of
different non-balanced data structures, such as quad-trees, k-d trees, and
radix trees (tries). The common feature of these structures is that they
repeatedly divide the search space into partitions that need not be of equal
size. Searches that are well matched to the partitioning rule can be very
fast.

These popular data structures were originally developed for in-memory usage.
In main memory, they are usually designed as a set of dynamically allocated
nodes linked by pointers. This is not suitable for direct storing on disk,
since these chains of pointers can be rather long which would require too many
disk accesses. In contrast, disk-based data structures should have a high
fanout to minimize I/O. The challenge addressed by SP-GiST is to map search
tree nodes to disk pages in such a way that a search need access only a few
disk pages, even if it traverses many nodes.

Like GiST, SP-GiST is meant to allow the development of custom data types with
the appropriate access methods, by an expert in the domain of the data type,
rather than a database expert.

Some of the information here is derived from Purdue University's SP-GiST
Indexing Project [web site](https://www.cs.purdue.edu/spgist/). The SP-GiST
implementation in PostgreSQL is primarily maintained by Teodor Sigaev and Oleg
Bartunov, and there is more information on their [web
site](http://www.sai.msu.su/~megera/wiki/spgist_dev).

* * *

[Prev](spgist.html "Chapter 69. SP-GiST Indexes")  | [Up](spgist.html "Chapter 69. SP-GiST Indexes") |  [Next](spgist-builtin-opclasses.html "69.2. Built-in Operator Classes")  
---|---|---  
Chapter 69. SP-GiST Indexes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  69.2. Built-in Operator Classes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spgist-intro.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

