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

Supported Versions: [16](/docs/16/gin-intro.html "PostgreSQL 16 -
70.1. Introduction") / [15](/docs/15/gin-intro.html "PostgreSQL 15 -
70.1. Introduction") / [14](/docs/14/gin-intro.html "PostgreSQL 14 -
70.1. Introduction") / [13](/docs/13/gin-intro.html "PostgreSQL 13 -
70.1. Introduction")

Unsupported versions: [12](/docs/12/gin-intro.html "PostgreSQL 12 -
70.1. Introduction") / [11](/docs/11/gin-intro.html "PostgreSQL 11 -
70.1. Introduction") / [10](/docs/10/gin-intro.html "PostgreSQL 10 -
70.1. Introduction") / [9.6](/docs/9.6/gin-intro.html "PostgreSQL 9.6 -
70.1. Introduction") / [9.5](/docs/9.5/gin-intro.html "PostgreSQL 9.5 -
70.1. Introduction") / [9.4](/docs/9.4/gin-intro.html "PostgreSQL 9.4 -
70.1. Introduction") / [9.3](/docs/9.3/gin-intro.html "PostgreSQL 9.3 -
70.1. Introduction") / [9.2](/docs/9.2/gin-intro.html "PostgreSQL 9.2 -
70.1. Introduction") / [9.1](/docs/9.1/gin-intro.html "PostgreSQL 9.1 -
70.1. Introduction") / [9.0](/docs/9.0/gin-intro.html "PostgreSQL 9.0 -
70.1. Introduction") / [8.4](/docs/8.4/gin-intro.html "PostgreSQL 8.4 -
70.1. Introduction") / [8.3](/docs/8.3/gin-intro.html "PostgreSQL 8.3 -
70.1. Introduction") / [8.2](/docs/8.2/gin-intro.html "PostgreSQL 8.2 -
70.1. Introduction")

__

70.1. Introduction  
---  
[Prev](gin.html "Chapter 70. GIN Indexes")  | [Up](gin.html "Chapter 70. GIN Indexes") | Chapter 70. GIN Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](gin-builtin-opclasses.html "70.2. Built-in Operator Classes")  
  
* * *

## 70.1. Introduction #

GIN stands for Generalized Inverted Index. GIN is designed for handling cases
where the items to be indexed are composite values, and the queries to be
handled by the index need to search for element values that appear within the
composite items. For example, the items could be documents, and the queries
could be searches for documents containing specific words.

We use the word _item_ to refer to a composite value that is to be indexed,
and the word _key_ to refer to an element value. GIN always stores and
searches for keys, not item values per se.

A GIN index stores a set of (key, posting list) pairs, where a _posting list_
is a set of row IDs in which the key occurs. The same row ID can appear in
multiple posting lists, since an item can contain more than one key. Each key
value is stored only once, so a GIN index is very compact for cases where the
same key appears many times.

GIN is generalized in the sense that the GIN access method code does not need
to know the specific operations that it accelerates. Instead, it uses custom
strategies defined for particular data types. The strategy defines how keys
are extracted from indexed items and query conditions, and how to determine
whether a row that contains some of the key values in a query actually
satisfies the query.

One advantage of GIN is that it allows the development of custom data types
with the appropriate access methods, by an expert in the domain of the data
type, rather than a database expert. This is much the same advantage as using
GiST.

The GIN implementation in PostgreSQL is primarily maintained by Teodor Sigaev
and Oleg Bartunov. There is more information about GIN on their
[website](http://www.sai.msu.su/~megera/wiki/Gin).

* * *

[Prev](gin.html "Chapter 70. GIN Indexes")  | [Up](gin.html "Chapter 70. GIN Indexes") |  [Next](gin-builtin-opclasses.html "70.2. Built-in Operator Classes")  
---|---|---  
Chapter 70. GIN Indexes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  70.2. Built-in Operator Classes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/gin-intro.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

