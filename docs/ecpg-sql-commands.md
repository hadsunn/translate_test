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

Supported Versions: [Current](/docs/current/ecpg-sql-commands.html "PostgreSQL
17 - 36.14. Embedded SQL Commands") ([17](/docs/17/ecpg-sql-commands.html
"PostgreSQL 17 - 36.14. Embedded SQL Commands")) / [16](/docs/16/ecpg-sql-
commands.html "PostgreSQL 16 - 36.14. Embedded SQL Commands") /
[15](/docs/15/ecpg-sql-commands.html "PostgreSQL 15 - 36.14. Embedded SQL
Commands") / [14](/docs/14/ecpg-sql-commands.html "PostgreSQL 14 -
36.14. Embedded SQL Commands") / [13](/docs/13/ecpg-sql-commands.html
"PostgreSQL 13 - 36.14. Embedded SQL Commands")

Development Versions: [18](/docs/18/ecpg-sql-commands.html "PostgreSQL 18 -
36.14. Embedded SQL Commands") / [devel](/docs/devel/ecpg-sql-commands.html
"PostgreSQL devel - 36.14. Embedded SQL Commands")

Unsupported versions: [12](/docs/12/ecpg-sql-commands.html "PostgreSQL 12 -
36.14. Embedded SQL Commands") / [11](/docs/11/ecpg-sql-commands.html
"PostgreSQL 11 - 36.14. Embedded SQL Commands") / [10](/docs/10/ecpg-sql-
commands.html "PostgreSQL 10 - 36.14. Embedded SQL Commands") /
[9.6](/docs/9.6/ecpg-sql-commands.html "PostgreSQL 9.6 - 36.14. Embedded SQL
Commands") / [9.5](/docs/9.5/ecpg-sql-commands.html "PostgreSQL 9.5 -
36.14. Embedded SQL Commands") / [9.4](/docs/9.4/ecpg-sql-commands.html
"PostgreSQL 9.4 - 36.14. Embedded SQL Commands") / [9.3](/docs/9.3/ecpg-sql-
commands.html "PostgreSQL 9.3 - 36.14. Embedded SQL Commands") /
[9.2](/docs/9.2/ecpg-sql-commands.html "PostgreSQL 9.2 - 36.14. Embedded SQL
Commands") / [9.1](/docs/9.1/ecpg-sql-commands.html "PostgreSQL 9.1 -
36.14. Embedded SQL Commands")

__

36.14. Embedded SQL Commands  
---  
[Prev](ecpg-cpp.html "36.13. C++ Applications")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") | Chapter 36. ECPG — Embedded SQL in C | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-allocate-descriptor.html "ALLOCATE DESCRIPTOR")  
  
* * *

## 36.14. Embedded SQL Commands #

[ALLOCATE DESCRIPTOR](ecpg-sql-allocate-descriptor.html) — allocate an SQL
descriptor area

[CONNECT](ecpg-sql-connect.html) — establish a database connection

[DEALLOCATE DESCRIPTOR](ecpg-sql-deallocate-descriptor.html) — deallocate an
SQL descriptor area

[DECLARE](ecpg-sql-declare.html) — define a cursor

[DECLARE STATEMENT](ecpg-sql-declare-statement.html) — declare SQL statement
identifier

[DESCRIBE](ecpg-sql-describe.html) — obtain information about a prepared
statement or result set

[DISCONNECT](ecpg-sql-disconnect.html) — terminate a database connection

[EXECUTE IMMEDIATE](ecpg-sql-execute-immediate.html) — dynamically prepare and
execute a statement

[GET DESCRIPTOR](ecpg-sql-get-descriptor.html) — get information from an SQL
descriptor area

[OPEN](ecpg-sql-open.html) — open a dynamic cursor

[PREPARE](ecpg-sql-prepare.html) — prepare a statement for execution

[SET AUTOCOMMIT](ecpg-sql-set-autocommit.html) — set the autocommit behavior
of the current session

[SET CONNECTION](ecpg-sql-set-connection.html) — select a database connection

[SET DESCRIPTOR](ecpg-sql-set-descriptor.html) — set information in an SQL
descriptor area

[TYPE](ecpg-sql-type.html) — define a new data type

[VAR](ecpg-sql-var.html) — define a variable

[WHENEVER](ecpg-sql-whenever.html) — specify the action to be taken when an
SQL statement causes a specific class condition to be raised

This section describes all SQL commands that are specific to embedded SQL.
Also refer to the SQL commands listed in [SQL Commands](sql-commands.html "SQL
Commands"), which can also be used in embedded SQL, unless stated otherwise.

* * *

[Prev](ecpg-cpp.html "36.13. C++ Applications")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") |  [Next](ecpg-sql-allocate-descriptor.html "ALLOCATE DESCRIPTOR")  
---|---|---  
36.13. C++ Applications  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALLOCATE DESCRIPTOR  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-commands.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

