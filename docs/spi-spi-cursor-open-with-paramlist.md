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

Supported Versions: [Current](/docs/current/spi-spi-cursor-open-with-
paramlist.html "PostgreSQL 17 - SPI_cursor_open_with_paramlist")
([17](/docs/17/spi-spi-cursor-open-with-paramlist.html "PostgreSQL 17 -
SPI_cursor_open_with_paramlist")) / [16](/docs/16/spi-spi-cursor-open-with-
paramlist.html "PostgreSQL 16 - SPI_cursor_open_with_paramlist") /
[15](/docs/15/spi-spi-cursor-open-with-paramlist.html "PostgreSQL 15 -
SPI_cursor_open_with_paramlist") / [14](/docs/14/spi-spi-cursor-open-with-
paramlist.html "PostgreSQL 14 - SPI_cursor_open_with_paramlist") /
[13](/docs/13/spi-spi-cursor-open-with-paramlist.html "PostgreSQL 13 -
SPI_cursor_open_with_paramlist")

Development Versions: [18](/docs/18/spi-spi-cursor-open-with-paramlist.html
"PostgreSQL 18 - SPI_cursor_open_with_paramlist") / [devel](/docs/devel/spi-
spi-cursor-open-with-paramlist.html "PostgreSQL devel -
SPI_cursor_open_with_paramlist")

Unsupported versions: [12](/docs/12/spi-spi-cursor-open-with-paramlist.html
"PostgreSQL 12 - SPI_cursor_open_with_paramlist") / [11](/docs/11/spi-spi-
cursor-open-with-paramlist.html "PostgreSQL 11 -
SPI_cursor_open_with_paramlist") / [10](/docs/10/spi-spi-cursor-open-with-
paramlist.html "PostgreSQL 10 - SPI_cursor_open_with_paramlist") /
[9.6](/docs/9.6/spi-spi-cursor-open-with-paramlist.html "PostgreSQL 9.6 -
SPI_cursor_open_with_paramlist") / [9.5](/docs/9.5/spi-spi-cursor-open-with-
paramlist.html "PostgreSQL 9.5 - SPI_cursor_open_with_paramlist") /
[9.4](/docs/9.4/spi-spi-cursor-open-with-paramlist.html "PostgreSQL 9.4 -
SPI_cursor_open_with_paramlist") / [9.3](/docs/9.3/spi-spi-cursor-open-with-
paramlist.html "PostgreSQL 9.3 - SPI_cursor_open_with_paramlist") /
[9.2](/docs/9.2/spi-spi-cursor-open-with-paramlist.html "PostgreSQL 9.2 -
SPI_cursor_open_with_paramlist") / [9.1](/docs/9.1/spi-spi-cursor-open-with-
paramlist.html "PostgreSQL 9.1 - SPI_cursor_open_with_paramlist") /
[9.0](/docs/9.0/spi-spi-cursor-open-with-paramlist.html "PostgreSQL 9.0 -
SPI_cursor_open_with_paramlist")

__

SPI_cursor_open_with_paramlist  
---  
[Prev](spi-spi-cursor-open-with-args.html "SPI_cursor_open_with_args")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-cursor-parse-open.html "SPI_cursor_parse_open")  
  
* * *

## SPI_cursor_open_with_paramlist

SPI_cursor_open_with_paramlist — set up a cursor using parameters

## Synopsis

    
    
    Portal SPI_cursor_open_with_paramlist(const char *_name_ ,
                                          SPIPlanPtr _plan_ ,
                                          ParamListInfo _params_ ,
                                          bool _read_only_)
    

## Description

`SPI_cursor_open_with_paramlist` sets up a cursor (internally, a portal) that
will execute a statement prepared by `SPI_prepare`. This function is
equivalent to `SPI_cursor_open` except that information about the parameter
values to be passed to the query is presented differently. The `ParamListInfo`
representation can be convenient for passing down values that are already
available in that format. It also supports use of dynamic parameter sets via
hook functions specified in `ParamListInfo`.

The passed-in parameter data will be copied into the cursor's portal, so it
can be freed while the cursor still exists.

## Arguments

`const char * _`name`_`

    

name for portal, or `NULL` to let the system select a name

`SPIPlanPtr _`plan`_`

    

prepared statement (returned by `SPI_prepare`)

`ParamListInfo _`params`_`

    

data structure containing parameter types and values; NULL if none

`bool _`read_only`_`

    

`true` for read-only execution

## Return Value

Pointer to portal containing the cursor. Note there is no error return
convention; any error will be reported via `elog`.

* * *

[Prev](spi-spi-cursor-open-with-args.html "SPI_cursor_open_with_args")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-cursor-parse-open.html "SPI_cursor_parse_open")  
---|---|---  
SPI_cursor_open_with_args  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_cursor_parse_open  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-cursor-open-with-
paramlist.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

