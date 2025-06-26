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

Supported Versions: [Current](/docs/current/spgist.html "PostgreSQL 17 -
Chapter 69. SP-GiST Indexes") ([17](/docs/17/spgist.html "PostgreSQL 17 -
Chapter 69. SP-GiST Indexes")) / [16](/docs/16/spgist.html "PostgreSQL 16 -
Chapter 69. SP-GiST Indexes") / [15](/docs/15/spgist.html "PostgreSQL 15 -
Chapter 69. SP-GiST Indexes") / [14](/docs/14/spgist.html "PostgreSQL 14 -
Chapter 69. SP-GiST Indexes") / [13](/docs/13/spgist.html "PostgreSQL 13 -
Chapter 69. SP-GiST Indexes")

Development Versions: [18](/docs/18/spgist.html "PostgreSQL 18 -
Chapter 69. SP-GiST Indexes") / [devel](/docs/devel/spgist.html "PostgreSQL
devel - Chapter 69. SP-GiST Indexes")

Unsupported versions: [12](/docs/12/spgist.html "PostgreSQL 12 -
Chapter 69. SP-GiST Indexes") / [11](/docs/11/spgist.html "PostgreSQL 11 -
Chapter 69. SP-GiST Indexes") / [10](/docs/10/spgist.html "PostgreSQL 10 -
Chapter 69. SP-GiST Indexes") / [9.6](/docs/9.6/spgist.html "PostgreSQL 9.6 -
Chapter 69. SP-GiST Indexes") / [9.5](/docs/9.5/spgist.html "PostgreSQL 9.5 -
Chapter 69. SP-GiST Indexes") / [9.4](/docs/9.4/spgist.html "PostgreSQL 9.4 -
Chapter 69. SP-GiST Indexes") / [9.3](/docs/9.3/spgist.html "PostgreSQL 9.3 -
Chapter 69. SP-GiST Indexes") / [9.2](/docs/9.2/spgist.html "PostgreSQL 9.2 -
Chapter 69. SP-GiST Indexes")

__

Chapter 69. SP-GiST Indexes  
---  
[Prev](gist-examples.html "68.5. Examples")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spgist-intro.html "69.1. Introduction")  
  
* * *

## Chapter 69. SP-GiST Indexes

**Table of Contents**

[69.1. Introduction](spgist-intro.html)

[69.2. Built-in Operator Classes](spgist-builtin-opclasses.html)

[69.3. Extensibility](spgist-extensibility.html)

[69.4. Implementation](spgist-implementation.html)

    

[69.4.1. SP-GiST Limits](spgist-implementation.html#SPGIST-LIMITS)

[69.4.2. SP-GiST Without Node Labels](spgist-implementation.html#SPGIST-NULL-
LABELS)

[69.4.3. “All-the-Same” Inner Tuples](spgist-implementation.html#SPGIST-ALL-
THE-SAME)

[69.5. Examples](spgist-examples.html)

* * *

[Prev](gist-examples.html "68.5. Examples")  | [Up](internals.html "Part VII. Internals") |  [Next](spgist-intro.html "69.1. Introduction")  
---|---|---  
68.5. Examples  | [Home](index.html "PostgreSQL 16.9 Documentation") |  69.1. Introduction  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spgist.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

