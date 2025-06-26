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

Supported Versions: [Current](/docs/current/spi-spi-cursor-parse-open.html
"PostgreSQL 17 - SPI_cursor_parse_open") ([17](/docs/17/spi-spi-cursor-parse-
open.html "PostgreSQL 17 - SPI_cursor_parse_open")) / [16](/docs/16/spi-spi-
cursor-parse-open.html "PostgreSQL 16 - SPI_cursor_parse_open") /
[15](/docs/15/spi-spi-cursor-parse-open.html "PostgreSQL 15 -
SPI_cursor_parse_open") / [14](/docs/14/spi-spi-cursor-parse-open.html
"PostgreSQL 14 - SPI_cursor_parse_open")

Development Versions: [18](/docs/18/spi-spi-cursor-parse-open.html "PostgreSQL
18 - SPI_cursor_parse_open") / [devel](/docs/devel/spi-spi-cursor-parse-
open.html "PostgreSQL devel - SPI_cursor_parse_open")

__

SPI_cursor_parse_open  
---  
[Prev](spi-spi-cursor-open-with-paramlist.html "SPI_cursor_open_with_paramlist")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-cursor-find.html "SPI_cursor_find")  
  
* * *

## SPI_cursor_parse_open

SPI_cursor_parse_open — set up a cursor using a query string and parameters

## Synopsis

    
    
    Portal SPI_cursor_parse_open(const char *_name_ ,
                                 const char *_command_ ,
                                 const SPIParseOpenOptions * _options_)
    

## Description

`SPI_cursor_parse_open` sets up a cursor (internally, a portal) that will
execute the specified query string. This is comparable to `SPI_prepare_cursor`
followed by `SPI_cursor_open_with_paramlist`, except that parameter references
within the query string are handled entirely by supplying a `ParamListInfo`
object.

For one-time query execution, this function should be preferred over
`SPI_prepare_cursor` followed by `SPI_cursor_open_with_paramlist`. If the same
command is to be executed with many different parameters, either method might
be faster, depending on the cost of re-planning versus the benefit of custom
plans.

The _`options->params`_ object should normally mark each parameter with the
`PARAM_FLAG_CONST` flag, since a one-shot plan is always used for the query.

The passed-in parameter data will be copied into the cursor's portal, so it
can be freed while the cursor still exists.

## Arguments

`const char * _`name`_`

    

name for portal, or `NULL` to let the system select a name

`const char * _`command`_`

    

command string

`const SPIParseOpenOptions * _`options`_`

    

struct containing optional arguments

Callers should always zero out the entire _`options`_ struct, then fill
whichever fields they want to set. This ensures forward compatibility of code,
since any fields that are added to the struct in future will be defined to
behave backwards-compatibly if they are zero. The currently available
_`options`_ fields are:

`ParamListInfo _`params`_`

    

data structure containing query parameter types and values; NULL if none

`int _`cursorOptions`_`

    

integer bit mask of cursor options; zero produces default behavior

`bool _`read_only`_`

    

`true` for read-only execution

## Return Value

Pointer to portal containing the cursor. Note there is no error return
convention; any error will be reported via `elog`.

* * *

[Prev](spi-spi-cursor-open-with-paramlist.html "SPI_cursor_open_with_paramlist")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-cursor-find.html "SPI_cursor_find")  
---|---|---  
SPI_cursor_open_with_paramlist  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_cursor_find  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-cursor-parse-
open.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

