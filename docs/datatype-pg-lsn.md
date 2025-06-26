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

Supported Versions: [Current](/docs/current/datatype-pg-lsn.html "PostgreSQL
17 - 8.20. pg_lsn Type") ([17](/docs/17/datatype-pg-lsn.html "PostgreSQL 17 -
8.20. pg_lsn Type")) / [16](/docs/16/datatype-pg-lsn.html "PostgreSQL 16 -
8.20. pg_lsn Type") / [15](/docs/15/datatype-pg-lsn.html "PostgreSQL 15 -
8.20. pg_lsn Type") / [14](/docs/14/datatype-pg-lsn.html "PostgreSQL 14 -
8.20. pg_lsn Type") / [13](/docs/13/datatype-pg-lsn.html "PostgreSQL 13 -
8.20. pg_lsn Type")

Development Versions: [18](/docs/18/datatype-pg-lsn.html "PostgreSQL 18 -
8.20. pg_lsn Type") / [devel](/docs/devel/datatype-pg-lsn.html "PostgreSQL
devel - 8.20. pg_lsn Type")

Unsupported versions: [12](/docs/12/datatype-pg-lsn.html "PostgreSQL 12 -
8.20. pg_lsn Type") / [11](/docs/11/datatype-pg-lsn.html "PostgreSQL 11 -
8.20. pg_lsn Type") / [10](/docs/10/datatype-pg-lsn.html "PostgreSQL 10 -
8.20. pg_lsn Type") / [9.6](/docs/9.6/datatype-pg-lsn.html "PostgreSQL 9.6 -
8.20. pg_lsn Type") / [9.5](/docs/9.5/datatype-pg-lsn.html "PostgreSQL 9.5 -
8.20. pg_lsn Type") / [9.4](/docs/9.4/datatype-pg-lsn.html "PostgreSQL 9.4 -
8.20. pg_lsn Type")

__

8.20. `pg_lsn` Type  
---  
[Prev](datatype-oid.html "8.19. Object Identifier Types")  | [Up](datatype.html "Chapter 8. Data Types") | Chapter 8. Data Types | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datatype-pseudo.html "8.21. Pseudo-Types")  
  
* * *

## 8.20. `pg_lsn` Type #

The `pg_lsn` data type can be used to store LSN (Log Sequence Number) data
which is a pointer to a location in the WAL. This type is a representation of
`XLogRecPtr` and an internal system type of PostgreSQL.

Internally, an LSN is a 64-bit integer, representing a byte position in the
write-ahead log stream. It is printed as two hexadecimal numbers of up to 8
digits each, separated by a slash; for example, `16/B374D848`. The `pg_lsn`
type supports the standard comparison operators, like `=` and `>`. Two LSNs
can be subtracted using the `-` operator; the result is the number of bytes
separating those write-ahead log locations. Also the number of bytes can be
added into and subtracted from LSN using the `+(pg_lsn,numeric)` and
`-(pg_lsn,numeric)` operators, respectively. Note that the calculated LSN
should be in the range of `pg_lsn` type, i.e., between `0/0` and
`FFFFFFFF/FFFFFFFF`.

* * *

[Prev](datatype-oid.html "8.19. Object Identifier Types")  | [Up](datatype.html "Chapter 8. Data Types") |  [Next](datatype-pseudo.html "8.21. Pseudo-Types")  
---|---|---  
8.19. Object Identifier Types  | [Home](index.html "PostgreSQL 16.9 Documentation") |  8.21. Pseudo-Types  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datatype-pg-lsn.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

