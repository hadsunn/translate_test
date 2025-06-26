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

Supported Versions: [Current](/docs/current/spi-spi-cursor-move.html
"PostgreSQL 17 - SPI_cursor_move") ([17](/docs/17/spi-spi-cursor-move.html
"PostgreSQL 17 - SPI_cursor_move")) / [16](/docs/16/spi-spi-cursor-move.html
"PostgreSQL 16 - SPI_cursor_move") / [15](/docs/15/spi-spi-cursor-move.html
"PostgreSQL 15 - SPI_cursor_move") / [14](/docs/14/spi-spi-cursor-move.html
"PostgreSQL 14 - SPI_cursor_move") / [13](/docs/13/spi-spi-cursor-move.html
"PostgreSQL 13 - SPI_cursor_move")

Development Versions: [18](/docs/18/spi-spi-cursor-move.html "PostgreSQL 18 -
SPI_cursor_move") / [devel](/docs/devel/spi-spi-cursor-move.html "PostgreSQL
devel - SPI_cursor_move")

Unsupported versions: [12](/docs/12/spi-spi-cursor-move.html "PostgreSQL 12 -
SPI_cursor_move") / [11](/docs/11/spi-spi-cursor-move.html "PostgreSQL 11 -
SPI_cursor_move") / [10](/docs/10/spi-spi-cursor-move.html "PostgreSQL 10 -
SPI_cursor_move") / [9.6](/docs/9.6/spi-spi-cursor-move.html "PostgreSQL 9.6 -
SPI_cursor_move") / [9.5](/docs/9.5/spi-spi-cursor-move.html "PostgreSQL 9.5 -
SPI_cursor_move") / [9.4](/docs/9.4/spi-spi-cursor-move.html "PostgreSQL 9.4 -
SPI_cursor_move") / [9.3](/docs/9.3/spi-spi-cursor-move.html "PostgreSQL 9.3 -
SPI_cursor_move") / [9.2](/docs/9.2/spi-spi-cursor-move.html "PostgreSQL 9.2 -
SPI_cursor_move") / [9.1](/docs/9.1/spi-spi-cursor-move.html "PostgreSQL 9.1 -
SPI_cursor_move") / [9.0](/docs/9.0/spi-spi-cursor-move.html "PostgreSQL 9.0 -
SPI_cursor_move") / [8.4](/docs/8.4/spi-spi-cursor-move.html "PostgreSQL 8.4 -
SPI_cursor_move") / [8.3](/docs/8.3/spi-spi-cursor-move.html "PostgreSQL 8.3 -
SPI_cursor_move") / [8.2](/docs/8.2/spi-spi-cursor-move.html "PostgreSQL 8.2 -
SPI_cursor_move") / [8.1](/docs/8.1/spi-spi-cursor-move.html "PostgreSQL 8.1 -
SPI_cursor_move") / [8.0](/docs/8.0/spi-spi-cursor-move.html "PostgreSQL 8.0 -
SPI_cursor_move") / [7.4](/docs/7.4/spi-spi-cursor-move.html "PostgreSQL 7.4 -
SPI_cursor_move")

__

SPI_cursor_move  
---  
[Prev](spi-spi-cursor-fetch.html "SPI_cursor_fetch")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-scroll-cursor-fetch.html "SPI_scroll_cursor_fetch")  
  
* * *

## SPI_cursor_move

SPI_cursor_move — move a cursor

## Synopsis

    
    
    void SPI_cursor_move(Portal _portal_ , bool _forward_ , long _count_)
    

## Description

`SPI_cursor_move` skips over some number of rows in a cursor. This is
equivalent to a subset of the SQL command `MOVE` (see `SPI_scroll_cursor_move`
for more functionality).

## Arguments

`Portal _`portal`_`

    

portal containing the cursor

`bool _`forward`_`

    

true for move forward, false for move backward

`long _`count`_`

    

maximum number of rows to move

## Notes

Moving backward may fail if the cursor's plan was not created with the
`CURSOR_OPT_SCROLL` option.

* * *

[Prev](spi-spi-cursor-fetch.html "SPI_cursor_fetch")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-scroll-cursor-fetch.html "SPI_scroll_cursor_fetch")  
---|---|---  
SPI_cursor_fetch  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_scroll_cursor_fetch  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-cursor-move.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

