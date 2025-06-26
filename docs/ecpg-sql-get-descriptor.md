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

Supported Versions: [Current](/docs/current/ecpg-sql-get-descriptor.html
"PostgreSQL 17 - GET DESCRIPTOR") ([17](/docs/17/ecpg-sql-get-descriptor.html
"PostgreSQL 17 - GET DESCRIPTOR")) / [16](/docs/16/ecpg-sql-get-
descriptor.html "PostgreSQL 16 - GET DESCRIPTOR") / [15](/docs/15/ecpg-sql-
get-descriptor.html "PostgreSQL 15 - GET DESCRIPTOR") / [14](/docs/14/ecpg-
sql-get-descriptor.html "PostgreSQL 14 - GET DESCRIPTOR") /
[13](/docs/13/ecpg-sql-get-descriptor.html "PostgreSQL 13 - GET DESCRIPTOR")

Development Versions: [18](/docs/18/ecpg-sql-get-descriptor.html "PostgreSQL
18 - GET DESCRIPTOR") / [devel](/docs/devel/ecpg-sql-get-descriptor.html
"PostgreSQL devel - GET DESCRIPTOR")

Unsupported versions: [12](/docs/12/ecpg-sql-get-descriptor.html "PostgreSQL
12 - GET DESCRIPTOR") / [11](/docs/11/ecpg-sql-get-descriptor.html "PostgreSQL
11 - GET DESCRIPTOR") / [10](/docs/10/ecpg-sql-get-descriptor.html "PostgreSQL
10 - GET DESCRIPTOR") / [9.6](/docs/9.6/ecpg-sql-get-descriptor.html
"PostgreSQL 9.6 - GET DESCRIPTOR") / [9.5](/docs/9.5/ecpg-sql-get-
descriptor.html "PostgreSQL 9.5 - GET DESCRIPTOR") / [9.4](/docs/9.4/ecpg-sql-
get-descriptor.html "PostgreSQL 9.4 - GET DESCRIPTOR") / [9.3](/docs/9.3/ecpg-
sql-get-descriptor.html "PostgreSQL 9.3 - GET DESCRIPTOR") /
[9.2](/docs/9.2/ecpg-sql-get-descriptor.html "PostgreSQL 9.2 - GET
DESCRIPTOR") / [9.1](/docs/9.1/ecpg-sql-get-descriptor.html "PostgreSQL 9.1 -
GET DESCRIPTOR")

__

GET DESCRIPTOR  
---  
[Prev](ecpg-sql-execute-immediate.html "EXECUTE IMMEDIATE")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-open.html "OPEN")  
  
* * *

## GET DESCRIPTOR

GET DESCRIPTOR — get information from an SQL descriptor area

## Synopsis

    
    
    GET DESCRIPTOR _descriptor_name_ _:cvariable_ = _descriptor_header_item_ [, ... ]
    GET DESCRIPTOR _descriptor_name_ VALUE _column_number_ _:cvariable_ = _descriptor_item_ [, ... ]
    

## Description

`GET DESCRIPTOR` retrieves information about a query result set from an SQL
descriptor area and stores it into host variables. A descriptor area is
typically populated using `FETCH` or `SELECT` before using this command to
transfer the information into host language variables.

This command has two forms: The first form retrieves descriptor “header”
items, which apply to the result set in its entirety. One example is the row
count. The second form, which requires the column number as additional
parameter, retrieves information about a particular column. Examples are the
column name and the actual column value.

## Parameters

_`descriptor_name`_ #

    

A descriptor name.

_`descriptor_header_item`_ #

    

A token identifying which header information item to retrieve. Only `COUNT`,
to get the number of columns in the result set, is currently supported.

_`column_number`_ #

    

The number of the column about which information is to be retrieved. The count
starts at 1.

_`descriptor_item`_ #

    

A token identifying which item of information about a column to retrieve. See
[Section 36.7.1](ecpg-descriptors.html#ECPG-NAMED-DESCRIPTORS "36.7.1. Named
SQL Descriptor Areas") for a list of supported items.

_`cvariable`_ #

    

A host variable that will receive the data retrieved from the descriptor area.

## Examples

An example to retrieve the number of columns in a result set:

    
    
    EXEC SQL GET DESCRIPTOR d :d_count = COUNT;
    

An example to retrieve a data length in the first column:

    
    
    EXEC SQL GET DESCRIPTOR d VALUE 1 :d_returned_octet_length = RETURNED_OCTET_LENGTH;
    

An example to retrieve the data body of the second column as a string:

    
    
    EXEC SQL GET DESCRIPTOR d VALUE 2 :d_data = DATA;
    

Here is an example for a whole procedure of executing `SELECT
current_database();` and showing the number of columns, the column data
length, and the column data:

    
    
    int
    main(void)
    {
    EXEC SQL BEGIN DECLARE SECTION;
        int  d_count;
        char d_data[1024];
        int  d_returned_octet_length;
    EXEC SQL END DECLARE SECTION;
    
        EXEC SQL CONNECT TO testdb AS con1 USER testuser;
        EXEC SQL SELECT pg_catalog.set_config('search_path', '', false); EXEC SQL COMMIT;
        EXEC SQL ALLOCATE DESCRIPTOR d;
    
        /* Declare, open a cursor, and assign a descriptor to the cursor  */
        EXEC SQL DECLARE cur CURSOR FOR SELECT current_database();
        EXEC SQL OPEN cur;
        EXEC SQL FETCH NEXT FROM cur INTO SQL DESCRIPTOR d;
    
        /* Get a number of total columns */
        EXEC SQL GET DESCRIPTOR d :d_count = COUNT;
        printf("d_count                 = %d\n", d_count);
    
        /* Get length of a returned column */
        EXEC SQL GET DESCRIPTOR d VALUE 1 :d_returned_octet_length = RETURNED_OCTET_LENGTH;
        printf("d_returned_octet_length = %d\n", d_returned_octet_length);
    
        /* Fetch the returned column as a string */
        EXEC SQL GET DESCRIPTOR d VALUE 1 :d_data = DATA;
        printf("d_data                  = %s\n", d_data);
    
        /* Closing */
        EXEC SQL CLOSE cur;
        EXEC SQL COMMIT;
    
        EXEC SQL DEALLOCATE DESCRIPTOR d;
        EXEC SQL DISCONNECT ALL;
    
        return 0;
    }
    

When the example is executed, the result will look like this:

    
    
    d_count                 = 1
    d_returned_octet_length = 6
    d_data                  = testdb
    

## Compatibility

`GET DESCRIPTOR` is specified in the SQL standard.

## See Also

[ALLOCATE DESCRIPTOR](ecpg-sql-allocate-descriptor.html "ALLOCATE
DESCRIPTOR"), [SET DESCRIPTOR](ecpg-sql-set-descriptor.html "SET DESCRIPTOR")

* * *

[Prev](ecpg-sql-execute-immediate.html "EXECUTE IMMEDIATE")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-sql-open.html "OPEN")  
---|---|---  
EXECUTE IMMEDIATE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  OPEN  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-get-descriptor.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

