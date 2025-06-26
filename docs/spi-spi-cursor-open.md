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

Supported Versions: [Current](/docs/current/spi-spi-cursor-open.html
"PostgreSQL 17 - SPI_cursor_open") ([17](/docs/17/spi-spi-cursor-open.html
"PostgreSQL 17 - SPI_cursor_open")) / [16](/docs/16/spi-spi-cursor-open.html
"PostgreSQL 16 - SPI_cursor_open") / [15](/docs/15/spi-spi-cursor-open.html
"PostgreSQL 15 - SPI_cursor_open") / [14](/docs/14/spi-spi-cursor-open.html
"PostgreSQL 14 - SPI_cursor_open") / [13](/docs/13/spi-spi-cursor-open.html
"PostgreSQL 13 - SPI_cursor_open")

Development Versions: [18](/docs/18/spi-spi-cursor-open.html "PostgreSQL 18 -
SPI_cursor_open") / [devel](/docs/devel/spi-spi-cursor-open.html "PostgreSQL
devel - SPI_cursor_open")

Unsupported versions: [12](/docs/12/spi-spi-cursor-open.html "PostgreSQL 12 -
SPI_cursor_open") / [11](/docs/11/spi-spi-cursor-open.html "PostgreSQL 11 -
SPI_cursor_open") / [10](/docs/10/spi-spi-cursor-open.html "PostgreSQL 10 -
SPI_cursor_open") / [9.6](/docs/9.6/spi-spi-cursor-open.html "PostgreSQL 9.6 -
SPI_cursor_open") / [9.5](/docs/9.5/spi-spi-cursor-open.html "PostgreSQL 9.5 -
SPI_cursor_open") / [9.4](/docs/9.4/spi-spi-cursor-open.html "PostgreSQL 9.4 -
SPI_cursor_open") / [9.3](/docs/9.3/spi-spi-cursor-open.html "PostgreSQL 9.3 -
SPI_cursor_open") / [9.2](/docs/9.2/spi-spi-cursor-open.html "PostgreSQL 9.2 -
SPI_cursor_open") / [9.1](/docs/9.1/spi-spi-cursor-open.html "PostgreSQL 9.1 -
SPI_cursor_open") / [9.0](/docs/9.0/spi-spi-cursor-open.html "PostgreSQL 9.0 -
SPI_cursor_open") / [8.4](/docs/8.4/spi-spi-cursor-open.html "PostgreSQL 8.4 -
SPI_cursor_open") / [8.3](/docs/8.3/spi-spi-cursor-open.html "PostgreSQL 8.3 -
SPI_cursor_open") / [8.2](/docs/8.2/spi-spi-cursor-open.html "PostgreSQL 8.2 -
SPI_cursor_open") / [8.1](/docs/8.1/spi-spi-cursor-open.html "PostgreSQL 8.1 -
SPI_cursor_open") / [8.0](/docs/8.0/spi-spi-cursor-open.html "PostgreSQL 8.0 -
SPI_cursor_open") / [7.4](/docs/7.4/spi-spi-cursor-open.html "PostgreSQL 7.4 -
SPI_cursor_open")

__

SPI_cursor_open  
---  
[Prev](spi-spi-execp.html "SPI_execp")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-cursor-open-with-args.html "SPI_cursor_open_with_args")  
  
* * *

## SPI_cursor_open

SPI_cursor_open — set up a cursor using a statement created with `SPI_prepare`

## Synopsis

    
    
    Portal SPI_cursor_open(const char * _name_ , SPIPlanPtr _plan_ ,
                           Datum * _values_ , const char * _nulls_ ,
                           bool _read_only_)
    

## Description

`SPI_cursor_open` sets up a cursor (internally, a portal) that will execute a
statement prepared by `SPI_prepare`. The parameters have the same meanings as
the corresponding parameters to `SPI_execute_plan`.

Using a cursor instead of executing the statement directly has two benefits.
First, the result rows can be retrieved a few at a time, avoiding memory
overrun for queries that return many rows. Second, a portal can outlive the
current C function (it can, in fact, live to the end of the current
transaction). Returning the portal name to the C function's caller provides a
way of returning a row set as result.

The passed-in parameter data will be copied into the cursor's portal, so it
can be freed while the cursor still exists.

## Arguments

`const char * _`name`_`

    

name for portal, or `NULL` to let the system select a name

`SPIPlanPtr _`plan`_`

    

prepared statement (returned by `SPI_prepare`)

`Datum * _`values`_`

    

An array of actual parameter values. Must have same length as the statement's
number of arguments.

`const char * _`nulls`_`

    

An array describing which parameters are null. Must have same length as the
statement's number of arguments.

If _`nulls`_ is `NULL` then `SPI_cursor_open` assumes that no parameters are
null. Otherwise, each entry of the _`nulls`_ array should be `' '` if the
corresponding parameter value is non-null, or `'n'` if the corresponding
parameter value is null. (In the latter case, the actual value in the
corresponding _`values`_ entry doesn't matter.) Note that _`nulls`_ is not a
text string, just an array: it does not need a `'\0'` terminator.

`bool _`read_only`_`

    

`true` for read-only execution

## Return Value

Pointer to portal containing the cursor. Note there is no error return
convention; any error will be reported via `elog`.

* * *

[Prev](spi-spi-execp.html "SPI_execp")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-cursor-open-with-args.html "SPI_cursor_open_with_args")  
---|---|---  
SPI_execp  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_cursor_open_with_args  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-cursor-open.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

