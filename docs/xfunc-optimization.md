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

Supported Versions: [Current](/docs/current/xfunc-optimization.html
"PostgreSQL 17 - 38.11. Function Optimization Information")
([17](/docs/17/xfunc-optimization.html "PostgreSQL 17 - 38.11. Function
Optimization Information")) / [16](/docs/16/xfunc-optimization.html
"PostgreSQL 16 - 38.11. Function Optimization Information") /
[15](/docs/15/xfunc-optimization.html "PostgreSQL 15 - 38.11. Function
Optimization Information") / [14](/docs/14/xfunc-optimization.html "PostgreSQL
14 - 38.11. Function Optimization Information") / [13](/docs/13/xfunc-
optimization.html "PostgreSQL 13 - 38.11. Function Optimization Information")

Development Versions: [18](/docs/18/xfunc-optimization.html "PostgreSQL 18 -
38.11. Function Optimization Information") / [devel](/docs/devel/xfunc-
optimization.html "PostgreSQL devel - 38.11. Function Optimization
Information")

Unsupported versions: [12](/docs/12/xfunc-optimization.html "PostgreSQL 12 -
38.11. Function Optimization Information")

__

38.11. Function Optimization Information  
---  
[Prev](xfunc-c.html "38.10. C-Language Functions")  | [Up](extend.html "Chapter 38. Extending SQL") | Chapter 38. Extending SQL | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](xaggr.html "38.12. User-Defined Aggregates")  
  
* * *

## 38.11. Function Optimization Information #

By default, a function is just a “black box” that the database system knows
very little about the behavior of. However, that means that queries using the
function may be executed much less efficiently than they could be. It is
possible to supply additional knowledge that helps the planner optimize
function calls.

Some basic facts can be supplied by declarative annotations provided in the
[`CREATE FUNCTION`](sql-createfunction.html "CREATE FUNCTION") command. Most
important of these is the function's [volatility category](xfunc-
volatility.html "38.7. Function Volatility Categories") (`IMMUTABLE`,
`STABLE`, or `VOLATILE`); one should always be careful to specify this
correctly when defining a function. The parallel safety property (`PARALLEL
UNSAFE`, `PARALLEL RESTRICTED`, or `PARALLEL SAFE`) must also be specified if
you hope to use the function in parallelized queries. It can also be useful to
specify the function's estimated execution cost, and/or the number of rows a
set-returning function is estimated to return. However, the declarative way of
specifying those two facts only allows specifying a constant value, which is
often inadequate.

It is also possible to attach a _planner support function_ to an SQL-callable
function (called its _target function_), and thereby provide knowledge about
the target function that is too complex to be represented declaratively.
Planner support functions have to be written in C (although their target
functions might not be), so this is an advanced feature that relatively few
people will use.

A planner support function must have the SQL signature

    
    
    supportfn(internal) returns internal
    

It is attached to its target function by specifying the `SUPPORT` clause when
creating the target function.

The details of the API for planner support functions can be found in file
`src/include/nodes/supportnodes.h` in the PostgreSQL source code. Here we
provide just an overview of what planner support functions can do. The set of
possible requests to a support function is extensible, so more things might be
possible in future versions.

Some function calls can be simplified during planning based on properties
specific to the function. For example, `int4mul(n, 1)` could be simplified to
just `n`. This type of transformation can be performed by a planner support
function, by having it implement the `SupportRequestSimplify` request type.
The support function will be called for each instance of its target function
found in a query parse tree. If it finds that the particular call can be
simplified into some other form, it can build and return a parse tree
representing that expression. This will automatically work for operators based
on the function, too — in the example just given, `n * 1` would also be
simplified to `n`. (But note that this is just an example; this particular
optimization is not actually performed by standard PostgreSQL.) We make no
guarantee that PostgreSQL will never call the target function in cases that
the support function could simplify. Ensure rigorous equivalence between the
simplified expression and an actual execution of the target function.

For target functions that return `boolean`, it is often useful to estimate the
fraction of rows that will be selected by a `WHERE` clause using that
function. This can be done by a support function that implements the
`SupportRequestSelectivity` request type.

If the target function's run time is highly dependent on its inputs, it may be
useful to provide a non-constant cost estimate for it. This can be done by a
support function that implements the `SupportRequestCost` request type.

For target functions that return sets, it is often useful to provide a non-
constant estimate for the number of rows that will be returned. This can be
done by a support function that implements the `SupportRequestRows` request
type.

For target functions that return `boolean`, it may be possible to convert a
function call appearing in `WHERE` into an indexable operator clause or
clauses. The converted clauses might be exactly equivalent to the function's
condition, or they could be somewhat weaker (that is, they might accept some
values that the function condition does not). In the latter case the index
condition is said to be _lossy_ ; it can still be used to scan an index, but
the function call will have to be executed for each row returned by the index
to see if it really passes the `WHERE` condition or not. To create such
conditions, the support function must implement the
`SupportRequestIndexCondition` request type.

* * *

[Prev](xfunc-c.html "38.10. C-Language Functions")  | [Up](extend.html "Chapter 38. Extending SQL") |  [Next](xaggr.html "38.12. User-Defined Aggregates")  
---|---|---  
38.10. C-Language Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  38.12. User-Defined Aggregates  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/xfunc-optimization.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

