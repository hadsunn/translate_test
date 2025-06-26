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

Supported Versions: [Current](/docs/current/spi-spi-prepare-cursor.html
"PostgreSQL 17 - SPI_prepare_cursor") ([17](/docs/17/spi-spi-prepare-
cursor.html "PostgreSQL 17 - SPI_prepare_cursor")) / [16](/docs/16/spi-spi-
prepare-cursor.html "PostgreSQL 16 - SPI_prepare_cursor") / [15](/docs/15/spi-
spi-prepare-cursor.html "PostgreSQL 15 - SPI_prepare_cursor") /
[14](/docs/14/spi-spi-prepare-cursor.html "PostgreSQL 14 -
SPI_prepare_cursor") / [13](/docs/13/spi-spi-prepare-cursor.html "PostgreSQL
13 - SPI_prepare_cursor")

Development Versions: [18](/docs/18/spi-spi-prepare-cursor.html "PostgreSQL 18
- SPI_prepare_cursor") / [devel](/docs/devel/spi-spi-prepare-cursor.html
"PostgreSQL devel - SPI_prepare_cursor")

Unsupported versions: [12](/docs/12/spi-spi-prepare-cursor.html "PostgreSQL 12
- SPI_prepare_cursor") / [11](/docs/11/spi-spi-prepare-cursor.html "PostgreSQL
11 - SPI_prepare_cursor") / [10](/docs/10/spi-spi-prepare-cursor.html
"PostgreSQL 10 - SPI_prepare_cursor") / [9.6](/docs/9.6/spi-spi-prepare-
cursor.html "PostgreSQL 9.6 - SPI_prepare_cursor") / [9.5](/docs/9.5/spi-spi-
prepare-cursor.html "PostgreSQL 9.5 - SPI_prepare_cursor") /
[9.4](/docs/9.4/spi-spi-prepare-cursor.html "PostgreSQL 9.4 -
SPI_prepare_cursor") / [9.3](/docs/9.3/spi-spi-prepare-cursor.html "PostgreSQL
9.3 - SPI_prepare_cursor") / [9.2](/docs/9.2/spi-spi-prepare-cursor.html
"PostgreSQL 9.2 - SPI_prepare_cursor") / [9.1](/docs/9.1/spi-spi-prepare-
cursor.html "PostgreSQL 9.1 - SPI_prepare_cursor") / [9.0](/docs/9.0/spi-spi-
prepare-cursor.html "PostgreSQL 9.0 - SPI_prepare_cursor") /
[8.4](/docs/8.4/spi-spi-prepare-cursor.html "PostgreSQL 8.4 -
SPI_prepare_cursor") / [8.3](/docs/8.3/spi-spi-prepare-cursor.html "PostgreSQL
8.3 - SPI_prepare_cursor")

__

SPI_prepare_cursor  
---  
[Prev](spi-spi-prepare.html "SPI_prepare")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-prepare-extended.html "SPI_prepare_extended")  
  
* * *

## SPI_prepare_cursor

SPI_prepare_cursor — prepare a statement, without executing it yet

## Synopsis

    
    
    SPIPlanPtr SPI_prepare_cursor(const char * _command_ , int _nargs_ ,
                                  Oid * _argtypes_ , int _cursorOptions_)
    

## Description

`SPI_prepare_cursor` is identical to `SPI_prepare`, except that it also allows
specification of the planner's “cursor options” parameter. This is a bit mask
having the values shown in `nodes/parsenodes.h` for the `options` field of
`DeclareCursorStmt`. `SPI_prepare` always takes the cursor options as zero.

This function is now deprecated in favor of `SPI_prepare_extended`.

## Arguments

`const char * _`command`_`

    

command string

`int _`nargs`_`

    

number of input parameters (`$1`, `$2`, etc.)

`Oid * _`argtypes`_`

    

pointer to an array containing the OIDs of the data types of the parameters

`int _`cursorOptions`_`

    

integer bit mask of cursor options; zero produces default behavior

## Return Value

`SPI_prepare_cursor` has the same return conventions as `SPI_prepare`.

## Notes

Useful bits to set in _`cursorOptions`_ include `CURSOR_OPT_SCROLL`,
`CURSOR_OPT_NO_SCROLL`, `CURSOR_OPT_FAST_PLAN`, `CURSOR_OPT_GENERIC_PLAN`, and
`CURSOR_OPT_CUSTOM_PLAN`. Note in particular that `CURSOR_OPT_HOLD` is
ignored.

* * *

[Prev](spi-spi-prepare.html "SPI_prepare")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-prepare-extended.html "SPI_prepare_extended")  
---|---|---  
SPI_prepare  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_prepare_extended  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-prepare-cursor.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

