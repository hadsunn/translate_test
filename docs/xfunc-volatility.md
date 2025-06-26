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

Supported Versions: [Current](/docs/current/xfunc-volatility.html "PostgreSQL
17 - 38.7. Function Volatility Categories") ([17](/docs/17/xfunc-
volatility.html "PostgreSQL 17 - 38.7. Function Volatility Categories")) /
[16](/docs/16/xfunc-volatility.html "PostgreSQL 16 - 38.7. Function Volatility
Categories") / [15](/docs/15/xfunc-volatility.html "PostgreSQL 15 -
38.7. Function Volatility Categories") / [14](/docs/14/xfunc-volatility.html
"PostgreSQL 14 - 38.7. Function Volatility Categories") / [13](/docs/13/xfunc-
volatility.html "PostgreSQL 13 - 38.7. Function Volatility Categories")

Development Versions: [18](/docs/18/xfunc-volatility.html "PostgreSQL 18 -
38.7. Function Volatility Categories") / [devel](/docs/devel/xfunc-
volatility.html "PostgreSQL devel - 38.7. Function Volatility Categories")

Unsupported versions: [12](/docs/12/xfunc-volatility.html "PostgreSQL 12 -
38.7. Function Volatility Categories") / [11](/docs/11/xfunc-volatility.html
"PostgreSQL 11 - 38.7. Function Volatility Categories") / [10](/docs/10/xfunc-
volatility.html "PostgreSQL 10 - 38.7. Function Volatility Categories") /
[9.6](/docs/9.6/xfunc-volatility.html "PostgreSQL 9.6 - 38.7. Function
Volatility Categories") / [9.5](/docs/9.5/xfunc-volatility.html "PostgreSQL
9.5 - 38.7. Function Volatility Categories") / [9.4](/docs/9.4/xfunc-
volatility.html "PostgreSQL 9.4 - 38.7. Function Volatility Categories") /
[9.3](/docs/9.3/xfunc-volatility.html "PostgreSQL 9.3 - 38.7. Function
Volatility Categories") / [9.2](/docs/9.2/xfunc-volatility.html "PostgreSQL
9.2 - 38.7. Function Volatility Categories") / [9.1](/docs/9.1/xfunc-
volatility.html "PostgreSQL 9.1 - 38.7. Function Volatility Categories") /
[9.0](/docs/9.0/xfunc-volatility.html "PostgreSQL 9.0 - 38.7. Function
Volatility Categories") / [8.4](/docs/8.4/xfunc-volatility.html "PostgreSQL
8.4 - 38.7. Function Volatility Categories") / [8.3](/docs/8.3/xfunc-
volatility.html "PostgreSQL 8.3 - 38.7. Function Volatility Categories") /
[8.2](/docs/8.2/xfunc-volatility.html "PostgreSQL 8.2 - 38.7. Function
Volatility Categories") / [8.1](/docs/8.1/xfunc-volatility.html "PostgreSQL
8.1 - 38.7. Function Volatility Categories") / [8.0](/docs/8.0/xfunc-
volatility.html "PostgreSQL 8.0 - 38.7. Function Volatility Categories")

__

38.7. Function Volatility Categories  
---  
[Prev](xfunc-overload.html "38.6. Function Overloading")  | [Up](extend.html "Chapter 38. Extending SQL") | Chapter 38. Extending SQL | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](xfunc-pl.html "38.8. Procedural Language Functions")  
  
* * *

## 38.7. Function Volatility Categories #

