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

Supported Versions: [Current](/docs/current/spi-spi-execp.html "PostgreSQL 17
- SPI_execp") ([17](/docs/17/spi-spi-execp.html "PostgreSQL 17 - SPI_execp"))
/ [16](/docs/16/spi-spi-execp.html "PostgreSQL 16 - SPI_execp") /
[15](/docs/15/spi-spi-execp.html "PostgreSQL 15 - SPI_execp") /
[14](/docs/14/spi-spi-execp.html "PostgreSQL 14 - SPI_execp") /
[13](/docs/13/spi-spi-execp.html "PostgreSQL 13 - SPI_execp")

Development Versions: [18](/docs/18/spi-spi-execp.html "PostgreSQL 18 -
SPI_execp") / [devel](/docs/devel/spi-spi-execp.html "PostgreSQL devel -
SPI_execp")

Unsupported versions: [12](/docs/12/spi-spi-execp.html "PostgreSQL 12 -
SPI_execp") / [11](/docs/11/spi-spi-execp.html "PostgreSQL 11 - SPI_execp") /
[10](/docs/10/spi-spi-execp.html "PostgreSQL 10 - SPI_execp") /
[9.6](/docs/9.6/spi-spi-execp.html "PostgreSQL 9.6 - SPI_execp") /
[9.5](/docs/9.5/spi-spi-execp.html "PostgreSQL 9.5 - SPI_execp") /
[9.4](/docs/9.4/spi-spi-execp.html "PostgreSQL 9.4 - SPI_execp") /
[9.3](/docs/9.3/spi-spi-execp.html "PostgreSQL 9.3 - SPI_execp") /
[9.2](/docs/9.2/spi-spi-execp.html "PostgreSQL 9.2 - SPI_execp") /
[9.1](/docs/9.1/spi-spi-execp.html "PostgreSQL 9.1 - SPI_execp") /
[9.0](/docs/9.0/spi-spi-execp.html "PostgreSQL 9.0 - SPI_execp") /
[8.4](/docs/8.4/spi-spi-execp.html "PostgreSQL 8.4 - SPI_execp") /
[8.3](/docs/8.3/spi-spi-execp.html "PostgreSQL 8.3 - SPI_execp") /
[8.2](/docs/8.2/spi-spi-execp.html "PostgreSQL 8.2 - SPI_execp") /
[8.1](/docs/8.1/spi-spi-execp.html "PostgreSQL 8.1 - SPI_execp") /
[8.0](/docs/8.0/spi-spi-execp.html "PostgreSQL 8.0 - SPI_execp") /
[7.4](/docs/7.4/spi-spi-execp.html "PostgreSQL 7.4 - SPI_execp")

__

SPI_execp  
---  
[Prev](spi-spi-execute-plan-with-paramlist.html "SPI_execute_plan_with_paramlist")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-cursor-open.html "SPI_cursor_open")  
  
* * *

## SPI_execp

SPI_execp — execute a statement in read/write mode

## Synopsis

    
    
    int SPI_execp(SPIPlanPtr _plan_ , Datum * _values_ , const char * _nulls_ , long _count_)
    

## Description

`SPI_execp` is the same as `SPI_execute_plan`, with the latter's _`read_only`_
parameter always taken as `false`.

## Arguments

`SPIPlanPtr _`plan`_`

    

prepared statement (returned by `SPI_prepare`)

`Datum * _`values`_`

    

An array of actual parameter values. Must have same length as the statement's
number of arguments.

`const char * _`nulls`_`

    

An array describing which parameters are null. Must have same length as the
statement's number of arguments.

If _`nulls`_ is `NULL` then `SPI_execp` assumes that no parameters are null.
Otherwise, each entry of the _`nulls`_ array should be `' '` if the
corresponding parameter value is non-null, or `'n'` if the corresponding
parameter value is null. (In the latter case, the actual value in the
corresponding _`values`_ entry doesn't matter.) Note that _`nulls`_ is not a
text string, just an array: it does not need a `'\0'` terminator.

`long _`count`_`

    

maximum number of rows to return, or `0` for no limit

## Return Value

See `SPI_execute_plan`.

`SPI_processed` and `SPI_tuptable` are set as in `SPI_execute` if successful.

* * *

[Prev](spi-spi-execute-plan-with-paramlist.html "SPI_execute_plan_with_paramlist")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-cursor-open.html "SPI_cursor_open")  
---|---|---  
SPI_execute_plan_with_paramlist  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_cursor_open  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-execp.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

