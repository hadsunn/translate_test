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

Supported Versions: [Current](/docs/current/libpq-build.html "PostgreSQL 17 -
34.21. Building libpq Programs") ([17](/docs/17/libpq-build.html "PostgreSQL
17 - 34.21. Building libpq Programs")) / [16](/docs/16/libpq-build.html
"PostgreSQL 16 - 34.21. Building libpq Programs") / [15](/docs/15/libpq-
build.html "PostgreSQL 15 - 34.21. Building libpq Programs") /
[14](/docs/14/libpq-build.html "PostgreSQL 14 - 34.21. Building libpq
Programs") / [13](/docs/13/libpq-build.html "PostgreSQL 13 - 34.21. Building
libpq Programs")

Development Versions: [18](/docs/18/libpq-build.html "PostgreSQL 18 -
34.21. Building libpq Programs") / [devel](/docs/devel/libpq-build.html
"PostgreSQL devel - 34.21. Building libpq Programs")

Unsupported versions: [12](/docs/12/libpq-build.html "PostgreSQL 12 -
34.21. Building libpq Programs") / [11](/docs/11/libpq-build.html "PostgreSQL
11 - 34.21. Building libpq Programs") / [10](/docs/10/libpq-build.html
"PostgreSQL 10 - 34.21. Building libpq Programs") / [9.6](/docs/9.6/libpq-
build.html "PostgreSQL 9.6 - 34.21. Building libpq Programs") /
[9.5](/docs/9.5/libpq-build.html "PostgreSQL 9.5 - 34.21. Building libpq
Programs") / [9.4](/docs/9.4/libpq-build.html "PostgreSQL 9.4 -
34.21. Building libpq Programs") / [9.3](/docs/9.3/libpq-build.html
"PostgreSQL 9.3 - 34.21. Building libpq Programs") / [9.2](/docs/9.2/libpq-
build.html "PostgreSQL 9.2 - 34.21. Building libpq Programs") /
[9.1](/docs/9.1/libpq-build.html "PostgreSQL 9.1 - 34.21. Building libpq
Programs") / [9.0](/docs/9.0/libpq-build.html "PostgreSQL 9.0 -
34.21. Building libpq Programs") / [8.4](/docs/8.4/libpq-build.html
"PostgreSQL 8.4 - 34.21. Building libpq Programs") / [8.3](/docs/8.3/libpq-
build.html "PostgreSQL 8.3 - 34.21. Building libpq Programs") /
[8.2](/docs/8.2/libpq-build.html "PostgreSQL 8.2 - 34.21. Building libpq
Programs") / [8.1](/docs/8.1/libpq-build.html "PostgreSQL 8.1 -
34.21. Building libpq Programs") / [8.0](/docs/8.0/libpq-build.html
"PostgreSQL 8.0 - 34.21. Building libpq Programs") / [7.4](/docs/7.4/libpq-
build.html "PostgreSQL 7.4 - 34.21. Building libpq Programs") /
[7.3](/docs/7.3/libpq-build.html "PostgreSQL 7.3 - 34.21. Building libpq
Programs") / [7.2](/docs/7.2/libpq-build.html "PostgreSQL 7.2 -
34.21. Building libpq Programs")

__

34.21. Building libpq Programs  
---  
[Prev](libpq-threading.html "34.20. Behavior in Threaded Programs")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-example.html "34.22. Example Programs")  
  
* * *

## 34.21. Building libpq Programs #

To build (i.e., compile and link) a program using libpq you need to do all of
the following things:

  * Include the `libpq-fe.h` header file:
        
        #include <libpq-fe.h>
        

If you failed to do that then you will normally get error messages from your
compiler similar to:

        
        foo.c: In function `main':
        foo.c:34: `PGconn' undeclared (first use in this function)
        foo.c:35: `PGresult' undeclared (first use in this function)
        foo.c:54: `CONNECTION_BAD' undeclared (first use in this function)
        foo.c:68: `PGRES_COMMAND_OK' undeclared (first use in this function)
        foo.c:95: `PGRES_TUPLES_OK' undeclared (first use in this function)
        

  * Point your compiler to the directory where the PostgreSQL header files were installed, by supplying the `-I _`directory`_` option to your compiler. (In some cases the compiler will look into the directory in question by default, so you can omit this option.) For instance, your compile command line could look like:
        
        cc -c -I/usr/local/pgsql/include testprog.c
        

If you are using makefiles then add the option to the `CPPFLAGS` variable:

        
        CPPFLAGS += -I/usr/local/pgsql/include
        

If there is any chance that your program might be compiled by other users then
you should not hardcode the directory location like that. Instead, you can run
the utility `pg_config` to find out where the header files are on the local
system:

        
        $ pg_config --includedir
        /usr/local/include
        

If you have `pkg-config` installed, you can run instead:

        
        $ pkg-config --cflags libpq
        -I/usr/local/include
        

Note that this will already include the `-I` in front of the path.

Failure to specify the correct option to the compiler will result in an error
message such as:

        
        testlibpq.c:8:22: libpq-fe.h: No such file or directory
        

  * When linking the final program, specify the option `-lpq` so that the libpq library gets pulled in, as well as the option `-L _`directory`_` to point the compiler to the directory where the libpq library resides. (Again, the compiler will search some directories by default.) For maximum portability, put the `-L` option before the `-lpq` option. For example:
        
        cc -o testprog testprog1.o testprog2.o -L/usr/local/pgsql/lib -lpq
        

You can find out the library directory using `pg_config` as well:

        
        $ pg_config --libdir
        /usr/local/pgsql/lib
        

Or again use `pkg-config`:

        
        $ pkg-config --libs libpq
        -L/usr/local/pgsql/lib -lpq
        

Note again that this prints the full options, not only the path.

Error messages that point to problems in this area could look like the
following:

        
        testlibpq.o: In function `main':
        testlibpq.o(.text+0x60): undefined reference to `PQsetdbLogin'
        testlibpq.o(.text+0x71): undefined reference to `PQstatus'
        testlibpq.o(.text+0xa4): undefined reference to `PQerrorMessage'
        

This means you forgot `-lpq`.

        
        /usr/bin/ld: cannot find -lpq
        

This means you forgot the `-L` option or did not specify the right directory.

* * *

[Prev](libpq-threading.html "34.20. Behavior in Threaded Programs")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](libpq-example.html "34.22. Example Programs")  
---|---|---  
34.20. Behavior in Threaded Programs  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.22. Example Programs  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-build.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

