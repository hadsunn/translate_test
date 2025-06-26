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

Supported Versions: [Current](/docs/current/catalog-pg-proc.html "PostgreSQL
17 - 53.39. pg_proc") ([17](/docs/17/catalog-pg-proc.html "PostgreSQL 17 -
53.39. pg_proc")) / [16](/docs/16/catalog-pg-proc.html "PostgreSQL 16 -
53.39. pg_proc") / [15](/docs/15/catalog-pg-proc.html "PostgreSQL 15 -
53.39. pg_proc") / [14](/docs/14/catalog-pg-proc.html "PostgreSQL 14 -
53.39. pg_proc") / [13](/docs/13/catalog-pg-proc.html "PostgreSQL 13 -
53.39. pg_proc")

Development Versions: [18](/docs/18/catalog-pg-proc.html "PostgreSQL 18 -
53.39. pg_proc") / [devel](/docs/devel/catalog-pg-proc.html "PostgreSQL devel
- 53.39. pg_proc")

Unsupported versions: [12](/docs/12/catalog-pg-proc.html "PostgreSQL 12 -
53.39. pg_proc") / [11](/docs/11/catalog-pg-proc.html "PostgreSQL 11 -
53.39. pg_proc") / [10](/docs/10/catalog-pg-proc.html "PostgreSQL 10 -
53.39. pg_proc") / [9.6](/docs/9.6/catalog-pg-proc.html "PostgreSQL 9.6 -
53.39. pg_proc") / [9.5](/docs/9.5/catalog-pg-proc.html "PostgreSQL 9.5 -
53.39. pg_proc") / [9.4](/docs/9.4/catalog-pg-proc.html "PostgreSQL 9.4 -
53.39. pg_proc") / [9.3](/docs/9.3/catalog-pg-proc.html "PostgreSQL 9.3 -
53.39. pg_proc") / [9.2](/docs/9.2/catalog-pg-proc.html "PostgreSQL 9.2 -
53.39. pg_proc") / [9.1](/docs/9.1/catalog-pg-proc.html "PostgreSQL 9.1 -
53.39. pg_proc") / [9.0](/docs/9.0/catalog-pg-proc.html "PostgreSQL 9.0 -
53.39. pg_proc") / [8.4](/docs/8.4/catalog-pg-proc.html "PostgreSQL 8.4 -
53.39. pg_proc") / [8.3](/docs/8.3/catalog-pg-proc.html "PostgreSQL 8.3 -
53.39. pg_proc") / [8.2](/docs/8.2/catalog-pg-proc.html "PostgreSQL 8.2 -
53.39. pg_proc") / [8.1](/docs/8.1/catalog-pg-proc.html "PostgreSQL 8.1 -
53.39. pg_proc") / [8.0](/docs/8.0/catalog-pg-proc.html "PostgreSQL 8.0 -
53.39. pg_proc") / [7.4](/docs/7.4/catalog-pg-proc.html "PostgreSQL 7.4 -
53.39. pg_proc") / [7.3](/docs/7.3/catalog-pg-proc.html "PostgreSQL 7.3 -
53.39. pg_proc") / [7.2](/docs/7.2/catalog-pg-proc.html "PostgreSQL 7.2 -
53.39. pg_proc") / [7.1](/docs/7.1/catalog-pg-proc.html "PostgreSQL 7.1 -
53.39. pg_proc")

__

53.39. `pg_proc`  
---  
[Prev](catalog-pg-policy.html "53.38. pg_policy")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-publication.html "53.40. pg_publication")  
  
* * *

## 53.39. `pg_proc` #

The catalog `pg_proc` stores information about functions, procedures,
aggregate functions, and window functions (collectively also known as
routines). See [CREATE FUNCTION](sql-createfunction.html "CREATE FUNCTION"),
[CREATE PROCEDURE](sql-createprocedure.html "CREATE PROCEDURE"), and [Section
38.3](xfunc.html "38.3. User-Defined Functions") for more information.

If `prokind` indicates that the entry is for an aggregate function, there
should be a matching row in [`pg_aggregate`](catalog-pg-aggregate.html
"53.2. pg_aggregate").

**Table  53.39. `pg_proc` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`proname` `name` Name of the function  
`pronamespace` `oid` (references [`pg_namespace`](catalog-pg-namespace.html
"53.32. pg_namespace").`oid`) The OID of the namespace that contains this
function  
`proowner` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the function  
`prolang` `oid` (references [`pg_language`](catalog-pg-language.html
"53.29. pg_language").`oid`) Implementation language or call interface of this
function  
`procost` `float4` Estimated execution cost (in units of
[cpu_operator_cost](runtime-config-query.html#GUC-CPU-OPERATOR-COST)); if
`proretset`, this is cost per row returned  
`prorows` `float4` Estimated number of result rows (zero if not `proretset`)  
`provariadic` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) Data type of the variadic array parameter's elements,
or zero if the function does not have a variadic parameter  
`prosupport` `regproc` (references [`pg_proc`](catalog-pg-proc.html
"53.39. pg_proc").`oid`) Planner support function for this function (see
[Section 38.11](xfunc-optimization.html "38.11. Function Optimization
Information")), or zero if none  
`prokind` `char` `f` for a normal function, `p` for a procedure, `a` for an
aggregate function, or `w` for a window function  
`prosecdef` `bool` Function is a security definer (i.e., a “setuid” function)  
`proleakproof` `bool` The function has no side effects. No information about
the arguments is conveyed except via the return value. Any function that might
throw an error depending on the values of its arguments is not leak-proof.  
`proisstrict` `bool` Function returns null if any call argument is null. In
that case the function won't actually be called at all. Functions that are not
“strict” must be prepared to handle null inputs.  
`proretset` `bool` Function returns a set (i.e., multiple values of the
specified data type)  
`provolatile` `char` `provolatile` tells whether the function's result depends
only on its input arguments, or is affected by outside factors. It is `i` for
“immutable” functions, which always deliver the same result for the same
inputs. It is `s` for “stable” functions, whose results (for fixed inputs) do
not change within a scan. It is `v` for “volatile” functions, whose results
might change at any time. (Use `v` also for functions with side-effects, so
that calls to them cannot get optimized away.)  
`proparallel` `char` `proparallel` tells whether the function can be safely
run in parallel mode. It is `s` for functions which are safe to run in
parallel mode without restriction. It is `r` for functions which can be run in
parallel mode, but their execution is restricted to the parallel group leader;
parallel worker processes cannot invoke these functions. It is `u` for
functions which are unsafe in parallel mode; the presence of such a function
forces a serial execution plan.  
`pronargs` `int2` Number of input arguments  
`pronargdefaults` `int2` Number of arguments that have defaults  
`prorettype` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) Data type of the return value  
`proargtypes` `oidvector` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) An array of the data types of the function arguments.
This includes only input arguments (including `INOUT` and `VARIADIC`
arguments), and thus represents the call signature of the function.  
`proallargtypes` `oid[]` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) An array of the data types of the function arguments.
This includes all arguments (including `OUT` and `INOUT` arguments); however,
if all the arguments are `IN` arguments, this field will be null. Note that
subscripting is 1-based, whereas for historical reasons `proargtypes` is
subscripted from 0.  
`proargmodes` `char[]` An array of the modes of the function arguments,
encoded as `i` for `IN` arguments, `o` for `OUT` arguments, `b` for `INOUT`
arguments, `v` for `VARIADIC` arguments, `t` for `TABLE` arguments. If all the
arguments are `IN` arguments, this field will be null. Note that subscripts
correspond to positions of `proallargtypes` not `proargtypes`.  
`proargnames` `text[]` An array of the names of the function arguments.
Arguments without a name are set to empty strings in the array. If none of the
arguments have a name, this field will be null. Note that subscripts
correspond to positions of `proallargtypes` not `proargtypes`.  
`proargdefaults` `pg_node_tree` Expression trees (in `nodeToString()`
representation) for default values. This is a list with `pronargdefaults`
elements, corresponding to the last _`N`_ _input_ arguments (i.e., the last
_`N`_ `proargtypes` positions). If none of the arguments have defaults, this
field will be null.  
`protrftypes` `oid[]` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) An array of the argument/result data type(s) for
which to apply transforms (from the function's `TRANSFORM` clause). Null if
none.  
`prosrc` `text` This tells the function handler how to invoke the function. It
might be the actual source code of the function for interpreted languages, a
link symbol, a file name, or just about anything else, depending on the
implementation language/call convention.  
`probin` `text` Additional information about how to invoke the function.
Again, the interpretation is language-specific.  
`prosqlbody` `pg_node_tree` Pre-parsed SQL function body. This is used for
SQL-language functions when the body is given in SQL-standard notation rather
than as a string literal. It's null in other cases.  
`proconfig` `text[]` Function's local settings for run-time configuration
variables  
`proacl` `aclitem[]` Access privileges; see [Section 5.7](ddl-priv.html
"5.7. Privileges") for details  
  
  

For compiled functions, both built-in and dynamically loaded, `prosrc`
contains the function's C-language name (link symbol). For SQL-language
functions, `prosrc` contains the function's source text if that is specified
as a string literal; but if the function body is specified in SQL-standard
style, `prosrc` is unused (typically it's an empty string) and `prosqlbody`
contains the pre-parsed definition. For all other currently-known language
types, `prosrc` contains the function's source text. `probin` is null except
for dynamically-loaded C functions, for which it gives the name of the shared
library file containing the function.

* * *

[Prev](catalog-pg-policy.html "53.38. pg_policy")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-publication.html "53.40. pg_publication")  
---|---|---  
53.38. `pg_policy`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.40. `pg_publication`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-proc.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

