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

Supported Versions: [Current](/docs/current/xfunc-overload.html "PostgreSQL 17
- 38.6. Function Overloading") ([17](/docs/17/xfunc-overload.html "PostgreSQL
17 - 38.6. Function Overloading")) / [16](/docs/16/xfunc-overload.html
"PostgreSQL 16 - 38.6. Function Overloading") / [15](/docs/15/xfunc-
overload.html "PostgreSQL 15 - 38.6. Function Overloading") /
[14](/docs/14/xfunc-overload.html "PostgreSQL 14 - 38.6. Function
Overloading") / [13](/docs/13/xfunc-overload.html "PostgreSQL 13 -
38.6. Function Overloading")

Development Versions: [18](/docs/18/xfunc-overload.html "PostgreSQL 18 -
38.6. Function Overloading") / [devel](/docs/devel/xfunc-overload.html
"PostgreSQL devel - 38.6. Function Overloading")

Unsupported versions: [12](/docs/12/xfunc-overload.html "PostgreSQL 12 -
38.6. Function Overloading") / [11](/docs/11/xfunc-overload.html "PostgreSQL
11 - 38.6. Function Overloading") / [10](/docs/10/xfunc-overload.html
"PostgreSQL 10 - 38.6. Function Overloading") / [9.6](/docs/9.6/xfunc-
overload.html "PostgreSQL 9.6 - 38.6. Function Overloading") /
[9.5](/docs/9.5/xfunc-overload.html "PostgreSQL 9.5 - 38.6. Function
Overloading") / [9.4](/docs/9.4/xfunc-overload.html "PostgreSQL 9.4 -
38.6. Function Overloading") / [9.3](/docs/9.3/xfunc-overload.html "PostgreSQL
9.3 - 38.6. Function Overloading") / [9.2](/docs/9.2/xfunc-overload.html
"PostgreSQL 9.2 - 38.6. Function Overloading") / [9.1](/docs/9.1/xfunc-
overload.html "PostgreSQL 9.1 - 38.6. Function Overloading") /
[9.0](/docs/9.0/xfunc-overload.html "PostgreSQL 9.0 - 38.6. Function
Overloading") / [8.4](/docs/8.4/xfunc-overload.html "PostgreSQL 8.4 -
38.6. Function Overloading") / [8.3](/docs/8.3/xfunc-overload.html "PostgreSQL
8.3 - 38.6. Function Overloading") / [8.2](/docs/8.2/xfunc-overload.html
"PostgreSQL 8.2 - 38.6. Function Overloading") / [8.1](/docs/8.1/xfunc-
overload.html "PostgreSQL 8.1 - 38.6. Function Overloading") /
[8.0](/docs/8.0/xfunc-overload.html "PostgreSQL 8.0 - 38.6. Function
Overloading") / [7.4](/docs/7.4/xfunc-overload.html "PostgreSQL 7.4 -
38.6. Function Overloading") / [7.3](/docs/7.3/xfunc-overload.html "PostgreSQL
7.3 - 38.6. Function Overloading") / [7.2](/docs/7.2/xfunc-overload.html
"PostgreSQL 7.2 - 38.6. Function Overloading") / [7.1](/docs/7.1/xfunc-
overload.html "PostgreSQL 7.1 - 38.6. Function Overloading")

__

38.6. Function Overloading  
---  
[Prev](xfunc-sql.html "38.5. Query Language \(SQL\) Functions")  | [Up](extend.html "Chapter 38. Extending SQL") | Chapter 38. Extending SQL | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](xfunc-volatility.html "38.7. Function Volatility Categories")  
  
* * *

## 38.6. Function Overloading #

More than one function can be defined with the same SQL name, so long as the
arguments they take are different. In other words, function names can be
_overloaded_. Whether or not you use it, this capability entails security
precautions when calling functions in databases where some users mistrust
other users; see [Section 10.3](typeconv-func.html "10.3. Functions"). When a
query is executed, the server will determine which function to call from the
data types and the number of the provided arguments. Overloading can also be
used to simulate functions with a variable number of arguments, up to a finite
maximum number.

When creating a family of overloaded functions, one should be careful not to
create ambiguities. For instance, given the functions:

    
    
    CREATE FUNCTION test(int, real) RETURNS ...
    CREATE FUNCTION test(smallint, double precision) RETURNS ...
    

it is not immediately clear which function would be called with some trivial
input like `test(1, 1.5)`. The currently implemented resolution rules are
described in [Chapter 10](typeconv.html "Chapter 10. Type Conversion"), but it
is unwise to design a system that subtly relies on this behavior.

A function that takes a single argument of a composite type should generally
not have the same name as any attribute (field) of that type. Recall that
`_`attribute`_(_`table`_)` is considered equivalent to
`_`table`_._`attribute`_`. In the case that there is an ambiguity between a
function on a composite type and an attribute of the composite type, the
attribute will always be used. It is possible to override that choice by
schema-qualifying the function name (that is, `_`schema`_._`func`_(_`table`_)`
) but it's better to avoid the problem by not choosing conflicting names.

Another possible conflict is between variadic and non-variadic functions. For
instance, it is possible to create both `foo(numeric)` and `foo(VARIADIC
numeric[])`. In this case it is unclear which one should be matched to a call
providing a single numeric argument, such as `foo(10.1)`. The rule is that the
function appearing earlier in the search path is used, or if the two functions
are in the same schema, the non-variadic one is preferred.

When overloading C-language functions, there is an additional constraint: The
C name of each function in the family of overloaded functions must be
different from the C names of all other functions, either internal or
dynamically loaded. If this rule is violated, the behavior is not portable.
You might get a run-time linker error, or one of the functions will get called
(usually the internal one). The alternative form of the `AS` clause for the
SQL `CREATE FUNCTION` command decouples the SQL function name from the
function name in the C source code. For instance:

    
    
    CREATE FUNCTION test(int) RETURNS int
        AS '_filename_ ', 'test_1arg'
        LANGUAGE C;
    CREATE FUNCTION test(int, int) RETURNS int
        AS '_filename_ ', 'test_2arg'
        LANGUAGE C;
    

The names of the C functions here reflect one of many possible conventions.

* * *

[Prev](xfunc-sql.html "38.5. Query Language \(SQL\) Functions")  | [Up](extend.html "Chapter 38. Extending SQL") |  [Next](xfunc-volatility.html "38.7. Function Volatility Categories")  
---|---|---  
38.5. Query Language (SQL) Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  38.7. Function Volatility Categories  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/xfunc-overload.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

