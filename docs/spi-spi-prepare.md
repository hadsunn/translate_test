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

Supported Versions: [Current](/docs/current/spi-spi-prepare.html "PostgreSQL
17 - SPI_prepare") ([17](/docs/17/spi-spi-prepare.html "PostgreSQL 17 -
SPI_prepare")) / [16](/docs/16/spi-spi-prepare.html "PostgreSQL 16 -
SPI_prepare") / [15](/docs/15/spi-spi-prepare.html "PostgreSQL 15 -
SPI_prepare") / [14](/docs/14/spi-spi-prepare.html "PostgreSQL 14 -
SPI_prepare") / [13](/docs/13/spi-spi-prepare.html "PostgreSQL 13 -
SPI_prepare")

Development Versions: [18](/docs/18/spi-spi-prepare.html "PostgreSQL 18 -
SPI_prepare") / [devel](/docs/devel/spi-spi-prepare.html "PostgreSQL devel -
SPI_prepare")

Unsupported versions: [12](/docs/12/spi-spi-prepare.html "PostgreSQL 12 -
SPI_prepare") / [11](/docs/11/spi-spi-prepare.html "PostgreSQL 11 -
SPI_prepare") / [10](/docs/10/spi-spi-prepare.html "PostgreSQL 10 -
SPI_prepare") / [9.6](/docs/9.6/spi-spi-prepare.html "PostgreSQL 9.6 -
SPI_prepare") / [9.5](/docs/9.5/spi-spi-prepare.html "PostgreSQL 9.5 -
SPI_prepare") / [9.4](/docs/9.4/spi-spi-prepare.html "PostgreSQL 9.4 -
SPI_prepare") / [9.3](/docs/9.3/spi-spi-prepare.html "PostgreSQL 9.3 -
SPI_prepare") / [9.2](/docs/9.2/spi-spi-prepare.html "PostgreSQL 9.2 -
SPI_prepare") / [9.1](/docs/9.1/spi-spi-prepare.html "PostgreSQL 9.1 -
SPI_prepare") / [9.0](/docs/9.0/spi-spi-prepare.html "PostgreSQL 9.0 -
SPI_prepare") / [8.4](/docs/8.4/spi-spi-prepare.html "PostgreSQL 8.4 -
SPI_prepare") / [8.3](/docs/8.3/spi-spi-prepare.html "PostgreSQL 8.3 -
SPI_prepare") / [8.2](/docs/8.2/spi-spi-prepare.html "PostgreSQL 8.2 -
SPI_prepare") / [8.1](/docs/8.1/spi-spi-prepare.html "PostgreSQL 8.1 -
SPI_prepare") / [8.0](/docs/8.0/spi-spi-prepare.html "PostgreSQL 8.0 -
SPI_prepare") / [7.4](/docs/7.4/spi-spi-prepare.html "PostgreSQL 7.4 -
SPI_prepare")

__

SPI_prepare  
---  
[Prev](spi-spi-execute-with-args.html "SPI_execute_with_args")  | [Up](spi-interface.html "47.1. Interface Functions") | 47.1. Interface Functions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-prepare-cursor.html "SPI_prepare_cursor")  
  
* * *

## SPI_prepare

SPI_prepare — prepare a statement, without executing it yet

## Synopsis

    
    
    SPIPlanPtr SPI_prepare(const char * _command_ , int _nargs_ , Oid * _argtypes_)
    

## Description

`SPI_prepare` creates and returns a prepared statement for the specified
command, but doesn't execute the command. The prepared statement can later be
executed repeatedly using `SPI_execute_plan`.

When the same or a similar command is to be executed repeatedly, it is
generally advantageous to perform parse analysis only once, and might
furthermore be advantageous to re-use an execution plan for the command.
`SPI_prepare` converts a command string into a prepared statement that
encapsulates the results of parse analysis. The prepared statement also
provides a place for caching an execution plan if it is found that generating
a custom plan for each execution is not helpful.

A prepared command can be generalized by writing parameters (`$1`, `$2`, etc.)
in place of what would be constants in a normal command. The actual values of
the parameters are then specified when `SPI_execute_plan` is called. This
allows the prepared command to be used over a wider range of situations than
would be possible without parameters.

The statement returned by `SPI_prepare` can be used only in the current
invocation of the C function, since `SPI_finish` frees memory allocated for
such a statement. But the statement can be saved for longer using the
functions `SPI_keepplan` or `SPI_saveplan`.

## Arguments

`const char * _`command`_`

    

command string

`int _`nargs`_`

    

number of input parameters (`$1`, `$2`, etc.)

`Oid * _`argtypes`_`

    

pointer to an array containing the OIDs of the data types of the parameters

## Return Value

`SPI_prepare` returns a non-null pointer to an `SPIPlan`, which is an opaque
struct representing a prepared statement. On error, `NULL` will be returned,
and `SPI_result` will be set to one of the same error codes used by
`SPI_execute`, except that it is set to `SPI_ERROR_ARGUMENT` if _`command`_ is
`NULL`, or if _`nargs`_ is less than 0, or if _`nargs`_ is greater than 0 and
_`argtypes`_ is `NULL`.

## Notes

If no parameters are defined, a generic plan will be created at the first use
of `SPI_execute_plan`, and used for all subsequent executions as well. If
there are parameters, the first few uses of `SPI_execute_plan` will generate
custom plans that are specific to the supplied parameter values. After enough
uses of the same prepared statement, `SPI_execute_plan` will build a generic
plan, and if that is not too much more expensive than the custom plans, it
will start using the generic plan instead of re-planning each time. If this
default behavior is unsuitable, you can alter it by passing the
`CURSOR_OPT_GENERIC_PLAN` or `CURSOR_OPT_CUSTOM_PLAN` flag to
`SPI_prepare_cursor`, to force use of generic or custom plans respectively.

Although the main point of a prepared statement is to avoid repeated parse
analysis and planning of the statement, PostgreSQL will force re-analysis and
re-planning of the statement before using it whenever database objects used in
the statement have undergone definitional (DDL) changes since the previous use
of the prepared statement. Also, if the value of [search_path](runtime-config-
client.html#GUC-SEARCH-PATH) changes from one use to the next, the statement
will be re-parsed using the new `search_path`. (This latter behavior is new as
of PostgreSQL 9.3.) See [PREPARE](sql-prepare.html "PREPARE") for more
information about the behavior of prepared statements.

This function should only be called from a connected C function.

`SPIPlanPtr` is declared as a pointer to an opaque struct type in `spi.h`. It
is unwise to try to access its contents directly, as that makes your code much
more likely to break in future revisions of PostgreSQL.

The name `SPIPlanPtr` is somewhat historical, since the data structure no
longer necessarily contains an execution plan.

* * *

[Prev](spi-spi-execute-with-args.html "SPI_execute_with_args")  | [Up](spi-interface.html "47.1. Interface Functions") |  [Next](spi-spi-prepare-cursor.html "SPI_prepare_cursor")  
---|---|---  
SPI_execute_with_args  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_prepare_cursor  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-prepare.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

