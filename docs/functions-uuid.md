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

Supported Versions: [Current](/docs/current/functions-uuid.html "PostgreSQL 17
- 9.14. UUID Functions") ([17](/docs/17/functions-uuid.html "PostgreSQL 17 -
9.14. UUID Functions")) / [16](/docs/16/functions-uuid.html "PostgreSQL 16 -
9.14. UUID Functions") / [15](/docs/15/functions-uuid.html "PostgreSQL 15 -
9.14. UUID Functions") / [14](/docs/14/functions-uuid.html "PostgreSQL 14 -
9.14. UUID Functions") / [13](/docs/13/functions-uuid.html "PostgreSQL 13 -
9.14. UUID Functions")

Development Versions: [18](/docs/18/functions-uuid.html "PostgreSQL 18 -
9.14. UUID Functions") / [devel](/docs/devel/functions-uuid.html "PostgreSQL
devel - 9.14. UUID Functions")

__

9.14. UUID Functions  
---  
[Prev](functions-textsearch.html "9.13. Text Search Functions and Operators")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions-xml.html "9.15. XML Functions")  
  
* * *

## 9.14. UUID Functions #

PostgreSQL includes one function to generate a UUID:

    
    
    gen_random_uuid () → uuid
    

This function returns a version 4 (random) UUID. This is the most commonly
used type of UUID and is appropriate for most applications.

The [uuid-ossp](uuid-ossp.html "F.49. uuid-ossp — a UUID generator") module
provides additional functions that implement other standard algorithms for
generating UUIDs.

PostgreSQL also provides the usual comparison operators shown in [Table
9.1](functions-comparison.html#FUNCTIONS-COMPARISON-OP-TABLE
"Table 9.1. Comparison Operators") for UUIDs.

* * *

[Prev](functions-textsearch.html "9.13. Text Search Functions and Operators")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](functions-xml.html "9.15. XML Functions")  
---|---|---  
9.13. Text Search Functions and Operators  | [Home](index.html "PostgreSQL 16.9 Documentation") |  9.15. XML Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-uuid.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

