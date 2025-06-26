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

Supported Versions: [Current](/docs/current/spi-spi-execute-plan.html
"PostgreSQL 17 - SPI_execute_plan") ([17](/docs/17/spi-spi-execute-plan.html
"PostgreSQL 17 - SPI_execute_plan")) / [16](/docs/16/spi-spi-execute-plan.html
"PostgreSQL 16 - SPI_execute_plan") / [15](/docs/15/spi-spi-execute-plan.html
"PostgreSQL 15 - SPI_execute_plan") / [14](/docs/14/spi-spi-execute-plan.html
"PostgreSQL 14 - SPI_execute_plan") / [13](/docs/13/spi-spi-execute-plan.html
"PostgreSQL 13 - SPI_execute_plan")

Development Versions: [18](/docs/18/spi-spi-execute-plan.html "PostgreSQL 18 -
SPI_execute_plan") / [devel](/docs/devel/spi-spi-execute-plan.html "PostgreSQL
devel - SPI_execute_plan")

Unsupported versions: [12](/docs/12/spi-spi-execute-plan.html "PostgreSQL 12 -
SPI_execute_plan") / [11](/docs/11/spi-spi-execute-plan.html "PostgreSQL 11 -
SPI_execute_plan") / [10](/docs/10/spi-spi-execute-plan.html "PostgreSQL 10 -
SPI_execute_plan") / [9.6](/docs/9.6/spi-spi-execute-plan.html "PostgreSQL 9.6
- SPI_execute_plan") / [9.5](/docs/9.5/spi-spi-execute-plan.html "PostgreSQL
9.5 - SPI_execute_plan") / [9.4](/docs/9.4/spi-spi-execute-plan.html
"PostgreSQL 9.4 - SPI_execute_plan") / [9.3](/docs/9.3/spi-spi-execute-
plan.html "PostgreSQL 9.3 - SPI_execute_plan") / [9.2](/docs/9.2/spi-spi-
execute-plan.html "PostgreSQL 9.2 - SPI_execute_plan") / [9.1](/docs/9.1/spi-
spi-execute-plan.html "PostgreSQL 9.1 - SPI_execute_plan") /
[9.0](/docs/9.0/spi-spi-execute-plan.html "PostgreSQL 9.0 - SPI_execute_plan")
/ [8.4](/docs/8.4/spi-spi-execute-plan.html "PostgreSQL 8.4 -
SPI_execute_plan") / [8.3](/docs/8.3/spi-spi-execute-plan.html "PostgreSQL 8.3
- SPI_execute_plan") / [8.2](/docs/8.2/spi-spi-execute-plan.html "PostgreSQL
8.2 - SPI_execute_plan") / [8.1](/docs/8.1/spi-spi-execute-plan.html
"PostgreSQL 8.1 - SPI_execute_plan") / [8.0](/docs/8.0/spi-spi-execute-
plan.html "PostgreSQL 8.0 - SPI_execute_plan")

__

SPI_execute_plan  
---  
[Prev](spi-spi-is-cursor-plan.html "SPI_is_cursor_plan")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-execute-plan-extended.html "SPI_execute_plan_extended")  
  
* * *

## SPI_execute_plan

SPI_execute_plan — execute a statement prepared by `SPI_prepare`

## Synopsis

    
    
    int SPI_execute_plan(SPIPlanPtr _plan_ , Datum * _values_ , const char * _nulls_ ,
                         bool _read_only_ , long _count_)
    

## Description

`SPI_execute_plan` executes a statement prepared by `SPI_prepare` or one of
its siblings. _`read_only`_ and _`count`_ have the same interpretation as in
`SPI_execute`.

## Arguments

`SPIPlanPtr _`plan`_`

    

prepared statement (returned by `SPI_prepare`)

`Datum * _`values`_`

    

An array of actual parameter values. Must have same length as the statement's
number of arguments.

`const char * _`nulls`_`

    

An array describing which parameters are null. Must have same length as the
statement's number of arguments.

If _`nulls`_ is `NULL` then `SPI_execute_plan` assumes that no parameters are
null. Otherwise, each entry of the _`nulls`_ array should be `' '` if the
corresponding parameter value is non-null, or `'n'` if the corresponding
parameter value is null. (In the latter case, the actual value in the
corresponding _`values`_ entry doesn't matter.) Note that _`nulls`_ is not a
text string, just an array: it does not need a `'\0'` terminator.

`bool _`read_only`_`

    

`true` for read-only execution

`long _`count`_`

    

maximum number of rows to return, or `0` for no limit

## Return Value

The return value is the same as for `SPI_execute`, with the following
additional possible error (negative) results:

`SPI_ERROR_ARGUMENT`

    

if _`plan`_ is `NULL` or invalid, or _`count`_ is less than 0

`SPI_ERROR_PARAM`

    

if _`values`_ is `NULL` and _`plan`_ was prepared with some parameters

`SPI_processed` and `SPI_tuptable` are set as in `SPI_execute` if successful.

* * *

[Prev](spi-spi-is-cursor-plan.html "SPI_is_cursor_plan")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-execute-plan-extended.html "SPI_execute_plan_extended")  
---|---|---  
SPI_is_cursor_plan  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_execute_plan_extended  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-execute-plan.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

