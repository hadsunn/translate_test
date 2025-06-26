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

Supported Versions: [Current](/docs/current/spi-spi-cursor-open-with-args.html
"PostgreSQL 17 - SPI_cursor_open_with_args") ([17](/docs/17/spi-spi-cursor-
open-with-args.html "PostgreSQL 17 - SPI_cursor_open_with_args")) /
[16](/docs/16/spi-spi-cursor-open-with-args.html "PostgreSQL 16 -
SPI_cursor_open_with_args") / [15](/docs/15/spi-spi-cursor-open-with-args.html
"PostgreSQL 15 - SPI_cursor_open_with_args") / [14](/docs/14/spi-spi-cursor-
open-with-args.html "PostgreSQL 14 - SPI_cursor_open_with_args") /
[13](/docs/13/spi-spi-cursor-open-with-args.html "PostgreSQL 13 -
SPI_cursor_open_with_args")

Development Versions: [18](/docs/18/spi-spi-cursor-open-with-args.html
"PostgreSQL 18 - SPI_cursor_open_with_args") / [devel](/docs/devel/spi-spi-
cursor-open-with-args.html "PostgreSQL devel - SPI_cursor_open_with_args")

Unsupported versions: [12](/docs/12/spi-spi-cursor-open-with-args.html
"PostgreSQL 12 - SPI_cursor_open_with_args") / [11](/docs/11/spi-spi-cursor-
open-with-args.html "PostgreSQL 11 - SPI_cursor_open_with_args") /
[10](/docs/10/spi-spi-cursor-open-with-args.html "PostgreSQL 10 -
SPI_cursor_open_with_args") / [9.6](/docs/9.6/spi-spi-cursor-open-with-
args.html "PostgreSQL 9.6 - SPI_cursor_open_with_args") / [9.5](/docs/9.5/spi-
spi-cursor-open-with-args.html "PostgreSQL 9.5 - SPI_cursor_open_with_args") /
[9.4](/docs/9.4/spi-spi-cursor-open-with-args.html "PostgreSQL 9.4 -
SPI_cursor_open_with_args") / [9.3](/docs/9.3/spi-spi-cursor-open-with-
args.html "PostgreSQL 9.3 - SPI_cursor_open_with_args") / [9.2](/docs/9.2/spi-
spi-cursor-open-with-args.html "PostgreSQL 9.2 - SPI_cursor_open_with_args") /
[9.1](/docs/9.1/spi-spi-cursor-open-with-args.html "PostgreSQL 9.1 -
SPI_cursor_open_with_args") / [9.0](/docs/9.0/spi-spi-cursor-open-with-
args.html "PostgreSQL 9.0 - SPI_cursor_open_with_args") / [8.4](/docs/8.4/spi-
spi-cursor-open-with-args.html "PostgreSQL 8.4 - SPI_cursor_open_with_args")

__

SPI_cursor_open_with_args  
---  
[Prev](spi-spi-cursor-open.html "SPI_cursor_open")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-cursor-open-with-paramlist.html "SPI_cursor_open_with_paramlist")  
  
* * *

## SPI_cursor_open_with_args

SPI_cursor_open_with_args — set up a cursor using a query and parameters

## Synopsis

    
    
    Portal SPI_cursor_open_with_args(const char *_name_ ,
                                     const char *_command_ ,
                                     int _nargs_ , Oid *_argtypes_ ,
                                     Datum *_values_ , const char *_nulls_ ,
                                     bool _read_only_ , int _cursorOptions_)
    

## Description

`SPI_cursor_open_with_args` sets up a cursor (internally, a portal) that will
execute the specified query. Most of the parameters have the same meanings as
the corresponding parameters to `SPI_prepare_cursor` and `SPI_cursor_open`.

For one-time query execution, this function should be preferred over
`SPI_prepare_cursor` followed by `SPI_cursor_open`. If the same command is to
be executed with many different parameters, either method might be faster,
depending on the cost of re-planning versus the benefit of custom plans.

The passed-in parameter data will be copied into the cursor's portal, so it
can be freed while the cursor still exists.

This function is now deprecated in favor of `SPI_cursor_parse_open`, which
provides equivalent functionality using a more modern API for handling query
parameters.

## Arguments

`const char * _`name`_`

    

name for portal, or `NULL` to let the system select a name

`const char * _`command`_`

    

command string

`int _`nargs`_`

    

number of input parameters (`$1`, `$2`, etc.)

`Oid * _`argtypes`_`

    

an array of length _`nargs`_ , containing the OIDs of the data types of the
parameters

`Datum * _`values`_`

    

an array of length _`nargs`_ , containing the actual parameter values

`const char * _`nulls`_`

    

an array of length _`nargs`_ , describing which parameters are null

If _`nulls`_ is `NULL` then `SPI_cursor_open_with_args` assumes that no
parameters are null. Otherwise, each entry of the _`nulls`_ array should be `'
'` if the corresponding parameter value is non-null, or `'n'` if the
corresponding parameter value is null. (In the latter case, the actual value
in the corresponding _`values`_ entry doesn't matter.) Note that _`nulls`_ is
not a text string, just an array: it does not need a `'\0'` terminator.

`bool _`read_only`_`

    

`true` for read-only execution

`int _`cursorOptions`_`

    

integer bit mask of cursor options; zero produces default behavior

## Return Value

Pointer to portal containing the cursor. Note there is no error return
convention; any error will be reported via `elog`.

* * *

[Prev](spi-spi-cursor-open.html "SPI_cursor_open")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-cursor-open-with-paramlist.html "SPI_cursor_open_with_paramlist")  
---|---|---  
SPI_cursor_open  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_cursor_open_with_paramlist  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-cursor-open-with-
args.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

