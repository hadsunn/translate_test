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

Supported Versions: [Current](/docs/current/spi-interface.html "PostgreSQL 17
- 47.1. Interface Functions") ([17](/docs/17/spi-interface.html "PostgreSQL 17
- 47.1. Interface Functions")) / [16](/docs/16/spi-interface.html "PostgreSQL
16 - 47.1. Interface Functions") / [15](/docs/15/spi-interface.html
"PostgreSQL 15 - 47.1. Interface Functions") / [14](/docs/14/spi-
interface.html "PostgreSQL 14 - 47.1. Interface Functions") /
[13](/docs/13/spi-interface.html "PostgreSQL 13 - 47.1. Interface Functions")

Development Versions: [18](/docs/18/spi-interface.html "PostgreSQL 18 -
47.1. Interface Functions") / [devel](/docs/devel/spi-interface.html
"PostgreSQL devel - 47.1. Interface Functions")

Unsupported versions: [12](/docs/12/spi-interface.html "PostgreSQL 12 -
47.1. Interface Functions") / [11](/docs/11/spi-interface.html "PostgreSQL 11
- 47.1. Interface Functions") / [10](/docs/10/spi-interface.html "PostgreSQL
10 - 47.1. Interface Functions") / [9.6](/docs/9.6/spi-interface.html
"PostgreSQL 9.6 - 47.1. Interface Functions") / [9.5](/docs/9.5/spi-
interface.html "PostgreSQL 9.5 - 47.1. Interface Functions") /
[9.4](/docs/9.4/spi-interface.html "PostgreSQL 9.4 - 47.1. Interface
Functions") / [9.3](/docs/9.3/spi-interface.html "PostgreSQL 9.3 -
47.1. Interface Functions") / [9.2](/docs/9.2/spi-interface.html "PostgreSQL
9.2 - 47.1. Interface Functions") / [9.1](/docs/9.1/spi-interface.html
"PostgreSQL 9.1 - 47.1. Interface Functions") / [9.0](/docs/9.0/spi-
interface.html "PostgreSQL 9.0 - 47.1. Interface Functions") /
[8.4](/docs/8.4/spi-interface.html "PostgreSQL 8.4 - 47.1. Interface
Functions") / [8.3](/docs/8.3/spi-interface.html "PostgreSQL 8.3 -
47.1. Interface Functions") / [8.2](/docs/8.2/spi-interface.html "PostgreSQL
8.2 - 47.1. Interface Functions")

__

47.1. Interface Functions  
---  
[Prev](spi.html "Chapter 47. Server Programming Interface")  | [Up](spi.html "Chapter 47. Server Programming Interface") | Chapter 47. Server Programming Interface | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-connect.html "SPI_connect")  
  
* * *

## 47.1. Interface Functions #

[SPI_connect](spi-spi-connect.html) — connect a C function to the SPI manager

[SPI_finish](spi-spi-finish.html) — disconnect a C function from the SPI
manager

[SPI_execute](spi-spi-execute.html) — execute a command

[SPI_exec](spi-spi-exec.html) — execute a read/write command

[SPI_execute_extended](spi-spi-execute-extended.html) — execute a command with
out-of-line parameters

[SPI_execute_with_args](spi-spi-execute-with-args.html) — execute a command
with out-of-line parameters

[SPI_prepare](spi-spi-prepare.html) — prepare a statement, without executing
it yet

[SPI_prepare_cursor](spi-spi-prepare-cursor.html) — prepare a statement,
without executing it yet

[SPI_prepare_extended](spi-spi-prepare-extended.html) — prepare a statement,
without executing it yet

[SPI_prepare_params](spi-spi-prepare-params.html) — prepare a statement,
without executing it yet

[SPI_getargcount](spi-spi-getargcount.html) — return the number of arguments
needed by a statement prepared by `SPI_prepare`

[SPI_getargtypeid](spi-spi-getargtypeid.html) — return the data type OID for
an argument of a statement prepared by `SPI_prepare`

[SPI_is_cursor_plan](spi-spi-is-cursor-plan.html) — return `true` if a
statement prepared by `SPI_prepare` can be used with `SPI_cursor_open`

[SPI_execute_plan](spi-spi-execute-plan.html) — execute a statement prepared
by `SPI_prepare`

[SPI_execute_plan_extended](spi-spi-execute-plan-extended.html) — execute a
statement prepared by `SPI_prepare`

[SPI_execute_plan_with_paramlist](spi-spi-execute-plan-with-paramlist.html) —
execute a statement prepared by `SPI_prepare`

[SPI_execp](spi-spi-execp.html) — execute a statement in read/write mode

[SPI_cursor_open](spi-spi-cursor-open.html) — set up a cursor using a
statement created with `SPI_prepare`

[SPI_cursor_open_with_args](spi-spi-cursor-open-with-args.html) — set up a
cursor using a query and parameters

[SPI_cursor_open_with_paramlist](spi-spi-cursor-open-with-paramlist.html) —
set up a cursor using parameters

[SPI_cursor_parse_open](spi-spi-cursor-parse-open.html) — set up a cursor
using a query string and parameters

[SPI_cursor_find](spi-spi-cursor-find.html) — find an existing cursor by name

[SPI_cursor_fetch](spi-spi-cursor-fetch.html) — fetch some rows from a cursor

[SPI_cursor_move](spi-spi-cursor-move.html) — move a cursor

[SPI_scroll_cursor_fetch](spi-spi-scroll-cursor-fetch.html) — fetch some rows
from a cursor

[SPI_scroll_cursor_move](spi-spi-scroll-cursor-move.html) — move a cursor

[SPI_cursor_close](spi-spi-cursor-close.html) — close a cursor

[SPI_keepplan](spi-spi-keepplan.html) — save a prepared statement

[SPI_saveplan](spi-spi-saveplan.html) — save a prepared statement

[SPI_register_relation](spi-spi-register-relation.html) — make an ephemeral
named relation available by name in SPI queries

[SPI_unregister_relation](spi-spi-unregister-relation.html) — remove an
ephemeral named relation from the registry

[SPI_register_trigger_data](spi-spi-register-trigger-data.html) — make
ephemeral trigger data available in SPI queries

* * *

[Prev](spi.html "Chapter 47. Server Programming Interface")  | [Up](spi.html "Chapter 47. Server Programming Interface") |  [Next](spi-spi-connect.html "SPI_connect")  
---|---|---  
Chapter 47. Server Programming Interface  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_connect  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-interface.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

