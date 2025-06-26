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

Supported Versions: [Current](/docs/current/ecpg-process.html "PostgreSQL 17 -
36.10. Processing Embedded SQL Programs") ([17](/docs/17/ecpg-process.html
"PostgreSQL 17 - 36.10. Processing Embedded SQL Programs")) /
[16](/docs/16/ecpg-process.html "PostgreSQL 16 - 36.10. Processing Embedded
SQL Programs") / [15](/docs/15/ecpg-process.html "PostgreSQL 15 -
36.10. Processing Embedded SQL Programs") / [14](/docs/14/ecpg-process.html
"PostgreSQL 14 - 36.10. Processing Embedded SQL Programs") /
[13](/docs/13/ecpg-process.html "PostgreSQL 13 - 36.10. Processing Embedded
SQL Programs")

Development Versions: [18](/docs/18/ecpg-process.html "PostgreSQL 18 -
36.10. Processing Embedded SQL Programs") / [devel](/docs/devel/ecpg-
process.html "PostgreSQL devel - 36.10. Processing Embedded SQL Programs")

Unsupported versions: [12](/docs/12/ecpg-process.html "PostgreSQL 12 -
36.10. Processing Embedded SQL Programs") / [11](/docs/11/ecpg-process.html
"PostgreSQL 11 - 36.10. Processing Embedded SQL Programs") /
[10](/docs/10/ecpg-process.html "PostgreSQL 10 - 36.10. Processing Embedded
SQL Programs") / [9.6](/docs/9.6/ecpg-process.html "PostgreSQL 9.6 -
36.10. Processing Embedded SQL Programs") / [9.5](/docs/9.5/ecpg-process.html
"PostgreSQL 9.5 - 36.10. Processing Embedded SQL Programs") /
[9.4](/docs/9.4/ecpg-process.html "PostgreSQL 9.4 - 36.10. Processing Embedded
SQL Programs") / [9.3](/docs/9.3/ecpg-process.html "PostgreSQL 9.3 -
36.10. Processing Embedded SQL Programs") / [9.2](/docs/9.2/ecpg-process.html
"PostgreSQL 9.2 - 36.10. Processing Embedded SQL Programs") /
[9.1](/docs/9.1/ecpg-process.html "PostgreSQL 9.1 - 36.10. Processing Embedded
SQL Programs") / [9.0](/docs/9.0/ecpg-process.html "PostgreSQL 9.0 -
36.10. Processing Embedded SQL Programs") / [8.4](/docs/8.4/ecpg-process.html
"PostgreSQL 8.4 - 36.10. Processing Embedded SQL Programs") /
[8.3](/docs/8.3/ecpg-process.html "PostgreSQL 8.3 - 36.10. Processing Embedded
SQL Programs") / [8.2](/docs/8.2/ecpg-process.html "PostgreSQL 8.2 -
36.10. Processing Embedded SQL Programs") / [8.1](/docs/8.1/ecpg-process.html
"PostgreSQL 8.1 - 36.10. Processing Embedded SQL Programs") /
[8.0](/docs/8.0/ecpg-process.html "PostgreSQL 8.0 - 36.10. Processing Embedded
SQL Programs") / [7.4](/docs/7.4/ecpg-process.html "PostgreSQL 7.4 -
36.10. Processing Embedded SQL Programs") / [7.3](/docs/7.3/ecpg-process.html
"PostgreSQL 7.3 - 36.10. Processing Embedded SQL Programs")

__

36.10. Processing Embedded SQL Programs  
---  
[Prev](ecpg-preproc.html "36.9. Preprocessor Directives")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") | Chapter 36. ECPG — Embedded SQL in C | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-library.html "36.11. Library Functions")  
  
* * *

## 36.10. Processing Embedded SQL Programs #

Now that you have an idea how to form embedded SQL C programs, you probably
want to know how to compile them. Before compiling you run the file through
the embedded SQL C preprocessor, which converts the SQL statements you used to
special function calls. After compiling, you must link with a special library
that contains the needed functions. These functions fetch information from the
arguments, perform the SQL command using the libpq interface, and put the
result in the arguments specified for output.

The preprocessor program is called `ecpg` and is included in a normal
PostgreSQL installation. Embedded SQL programs are typically named with an
extension `.pgc`. If you have a program file called `prog1.pgc`, you can
preprocess it by simply calling:

    
    
    ecpg prog1.pgc
    

This will create a file called `prog1.c`. If your input files do not follow
the suggested naming pattern, you can specify the output file explicitly using
the `-o` option.

The preprocessed file can be compiled normally, for example:

    
    
    cc -c prog1.c
    

The generated C source files include header files from the PostgreSQL
installation, so if you installed PostgreSQL in a location that is not
searched by default, you have to add an option such as
`-I/usr/local/pgsql/include` to the compilation command line.

To link an embedded SQL program, you need to include the `libecpg` library,
like so:

    
    
    cc -o myprog prog1.o prog2.o ... -lecpg
    

Again, you might have to add an option like `-L/usr/local/pgsql/lib` to that
command line.

You can use `pg_config` or `pkg-config` with package name `libecpg` to get the
paths for your installation.

If you manage the build process of a larger project using make, it might be
convenient to include the following implicit rule to your makefiles:

    
    
    ECPG = ecpg
    
    %.c: %.pgc
            $(ECPG) $<
    

The complete syntax of the `ecpg` command is detailed in [ecpg](app-ecpg.html
"ecpg").

The ecpg library is thread-safe by default. However, you might need to use
some threading command-line options to compile your client code.

* * *

[Prev](ecpg-preproc.html "36.9. Preprocessor Directives")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") |  [Next](ecpg-library.html "36.11. Library Functions")  
---|---|---  
36.9. Preprocessor Directives  | [Home](index.html "PostgreSQL 16.9 Documentation") |  36.11. Library Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-process.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

