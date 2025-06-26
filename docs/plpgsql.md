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

Supported Versions: [Current](/docs/current/plpgsql.html "PostgreSQL 17 -
Chapter 43. PL/pgSQL — SQL Procedural Language") ([17](/docs/17/plpgsql.html
"PostgreSQL 17 - Chapter 43. PL/pgSQL — SQL Procedural Language")) /
[16](/docs/16/plpgsql.html "PostgreSQL 16 - Chapter 43. PL/pgSQL — SQL
Procedural Language") / [15](/docs/15/plpgsql.html "PostgreSQL 15 -
Chapter 43. PL/pgSQL — SQL Procedural Language") / [14](/docs/14/plpgsql.html
"PostgreSQL 14 - Chapter 43. PL/pgSQL — SQL Procedural Language") /
[13](/docs/13/plpgsql.html "PostgreSQL 13 - Chapter 43. PL/pgSQL — SQL
Procedural Language")

Development Versions: [18](/docs/18/plpgsql.html "PostgreSQL 18 -
Chapter 43. PL/pgSQL — SQL Procedural Language") /
[devel](/docs/devel/plpgsql.html "PostgreSQL devel - Chapter 43. PL/pgSQL —
SQL Procedural Language")

Unsupported versions: [12](/docs/12/plpgsql.html "PostgreSQL 12 -
Chapter 43. PL/pgSQL — SQL Procedural Language") / [11](/docs/11/plpgsql.html
"PostgreSQL 11 - Chapter 43. PL/pgSQL — SQL Procedural Language") /
[10](/docs/10/plpgsql.html "PostgreSQL 10 - Chapter 43. PL/pgSQL — SQL
Procedural Language") / [9.6](/docs/9.6/plpgsql.html "PostgreSQL 9.6 -
Chapter 43. PL/pgSQL — SQL Procedural Language") /
[9.5](/docs/9.5/plpgsql.html "PostgreSQL 9.5 - Chapter 43. PL/pgSQL — SQL
Procedural Language") / [9.4](/docs/9.4/plpgsql.html "PostgreSQL 9.4 -
Chapter 43. PL/pgSQL — SQL Procedural Language") /
[9.3](/docs/9.3/plpgsql.html "PostgreSQL 9.3 - Chapter 43. PL/pgSQL — SQL
Procedural Language") / [9.2](/docs/9.2/plpgsql.html "PostgreSQL 9.2 -
Chapter 43. PL/pgSQL — SQL Procedural Language") /
[9.1](/docs/9.1/plpgsql.html "PostgreSQL 9.1 - Chapter 43. PL/pgSQL — SQL
Procedural Language") / [9.0](/docs/9.0/plpgsql.html "PostgreSQL 9.0 -
Chapter 43. PL/pgSQL — SQL Procedural Language") /
[8.4](/docs/8.4/plpgsql.html "PostgreSQL 8.4 - Chapter 43. PL/pgSQL — SQL
Procedural Language") / [8.3](/docs/8.3/plpgsql.html "PostgreSQL 8.3 -
Chapter 43. PL/pgSQL — SQL Procedural Language") /
[8.2](/docs/8.2/plpgsql.html "PostgreSQL 8.2 - Chapter 43. PL/pgSQL — SQL
Procedural Language") / [8.1](/docs/8.1/plpgsql.html "PostgreSQL 8.1 -
Chapter 43. PL/pgSQL — SQL Procedural Language") /
[8.0](/docs/8.0/plpgsql.html "PostgreSQL 8.0 - Chapter 43. PL/pgSQL — SQL
Procedural Language") / [7.4](/docs/7.4/plpgsql.html "PostgreSQL 7.4 -
Chapter 43. PL/pgSQL — SQL Procedural Language") /
[7.3](/docs/7.3/plpgsql.html "PostgreSQL 7.3 - Chapter 43. PL/pgSQL — SQL
Procedural Language") / [7.2](/docs/7.2/plpgsql.html "PostgreSQL 7.2 -
Chapter 43. PL/pgSQL — SQL Procedural Language") /
[7.1](/docs/7.1/plpgsql.html "PostgreSQL 7.1 - Chapter 43. PL/pgSQL — SQL
Procedural Language")

__

Chapter 43. PL/pgSQL — SQL Procedural Language  
---  
[Prev](xplang-install.html "42.1. Installing Procedural Languages")  | [Up](server-programming.html "Part V. Server Programming") | Part V. Server Programming | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpgsql-overview.html "43.1. Overview")  
  
* * *

## Chapter 43. PL/pgSQL — SQL Procedural Language

**Table of Contents**

[43.1. Overview](plpgsql-overview.html)

    

[43.1.1. Advantages of Using PL/pgSQL](plpgsql-overview.html#PLPGSQL-
ADVANTAGES)

[43.1.2. Supported Argument and Result Data Types](plpgsql-
overview.html#PLPGSQL-ARGS-RESULTS)

[43.2. Structure of PL/pgSQL](plpgsql-structure.html)

[43.3. Declarations](plpgsql-declarations.html)

    

[43.3.1. Declaring Function Parameters](plpgsql-declarations.html#PLPGSQL-
DECLARATION-PARAMETERS)

[43.3.2. `ALIAS`](plpgsql-declarations.html#PLPGSQL-DECLARATION-ALIAS)

[43.3.3. Copying Types](plpgsql-declarations.html#PLPGSQL-DECLARATION-TYPE)

[43.3.4. Row Types](plpgsql-declarations.html#PLPGSQL-DECLARATION-ROWTYPES)

[43.3.5. Record Types](plpgsql-declarations.html#PLPGSQL-DECLARATION-RECORDS)

[43.3.6. Collation of PL/pgSQL Variables](plpgsql-declarations.html#PLPGSQL-
DECLARATION-COLLATION)

[43.4. Expressions](plpgsql-expressions.html)

[43.5. Basic Statements](plpgsql-statements.html)

    

[43.5.1. Assignment](plpgsql-statements.html#PLPGSQL-STATEMENTS-ASSIGNMENT)

[43.5.2. Executing SQL Commands](plpgsql-statements.html#PLPGSQL-STATEMENTS-
GENERAL-SQL)

[43.5.3. Executing a Command with a Single-Row Result](plpgsql-
statements.html#PLPGSQL-STATEMENTS-SQL-ONEROW)

[43.5.4. Executing Dynamic Commands](plpgsql-statements.html#PLPGSQL-
STATEMENTS-EXECUTING-DYN)

[43.5.5. Obtaining the Result Status](plpgsql-statements.html#PLPGSQL-
STATEMENTS-DIAGNOSTICS)

[43.5.6. Doing Nothing At All](plpgsql-statements.html#PLPGSQL-STATEMENTS-
NULL)

[43.6. Control Structures](plpgsql-control-structures.html)

    

[43.6.1. Returning from a Function](plpgsql-control-structures.html#PLPGSQL-
STATEMENTS-RETURNING)

[43.6.2. Returning from a Procedure](plpgsql-control-structures.html#PLPGSQL-
STATEMENTS-RETURNING-PROCEDURE)

[43.6.3. Calling a Procedure](plpgsql-control-structures.html#PLPGSQL-
STATEMENTS-CALLING-PROCEDURE)

[43.6.4. Conditionals](plpgsql-control-structures.html#PLPGSQL-CONDITIONALS)

[43.6.5. Simple Loops](plpgsql-control-structures.html#PLPGSQL-CONTROL-
STRUCTURES-LOOPS)

[43.6.6. Looping through Query Results](plpgsql-control-
structures.html#PLPGSQL-RECORDS-ITERATING)

[43.6.7. Looping through Arrays](plpgsql-control-structures.html#PLPGSQL-
FOREACH-ARRAY)

[43.6.8. Trapping Errors](plpgsql-control-structures.html#PLPGSQL-ERROR-
TRAPPING)

[43.6.9. Obtaining Execution Location Information](plpgsql-control-
structures.html#PLPGSQL-CALL-STACK)

[43.7. Cursors](plpgsql-cursors.html)

    

[43.7.1. Declaring Cursor Variables](plpgsql-cursors.html#PLPGSQL-CURSOR-
DECLARATIONS)

[43.7.2. Opening Cursors](plpgsql-cursors.html#PLPGSQL-CURSOR-OPENING)

[43.7.3. Using Cursors](plpgsql-cursors.html#PLPGSQL-CURSOR-USING)

[43.7.4. Looping through a Cursor's Result](plpgsql-cursors.html#PLPGSQL-
CURSOR-FOR-LOOP)

[43.8. Transaction Management](plpgsql-transactions.html)

[43.9. Errors and Messages](plpgsql-errors-and-messages.html)

    

[43.9.1. Reporting Errors and Messages](plpgsql-errors-and-
messages.html#PLPGSQL-STATEMENTS-RAISE)

[43.9.2. Checking Assertions](plpgsql-errors-and-messages.html#PLPGSQL-
STATEMENTS-ASSERT)

[43.10. Trigger Functions](plpgsql-trigger.html)

    

[43.10.1. Triggers on Data Changes](plpgsql-trigger.html#PLPGSQL-DML-TRIGGER)

[43.10.2. Triggers on Events](plpgsql-trigger.html#PLPGSQL-EVENT-TRIGGER)

[43.11. PL/pgSQL under the Hood](plpgsql-implementation.html)

    

[43.11.1. Variable Substitution](plpgsql-implementation.html#PLPGSQL-VAR-
SUBST)

[43.11.2. Plan Caching](plpgsql-implementation.html#PLPGSQL-PLAN-CACHING)

[43.12. Tips for Developing in PL/pgSQL](plpgsql-development-tips.html)

    

[43.12.1. Handling of Quotation Marks](plpgsql-development-tips.html#PLPGSQL-
QUOTE-TIPS)

[43.12.2. Additional Compile-Time and Run-Time Checks](plpgsql-development-
tips.html#PLPGSQL-EXTRA-CHECKS)

[43.13. Porting from Oracle PL/SQL](plpgsql-porting.html)

    

[43.13.1. Porting Examples](plpgsql-porting.html#PLPGSQL-PORTING-EXAMPLES)

[43.13.2. Other Things to Watch For](plpgsql-porting.html#PLPGSQL-PORTING-
OTHER)

[43.13.3. Appendix](plpgsql-porting.html#PLPGSQL-PORTING-APPENDIX)

* * *

[Prev](xplang-install.html "42.1. Installing Procedural Languages")  | [Up](server-programming.html "Part V. Server Programming") |  [Next](plpgsql-overview.html "43.1. Overview")  
---|---|---  
42.1. Installing Procedural Languages  | [Home](index.html "PostgreSQL 16.9 Documentation") |  43.1. Overview  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpgsql.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

