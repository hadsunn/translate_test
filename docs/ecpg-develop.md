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

Supported Versions: [Current](/docs/current/ecpg-develop.html "PostgreSQL 17 -
36.17. Internals") ([17](/docs/17/ecpg-develop.html "PostgreSQL 17 -
36.17. Internals")) / [16](/docs/16/ecpg-develop.html "PostgreSQL 16 -
36.17. Internals") / [15](/docs/15/ecpg-develop.html "PostgreSQL 15 -
36.17. Internals") / [14](/docs/14/ecpg-develop.html "PostgreSQL 14 -
36.17. Internals") / [13](/docs/13/ecpg-develop.html "PostgreSQL 13 -
36.17. Internals")

Development Versions: [18](/docs/18/ecpg-develop.html "PostgreSQL 18 -
36.17. Internals") / [devel](/docs/devel/ecpg-develop.html "PostgreSQL devel -
36.17. Internals")

Unsupported versions: [12](/docs/12/ecpg-develop.html "PostgreSQL 12 -
36.17. Internals") / [11](/docs/11/ecpg-develop.html "PostgreSQL 11 -
36.17. Internals") / [10](/docs/10/ecpg-develop.html "PostgreSQL 10 -
36.17. Internals") / [9.6](/docs/9.6/ecpg-develop.html "PostgreSQL 9.6 -
36.17. Internals") / [9.5](/docs/9.5/ecpg-develop.html "PostgreSQL 9.5 -
36.17. Internals") / [9.4](/docs/9.4/ecpg-develop.html "PostgreSQL 9.4 -
36.17. Internals") / [9.3](/docs/9.3/ecpg-develop.html "PostgreSQL 9.3 -
36.17. Internals") / [9.2](/docs/9.2/ecpg-develop.html "PostgreSQL 9.2 -
36.17. Internals") / [9.1](/docs/9.1/ecpg-develop.html "PostgreSQL 9.1 -
36.17. Internals") / [9.0](/docs/9.0/ecpg-develop.html "PostgreSQL 9.0 -
36.17. Internals") / [8.4](/docs/8.4/ecpg-develop.html "PostgreSQL 8.4 -
36.17. Internals") / [8.3](/docs/8.3/ecpg-develop.html "PostgreSQL 8.3 -
36.17. Internals") / [8.2](/docs/8.2/ecpg-develop.html "PostgreSQL 8.2 -
36.17. Internals") / [8.1](/docs/8.1/ecpg-develop.html "PostgreSQL 8.1 -
36.17. Internals") / [8.0](/docs/8.0/ecpg-develop.html "PostgreSQL 8.0 -
36.17. Internals") / [7.4](/docs/7.4/ecpg-develop.html "PostgreSQL 7.4 -
36.17. Internals") / [7.3](/docs/7.3/ecpg-develop.html "PostgreSQL 7.3 -
36.17. Internals") / [7.2](/docs/7.2/ecpg-develop.html "PostgreSQL 7.2 -
36.17. Internals") / [7.1](/docs/7.1/ecpg-develop.html "PostgreSQL 7.1 -
36.17. Internals")

__

36.17. Internals  
---  
[Prev](ecpg-oracle-compat.html "36.16. Oracle Compatibility Mode")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") | Chapter 36. ECPG — Embedded SQL in C | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](information-schema.html "Chapter 37. The Information Schema")  
  
* * *

## 36.17. Internals #

This section explains how ECPG works internally. This information can
occasionally be useful to help users understand how to use ECPG.

The first four lines written by `ecpg` to the output are fixed lines. Two are
comments and two are include lines necessary to interface to the library. Then
the preprocessor reads through the file and writes output. Normally it just
echoes everything to the output.

When it sees an `EXEC SQL` statement, it intervenes and changes it. The
command starts with `EXEC SQL` and ends with `;`. Everything in between is
treated as an SQL statement and parsed for variable substitution.

Variable substitution occurs when a symbol starts with a colon (`:`). The
variable with that name is looked up among the variables that were previously
declared within a `EXEC SQL DECLARE` section.

The most important function in the library is `ECPGdo`, which takes care of
executing most commands. It takes a variable number of arguments. This can
easily add up to 50 or so arguments, and we hope this will not be a problem on
any platform.

The arguments are:

A line number #

    

This is the line number of the original line; used in error messages only.

A string #

    

This is the SQL command that is to be issued. It is modified by the input
variables, i.e., the variables that where not known at compile time but are to
be entered in the command. Where the variables should go the string contains
`?`.

Input variables #

    

Every input variable causes ten arguments to be created. (See below.)

_`ECPGt_EOIT`_ #

    

An `enum` telling that there are no more input variables.

Output variables #

    

Every output variable causes ten arguments to be created. (See below.) These
variables are filled by the function.

_`ECPGt_EORT`_ #

    

An `enum` telling that there are no more variables.

For every variable that is part of the SQL command, the function gets ten
arguments:

  1. The type as a special symbol.

  2. A pointer to the value or a pointer to the pointer.

  3. The size of the variable if it is a `char` or `varchar`.

  4. The number of elements in the array (for array fetches).

  5. The offset to the next element in the array (for array fetches).

  6. The type of the indicator variable as a special symbol.

  7. A pointer to the indicator variable.

  8. 0

  9. The number of elements in the indicator array (for array fetches).

  10. The offset to the next element in the indicator array (for array fetches).

Note that not all SQL commands are treated in this way. For instance, an open
cursor statement like:

    
    
    EXEC SQL OPEN _cursor_ ;
    

is not copied to the output. Instead, the cursor's `DECLARE` command is used
at the position of the `OPEN` command because it indeed opens the cursor.

Here is a complete example describing the output of the preprocessor of a file
`foo.pgc` (details might change with each particular version of the
preprocessor):

    
    
    EXEC SQL BEGIN DECLARE SECTION;
    int index;
    int result;
    EXEC SQL END DECLARE SECTION;
    ...
    EXEC SQL SELECT res INTO :result FROM mytable WHERE index = :index;
    

is translated into:

    
    
    /* Processed by ecpg (2.6.0) */
    /* These two include files are added by the preprocessor */
    #include <ecpgtype.h>;
    #include <ecpglib.h>;
    
    /* exec sql begin declare section */
    
    #line 1 "foo.pgc"
    
     int index;
     int result;
    /* exec sql end declare section */
    ...
    ECPGdo(__LINE__, NULL, "SELECT res FROM mytable WHERE index = ?     ",
            ECPGt_int,&(index),1L,1L,sizeof(int),
            ECPGt_NO_INDICATOR, NULL , 0L, 0L, 0L, ECPGt_EOIT,
            ECPGt_int,&(result),1L,1L,sizeof(int),
            ECPGt_NO_INDICATOR, NULL , 0L, 0L, 0L, ECPGt_EORT);
    #line 147 "foo.pgc"
    
    

(The indentation here is added for readability and not something the
preprocessor does.)

* * *

[Prev](ecpg-oracle-compat.html "36.16. Oracle Compatibility Mode")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") |  [Next](information-schema.html "Chapter 37. The Information Schema")  
---|---|---  
36.16. Oracle Compatibility Mode  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 37. The Information Schema  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-develop.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

