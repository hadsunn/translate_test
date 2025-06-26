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

Supported Versions: [Current](/docs/current/sql-execute.html "PostgreSQL 17 -
EXECUTE") ([17](/docs/17/sql-execute.html "PostgreSQL 17 - EXECUTE")) /
[16](/docs/16/sql-execute.html "PostgreSQL 16 - EXECUTE") / [15](/docs/15/sql-
execute.html "PostgreSQL 15 - EXECUTE") / [14](/docs/14/sql-execute.html
"PostgreSQL 14 - EXECUTE") / [13](/docs/13/sql-execute.html "PostgreSQL 13 -
EXECUTE")

Development Versions: [18](/docs/18/sql-execute.html "PostgreSQL 18 -
EXECUTE") / [devel](/docs/devel/sql-execute.html "PostgreSQL devel - EXECUTE")

Unsupported versions: [12](/docs/12/sql-execute.html "PostgreSQL 12 -
EXECUTE") / [11](/docs/11/sql-execute.html "PostgreSQL 11 - EXECUTE") /
[10](/docs/10/sql-execute.html "PostgreSQL 10 - EXECUTE") /
[9.6](/docs/9.6/sql-execute.html "PostgreSQL 9.6 - EXECUTE") /
[9.5](/docs/9.5/sql-execute.html "PostgreSQL 9.5 - EXECUTE") /
[9.4](/docs/9.4/sql-execute.html "PostgreSQL 9.4 - EXECUTE") /
[9.3](/docs/9.3/sql-execute.html "PostgreSQL 9.3 - EXECUTE") /
[9.2](/docs/9.2/sql-execute.html "PostgreSQL 9.2 - EXECUTE") /
[9.1](/docs/9.1/sql-execute.html "PostgreSQL 9.1 - EXECUTE") /
[9.0](/docs/9.0/sql-execute.html "PostgreSQL 9.0 - EXECUTE") /
[8.4](/docs/8.4/sql-execute.html "PostgreSQL 8.4 - EXECUTE") /
[8.3](/docs/8.3/sql-execute.html "PostgreSQL 8.3 - EXECUTE") /
[8.2](/docs/8.2/sql-execute.html "PostgreSQL 8.2 - EXECUTE") /
[8.1](/docs/8.1/sql-execute.html "PostgreSQL 8.1 - EXECUTE") /
[8.0](/docs/8.0/sql-execute.html "PostgreSQL 8.0 - EXECUTE") /
[7.4](/docs/7.4/sql-execute.html "PostgreSQL 7.4 - EXECUTE") /
[7.3](/docs/7.3/sql-execute.html "PostgreSQL 7.3 - EXECUTE")

__

EXECUTE  
---  
[Prev](sql-end.html "END")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-explain.html "EXPLAIN")  
  
* * *

## EXECUTE

EXECUTE — execute a prepared statement

## Synopsis

    
    
    EXECUTE _name_ [ ( _parameter_ [, ...] ) ]
    

## Description

`EXECUTE` is used to execute a previously prepared statement. Since prepared
statements only exist for the duration of a session, the prepared statement
must have been created by a `PREPARE` statement executed earlier in the
current session.

If the `PREPARE` statement that created the statement specified some
parameters, a compatible set of parameters must be passed to the `EXECUTE`
statement, or else an error is raised. Note that (unlike functions) prepared
statements are not overloaded based on the type or number of their parameters;
the name of a prepared statement must be unique within a database session.

For more information on the creation and usage of prepared statements, see
[PREPARE](sql-prepare.html "PREPARE").

## Parameters

_`name`_

    

The name of the prepared statement to execute.

_`parameter`_

    

The actual value of a parameter to the prepared statement. This must be an
expression yielding a value that is compatible with the data type of this
parameter, as was determined when the prepared statement was created.

## Outputs

The command tag returned by `EXECUTE` is that of the prepared statement, and
not `EXECUTE`.

## Examples

Examples are given in [Examples](sql-prepare.html#SQL-PREPARE-EXAMPLES
"Examples") in the [PREPARE](sql-prepare.html "PREPARE") documentation.

## Compatibility

The SQL standard includes an `EXECUTE` statement, but it is only for use in
embedded SQL. This version of the `EXECUTE` statement also uses a somewhat
different syntax.

## See Also

[DEALLOCATE](sql-deallocate.html "DEALLOCATE"), [PREPARE](sql-prepare.html
"PREPARE")

* * *

[Prev](sql-end.html "END")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-explain.html "EXPLAIN")  
---|---|---  
END  | [Home](index.html "PostgreSQL 16.9 Documentation") |  EXPLAIN  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-execute.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

