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

Supported Versions: [Current](/docs/current/textsearch-limitations.html
"PostgreSQL 17 - 12.11. Limitations") ([17](/docs/17/textsearch-
limitations.html "PostgreSQL 17 - 12.11. Limitations")) /
[16](/docs/16/textsearch-limitations.html "PostgreSQL 16 -
12.11. Limitations") / [15](/docs/15/textsearch-limitations.html "PostgreSQL
15 - 12.11. Limitations") / [14](/docs/14/textsearch-limitations.html
"PostgreSQL 14 - 12.11. Limitations") / [13](/docs/13/textsearch-
limitations.html "PostgreSQL 13 - 12.11. Limitations")

Development Versions: [18](/docs/18/textsearch-limitations.html "PostgreSQL 18
- 12.11. Limitations") / [devel](/docs/devel/textsearch-limitations.html
"PostgreSQL devel - 12.11. Limitations")

Unsupported versions: [12](/docs/12/textsearch-limitations.html "PostgreSQL 12
- 12.11. Limitations") / [11](/docs/11/textsearch-limitations.html "PostgreSQL
11 - 12.11. Limitations") / [10](/docs/10/textsearch-limitations.html
"PostgreSQL 10 - 12.11. Limitations") / [9.6](/docs/9.6/textsearch-
limitations.html "PostgreSQL 9.6 - 12.11. Limitations") /
[9.5](/docs/9.5/textsearch-limitations.html "PostgreSQL 9.5 -
12.11. Limitations") / [9.4](/docs/9.4/textsearch-limitations.html "PostgreSQL
9.4 - 12.11. Limitations") / [9.3](/docs/9.3/textsearch-limitations.html
"PostgreSQL 9.3 - 12.11. Limitations") / [9.2](/docs/9.2/textsearch-
limitations.html "PostgreSQL 9.2 - 12.11. Limitations") /
[9.1](/docs/9.1/textsearch-limitations.html "PostgreSQL 9.1 -
12.11. Limitations") / [9.0](/docs/9.0/textsearch-limitations.html "PostgreSQL
9.0 - 12.11. Limitations") / [8.4](/docs/8.4/textsearch-limitations.html
"PostgreSQL 8.4 - 12.11. Limitations") / [8.3](/docs/8.3/textsearch-
limitations.html "PostgreSQL 8.3 - 12.11. Limitations")

__

12.11. Limitations  
---  
[Prev](textsearch-psql.html "12.10. psql Support")  | [Up](textsearch.html "Chapter 12. Full Text Search") | Chapter 12. Full Text Search | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](mvcc.html "Chapter 13. Concurrency Control")  
  
* * *

## 12.11. Limitations #

The current limitations of PostgreSQL's text search features are:

  * The length of each lexeme must be less than 2 kilobytes

  * The length of a `tsvector` (lexemes + positions) must be less than 1 megabyte

  * The number of lexemes must be less than 264

  * Position values in `tsvector` must be greater than 0 and no more than 16,383

  * The match distance in a `<_`N`_ >` (FOLLOWED BY) `tsquery` operator cannot be more than 16,384

  * No more than 256 positions per lexeme

  * The number of nodes (lexemes + operators) in a `tsquery` must be less than 32,768

For comparison, the PostgreSQL 8.1 documentation contained 10,441 unique
words, a total of 335,420 words, and the most frequent word “postgresql” was
mentioned 6,127 times in 655 documents.

Another example — the PostgreSQL mailing list archives contained 910,989
unique words with 57,491,343 lexemes in 461,020 messages.

* * *

[Prev](textsearch-psql.html "12.10. psql Support")  | [Up](textsearch.html "Chapter 12. Full Text Search") |  [Next](mvcc.html "Chapter 13. Concurrency Control")  
---|---|---  
12.10. psql Support  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 13. Concurrency Control  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/textsearch-limitations.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

