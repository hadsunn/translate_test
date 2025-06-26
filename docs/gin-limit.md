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

Supported Versions: [16](/docs/16/gin-limit.html "PostgreSQL 16 -
70.6. Limitations") / [15](/docs/15/gin-limit.html "PostgreSQL 15 -
70.6. Limitations") / [14](/docs/14/gin-limit.html "PostgreSQL 14 -
70.6. Limitations") / [13](/docs/13/gin-limit.html "PostgreSQL 13 -
70.6. Limitations")

Unsupported versions: [12](/docs/12/gin-limit.html "PostgreSQL 12 -
70.6. Limitations") / [11](/docs/11/gin-limit.html "PostgreSQL 11 -
70.6. Limitations") / [10](/docs/10/gin-limit.html "PostgreSQL 10 -
70.6. Limitations") / [9.6](/docs/9.6/gin-limit.html "PostgreSQL 9.6 -
70.6. Limitations") / [9.5](/docs/9.5/gin-limit.html "PostgreSQL 9.5 -
70.6. Limitations") / [9.4](/docs/9.4/gin-limit.html "PostgreSQL 9.4 -
70.6. Limitations") / [9.3](/docs/9.3/gin-limit.html "PostgreSQL 9.3 -
70.6. Limitations") / [9.2](/docs/9.2/gin-limit.html "PostgreSQL 9.2 -
70.6. Limitations") / [9.1](/docs/9.1/gin-limit.html "PostgreSQL 9.1 -
70.6. Limitations") / [9.0](/docs/9.0/gin-limit.html "PostgreSQL 9.0 -
70.6. Limitations") / [8.4](/docs/8.4/gin-limit.html "PostgreSQL 8.4 -
70.6. Limitations") / [8.3](/docs/8.3/gin-limit.html "PostgreSQL 8.3 -
70.6. Limitations") / [8.2](/docs/8.2/gin-limit.html "PostgreSQL 8.2 -
70.6. Limitations")

__

70.6. Limitations  
---  
[Prev](gin-tips.html "70.5. GIN Tips and Tricks")  | [Up](gin.html "Chapter 70. GIN Indexes") | Chapter 70. GIN Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](gin-examples.html "70.7. Examples")  
  
* * *

## 70.6. Limitations #

GIN assumes that indexable operators are strict. This means that
`extractValue` will not be called at all on a null item value (instead, a
placeholder index entry is created automatically), and `extractQuery` will not
be called on a null query value either (instead, the query is presumed to be
unsatisfiable). Note however that null key values contained within a non-null
composite item or query value are supported.

* * *

[Prev](gin-tips.html "70.5. GIN Tips and Tricks")  | [Up](gin.html "Chapter 70. GIN Indexes") |  [Next](gin-examples.html "70.7. Examples")  
---|---|---  
70.5. GIN Tips and Tricks  | [Home](index.html "PostgreSQL 16.9 Documentation") |  70.7. Examples  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/gin-limit.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

