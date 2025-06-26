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

Supported Versions: [Current](/docs/current/plpgsql-overview.html "PostgreSQL
17 - 43.1. Overview") ([17](/docs/17/plpgsql-overview.html "PostgreSQL 17 -
43.1. Overview")) / [16](/docs/16/plpgsql-overview.html "PostgreSQL 16 -
43.1. Overview") / [15](/docs/15/plpgsql-overview.html "PostgreSQL 15 -
43.1. Overview") / [14](/docs/14/plpgsql-overview.html "PostgreSQL 14 -
43.1. Overview") / [13](/docs/13/plpgsql-overview.html "PostgreSQL 13 -
43.1. Overview")

Development Versions: [18](/docs/18/plpgsql-overview.html "PostgreSQL 18 -
43.1. Overview") / [devel](/docs/devel/plpgsql-overview.html "PostgreSQL devel
- 43.1. Overview")

Unsupported versions: [12](/docs/12/plpgsql-overview.html "PostgreSQL 12 -
43.1. Overview") / [11](/docs/11/plpgsql-overview.html "PostgreSQL 11 -
43.1. Overview") / [10](/docs/10/plpgsql-overview.html "PostgreSQL 10 -
43.1. Overview") / [9.6](/docs/9.6/plpgsql-overview.html "PostgreSQL 9.6 -
43.1. Overview") / [9.5](/docs/9.5/plpgsql-overview.html "PostgreSQL 9.5 -
43.1. Overview") / [9.4](/docs/9.4/plpgsql-overview.html "PostgreSQL 9.4 -
43.1. Overview") / [9.3](/docs/9.3/plpgsql-overview.html "PostgreSQL 9.3 -
43.1. Overview") / [9.2](/docs/9.2/plpgsql-overview.html "PostgreSQL 9.2 -
43.1. Overview") / [9.1](/docs/9.1/plpgsql-overview.html "PostgreSQL 9.1 -
43.1. Overview") / [9.0](/docs/9.0/plpgsql-overview.html "PostgreSQL 9.0 -
43.1. Overview") / [8.4](/docs/8.4/plpgsql-overview.html "PostgreSQL 8.4 -
43.1. Overview") / [8.3](/docs/8.3/plpgsql-overview.html "PostgreSQL 8.3 -
43.1. Overview") / [8.2](/docs/8.2/plpgsql-overview.html "PostgreSQL 8.2 -
43.1. Overview")

__

43.1. Overview  
---  
[Prev](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") | Chapter 43. PL/pgSQL — SQL Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpgsql-structure.html "43.2. Structure of PL/pgSQL")  
  
* * *

## 43.1. Overview #

[43.1.1. Advantages of Using PL/pgSQL](plpgsql-overview.html#PLPGSQL-
ADVANTAGES)

[43.1.2. Supported Argument and Result Data Types](plpgsql-
overview.html#PLPGSQL-ARGS-RESULTS)

PL/pgSQL is a loadable procedural language for the PostgreSQL database system.
The design goals of PL/pgSQL were to create a loadable procedural language
that

  * can be used to create functions, procedures, and triggers,

  * adds control structures to the SQL language,

  * can perform complex computations,

  * inherits all user-defined types, functions, procedures, and operators,

  * can be defined to be trusted by the server,

  * is easy to use.

Functions created with PL/pgSQL can be used anywhere that built-in functions
could be used. For example, it is possible to create complex conditional
computation functions and later use them to define operators or use them in
index expressions.

In PostgreSQL 9.0 and later, PL/pgSQL is installed by default. However it is
still a loadable module, so especially security-conscious administrators could
choose to remove it.

### 43.1.1. Advantages of Using PL/pgSQL #

SQL is the language PostgreSQL and most other relational databases use as
query language. It's portable and easy to learn. But every SQL statement must
be executed individually by the database server.

That means that your client application must send each query to the database
server, wait for it to be processed, receive and process the results, do some
computation, then send further queries to the server. All this incurs
interprocess communication and will also incur network overhead if your client
is on a different machine than the database server.

With PL/pgSQL you can group a block of computation and a series of queries
_inside_ the database server, thus having the power of a procedural language
and the ease of use of SQL, but with considerable savings of client/server
communication overhead.

  * Extra round trips between client and server are eliminated

  * Intermediate results that the client does not need do not have to be marshaled or transferred between server and client

  * Multiple rounds of query parsing can be avoided

This can result in a considerable performance increase as compared to an
application that does not use stored functions.

Also, with PL/pgSQL you can use all the data types, operators and functions of
SQL.

### 43.1.2. Supported Argument and Result Data Types #

Functions written in PL/pgSQL can accept as arguments any scalar or array data
type supported by the server, and they can return a result of any of these
types. They can also accept or return any composite type (row type) specified
by name. It is also possible to declare a PL/pgSQL function as accepting
`record`, which means that any composite type will do as input, or as
returning `record`, which means that the result is a row type whose columns
are determined by specification in the calling query, as discussed in [Section
7.2.1.4](queries-table-expressions.html#QUERIES-TABLEFUNCTIONS "7.2.1.4. Table
Functions").

PL/pgSQL functions can be declared to accept a variable number of arguments by
using the `VARIADIC` marker. This works exactly the same way as for SQL
functions, as discussed in [Section 38.5.6](xfunc-sql.html#XFUNC-SQL-VARIADIC-
FUNCTIONS "38.5.6. SQL Functions with Variable Numbers of Arguments").

PL/pgSQL functions can also be declared to accept and return the polymorphic
types described in [Section 38.2.5](extend-type-system.html#EXTEND-TYPES-
POLYMORPHIC "38.2.5. Polymorphic Types"), thus allowing the actual data types
handled by the function to vary from call to call. Examples appear in [Section
43.3.1](plpgsql-declarations.html#PLPGSQL-DECLARATION-PARAMETERS
"43.3.1. Declaring Function Parameters").

PL/pgSQL functions can also be declared to return a “set” (or table) of any
data type that can be returned as a single instance. Such a function generates
its output by executing `RETURN NEXT` for each desired element of the result
set, or by using `RETURN QUERY` to output the result of evaluating a query.

Finally, a PL/pgSQL function can be declared to return `void` if it has no
useful return value. (Alternatively, it could be written as a procedure in
that case.)

PL/pgSQL functions can also be declared with output parameters in place of an
explicit specification of the return type. This does not add any fundamental
capability to the language, but it is often convenient, especially for
returning multiple values. The `RETURNS TABLE` notation can also be used in
place of `RETURNS SETOF`.

Specific examples appear in [Section 43.3.1](plpgsql-
declarations.html#PLPGSQL-DECLARATION-PARAMETERS "43.3.1. Declaring Function
Parameters") and [Section 43.6.1](plpgsql-control-structures.html#PLPGSQL-
STATEMENTS-RETURNING "43.6.1. Returning from a Function").

* * *

[Prev](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") |  [Next](plpgsql-structure.html "43.2. Structure of PL/pgSQL")  
---|---|---  
Chapter 43. PL/pgSQL — SQL Procedural Language  | [Home](index.html "PostgreSQL 16.9 Documentation") |  43.2. Structure of PL/pgSQL  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpgsql-overview.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

