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

Supported Versions: [Current](/docs/current/largeobjects.html "PostgreSQL 17 -
Chapter 35. Large Objects") ([17](/docs/17/largeobjects.html "PostgreSQL 17 -
Chapter 35. Large Objects")) / [16](/docs/16/largeobjects.html "PostgreSQL 16
- Chapter 35. Large Objects") / [15](/docs/15/largeobjects.html "PostgreSQL 15
- Chapter 35. Large Objects") / [14](/docs/14/largeobjects.html "PostgreSQL 14
- Chapter 35. Large Objects") / [13](/docs/13/largeobjects.html "PostgreSQL 13
- Chapter 35. Large Objects")

Development Versions: [18](/docs/18/largeobjects.html "PostgreSQL 18 -
Chapter 35. Large Objects") / [devel](/docs/devel/largeobjects.html
"PostgreSQL devel - Chapter 35. Large Objects")

Unsupported versions: [12](/docs/12/largeobjects.html "PostgreSQL 12 -
Chapter 35. Large Objects") / [11](/docs/11/largeobjects.html "PostgreSQL 11 -
Chapter 35. Large Objects") / [10](/docs/10/largeobjects.html "PostgreSQL 10 -
Chapter 35. Large Objects") / [9.6](/docs/9.6/largeobjects.html "PostgreSQL
9.6 - Chapter 35. Large Objects") / [9.5](/docs/9.5/largeobjects.html
"PostgreSQL 9.5 - Chapter 35. Large Objects") /
[9.4](/docs/9.4/largeobjects.html "PostgreSQL 9.4 - Chapter 35. Large
Objects") / [9.3](/docs/9.3/largeobjects.html "PostgreSQL 9.3 -
Chapter 35. Large Objects") / [9.2](/docs/9.2/largeobjects.html "PostgreSQL
9.2 - Chapter 35. Large Objects") / [9.1](/docs/9.1/largeobjects.html
"PostgreSQL 9.1 - Chapter 35. Large Objects") /
[9.0](/docs/9.0/largeobjects.html "PostgreSQL 9.0 - Chapter 35. Large
Objects") / [8.4](/docs/8.4/largeobjects.html "PostgreSQL 8.4 -
Chapter 35. Large Objects") / [8.3](/docs/8.3/largeobjects.html "PostgreSQL
8.3 - Chapter 35. Large Objects") / [8.2](/docs/8.2/largeobjects.html
"PostgreSQL 8.2 - Chapter 35. Large Objects") /
[8.1](/docs/8.1/largeobjects.html "PostgreSQL 8.1 - Chapter 35. Large
Objects") / [8.0](/docs/8.0/largeobjects.html "PostgreSQL 8.0 -
Chapter 35. Large Objects") / [7.4](/docs/7.4/largeobjects.html "PostgreSQL
7.4 - Chapter 35. Large Objects") / [7.3](/docs/7.3/largeobjects.html
"PostgreSQL 7.3 - Chapter 35. Large Objects") /
[7.2](/docs/7.2/largeobjects.html "PostgreSQL 7.2 - Chapter 35. Large
Objects") / [7.1](/docs/7.1/largeobjects.html "PostgreSQL 7.1 -
Chapter 35. Large Objects")

__

Chapter 35. Large Objects  
---  
[Prev](libpq-example.html "34.22. Example Programs")  | [Up](client-interfaces.html "Part IV. Client Interfaces") | Part IV. Client Interfaces | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](lo-intro.html "35.1. Introduction")  
  
* * *

## Chapter 35. Large Objects

**Table of Contents**

[35.1. Introduction](lo-intro.html)

[35.2. Implementation Features](lo-implementation.html)

[35.3. Client Interfaces](lo-interfaces.html)

    

[35.3.1. Creating a Large Object](lo-interfaces.html#LO-CREATE)

[35.3.2. Importing a Large Object](lo-interfaces.html#LO-IMPORT)

[35.3.3. Exporting a Large Object](lo-interfaces.html#LO-EXPORT)

[35.3.4. Opening an Existing Large Object](lo-interfaces.html#LO-OPEN)

[35.3.5. Writing Data to a Large Object](lo-interfaces.html#LO-WRITE)

[35.3.6. Reading Data from a Large Object](lo-interfaces.html#LO-READ)

[35.3.7. Seeking in a Large Object](lo-interfaces.html#LO-SEEK)

[35.3.8. Obtaining the Seek Position of a Large Object](lo-interfaces.html#LO-
TELL)

[35.3.9. Truncating a Large Object](lo-interfaces.html#LO-TRUNCATE)

[35.3.10. Closing a Large Object Descriptor](lo-interfaces.html#LO-CLOSE)

[35.3.11. Removing a Large Object](lo-interfaces.html#LO-UNLINK)

[35.4. Server-Side Functions](lo-funcs.html)

[35.5. Example Program](lo-examplesect.html)

PostgreSQL has a _large object_ facility, which provides stream-style access
to user data that is stored in a special large-object structure. Streaming
access is useful when working with data values that are too large to
manipulate conveniently as a whole.

This chapter describes the implementation and the programming and query
language interfaces to PostgreSQL large object data. We use the libpq C
library for the examples in this chapter, but most programming interfaces
native to PostgreSQL support equivalent functionality. Other interfaces might
use the large object interface internally to provide generic support for large
values. This is not described here.

* * *

[Prev](libpq-example.html "34.22. Example Programs")  | [Up](client-interfaces.html "Part IV. Client Interfaces") |  [Next](lo-intro.html "35.1. Introduction")  
---|---|---  
34.22. Example Programs  | [Home](index.html "PostgreSQL 16.9 Documentation") |  35.1. Introduction  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/largeobjects.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

