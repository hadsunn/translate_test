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

Supported Versions: [Current](/docs/current/plpgsql-expressions.html
"PostgreSQL 17 - 43.4. Expressions") ([17](/docs/17/plpgsql-expressions.html
"PostgreSQL 17 - 43.4. Expressions")) / [16](/docs/16/plpgsql-expressions.html
"PostgreSQL 16 - 43.4. Expressions") / [15](/docs/15/plpgsql-expressions.html
"PostgreSQL 15 - 43.4. Expressions") / [14](/docs/14/plpgsql-expressions.html
"PostgreSQL 14 - 43.4. Expressions") / [13](/docs/13/plpgsql-expressions.html
"PostgreSQL 13 - 43.4. Expressions")

Development Versions: [18](/docs/18/plpgsql-expressions.html "PostgreSQL 18 -
43.4. Expressions") / [devel](/docs/devel/plpgsql-expressions.html "PostgreSQL
devel - 43.4. Expressions")

Unsupported versions: [12](/docs/12/plpgsql-expressions.html "PostgreSQL 12 -
43.4. Expressions") / [11](/docs/11/plpgsql-expressions.html "PostgreSQL 11 -
43.4. Expressions") / [10](/docs/10/plpgsql-expressions.html "PostgreSQL 10 -
43.4. Expressions") / [9.6](/docs/9.6/plpgsql-expressions.html "PostgreSQL 9.6
- 43.4. Expressions") / [9.5](/docs/9.5/plpgsql-expressions.html "PostgreSQL
9.5 - 43.4. Expressions") / [9.4](/docs/9.4/plpgsql-expressions.html
"PostgreSQL 9.4 - 43.4. Expressions") / [9.3](/docs/9.3/plpgsql-
expressions.html "PostgreSQL 9.3 - 43.4. Expressions") /
[9.2](/docs/9.2/plpgsql-expressions.html "PostgreSQL 9.2 - 43.4. Expressions")
/ [9.1](/docs/9.1/plpgsql-expressions.html "PostgreSQL 9.1 -
43.4. Expressions") / [9.0](/docs/9.0/plpgsql-expressions.html "PostgreSQL 9.0
- 43.4. Expressions") / [8.4](/docs/8.4/plpgsql-expressions.html "PostgreSQL
8.4 - 43.4. Expressions") / [8.3](/docs/8.3/plpgsql-expressions.html
"PostgreSQL 8.3 - 43.4. Expressions") / [8.2](/docs/8.2/plpgsql-
expressions.html "PostgreSQL 8.2 - 43.4. Expressions") /
[8.1](/docs/8.1/plpgsql-expressions.html "PostgreSQL 8.1 - 43.4. Expressions")
/ [8.0](/docs/8.0/plpgsql-expressions.html "PostgreSQL 8.0 -
43.4. Expressions") / [7.4](/docs/7.4/plpgsql-expressions.html "PostgreSQL 7.4
- 43.4. Expressions") / [7.3](/docs/7.3/plpgsql-expressions.html "PostgreSQL
7.3 - 43.4. Expressions") / [7.2](/docs/7.2/plpgsql-expressions.html
"PostgreSQL 7.2 - 43.4. Expressions")

__

43.4. Expressions  
---  
[Prev](plpgsql-declarations.html "43.3. Declarations")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") | Chapter 43. PL/pgSQL — SQL Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpgsql-statements.html "43.5. Basic Statements")  
  
* * *

## 43.4. Expressions #

All expressions used in PL/pgSQL statements are processed using the server's
main SQL executor. For example, when you write a PL/pgSQL statement like

    
    
    IF _expression_ THEN ...
    

PL/pgSQL will evaluate the expression by feeding a query like

    
    
    SELECT _expression_
    

to the main SQL engine. While forming the `SELECT` command, any occurrences of
PL/pgSQL variable names are replaced by query parameters, as discussed in
detail in [Section 43.11.1](plpgsql-implementation.html#PLPGSQL-VAR-SUBST
"43.11.1. Variable Substitution"). This allows the query plan for the `SELECT`
to be prepared just once and then reused for subsequent evaluations with
different values of the variables. Thus, what really happens on first use of
an expression is essentially a `PREPARE` command. For example, if we have
declared two integer variables `x` and `y`, and we write

    
    
    IF x < y THEN ...
    

what happens behind the scenes is equivalent to

    
    
    PREPARE _statement_name_(integer, integer) AS SELECT $1 < $2;
    

and then this prepared statement is `EXECUTE`d for each execution of the `IF`
statement, with the current values of the PL/pgSQL variables supplied as
parameter values. Normally these details are not important to a PL/pgSQL user,
but they are useful to know when trying to diagnose a problem. More
information appears in [Section 43.11.2](plpgsql-implementation.html#PLPGSQL-
PLAN-CACHING "43.11.2. Plan Caching").

Since an _`expression`_ is converted to a `SELECT` command, it can contain the
same clauses that an ordinary `SELECT` would, except that it cannot include a
top-level `UNION`, `INTERSECT`, or `EXCEPT` clause. Thus for example one could
test whether a table is non-empty with

    
    
    IF count(*) > 0 FROM my_table THEN ...
    

since the _`expression`_ between `IF` and `THEN` is parsed as though it were
`SELECT count(*) > 0 FROM my_table`. The `SELECT` must produce a single
column, and not more than one row. (If it produces no rows, the result is
taken as NULL.)

* * *

[Prev](plpgsql-declarations.html "43.3. Declarations")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") |  [Next](plpgsql-statements.html "43.5. Basic Statements")  
---|---|---  
43.3. Declarations  | [Home](index.html "PostgreSQL 16.9 Documentation") |  43.5. Basic Statements  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpgsql-expressions.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

