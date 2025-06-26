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

Supported Versions: [Current](/docs/current/ecpg-preproc.html "PostgreSQL 17 -
36.9. Preprocessor Directives") ([17](/docs/17/ecpg-preproc.html "PostgreSQL
17 - 36.9. Preprocessor Directives")) / [16](/docs/16/ecpg-preproc.html
"PostgreSQL 16 - 36.9. Preprocessor Directives") / [15](/docs/15/ecpg-
preproc.html "PostgreSQL 15 - 36.9. Preprocessor Directives") /
[14](/docs/14/ecpg-preproc.html "PostgreSQL 14 - 36.9. Preprocessor
Directives") / [13](/docs/13/ecpg-preproc.html "PostgreSQL 13 -
36.9. Preprocessor Directives")

Development Versions: [18](/docs/18/ecpg-preproc.html "PostgreSQL 18 -
36.9. Preprocessor Directives") / [devel](/docs/devel/ecpg-preproc.html
"PostgreSQL devel - 36.9. Preprocessor Directives")

Unsupported versions: [12](/docs/12/ecpg-preproc.html "PostgreSQL 12 -
36.9. Preprocessor Directives") / [11](/docs/11/ecpg-preproc.html "PostgreSQL
11 - 36.9. Preprocessor Directives") / [10](/docs/10/ecpg-preproc.html
"PostgreSQL 10 - 36.9. Preprocessor Directives") / [9.6](/docs/9.6/ecpg-
preproc.html "PostgreSQL 9.6 - 36.9. Preprocessor Directives") /
[9.5](/docs/9.5/ecpg-preproc.html "PostgreSQL 9.5 - 36.9. Preprocessor
Directives") / [9.4](/docs/9.4/ecpg-preproc.html "PostgreSQL 9.4 -
36.9. Preprocessor Directives") / [9.3](/docs/9.3/ecpg-preproc.html
"PostgreSQL 9.3 - 36.9. Preprocessor Directives") / [9.2](/docs/9.2/ecpg-
preproc.html "PostgreSQL 9.2 - 36.9. Preprocessor Directives") /
[9.1](/docs/9.1/ecpg-preproc.html "PostgreSQL 9.1 - 36.9. Preprocessor
Directives") / [9.0](/docs/9.0/ecpg-preproc.html "PostgreSQL 9.0 -
36.9. Preprocessor Directives") / [8.4](/docs/8.4/ecpg-preproc.html
"PostgreSQL 8.4 - 36.9. Preprocessor Directives") / [8.3](/docs/8.3/ecpg-
preproc.html "PostgreSQL 8.3 - 36.9. Preprocessor Directives") /
[8.2](/docs/8.2/ecpg-preproc.html "PostgreSQL 8.2 - 36.9. Preprocessor
Directives")

__

36.9. Preprocessor Directives  
---  
[Prev](ecpg-errors.html "36.8. Error Handling")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") | Chapter 36. ECPG — Embedded SQL in C | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-process.html "36.10. Processing Embedded SQL Programs")  
  
* * *

## 36.9. Preprocessor Directives #

[36.9.1. Including Files](ecpg-preproc.html#ECPG-INCLUDE)

[36.9.2. The define and undef Directives](ecpg-preproc.html#ECPG-DEFINE)

[36.9.3. ifdef, ifndef, elif, else, and endif Directives](ecpg-
preproc.html#ECPG-IFDEF)

Several preprocessor directives are available that modify how the `ecpg`
preprocessor parses and processes a file.

### 36.9.1. Including Files #

To include an external file into your embedded SQL program, use:

    
    
    EXEC SQL INCLUDE _filename_ ;
    EXEC SQL INCLUDE <_filename_ >;
    EXEC SQL INCLUDE "_filename_ ";
    

The embedded SQL preprocessor will look for a file named `_`filename`_.h`,
preprocess it, and include it in the resulting C output. Thus, embedded SQL
statements in the included file are handled correctly.

The `ecpg` preprocessor will search a file at several directories in following
order:

  * current directory
  * `/usr/local/include`
  * PostgreSQL include directory, defined at build time (e.g., `/usr/local/pgsql/include`)
  * `/usr/include`

But when `EXEC SQL INCLUDE "_`filename`_ "` is used, only the current
directory is searched.

In each directory, the preprocessor will first look for the file name as
given, and if not found will append `.h` to the file name and try again
(unless the specified file name already has that suffix).

Note that `EXEC SQL INCLUDE` is _not_ the same as:

    
    
    #include <_filename_.h>
    

because this file would not be subject to SQL command preprocessing.
Naturally, you can continue to use the C `#include` directive to include other
header files.

### Note

The include file name is case-sensitive, even though the rest of the `EXEC SQL
INCLUDE` command follows the normal SQL case-sensitivity rules.

### 36.9.2. The define and undef Directives #

Similar to the directive `#define` that is known from C, embedded SQL has a
similar concept:

    
    
    EXEC SQL DEFINE _name_ ;
    EXEC SQL DEFINE _name_ _value_ ;
    

So you can define a name:

    
    
    EXEC SQL DEFINE HAVE_FEATURE;
    

And you can also define constants:

    
    
    EXEC SQL DEFINE MYNUMBER 12;
    EXEC SQL DEFINE MYSTRING 'abc';
    

Use `undef` to remove a previous definition:

    
    
    EXEC SQL UNDEF MYNUMBER;
    

Of course you can continue to use the C versions `#define` and `#undef` in
your embedded SQL program. The difference is where your defined values get
evaluated. If you use `EXEC SQL DEFINE` then the `ecpg` preprocessor evaluates
the defines and substitutes the values. For example if you write:

    
    
    EXEC SQL DEFINE MYNUMBER 12;
    ...
    EXEC SQL UPDATE Tbl SET col = MYNUMBER;
    

then `ecpg` will already do the substitution and your C compiler will never
see any name or identifier `MYNUMBER`. Note that you cannot use `#define` for
a constant that you are going to use in an embedded SQL query because in this
case the embedded SQL precompiler is not able to see this declaration.

If multiple input files are named on the `ecpg` preprocessor's command line,
the effects of `EXEC SQL DEFINE` and `EXEC SQL UNDEF` do not carry across
files: each file starts with only the symbols defined by `-D` switches on the
command line.

### 36.9.3. ifdef, ifndef, elif, else, and endif Directives #

You can use the following directives to compile code sections conditionally:

`EXEC SQL ifdef _`name`_ ;` #

    

Checks a _`name`_ and processes subsequent lines if _`name`_ has been defined
via `EXEC SQL define _`name`_`.

`EXEC SQL ifndef _`name`_ ;` #

    

Checks a _`name`_ and processes subsequent lines if _`name`_ has _not_ been
defined via `EXEC SQL define _`name`_`.

`EXEC SQL elif _`name`_ ;` #

    

Begins an optional alternative section after an `EXEC SQL ifdef _`name`_` or
`EXEC SQL ifndef _`name`_` directive. Any number of `elif` sections can
appear. Lines following an `elif` will be processed if _`name`_ has been
defined _and_ no previous section of the same `ifdef`/`ifndef`...`endif`
construct has been processed.

`EXEC SQL else;` #

    

Begins an optional, final alternative section after an `EXEC SQL ifdef
_`name`_` or `EXEC SQL ifndef _`name`_` directive. Subsequent lines will be
processed if no previous section of the same `ifdef`/`ifndef`...`endif`
construct has been processed.

`EXEC SQL endif;` #

    

Ends an `ifdef`/`ifndef`...`endif` construct. Subsequent lines are processed
normally.

`ifdef`/`ifndef`...`endif` constructs can be nested, up to 127 levels deep.

This example will compile exactly one of the three `SET TIMEZONE` commands:

    
    
    EXEC SQL ifdef TZVAR;
    EXEC SQL SET TIMEZONE TO TZVAR;
    EXEC SQL elif TZNAME;
    EXEC SQL SET TIMEZONE TO TZNAME;
    EXEC SQL else;
    EXEC SQL SET TIMEZONE TO 'GMT';
    EXEC SQL endif;
    

* * *

[Prev](ecpg-errors.html "36.8. Error Handling")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") |  [Next](ecpg-process.html "36.10. Processing Embedded SQL Programs")  
---|---|---  
36.8. Error Handling  | [Home](index.html "PostgreSQL 16.9 Documentation") |  36.10. Processing Embedded SQL Programs  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-preproc.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