Every function has a _volatility_ classification, with the possibilities being
`VOLATILE`, `STABLE`, or `IMMUTABLE`. `VOLATILE` is the default if the
[`CREATE FUNCTION`](sql-createfunction.html "CREATE FUNCTION") command does
not specify a category. The volatility category is a promise to the optimizer
about the behavior of the function:

  * A `VOLATILE` function can do anything, including modifying the database. It can return different results on successive calls with the same arguments. The optimizer makes no assumptions about the behavior of such functions. A query using a volatile function will re-evaluate the function at every row where its value is needed.

  * A `STABLE` function cannot modify the database and is guaranteed to return the same results given the same arguments for all rows within a single statement. This category allows the optimizer to optimize multiple calls of the function to a single call. In particular, it is safe to use an expression containing such a function in an index scan condition. (Since an index scan will evaluate the comparison value only once, not once at each row, it is not valid to use a `VOLATILE` function in an index scan condition.)

  * An `IMMUTABLE` function cannot modify the database and is guaranteed to return the same results given the same arguments forever. This category allows the optimizer to pre-evaluate the function when a query calls it with constant arguments. For example, a query like `SELECT ... WHERE x = 2 + 2` can be simplified on sight to `SELECT ... WHERE x = 4`, because the function underlying the integer addition operator is marked `IMMUTABLE`.

For best optimization results, you should label your functions with the
strictest volatility category that is valid for them.

Any function with side-effects _must_ be labeled `VOLATILE`, so that calls to
it cannot be optimized away. Even a function with no side-effects needs to be
labeled `VOLATILE` if its value can change within a single query; some
examples are `random()`, `currval()`, `timeofday()`.

Another important example is that the `current_timestamp` family of functions
qualify as `STABLE`, since their values do not change within a transaction.

There is relatively little difference between `STABLE` and `IMMUTABLE`
categories when considering simple interactive queries that are planned and
immediately executed: it doesn't matter a lot whether a function is executed
once during planning or once during query execution startup. But there is a
big difference if the plan is saved and reused later. Labeling a function
`IMMUTABLE` when it really isn't might allow it to be prematurely folded to a
constant during planning, resulting in a stale value being re-used during
subsequent uses of the plan. This is a hazard when using prepared statements
or when using function languages that cache plans (such as PL/pgSQL).

For functions written in SQL or in any of the standard procedural languages,
there is a second important property determined by the volatility category,
namely the visibility of any data changes that have been made by the SQL
command that is calling the function. A `VOLATILE` function will see such
changes, a `STABLE` or `IMMUTABLE` function will not. This behavior is
implemented using the snapshotting behavior of MVCC (see [Chapter
13](mvcc.html "Chapter 13. Concurrency Control")): `STABLE` and `IMMUTABLE`
functions use a snapshot established as of the start of the calling query,
whereas `VOLATILE` functions obtain a fresh snapshot at the start of each
query they execute.

### Note

Functions written in C can manage snapshots however they want, but it's
usually a good idea to make C functions work this way too.

Because of this snapshotting behavior, a function containing only `SELECT`
commands can safely be marked `STABLE`, even if it selects from tables that
might be undergoing modifications by concurrent queries. PostgreSQL will
execute all commands of a `STABLE` function using the snapshot established for
the calling query, and so it will see a fixed view of the database throughout
that query.

The same snapshotting behavior is used for `SELECT` commands within
`IMMUTABLE` functions. It is generally unwise to select from database tables
within an `IMMUTABLE` function at all, since the immutability will be broken
if the table contents ever change. However, PostgreSQL does not enforce that
you do not do that.

A common error is to label a function `IMMUTABLE` when its results depend on a
configuration parameter. For example, a function that manipulates timestamps
might well have results that depend on the [TimeZone](runtime-config-
client.html#GUC-TIMEZONE) setting. For safety, such functions should be
labeled `STABLE` instead.

### Note

PostgreSQL requires that `STABLE` and `IMMUTABLE` functions contain no SQL
commands other than `SELECT` to prevent data modification. (This is not a
completely bulletproof test, since such functions could still call `VOLATILE`
functions that modify the database. If you do that, you will find that the
`STABLE` or `IMMUTABLE` function does not notice the database changes applied
by the called function, since they are hidden from its snapshot.)

* * *

[Prev](xfunc-overload.html "38.6. Function Overloading")  | [Up](extend.html "Chapter 38. Extending SQL") |  [Next](xfunc-pl.html "38.8. Procedural Language Functions")  
---|---|---  
38.6. Function Overloading  | [Home](index.html "PostgreSQL 16.9 Documentation") |  38.8. Procedural Language Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/xfunc-volatility.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

