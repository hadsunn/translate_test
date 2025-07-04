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

Supported Versions: [Current](/docs/current/plhandler.html "PostgreSQL 17 -
Chapter 58. Writing a Procedural Language Handler")
([17](/docs/17/plhandler.html "PostgreSQL 17 - Chapter 58. Writing a
Procedural Language Handler")) / [16](/docs/16/plhandler.html "PostgreSQL 16 -
Chapter 58. Writing a Procedural Language Handler") /
[15](/docs/15/plhandler.html "PostgreSQL 15 - Chapter 58. Writing a Procedural
Language Handler") / [14](/docs/14/plhandler.html "PostgreSQL 14 -
Chapter 58. Writing a Procedural Language Handler") /
[13](/docs/13/plhandler.html "PostgreSQL 13 - Chapter 58. Writing a Procedural
Language Handler")

Development Versions: [18](/docs/18/plhandler.html "PostgreSQL 18 -
Chapter 58. Writing a Procedural Language Handler") /
[devel](/docs/devel/plhandler.html "PostgreSQL devel - Chapter 58. Writing a
Procedural Language Handler")

Unsupported versions: [12](/docs/12/plhandler.html "PostgreSQL 12 -
Chapter 58. Writing a Procedural Language Handler") /
[11](/docs/11/plhandler.html "PostgreSQL 11 - Chapter 58. Writing a Procedural
Language Handler") / [10](/docs/10/plhandler.html "PostgreSQL 10 -
Chapter 58. Writing a Procedural Language Handler") /
[9.6](/docs/9.6/plhandler.html "PostgreSQL 9.6 - Chapter 58. Writing a
Procedural Language Handler") / [9.5](/docs/9.5/plhandler.html "PostgreSQL 9.5
- Chapter 58. Writing a Procedural Language Handler") /
[9.4](/docs/9.4/plhandler.html "PostgreSQL 9.4 - Chapter 58. Writing a
Procedural Language Handler") / [9.3](/docs/9.3/plhandler.html "PostgreSQL 9.3
- Chapter 58. Writing a Procedural Language Handler") /
[9.2](/docs/9.2/plhandler.html "PostgreSQL 9.2 - Chapter 58. Writing a
Procedural Language Handler") / [9.1](/docs/9.1/plhandler.html "PostgreSQL 9.1
- Chapter 58. Writing a Procedural Language Handler") /
[9.0](/docs/9.0/plhandler.html "PostgreSQL 9.0 - Chapter 58. Writing a
Procedural Language Handler") / [8.4](/docs/8.4/plhandler.html "PostgreSQL 8.4
- Chapter 58. Writing a Procedural Language Handler") /
[8.3](/docs/8.3/plhandler.html "PostgreSQL 8.3 - Chapter 58. Writing a
Procedural Language Handler") / [8.2](/docs/8.2/plhandler.html "PostgreSQL 8.2
- Chapter 58. Writing a Procedural Language Handler") /
[8.1](/docs/8.1/plhandler.html "PostgreSQL 8.1 - Chapter 58. Writing a
Procedural Language Handler") / [8.0](/docs/8.0/plhandler.html "PostgreSQL 8.0
- Chapter 58. Writing a Procedural Language Handler") /
[7.4](/docs/7.4/plhandler.html "PostgreSQL 7.4 - Chapter 58. Writing a
Procedural Language Handler")

__

Chapter 58. Writing a Procedural Language Handler  
---  
[Prev](nls-programmer.html "57.2. For the Programmer")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](fdwhandler.html "Chapter 59. Writing a Foreign Data Wrapper")  
  
* * *

## Chapter 58. Writing a Procedural Language Handler

All calls to functions that are written in a language other than the current
“version 1” interface for compiled languages (this includes functions in user-
defined procedural languages and functions written in SQL) go through a _call
handler_ function for the specific language. It is the responsibility of the
call handler to execute the function in a meaningful way, such as by
interpreting the supplied source text. This chapter outlines how a new
procedural language's call handler can be written.

The call handler for a procedural language is a “normal” function that must be
written in a compiled language such as C, using the version-1 interface, and
registered with PostgreSQL as taking no arguments and returning the type
`language_handler`. This special pseudo-type identifies the function as a call
handler and prevents it from being called directly in SQL commands. For more
details on C language calling conventions and dynamic loading, see [Section
38.10](xfunc-c.html "38.10. C-Language Functions").

The call handler is called in the same way as any other function: It receives
a pointer to a `FunctionCallInfoBaseData` `struct` containing argument values
and information about the called function, and it is expected to return a
`Datum` result (and possibly set the `isnull` field of the
`FunctionCallInfoBaseData` structure, if it wishes to return an SQL null
result). The difference between a call handler and an ordinary callee function
is that the `flinfo->fn_oid` field of the `FunctionCallInfoBaseData` structure
will contain the OID of the actual function to be called, not of the call
handler itself. The call handler must use this field to determine which
function to execute. Also, the passed argument list has been set up according
to the declaration of the target function, not of the call handler.

It's up to the call handler to fetch the entry of the function from the
`pg_proc` system catalog and to analyze the argument and return types of the
called function. The `AS` clause from the `CREATE FUNCTION` command for the
function will be found in the `prosrc` column of the `pg_proc` row. This is
commonly source text in the procedural language, but in theory it could be
something else, such as a path name to a file, or anything else that tells the
call handler what to do in detail.

Often, the same function is called many times per SQL statement. A call
handler can avoid repeated lookups of information about the called function by
using the `flinfo->fn_extra` field. This will initially be `NULL`, but can be
set by the call handler to point at information about the called function. On
subsequent calls, if `flinfo->fn_extra` is already non-`NULL` then it can be
used and the information lookup step skipped. The call handler must make sure
that `flinfo->fn_extra` is made to point at memory that will live at least
until the end of the current query, since an `FmgrInfo` data structure could
be kept that long. One way to do this is to allocate the extra data in the
memory context specified by `flinfo->fn_mcxt`; such data will normally have
the same lifespan as the `FmgrInfo` itself. But the handler could also choose
to use a longer-lived memory context so that it can cache function definition
information across queries.

When a procedural-language function is invoked as a trigger, no arguments are
passed in the usual way, but the `FunctionCallInfoBaseData`'s `context` field
points at a `TriggerData` structure, rather than being `NULL` as it is in a
plain function call. A language handler should provide mechanisms for
procedural-language functions to get at the trigger information.

A template for a procedural-language handler written as a C extension is
provided in `src/test/modules/plsample`. This is a working sample
demonstrating one way to create a procedural-language handler, process
parameters, and return a value.

Although providing a call handler is sufficient to create a minimal procedural
language, there are two other functions that can optionally be provided to
make the language more convenient to use. These are a _validator_ and an
_inline handler_. A validator can be provided to allow language-specific
checking to be done during [CREATE FUNCTION](sql-createfunction.html "CREATE
FUNCTION"). An inline handler can be provided to allow the language to support
anonymous code blocks executed via the [DO](sql-do.html "DO") command.

If a validator is provided by a procedural language, it must be declared as a
function taking a single parameter of type `oid`. The validator's result is
ignored, so it is customarily declared to return `void`. The validator will be
called at the end of a `CREATE FUNCTION` command that has created or updated a
function written in the procedural language. The passed-in OID is the OID of
the function's `pg_proc` row. The validator must fetch this row in the usual
way, and do whatever checking is appropriate. First, call
`CheckFunctionValidatorAccess()` to diagnose explicit calls to the validator
that the user could not achieve through `CREATE FUNCTION`. Typical checks then
include verifying that the function's argument and result types are supported
by the language, and that the function's body is syntactically correct in the
language. If the validator finds the function to be okay, it should just
return. If it finds an error, it should report that via the normal `ereport()`
error reporting mechanism. Throwing an error will force a transaction rollback
and thus prevent the incorrect function definition from being committed.

Validator functions should typically honor the
[check_function_bodies](runtime-config-client.html#GUC-CHECK-FUNCTION-BODIES)
parameter: if it is turned off then any expensive or context-sensitive
checking should be skipped. If the language provides for code execution at
compilation time, the validator must suppress checks that would induce such
execution. In particular, this parameter is turned off by pg_dump so that it
can load procedural language functions without worrying about side effects or
dependencies of the function bodies on other database objects. (Because of
this requirement, the call handler should avoid assuming that the validator
has fully checked the function. The point of having a validator is not to let
the call handler omit checks, but to notify the user immediately if there are
obvious errors in a `CREATE FUNCTION` command.) While the choice of exactly
what to check is mostly left to the discretion of the validator function, note
that the core `CREATE FUNCTION` code only executes `SET` clauses attached to a
function when `check_function_bodies` is on. Therefore, checks whose results
might be affected by GUC parameters definitely should be skipped when
`check_function_bodies` is off, to avoid false failures when restoring a dump.

If an inline handler is provided by a procedural language, it must be declared
as a function taking a single parameter of type `internal`. The inline
handler's result is ignored, so it is customarily declared to return `void`.
The inline handler will be called when a `DO` statement is executed specifying
the procedural language. The parameter actually passed is a pointer to an
`InlineCodeBlock` struct, which contains information about the `DO`
statement's parameters, in particular the text of the anonymous code block to
be executed. The inline handler should execute this code and return.

It's recommended that you wrap all these function declarations, as well as the
`CREATE LANGUAGE` command itself, into an _extension_ so that a simple `CREATE
EXTENSION` command is sufficient to install the language. See [Section
38.17](extend-extensions.html "38.17. Packaging Related Objects into an
Extension") for information about writing extensions.

The procedural languages included in the standard distribution are good
references when trying to write your own language handler. Look into the
`src/pl` subdirectory of the source tree. The [CREATE LANGUAGE](sql-
createlanguage.html "CREATE LANGUAGE") reference page also has some useful
details.

* * *

[Prev](nls-programmer.html "57.2. For the Programmer")  | [Up](internals.html "Part VII. Internals") |  [Next](fdwhandler.html "Chapter 59. Writing a Foreign Data Wrapper")  
---|---|---  
57.2. For the Programmer  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 59. Writing a Foreign Data Wrapper  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plhandler.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

