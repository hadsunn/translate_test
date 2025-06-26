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

Supported Versions: [Current](/docs/current/sql-deallocate.html "PostgreSQL 17
- DEALLOCATE") ([17](/docs/17/sql-deallocate.html "PostgreSQL 17 -
DEALLOCATE")) / [16](/docs/16/sql-deallocate.html "PostgreSQL 16 -
DEALLOCATE") / [15](/docs/15/sql-deallocate.html "PostgreSQL 15 - DEALLOCATE")
/ [14](/docs/14/sql-deallocate.html "PostgreSQL 14 - DEALLOCATE") /
[13](/docs/13/sql-deallocate.html "PostgreSQL 13 - DEALLOCATE")

Development Versions: [18](/docs/18/sql-deallocate.html "PostgreSQL 18 -
DEALLOCATE") / [devel](/docs/devel/sql-deallocate.html "PostgreSQL devel -
DEALLOCATE")

Unsupported versions: [12](/docs/12/sql-deallocate.html "PostgreSQL 12 -
DEALLOCATE") / [11](/docs/11/sql-deallocate.html "PostgreSQL 11 - DEALLOCATE")
/ [10](/docs/10/sql-deallocate.html "PostgreSQL 10 - DEALLOCATE") /
[9.6](/docs/9.6/sql-deallocate.html "PostgreSQL 9.6 - DEALLOCATE") /
[9.5](/docs/9.5/sql-deallocate.html "PostgreSQL 9.5 - DEALLOCATE") /
[9.4](/docs/9.4/sql-deallocate.html "PostgreSQL 9.4 - DEALLOCATE") /
[9.3](/docs/9.3/sql-deallocate.html "PostgreSQL 9.3 - DEALLOCATE") /
[9.2](/docs/9.2/sql-deallocate.html "PostgreSQL 9.2 - DEALLOCATE") /
[9.1](/docs/9.1/sql-deallocate.html "PostgreSQL 9.1 - DEALLOCATE") /
[9.0](/docs/9.0/sql-deallocate.html "PostgreSQL 9.0 - DEALLOCATE") /
[8.4](/docs/8.4/sql-deallocate.html "PostgreSQL 8.4 - DEALLOCATE") /
[8.3](/docs/8.3/sql-deallocate.html "PostgreSQL 8.3 - DEALLOCATE") /
[8.2](/docs/8.2/sql-deallocate.html "PostgreSQL 8.2 - DEALLOCATE") /
[8.1](/docs/8.1/sql-deallocate.html "PostgreSQL 8.1 - DEALLOCATE") /
[8.0](/docs/8.0/sql-deallocate.html "PostgreSQL 8.0 - DEALLOCATE") /
[7.4](/docs/7.4/sql-deallocate.html "PostgreSQL 7.4 - DEALLOCATE") /
[7.3](/docs/7.3/sql-deallocate.html "PostgreSQL 7.3 - DEALLOCATE")

__

DEALLOCATE  
---  
[Prev](sql-createview.html "CREATE VIEW")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-declare.html "DECLARE")  
  
* * *

## DEALLOCATE

DEALLOCATE — deallocate a prepared statement

## Synopsis

    
    
    DEALLOCATE [ PREPARE ] { _name_ | ALL }
    

## Description

`DEALLOCATE` is used to deallocate a previously prepared SQL statement. If you
do not explicitly deallocate a prepared statement, it is deallocated when the
session ends.

For more information on prepared statements, see [PREPARE](sql-prepare.html
"PREPARE").

## Parameters

`PREPARE`

    

This key word is ignored.

_`name`_

    

The name of the prepared statement to deallocate.

`ALL`

    

Deallocate all prepared statements.

## Compatibility

The SQL standard includes a `DEALLOCATE` statement, but it is only for use in
embedded SQL.

## See Also

[EXECUTE](sql-execute.html "EXECUTE"), [PREPARE](sql-prepare.html "PREPARE")

* * *

[Prev](sql-createview.html "CREATE VIEW")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-declare.html "DECLARE")  
---|---|---  
CREATE VIEW  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DECLARE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-deallocate.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

