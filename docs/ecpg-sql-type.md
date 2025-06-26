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

Supported Versions: [Current](/docs/current/ecpg-sql-type.html "PostgreSQL 17
- TYPE") ([17](/docs/17/ecpg-sql-type.html "PostgreSQL 17 - TYPE")) /
[16](/docs/16/ecpg-sql-type.html "PostgreSQL 16 - TYPE") / [15](/docs/15/ecpg-
sql-type.html "PostgreSQL 15 - TYPE") / [14](/docs/14/ecpg-sql-type.html
"PostgreSQL 14 - TYPE") / [13](/docs/13/ecpg-sql-type.html "PostgreSQL 13 -
TYPE")

Development Versions: [18](/docs/18/ecpg-sql-type.html "PostgreSQL 18 - TYPE")
/ [devel](/docs/devel/ecpg-sql-type.html "PostgreSQL devel - TYPE")

Unsupported versions: [12](/docs/12/ecpg-sql-type.html "PostgreSQL 12 - TYPE")
/ [11](/docs/11/ecpg-sql-type.html "PostgreSQL 11 - TYPE") /
[10](/docs/10/ecpg-sql-type.html "PostgreSQL 10 - TYPE") /
[9.6](/docs/9.6/ecpg-sql-type.html "PostgreSQL 9.6 - TYPE") /
[9.5](/docs/9.5/ecpg-sql-type.html "PostgreSQL 9.5 - TYPE") /
[9.4](/docs/9.4/ecpg-sql-type.html "PostgreSQL 9.4 - TYPE") /
[9.3](/docs/9.3/ecpg-sql-type.html "PostgreSQL 9.3 - TYPE") /
[9.2](/docs/9.2/ecpg-sql-type.html "PostgreSQL 9.2 - TYPE") /
[9.1](/docs/9.1/ecpg-sql-type.html "PostgreSQL 9.1 - TYPE")

__

TYPE  
---  
[Prev](ecpg-sql-set-descriptor.html "SET DESCRIPTOR")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-var.html "VAR")  
  
* * *

## TYPE

TYPE — define a new data type

## Synopsis

    
    
    TYPE _type_name_ IS _ctype_
    

## Description

The `TYPE` command defines a new C type. It is equivalent to putting a
`typedef` into a declare section.

This command is only recognized when `ecpg` is run with the `-c` option.

## Parameters

_`type_name`_ #

    

The name for the new type. It must be a valid C type name.

_`ctype`_ #

    

A C type specification.

## Examples

    
    
    EXEC SQL TYPE customer IS
        struct
        {
            varchar name[50];
            int     phone;
        };
    
    EXEC SQL TYPE cust_ind IS
        struct ind
        {
            short   name_ind;
            short   phone_ind;
        };
    
    EXEC SQL TYPE c IS char reference;
    EXEC SQL TYPE ind IS union { int integer; short smallint; };
    EXEC SQL TYPE intarray IS int[AMOUNT];
    EXEC SQL TYPE str IS varchar[BUFFERSIZ];
    EXEC SQL TYPE string IS char[11];
    

Here is an example program that uses `EXEC SQL TYPE`:

    
    
    EXEC SQL WHENEVER SQLERROR SQLPRINT;
    
    EXEC SQL TYPE tt IS
        struct
        {
            varchar v[256];
            int     i;
        };
    
    EXEC SQL TYPE tt_ind IS
        struct ind {
            short   v_ind;
            short   i_ind;
        };
    
    int
    main(void)
    {
    EXEC SQL BEGIN DECLARE SECTION;
        tt t;
        tt_ind t_ind;
    EXEC SQL END DECLARE SECTION;
    
        EXEC SQL CONNECT TO testdb AS con1;
        EXEC SQL SELECT pg_catalog.set_config('search_path', '', false); EXEC SQL COMMIT;
    
        EXEC SQL SELECT current_database(), 256 INTO :t:t_ind LIMIT 1;
    
        printf("t.v = %s\n", t.v.arr);
        printf("t.i = %d\n", t.i);
    
        printf("t_ind.v_ind = %d\n", t_ind.v_ind);
        printf("t_ind.i_ind = %d\n", t_ind.i_ind);
    
        EXEC SQL DISCONNECT con1;
    
        return 0;
    }
    

The output from this program looks like this:

    
    
    t.v = testdb
    t.i = 256
    t_ind.v_ind = 0
    t_ind.i_ind = 0
    

## Compatibility

The `TYPE` command is a PostgreSQL extension.

* * *

[Prev](ecpg-sql-set-descriptor.html "SET DESCRIPTOR")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-sql-var.html "VAR")  
---|---|---  
SET DESCRIPTOR  | [Home](index.html "PostgreSQL 16.9 Documentation") |  VAR  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-type.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

