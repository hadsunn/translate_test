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

Supported Versions: [16](/docs/16/gist-intro.html "PostgreSQL 16 -
68.1. Introduction") / [15](/docs/15/gist-intro.html "PostgreSQL 15 -
68.1. Introduction") / [14](/docs/14/gist-intro.html "PostgreSQL 14 -
68.1. Introduction") / [13](/docs/13/gist-intro.html "PostgreSQL 13 -
68.1. Introduction")

Unsupported versions: [12](/docs/12/gist-intro.html "PostgreSQL 12 -
68.1. Introduction") / [11](/docs/11/gist-intro.html "PostgreSQL 11 -
68.1. Introduction") / [10](/docs/10/gist-intro.html "PostgreSQL 10 -
68.1. Introduction") / [9.6](/docs/9.6/gist-intro.html "PostgreSQL 9.6 -
68.1. Introduction") / [9.5](/docs/9.5/gist-intro.html "PostgreSQL 9.5 -
68.1. Introduction") / [9.4](/docs/9.4/gist-intro.html "PostgreSQL 9.4 -
68.1. Introduction") / [9.3](/docs/9.3/gist-intro.html "PostgreSQL 9.3 -
68.1. Introduction") / [9.2](/docs/9.2/gist-intro.html "PostgreSQL 9.2 -
68.1. Introduction") / [9.1](/docs/9.1/gist-intro.html "PostgreSQL 9.1 -
68.1. Introduction") / [9.0](/docs/9.0/gist-intro.html "PostgreSQL 9.0 -
68.1. Introduction") / [8.4](/docs/8.4/gist-intro.html "PostgreSQL 8.4 -
68.1. Introduction") / [8.3](/docs/8.3/gist-intro.html "PostgreSQL 8.3 -
68.1. Introduction") / [8.2](/docs/8.2/gist-intro.html "PostgreSQL 8.2 -
68.1. Introduction")

__

68.1. Introduction  
---  
[Prev](gist.html "Chapter 68. GiST Indexes")  | [Up](gist.html "Chapter 68. GiST Indexes") | Chapter 68. GiST Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](gist-builtin-opclasses.html "68.2. Built-in Operator Classes")  
  
* * *

## 68.1. Introduction #

GiST stands for Generalized Search Tree. It is a balanced, tree-structured
access method, that acts as a base template in which to implement arbitrary
indexing schemes. B-trees, R-trees and many other indexing schemes can be
implemented in GiST.

One advantage of GiST is that it allows the development of custom data types
with the appropriate access methods, by an expert in the domain of the data
type, rather than a database expert.

Some of the information here is derived from the University of California at
Berkeley's GiST Indexing Project [web site](http://gist.cs.berkeley.edu/) and
Marcel Kornacker's thesis, [Access Methods for Next-Generation Database
Systems](http://www.sai.msu.su/~megera/postgres/gist/papers/concurrency/access-
methods-for-next-generation.pdf.gz). The GiST implementation in PostgreSQL is
primarily maintained by Teodor Sigaev and Oleg Bartunov, and there is more
information on their [web site](http://www.sai.msu.su/~megera/postgres/gist/).

* * *

[Prev](gist.html "Chapter 68. GiST Indexes")  | [Up](gist.html "Chapter 68. GiST Indexes") |  [Next](gist-builtin-opclasses.html "68.2. Built-in Operator Classes")  
---|---|---  
Chapter 68. GiST Indexes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  68.2. Built-in Operator Classes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/gist-intro.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

