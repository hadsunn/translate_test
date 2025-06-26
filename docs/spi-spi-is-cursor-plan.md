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

Supported Versions: [Current](/docs/current/spi-spi-is-cursor-plan.html
"PostgreSQL 17 - SPI_is_cursor_plan") ([17](/docs/17/spi-spi-is-cursor-
plan.html "PostgreSQL 17 - SPI_is_cursor_plan")) / [16](/docs/16/spi-spi-is-
cursor-plan.html "PostgreSQL 16 - SPI_is_cursor_plan") / [15](/docs/15/spi-
spi-is-cursor-plan.html "PostgreSQL 15 - SPI_is_cursor_plan") /
[14](/docs/14/spi-spi-is-cursor-plan.html "PostgreSQL 14 -
SPI_is_cursor_plan") / [13](/docs/13/spi-spi-is-cursor-plan.html "PostgreSQL
13 - SPI_is_cursor_plan")

Development Versions: [18](/docs/18/spi-spi-is-cursor-plan.html "PostgreSQL 18
- SPI_is_cursor_plan") / [devel](/docs/devel/spi-spi-is-cursor-plan.html
"PostgreSQL devel - SPI_is_cursor_plan")

Unsupported versions: [12](/docs/12/spi-spi-is-cursor-plan.html "PostgreSQL 12
- SPI_is_cursor_plan") / [11](/docs/11/spi-spi-is-cursor-plan.html "PostgreSQL
11 - SPI_is_cursor_plan") / [10](/docs/10/spi-spi-is-cursor-plan.html
"PostgreSQL 10 - SPI_is_cursor_plan") / [9.6](/docs/9.6/spi-spi-is-cursor-
plan.html "PostgreSQL 9.6 - SPI_is_cursor_plan") / [9.5](/docs/9.5/spi-spi-is-
cursor-plan.html "PostgreSQL 9.5 - SPI_is_cursor_plan") / [9.4](/docs/9.4/spi-
spi-is-cursor-plan.html "PostgreSQL 9.4 - SPI_is_cursor_plan") /
[9.3](/docs/9.3/spi-spi-is-cursor-plan.html "PostgreSQL 9.3 -
SPI_is_cursor_plan") / [9.2](/docs/9.2/spi-spi-is-cursor-plan.html "PostgreSQL
9.2 - SPI_is_cursor_plan") / [9.1](/docs/9.1/spi-spi-is-cursor-plan.html
"PostgreSQL 9.1 - SPI_is_cursor_plan") / [9.0](/docs/9.0/spi-spi-is-cursor-
plan.html "PostgreSQL 9.0 - SPI_is_cursor_plan") / [8.4](/docs/8.4/spi-spi-is-
cursor-plan.html "PostgreSQL 8.4 - SPI_is_cursor_plan") / [8.3](/docs/8.3/spi-
spi-is-cursor-plan.html "PostgreSQL 8.3 - SPI_is_cursor_plan") /
[8.2](/docs/8.2/spi-spi-is-cursor-plan.html "PostgreSQL 8.2 -
SPI_is_cursor_plan") / [8.1](/docs/8.1/spi-spi-is-cursor-plan.html "PostgreSQL
8.1 - SPI_is_cursor_plan") / [8.0](/docs/8.0/spi-spi-is-cursor-plan.html
"PostgreSQL 8.0 - SPI_is_cursor_plan")

__

SPI_is_cursor_plan  
---  
[Prev](spi-spi-getargtypeid.html "SPI_getargtypeid")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-execute-plan.html "SPI_execute_plan")  
  
* * *

## SPI_is_cursor_plan

SPI_is_cursor_plan — return `true` if a statement prepared by `SPI_prepare`
can be used with `SPI_cursor_open`

## Synopsis

    
    
    bool SPI_is_cursor_plan(SPIPlanPtr _plan_)
    

## Description

`SPI_is_cursor_plan` returns `true` if a statement prepared by `SPI_prepare`
can be passed as an argument to `SPI_cursor_open`, or `false` if that is not
the case. The criteria are that the _`plan`_ represents one single command and
that this command returns tuples to the caller; for example, `SELECT` is
allowed unless it contains an `INTO` clause, and `UPDATE` is allowed only if
it contains a `RETURNING` clause.

## Arguments

`SPIPlanPtr _`plan`_`

    

prepared statement (returned by `SPI_prepare`)

## Return Value

`true` or `false` to indicate if the _`plan`_ can produce a cursor or not,
with `SPI_result` set to zero. If it is not possible to determine the answer
(for example, if the _`plan`_ is `NULL` or invalid, or if called when not
connected to SPI), then `SPI_result` is set to a suitable error code and
`false` is returned.

* * *

[Prev](spi-spi-getargtypeid.html "SPI_getargtypeid")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-execute-plan.html "SPI_execute_plan")  
---|---|---  
SPI_getargtypeid  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_execute_plan  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-is-cursor-plan.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

