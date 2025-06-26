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

Supported Versions: [Current](/docs/current/spi.html "PostgreSQL 17 -
Chapter 47. Server Programming Interface") ([17](/docs/17/spi.html "PostgreSQL
17 - Chapter 47. Server Programming Interface")) / [16](/docs/16/spi.html
"PostgreSQL 16 - Chapter 47. Server Programming Interface") /
[15](/docs/15/spi.html "PostgreSQL 15 - Chapter 47. Server Programming
Interface") / [14](/docs/14/spi.html "PostgreSQL 14 - Chapter 47. Server
Programming Interface") / [13](/docs/13/spi.html "PostgreSQL 13 -
Chapter 47. Server Programming Interface")

Development Versions: [18](/docs/18/spi.html "PostgreSQL 18 -
Chapter 47. Server Programming Interface") / [devel](/docs/devel/spi.html
"PostgreSQL devel - Chapter 47. Server Programming Interface")

Unsupported versions: [12](/docs/12/spi.html "PostgreSQL 12 -
Chapter 47. Server Programming Interface") / [11](/docs/11/spi.html
"PostgreSQL 11 - Chapter 47. Server Programming Interface") /
[10](/docs/10/spi.html "PostgreSQL 10 - Chapter 47. Server Programming
Interface") / [9.6](/docs/9.6/spi.html "PostgreSQL 9.6 - Chapter 47. Server
Programming Interface") / [9.5](/docs/9.5/spi.html "PostgreSQL 9.5 -
Chapter 47. Server Programming Interface") / [9.4](/docs/9.4/spi.html
"PostgreSQL 9.4 - Chapter 47. Server Programming Interface") /
[9.3](/docs/9.3/spi.html "PostgreSQL 9.3 - Chapter 47. Server Programming
Interface") / [9.2](/docs/9.2/spi.html "PostgreSQL 9.2 - Chapter 47. Server
Programming Interface") / [9.1](/docs/9.1/spi.html "PostgreSQL 9.1 -
Chapter 47. Server Programming Interface") / [9.0](/docs/9.0/spi.html
"PostgreSQL 9.0 - Chapter 47. Server Programming Interface") /
[8.4](/docs/8.4/spi.html "PostgreSQL 8.4 - Chapter 47. Server Programming
Interface") / [8.3](/docs/8.3/spi.html "PostgreSQL 8.3 - Chapter 47. Server
Programming Interface") / [8.2](/docs/8.2/spi.html "PostgreSQL 8.2 -
Chapter 47. Server Programming Interface") / [8.1](/docs/8.1/spi.html
"PostgreSQL 8.1 - Chapter 47. Server Programming Interface") /
[8.0](/docs/8.0/spi.html "PostgreSQL 8.0 - Chapter 47. Server Programming
Interface") / [7.4](/docs/7.4/spi.html "PostgreSQL 7.4 - Chapter 47. Server
Programming Interface") / [7.3](/docs/7.3/spi.html "PostgreSQL 7.3 -
Chapter 47. Server Programming Interface") / [7.2](/docs/7.2/spi.html
"PostgreSQL 7.2 - Chapter 47. Server Programming Interface") /
[7.1](/docs/7.1/spi.html "PostgreSQL 7.1 - Chapter 47. Server Programming
Interface")

__

Chapter 47. Server Programming Interface  
---  
[Prev](plpython-envar.html "46.11. Environment Variables")  | [Up](server-programming.html "Part V. Server Programming") | Part V. Server Programming | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-interface.html "47.1. Interface Functions")  
  
* * *

## Chapter 47. Server Programming Interface

**Table of Contents**

[47.1. Interface Functions](spi-interface.html)

    

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

[47.2. Interface Support Functions](spi-interface-support.html)

    

[SPI_fname](spi-spi-fname.html) — determine the column name for the specified
column number

[SPI_fnumber](spi-spi-fnumber.html) — determine the column number for the
specified column name

[SPI_getvalue](spi-spi-getvalue.html) — return the string value of the
specified column

[SPI_getbinval](spi-spi-getbinval.html) — return the binary value of the
specified column

[SPI_gettype](spi-spi-gettype.html) — return the data type name of the
specified column

[SPI_gettypeid](spi-spi-gettypeid.html) — return the data type OID of the
specified column

[SPI_getrelname](spi-spi-getrelname.html) — return the name of the specified
relation

[SPI_getnspname](spi-spi-getnspname.html) — return the namespace of the
specified relation

[SPI_result_code_string](spi-spi-result-code-string.html) — return error code
as string

[47.3. Memory Management](spi-memory.html)

    

[SPI_palloc](spi-spi-palloc.html) — allocate memory in the upper executor
context

[SPI_repalloc](spi-realloc.html) — reallocate memory in the upper executor
context

[SPI_pfree](spi-spi-pfree.html) — free memory in the upper executor context

[SPI_copytuple](spi-spi-copytuple.html) — make a copy of a row in the upper
executor context

[SPI_returntuple](spi-spi-returntuple.html) — prepare to return a tuple as a
Datum

[SPI_modifytuple](spi-spi-modifytuple.html) — create a row by replacing
selected fields of a given row

[SPI_freetuple](spi-spi-freetuple.html) — free a row allocated in the upper
executor context

[SPI_freetuptable](spi-spi-freetupletable.html) — free a row set created by
`SPI_execute` or a similar function

[SPI_freeplan](spi-spi-freeplan.html) — free a previously saved prepared
statement

[47.4. Transaction Management](spi-transaction.html)

    

[SPI_commit](spi-spi-commit.html) — commit the current transaction

[SPI_rollback](spi-spi-rollback.html) — abort the current transaction

[SPI_start_transaction](spi-spi-start-transaction.html) — obsolete function

[47.5. Visibility of Data Changes](spi-visibility.html)

[47.6. Examples](spi-examples.html)

The _Server Programming Interface_ (SPI) gives writers of user-defined C
functions the ability to run SQL commands inside their functions or
procedures. SPI is a set of interface functions to simplify access to the
parser, planner, and executor. SPI also does some memory management.

### Note

The available procedural languages provide various means to execute SQL
commands from functions. Most of these facilities are based on SPI, so this
documentation might be of use for users of those languages as well.

Note that if a command invoked via SPI fails, then control will not be
returned to your C function. Rather, the transaction or subtransaction in
which your C function executes will be rolled back. (This might seem
surprising given that the SPI functions mostly have documented error-return
conventions. Those conventions only apply for errors detected within the SPI
functions themselves, however.) It is possible to recover control after an
error by establishing your own subtransaction surrounding SPI calls that might
fail.

SPI functions return a nonnegative result on success (either via a returned
integer value or in the global variable `SPI_result`, as described below). On
error, a negative result or `NULL` will be returned.

Source code files that use SPI must include the header file `executor/spi.h`.

* * *

[Prev](plpython-envar.html "46.11. Environment Variables")  | [Up](server-programming.html "Part V. Server Programming") |  [Next](spi-interface.html "47.1. Interface Functions")  
---|---|---  
46.11. Environment Variables  | [Home](index.html "PostgreSQL 16.9 Documentation") |  47.1. Interface Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

