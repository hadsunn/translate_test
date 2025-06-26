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

Supported Versions: [Current](/docs/current/app-ecpg.html "PostgreSQL 17 -
ecpg") ([17](/docs/17/app-ecpg.html "PostgreSQL 17 - ecpg")) /
[16](/docs/16/app-ecpg.html "PostgreSQL 16 - ecpg") / [15](/docs/15/app-
ecpg.html "PostgreSQL 15 - ecpg") / [14](/docs/14/app-ecpg.html "PostgreSQL 14
- ecpg") / [13](/docs/13/app-ecpg.html "PostgreSQL 13 - ecpg")

Development Versions: [18](/docs/18/app-ecpg.html "PostgreSQL 18 - ecpg") /
[devel](/docs/devel/app-ecpg.html "PostgreSQL devel - ecpg")

Unsupported versions: [12](/docs/12/app-ecpg.html "PostgreSQL 12 - ecpg") /
[11](/docs/11/app-ecpg.html "PostgreSQL 11 - ecpg") / [10](/docs/10/app-
ecpg.html "PostgreSQL 10 - ecpg") / [9.6](/docs/9.6/app-ecpg.html "PostgreSQL
9.6 - ecpg") / [9.5](/docs/9.5/app-ecpg.html "PostgreSQL 9.5 - ecpg") /
[9.4](/docs/9.4/app-ecpg.html "PostgreSQL 9.4 - ecpg") / [9.3](/docs/9.3/app-
ecpg.html "PostgreSQL 9.3 - ecpg") / [9.2](/docs/9.2/app-ecpg.html "PostgreSQL
9.2 - ecpg") / [9.1](/docs/9.1/app-ecpg.html "PostgreSQL 9.1 - ecpg") /
[9.0](/docs/9.0/app-ecpg.html "PostgreSQL 9.0 - ecpg") / [8.4](/docs/8.4/app-
ecpg.html "PostgreSQL 8.4 - ecpg") / [8.3](/docs/8.3/app-ecpg.html "PostgreSQL
8.3 - ecpg") / [8.2](/docs/8.2/app-ecpg.html "PostgreSQL 8.2 - ecpg") /
[8.1](/docs/8.1/app-ecpg.html "PostgreSQL 8.1 - ecpg") / [8.0](/docs/8.0/app-
ecpg.html "PostgreSQL 8.0 - ecpg") / [7.4](/docs/7.4/app-ecpg.html "PostgreSQL
7.4 - ecpg") / [7.3](/docs/7.3/app-ecpg.html "PostgreSQL 7.3 - ecpg") /
[7.2](/docs/7.2/app-ecpg.html "PostgreSQL 7.2 - ecpg") / [7.1](/docs/7.1/app-
ecpg.html "PostgreSQL 7.1 - ecpg")

__

ecpg  
---  
[Prev](app-dropuser.html "dropuser")  | [Up](reference-client.html "PostgreSQL Client Applications") | PostgreSQL Client Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](app-pgamcheck.html "pg_amcheck")  
  
* * *

## ecpg

ecpg — embedded SQL C preprocessor

## Synopsis

`ecpg` [_`option`_...] _`file`_...

## Description

`ecpg` is the embedded SQL preprocessor for C programs. It converts C programs
with embedded SQL statements to normal C code by replacing the SQL invocations
with special function calls. The output files can then be processed with any C
compiler tool chain.

`ecpg` will convert each input file given on the command line to the
corresponding C output file. If an input file name does not have any
extension, `.pgc` is assumed. The file's extension will be replaced by `.c` to
construct the output file name. But the output file name can be overridden
using the `-o` option.

If an input file name is just `-`, `ecpg` reads the program from standard
input (and writes to standard output, unless that is overridden with `-o`).

This reference page does not describe the embedded SQL language. See [Chapter
36](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") for more information on
that topic.

## Options

`ecpg` accepts the following command-line arguments:

`-c`

    

Automatically generate certain C code from SQL code. Currently, this works for
`EXEC SQL TYPE`.

`-C _`mode`_`

    

Set a compatibility mode. _`mode`_ can be `INFORMIX`, `INFORMIX_SE`, or
`ORACLE`.

`-D _`symbol`_[=_`value`_]`

    

Define a preprocessor symbol, equivalently to the `EXEC SQL DEFINE` directive.
If no _`value`_ is specified, the symbol is defined with the value `1`.

`-h`

    

Process header files. When this option is specified, the output file extension
becomes `.h` not `.c`, and the default input file extension is `.pgh` not
`.pgc`. Also, the `-c` option is forced on.

`-i`

    

Parse system include files as well.

`-I _`directory`_`

    

Specify an additional include path, used to find files included via `EXEC SQL
INCLUDE`. Defaults are `.` (current directory), `/usr/local/include`, the
PostgreSQL include directory which is defined at compile time (default:
`/usr/local/pgsql/include`), and `/usr/include`, in that order.

`-o _`filename`_`

    

Specifies that `ecpg` should write all its output to the given _`filename`_.
Write `-o -` to send all output to standard output.

`-r _`option`_`

    

Selects run-time behavior. _`Option`_ can be one of the following:

`no_indicator`

    

Do not use indicators but instead use special values to represent null values.
Historically there have been databases using this approach.

`prepare`

    

Prepare all statements before using them. Libecpg will keep a cache of
prepared statements and reuse a statement if it gets executed again. If the
cache runs full, libecpg will free the least used statement.

`questionmarks`

    

Allow question mark as placeholder for compatibility reasons. This used to be
the default long ago.

`-t`

    

Turn on autocommit of transactions. In this mode, each SQL command is
automatically committed unless it is inside an explicit transaction block. In
the default mode, commands are committed only when `EXEC SQL COMMIT` is
issued.

`-v`

    

Print additional information including the version and the "include" path.

`--version`

    

Print the ecpg version and exit.

`-?`  
`--help`

    

Show help about ecpg command line arguments, and exit.

## Notes

When compiling the preprocessed C code files, the compiler needs to be able to
find the ECPG header files in the PostgreSQL include directory. Therefore, you
might have to use the `-I` option when invoking the compiler (e.g.,
`-I/usr/local/pgsql/include`).

Programs using C code with embedded SQL have to be linked against the
`libecpg` library, for example using the linker options
`-L/usr/local/pgsql/lib -lecpg`.

The value of either of these directories that is appropriate for the
installation can be found out using [pg_config](app-pgconfig.html
"pg_config").

## Examples

If you have an embedded SQL C source file named `prog1.pgc`, you can create an
executable program using the following sequence of commands:

    
    
    ecpg prog1.pgc
    cc -I/usr/local/pgsql/include -c prog1.c
    cc -o prog1 prog1.o -L/usr/local/pgsql/lib -lecpg
    

* * *

[Prev](app-dropuser.html "dropuser")  | [Up](reference-client.html "PostgreSQL Client Applications") |  [Next](app-pgamcheck.html "pg_amcheck")  
---|---|---  
dropuser  | [Home](index.html "PostgreSQL 16.9 Documentation") |  pg_amcheck  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/app-ecpg.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

