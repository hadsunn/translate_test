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

Supported Versions: [Current](/docs/current/spi-spi-freeplan.html "PostgreSQL
17 - SPI_freeplan") ([17](/docs/17/spi-spi-freeplan.html "PostgreSQL 17 -
SPI_freeplan")) / [16](/docs/16/spi-spi-freeplan.html "PostgreSQL 16 -
SPI_freeplan") / [15](/docs/15/spi-spi-freeplan.html "PostgreSQL 15 -
SPI_freeplan") / [14](/docs/14/spi-spi-freeplan.html "PostgreSQL 14 -
SPI_freeplan") / [13](/docs/13/spi-spi-freeplan.html "PostgreSQL 13 -
SPI_freeplan")

Development Versions: [18](/docs/18/spi-spi-freeplan.html "PostgreSQL 18 -
SPI_freeplan") / [devel](/docs/devel/spi-spi-freeplan.html "PostgreSQL devel -
SPI_freeplan")

Unsupported versions: [12](/docs/12/spi-spi-freeplan.html "PostgreSQL 12 -
SPI_freeplan") / [11](/docs/11/spi-spi-freeplan.html "PostgreSQL 11 -
SPI_freeplan") / [10](/docs/10/spi-spi-freeplan.html "PostgreSQL 10 -
SPI_freeplan") / [9.6](/docs/9.6/spi-spi-freeplan.html "PostgreSQL 9.6 -
SPI_freeplan") / [9.5](/docs/9.5/spi-spi-freeplan.html "PostgreSQL 9.5 -
SPI_freeplan") / [9.4](/docs/9.4/spi-spi-freeplan.html "PostgreSQL 9.4 -
SPI_freeplan") / [9.3](/docs/9.3/spi-spi-freeplan.html "PostgreSQL 9.3 -
SPI_freeplan") / [9.2](/docs/9.2/spi-spi-freeplan.html "PostgreSQL 9.2 -
SPI_freeplan") / [9.1](/docs/9.1/spi-spi-freeplan.html "PostgreSQL 9.1 -
SPI_freeplan") / [9.0](/docs/9.0/spi-spi-freeplan.html "PostgreSQL 9.0 -
SPI_freeplan") / [8.4](/docs/8.4/spi-spi-freeplan.html "PostgreSQL 8.4 -
SPI_freeplan") / [8.3](/docs/8.3/spi-spi-freeplan.html "PostgreSQL 8.3 -
SPI_freeplan") / [8.2](/docs/8.2/spi-spi-freeplan.html "PostgreSQL 8.2 -
SPI_freeplan") / [8.1](/docs/8.1/spi-spi-freeplan.html "PostgreSQL 8.1 -
SPI_freeplan") / [8.0](/docs/8.0/spi-spi-freeplan.html "PostgreSQL 8.0 -
SPI_freeplan") / [7.4](/docs/7.4/spi-spi-freeplan.html "PostgreSQL 7.4 -
SPI_freeplan")

__

SPI_freeplan  
---  
[Prev](spi-spi-freetupletable.html "SPI_freetuptable")  | [Up](spi-memory.html "47.3. Memory Management") | 47.3. Memory Management | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-transaction.html "47.4. Transaction Management")  
  
* * *

## SPI_freeplan

SPI_freeplan — free a previously saved prepared statement

## Synopsis

    
    
    int SPI_freeplan(SPIPlanPtr _plan_)
    

## Description

`SPI_freeplan` releases a prepared statement previously returned by
`SPI_prepare` or saved by `SPI_keepplan` or `SPI_saveplan`.

## Arguments

`SPIPlanPtr _`plan`_`

    

pointer to statement to free

## Return Value

0 on success; `SPI_ERROR_ARGUMENT` if _`plan`_ is `NULL` or invalid

* * *

[Prev](spi-spi-freetupletable.html "SPI_freetuptable")  | [Up](spi-memory.html "47.3. Memory Management") |  [Next](spi-transaction.html "47.4. Transaction Management")  
---|---|---  
SPI_freetuptable  | [Home](index.html "PostgreSQL 16.9 Documentation") |  47.4. Transaction Management  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-freeplan.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

