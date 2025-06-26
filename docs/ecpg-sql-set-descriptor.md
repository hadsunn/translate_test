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

Supported Versions: [Current](/docs/current/ecpg-sql-set-descriptor.html
"PostgreSQL 17 - SET DESCRIPTOR") ([17](/docs/17/ecpg-sql-set-descriptor.html
"PostgreSQL 17 - SET DESCRIPTOR")) / [16](/docs/16/ecpg-sql-set-
descriptor.html "PostgreSQL 16 - SET DESCRIPTOR") / [15](/docs/15/ecpg-sql-
set-descriptor.html "PostgreSQL 15 - SET DESCRIPTOR") / [14](/docs/14/ecpg-
sql-set-descriptor.html "PostgreSQL 14 - SET DESCRIPTOR") /
[13](/docs/13/ecpg-sql-set-descriptor.html "PostgreSQL 13 - SET DESCRIPTOR")

Development Versions: [18](/docs/18/ecpg-sql-set-descriptor.html "PostgreSQL
18 - SET DESCRIPTOR") / [devel](/docs/devel/ecpg-sql-set-descriptor.html
"PostgreSQL devel - SET DESCRIPTOR")

Unsupported versions: [12](/docs/12/ecpg-sql-set-descriptor.html "PostgreSQL
12 - SET DESCRIPTOR") / [11](/docs/11/ecpg-sql-set-descriptor.html "PostgreSQL
11 - SET DESCRIPTOR") / [10](/docs/10/ecpg-sql-set-descriptor.html "PostgreSQL
10 - SET DESCRIPTOR") / [9.6](/docs/9.6/ecpg-sql-set-descriptor.html
"PostgreSQL 9.6 - SET DESCRIPTOR") / [9.5](/docs/9.5/ecpg-sql-set-
descriptor.html "PostgreSQL 9.5 - SET DESCRIPTOR") / [9.4](/docs/9.4/ecpg-sql-
set-descriptor.html "PostgreSQL 9.4 - SET DESCRIPTOR") / [9.3](/docs/9.3/ecpg-
sql-set-descriptor.html "PostgreSQL 9.3 - SET DESCRIPTOR") /
[9.2](/docs/9.2/ecpg-sql-set-descriptor.html "PostgreSQL 9.2 - SET
DESCRIPTOR") / [9.1](/docs/9.1/ecpg-sql-set-descriptor.html "PostgreSQL 9.1 -
SET DESCRIPTOR")

__

SET DESCRIPTOR  
---  
[Prev](ecpg-sql-set-connection.html "SET CONNECTION")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-type.html "TYPE")  
  
* * *

## SET DESCRIPTOR

SET DESCRIPTOR — set information in an SQL descriptor area

## Synopsis

    
    
    SET DESCRIPTOR _descriptor_name_ _descriptor_header_item_ = _value_ [, ... ]
    SET DESCRIPTOR _descriptor_name_ VALUE _number_ _descriptor_item_ = _value_ [, ...]
    

## Description

`SET DESCRIPTOR` populates an SQL descriptor area with values. The descriptor
area is then typically used to bind parameters in a prepared query execution.

This command has two forms: The first form applies to the descriptor “header”,
which is independent of a particular datum. The second form assigns values to
particular datums, identified by number.

## Parameters

_`descriptor_name`_ #

    

A descriptor name.

_`descriptor_header_item`_ #

    

A token identifying which header information item to set. Only `COUNT`, to set
the number of descriptor items, is currently supported.

_`number`_ #

    

The number of the descriptor item to set. The count starts at 1.

_`descriptor_item`_ #

    

A token identifying which item of information to set in the descriptor. See
[Section 36.7.1](ecpg-descriptors.html#ECPG-NAMED-DESCRIPTORS "36.7.1. Named
SQL Descriptor Areas") for a list of supported items.

_`value`_ #

    

A value to store into the descriptor item. This can be an SQL constant or a
host variable.

## Examples

    
    
    EXEC SQL SET DESCRIPTOR indesc COUNT = 1;
    EXEC SQL SET DESCRIPTOR indesc VALUE 1 DATA = 2;
    EXEC SQL SET DESCRIPTOR indesc VALUE 1 DATA = :val1;
    EXEC SQL SET DESCRIPTOR indesc VALUE 2 INDICATOR = :val1, DATA = 'some string';
    EXEC SQL SET DESCRIPTOR indesc VALUE 2 INDICATOR = :val2null, DATA = :val2;
    

## Compatibility

`SET DESCRIPTOR` is specified in the SQL standard.

## See Also

[ALLOCATE DESCRIPTOR](ecpg-sql-allocate-descriptor.html "ALLOCATE
DESCRIPTOR"), [GET DESCRIPTOR](ecpg-sql-get-descriptor.html "GET DESCRIPTOR")

* * *

[Prev](ecpg-sql-set-connection.html "SET CONNECTION")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-sql-type.html "TYPE")  
---|---|---  
SET CONNECTION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  TYPE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-set-descriptor.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

