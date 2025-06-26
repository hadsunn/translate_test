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

Supported Versions: [Current](/docs/current/ecpg-sql-describe.html "PostgreSQL
17 - DESCRIBE") ([17](/docs/17/ecpg-sql-describe.html "PostgreSQL 17 -
DESCRIBE")) / [16](/docs/16/ecpg-sql-describe.html "PostgreSQL 16 - DESCRIBE")
/ [15](/docs/15/ecpg-sql-describe.html "PostgreSQL 15 - DESCRIBE") /
[14](/docs/14/ecpg-sql-describe.html "PostgreSQL 14 - DESCRIBE") /
[13](/docs/13/ecpg-sql-describe.html "PostgreSQL 13 - DESCRIBE")

Development Versions: [18](/docs/18/ecpg-sql-describe.html "PostgreSQL 18 -
DESCRIBE") / [devel](/docs/devel/ecpg-sql-describe.html "PostgreSQL devel -
DESCRIBE")

Unsupported versions: [12](/docs/12/ecpg-sql-describe.html "PostgreSQL 12 -
DESCRIBE") / [11](/docs/11/ecpg-sql-describe.html "PostgreSQL 11 - DESCRIBE")
/ [10](/docs/10/ecpg-sql-describe.html "PostgreSQL 10 - DESCRIBE") /
[9.6](/docs/9.6/ecpg-sql-describe.html "PostgreSQL 9.6 - DESCRIBE") /
[9.5](/docs/9.5/ecpg-sql-describe.html "PostgreSQL 9.5 - DESCRIBE") /
[9.4](/docs/9.4/ecpg-sql-describe.html "PostgreSQL 9.4 - DESCRIBE") /
[9.3](/docs/9.3/ecpg-sql-describe.html "PostgreSQL 9.3 - DESCRIBE") /
[9.2](/docs/9.2/ecpg-sql-describe.html "PostgreSQL 9.2 - DESCRIBE") /
[9.1](/docs/9.1/ecpg-sql-describe.html "PostgreSQL 9.1 - DESCRIBE")

__

DESCRIBE  
---  
[Prev](ecpg-sql-declare-statement.html "DECLARE STATEMENT")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-disconnect.html "DISCONNECT")  
  
* * *

## DESCRIBE

DESCRIBE — obtain information about a prepared statement or result set

## Synopsis

    
    
    DESCRIBE [ OUTPUT ] _prepared_name_ USING [ SQL ] DESCRIPTOR _descriptor_name_
    DESCRIBE [ OUTPUT ] _prepared_name_ INTO [ SQL ] DESCRIPTOR _descriptor_name_
    DESCRIBE [ OUTPUT ] _prepared_name_ INTO _sqlda_name_
    

## Description

`DESCRIBE` retrieves metadata information about the result columns contained
in a prepared statement, without actually fetching a row.

## Parameters

_`prepared_name`_ #

    

The name of a prepared statement. This can be an SQL identifier or a host
variable.

_`descriptor_name`_ #

    

A descriptor name. It is case sensitive. It can be an SQL identifier or a host
variable.

_`sqlda_name`_ #

    

The name of an SQLDA variable.

## Examples

    
    
    EXEC SQL ALLOCATE DESCRIPTOR mydesc;
    EXEC SQL PREPARE stmt1 FROM :sql_stmt;
    EXEC SQL DESCRIBE stmt1 INTO SQL DESCRIPTOR mydesc;
    EXEC SQL GET DESCRIPTOR mydesc VALUE 1 :charvar = NAME;
    EXEC SQL DEALLOCATE DESCRIPTOR mydesc;
    

## Compatibility

`DESCRIBE` is specified in the SQL standard.

## See Also

[ALLOCATE DESCRIPTOR](ecpg-sql-allocate-descriptor.html "ALLOCATE
DESCRIPTOR"), [GET DESCRIPTOR](ecpg-sql-get-descriptor.html "GET DESCRIPTOR")

* * *

[Prev](ecpg-sql-declare-statement.html "DECLARE STATEMENT")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-sql-disconnect.html "DISCONNECT")  
---|---|---  
DECLARE STATEMENT  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DISCONNECT  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-describe.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

