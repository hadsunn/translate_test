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

Supported Versions: [Current](/docs/current/spi-spi-keepplan.html "PostgreSQL
17 - SPI_keepplan") ([17](/docs/17/spi-spi-keepplan.html "PostgreSQL 17 -
SPI_keepplan")) / [16](/docs/16/spi-spi-keepplan.html "PostgreSQL 16 -
SPI_keepplan") / [15](/docs/15/spi-spi-keepplan.html "PostgreSQL 15 -
SPI_keepplan") / [14](/docs/14/spi-spi-keepplan.html "PostgreSQL 14 -
SPI_keepplan") / [13](/docs/13/spi-spi-keepplan.html "PostgreSQL 13 -
SPI_keepplan")

Development Versions: [18](/docs/18/spi-spi-keepplan.html "PostgreSQL 18 -
SPI_keepplan") / [devel](/docs/devel/spi-spi-keepplan.html "PostgreSQL devel -
SPI_keepplan")

Unsupported versions: [12](/docs/12/spi-spi-keepplan.html "PostgreSQL 12 -
SPI_keepplan") / [11](/docs/11/spi-spi-keepplan.html "PostgreSQL 11 -
SPI_keepplan") / [10](/docs/10/spi-spi-keepplan.html "PostgreSQL 10 -
SPI_keepplan") / [9.6](/docs/9.6/spi-spi-keepplan.html "PostgreSQL 9.6 -
SPI_keepplan") / [9.5](/docs/9.5/spi-spi-keepplan.html "PostgreSQL 9.5 -
SPI_keepplan") / [9.4](/docs/9.4/spi-spi-keepplan.html "PostgreSQL 9.4 -
SPI_keepplan") / [9.3](/docs/9.3/spi-spi-keepplan.html "PostgreSQL 9.3 -
SPI_keepplan") / [9.2](/docs/9.2/spi-spi-keepplan.html "PostgreSQL 9.2 -
SPI_keepplan")

__

SPI_keepplan  
---  
[Prev](spi-spi-cursor-close.html "SPI_cursor_close")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-saveplan.html "SPI_saveplan")  
  
* * *

## SPI_keepplan

SPI_keepplan — save a prepared statement

## Synopsis

    
    
    int SPI_keepplan(SPIPlanPtr _plan_)
    

## Description

`SPI_keepplan` saves a passed statement (prepared by `SPI_prepare`) so that it
will not be freed by `SPI_finish` nor by the transaction manager. This gives
you the ability to reuse prepared statements in the subsequent invocations of
your C function in the current session.

## Arguments

`SPIPlanPtr _`plan`_`

    

the prepared statement to be saved

## Return Value

0 on success; `SPI_ERROR_ARGUMENT` if _`plan`_ is `NULL` or invalid

## Notes

The passed-in statement is relocated to permanent storage by means of pointer
adjustment (no data copying is required). If you later wish to delete it, use
`SPI_freeplan` on it.

* * *

[Prev](spi-spi-cursor-close.html "SPI_cursor_close")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-saveplan.html "SPI_saveplan")  
---|---|---  
SPI_cursor_close  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_saveplan  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-keepplan.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

