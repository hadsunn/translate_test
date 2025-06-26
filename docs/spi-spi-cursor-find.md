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

Supported Versions: [Current](/docs/current/spi-spi-cursor-find.html
"PostgreSQL 17 - SPI_cursor_find") ([17](/docs/17/spi-spi-cursor-find.html
"PostgreSQL 17 - SPI_cursor_find")) / [16](/docs/16/spi-spi-cursor-find.html
"PostgreSQL 16 - SPI_cursor_find") / [15](/docs/15/spi-spi-cursor-find.html
"PostgreSQL 15 - SPI_cursor_find") / [14](/docs/14/spi-spi-cursor-find.html
"PostgreSQL 14 - SPI_cursor_find") / [13](/docs/13/spi-spi-cursor-find.html
"PostgreSQL 13 - SPI_cursor_find")

Development Versions: [18](/docs/18/spi-spi-cursor-find.html "PostgreSQL 18 -
SPI_cursor_find") / [devel](/docs/devel/spi-spi-cursor-find.html "PostgreSQL
devel - SPI_cursor_find")

Unsupported versions: [12](/docs/12/spi-spi-cursor-find.html "PostgreSQL 12 -
SPI_cursor_find") / [11](/docs/11/spi-spi-cursor-find.html "PostgreSQL 11 -
SPI_cursor_find") / [10](/docs/10/spi-spi-cursor-find.html "PostgreSQL 10 -
SPI_cursor_find") / [9.6](/docs/9.6/spi-spi-cursor-find.html "PostgreSQL 9.6 -
SPI_cursor_find") / [9.5](/docs/9.5/spi-spi-cursor-find.html "PostgreSQL 9.5 -
SPI_cursor_find") / [9.4](/docs/9.4/spi-spi-cursor-find.html "PostgreSQL 9.4 -
SPI_cursor_find") / [9.3](/docs/9.3/spi-spi-cursor-find.html "PostgreSQL 9.3 -
SPI_cursor_find") / [9.2](/docs/9.2/spi-spi-cursor-find.html "PostgreSQL 9.2 -
SPI_cursor_find") / [9.1](/docs/9.1/spi-spi-cursor-find.html "PostgreSQL 9.1 -
SPI_cursor_find") / [9.0](/docs/9.0/spi-spi-cursor-find.html "PostgreSQL 9.0 -
SPI_cursor_find") / [8.4](/docs/8.4/spi-spi-cursor-find.html "PostgreSQL 8.4 -
SPI_cursor_find") / [8.3](/docs/8.3/spi-spi-cursor-find.html "PostgreSQL 8.3 -
SPI_cursor_find") / [8.2](/docs/8.2/spi-spi-cursor-find.html "PostgreSQL 8.2 -
SPI_cursor_find") / [8.1](/docs/8.1/spi-spi-cursor-find.html "PostgreSQL 8.1 -
SPI_cursor_find") / [8.0](/docs/8.0/spi-spi-cursor-find.html "PostgreSQL 8.0 -
SPI_cursor_find") / [7.4](/docs/7.4/spi-spi-cursor-find.html "PostgreSQL 7.4 -
SPI_cursor_find")

__

SPI_cursor_find  
---  
[Prev](spi-spi-cursor-parse-open.html "SPI_cursor_parse_open")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-cursor-fetch.html "SPI_cursor_fetch")  
  
* * *

## SPI_cursor_find

SPI_cursor_find — find an existing cursor by name

## Synopsis

    
    
    Portal SPI_cursor_find(const char * _name_)
    

## Description

`SPI_cursor_find` finds an existing portal by name. This is primarily useful
to resolve a cursor name returned as text by some other function.

## Arguments

`const char * _`name`_`

    

name of the portal

## Return Value

pointer to the portal with the specified name, or `NULL` if none was found

## Notes

Beware that this function can return a `Portal` object that does not have
cursor-like properties; for example it might not return tuples. If you simply
pass the `Portal` pointer to other SPI functions, they can defend themselves
against such cases, but caution is appropriate when directly inspecting the
`Portal`.

* * *

[Prev](spi-spi-cursor-parse-open.html "SPI_cursor_parse_open")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-cursor-fetch.html "SPI_cursor_fetch")  
---|---|---  
SPI_cursor_parse_open  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_cursor_fetch  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-cursor-find.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

