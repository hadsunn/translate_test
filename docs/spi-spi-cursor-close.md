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

Supported Versions: [Current](/docs/current/spi-spi-cursor-close.html
"PostgreSQL 17 - SPI_cursor_close") ([17](/docs/17/spi-spi-cursor-close.html
"PostgreSQL 17 - SPI_cursor_close")) / [16](/docs/16/spi-spi-cursor-close.html
"PostgreSQL 16 - SPI_cursor_close") / [15](/docs/15/spi-spi-cursor-close.html
"PostgreSQL 15 - SPI_cursor_close") / [14](/docs/14/spi-spi-cursor-close.html
"PostgreSQL 14 - SPI_cursor_close") / [13](/docs/13/spi-spi-cursor-close.html
"PostgreSQL 13 - SPI_cursor_close")

Development Versions: [18](/docs/18/spi-spi-cursor-close.html "PostgreSQL 18 -
SPI_cursor_close") / [devel](/docs/devel/spi-spi-cursor-close.html "PostgreSQL
devel - SPI_cursor_close")

Unsupported versions: [12](/docs/12/spi-spi-cursor-close.html "PostgreSQL 12 -
SPI_cursor_close") / [11](/docs/11/spi-spi-cursor-close.html "PostgreSQL 11 -
SPI_cursor_close") / [10](/docs/10/spi-spi-cursor-close.html "PostgreSQL 10 -
SPI_cursor_close") / [9.6](/docs/9.6/spi-spi-cursor-close.html "PostgreSQL 9.6
- SPI_cursor_close") / [9.5](/docs/9.5/spi-spi-cursor-close.html "PostgreSQL
9.5 - SPI_cursor_close") / [9.4](/docs/9.4/spi-spi-cursor-close.html
"PostgreSQL 9.4 - SPI_cursor_close") / [9.3](/docs/9.3/spi-spi-cursor-
close.html "PostgreSQL 9.3 - SPI_cursor_close") / [9.2](/docs/9.2/spi-spi-
cursor-close.html "PostgreSQL 9.2 - SPI_cursor_close") / [9.1](/docs/9.1/spi-
spi-cursor-close.html "PostgreSQL 9.1 - SPI_cursor_close") /
[9.0](/docs/9.0/spi-spi-cursor-close.html "PostgreSQL 9.0 - SPI_cursor_close")
/ [8.4](/docs/8.4/spi-spi-cursor-close.html "PostgreSQL 8.4 -
SPI_cursor_close") / [8.3](/docs/8.3/spi-spi-cursor-close.html "PostgreSQL 8.3
- SPI_cursor_close") / [8.2](/docs/8.2/spi-spi-cursor-close.html "PostgreSQL
8.2 - SPI_cursor_close") / [8.1](/docs/8.1/spi-spi-cursor-close.html
"PostgreSQL 8.1 - SPI_cursor_close") / [8.0](/docs/8.0/spi-spi-cursor-
close.html "PostgreSQL 8.0 - SPI_cursor_close") / [7.4](/docs/7.4/spi-spi-
cursor-close.html "PostgreSQL 7.4 - SPI_cursor_close")

__

SPI_cursor_close  
---  
[Prev](spi-spi-scroll-cursor-move.html "SPI_scroll_cursor_move")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-keepplan.html "SPI_keepplan")  
  
* * *

## SPI_cursor_close

SPI_cursor_close — close a cursor

## Synopsis

    
    
    void SPI_cursor_close(Portal _portal_)
    

## Description

`SPI_cursor_close` closes a previously created cursor and releases its portal
storage.

All open cursors are closed automatically at the end of a transaction.
`SPI_cursor_close` need only be invoked if it is desirable to release
resources sooner.

## Arguments

`Portal _`portal`_`

    

portal containing the cursor

* * *

[Prev](spi-spi-scroll-cursor-move.html "SPI_scroll_cursor_move")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-keepplan.html "SPI_keepplan")  
---|---|---  
SPI_scroll_cursor_move  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_keepplan  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-cursor-close.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

