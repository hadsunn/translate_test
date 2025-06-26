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

Supported Versions: [Current](/docs/current/spi-transaction.html "PostgreSQL
17 - 47.4. Transaction Management") ([17](/docs/17/spi-transaction.html
"PostgreSQL 17 - 47.4. Transaction Management")) / [16](/docs/16/spi-
transaction.html "PostgreSQL 16 - 47.4. Transaction Management") /
[15](/docs/15/spi-transaction.html "PostgreSQL 15 - 47.4. Transaction
Management") / [14](/docs/14/spi-transaction.html "PostgreSQL 14 -
47.4. Transaction Management") / [13](/docs/13/spi-transaction.html
"PostgreSQL 13 - 47.4. Transaction Management")

Development Versions: [18](/docs/18/spi-transaction.html "PostgreSQL 18 -
47.4. Transaction Management") / [devel](/docs/devel/spi-transaction.html
"PostgreSQL devel - 47.4. Transaction Management")

Unsupported versions: [12](/docs/12/spi-transaction.html "PostgreSQL 12 -
47.4. Transaction Management") / [11](/docs/11/spi-transaction.html
"PostgreSQL 11 - 47.4. Transaction Management")

__

47.4. Transaction Management  
---  
[Prev](spi-spi-freeplan.html "SPI_freeplan")  | [Up](spi.html "Chapter 47. Server Programming Interface") | Chapter 47. Server Programming Interface | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-commit.html "SPI_commit")  
  
* * *

## 47.4. Transaction Management #

[SPI_commit](spi-spi-commit.html) — commit the current transaction

[SPI_rollback](spi-spi-rollback.html) — abort the current transaction

[SPI_start_transaction](spi-spi-start-transaction.html) — obsolete function

It is not possible to run transaction control commands such as `COMMIT` and
`ROLLBACK` through SPI functions such as `SPI_execute`. There are, however,
separate interface functions that allow transaction control through SPI.

It is not generally safe and sensible to start and end transactions in
arbitrary user-defined SQL-callable functions without taking into account the
context in which they are called. For example, a transaction boundary in the
middle of a function that is part of a complex SQL expression that is part of
some SQL command will probably result in obscure internal errors or crashes.
The interface functions presented here are primarily intended to be used by
procedural language implementations to support transaction management in SQL-
level procedures that are invoked by the `CALL` command, taking the context of
the `CALL` invocation into account. SPI-using procedures implemented in C can
implement the same logic, but the details of that are beyond the scope of this
documentation.

* * *

[Prev](spi-spi-freeplan.html "SPI_freeplan")  | [Up](spi.html "Chapter 47. Server Programming Interface") |  [Next](spi-spi-commit.html "SPI_commit")  
---|---|---  
SPI_freeplan  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_commit  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-transaction.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

