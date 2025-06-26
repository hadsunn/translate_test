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

Supported Versions: [Current](/docs/current/xproc.html "PostgreSQL 17 -
38.4. User-Defined Procedures") ([17](/docs/17/xproc.html "PostgreSQL 17 -
38.4. User-Defined Procedures")) / [16](/docs/16/xproc.html "PostgreSQL 16 -
38.4. User-Defined Procedures") / [15](/docs/15/xproc.html "PostgreSQL 15 -
38.4. User-Defined Procedures") / [14](/docs/14/xproc.html "PostgreSQL 14 -
38.4. User-Defined Procedures") / [13](/docs/13/xproc.html "PostgreSQL 13 -
38.4. User-Defined Procedures")

Development Versions: [18](/docs/18/xproc.html "PostgreSQL 18 - 38.4. User-
Defined Procedures") / [devel](/docs/devel/xproc.html "PostgreSQL devel -
38.4. User-Defined Procedures")

Unsupported versions: [12](/docs/12/xproc.html "PostgreSQL 12 - 38.4. User-
Defined Procedures") / [11](/docs/11/xproc.html "PostgreSQL 11 - 38.4. User-
Defined Procedures")

__

38.4. User-Defined Procedures  
---  
[Prev](xfunc.html "38.3. User-Defined Functions")  | [Up](extend.html "Chapter 38. Extending SQL") | Chapter 38. Extending SQL | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](xfunc-sql.html "38.5. Query Language \(SQL\) Functions")  
  
* * *

## 38.4. User-Defined Procedures #

A procedure is a database object similar to a function. The key differences
are:

  * Procedures are defined with the [`CREATE PROCEDURE`](sql-createprocedure.html "CREATE PROCEDURE") command, not `CREATE FUNCTION`.

  * Procedures do not return a function value; hence `CREATE PROCEDURE` lacks a `RETURNS` clause. However, procedures can instead return data to their callers via output parameters.

  * While a function is called as part of a query or DML command, a procedure is called in isolation using the [`CALL`](sql-call.html "CALL") command.

  * A procedure can commit or roll back transactions during its execution (then automatically beginning a new transaction), so long as the invoking `CALL` command is not part of an explicit transaction block. A function cannot do that.

  * Certain function attributes, such as strictness, don't apply to procedures. Those attributes control how the function is used in a query, which isn't relevant to procedures.

The explanations in the following sections about how to define user-defined
functions apply to procedures as well, except for the points made above.

Collectively, functions and procedures are also known as _routines_. There are
commands such as [`ALTER ROUTINE`](sql-alterroutine.html "ALTER ROUTINE") and
[`DROP ROUTINE`](sql-droproutine.html "DROP ROUTINE") that can operate on
functions and procedures without having to know which kind it is. Note,
however, that there is no `CREATE ROUTINE` command.

* * *

[Prev](xfunc.html "38.3. User-Defined Functions")  | [Up](extend.html "Chapter 38. Extending SQL") |  [Next](xfunc-sql.html "38.5. Query Language \(SQL\) Functions")  
---|---|---  
38.3. User-Defined Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  38.5. Query Language (SQL) Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/xproc.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

