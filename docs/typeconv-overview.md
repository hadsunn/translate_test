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

Supported Versions: [Current](/docs/current/typeconv-overview.html "PostgreSQL
17 - 10.1. Overview") ([17](/docs/17/typeconv-overview.html "PostgreSQL 17 -
10.1. Overview")) / [16](/docs/16/typeconv-overview.html "PostgreSQL 16 -
10.1. Overview") / [15](/docs/15/typeconv-overview.html "PostgreSQL 15 -
10.1. Overview") / [14](/docs/14/typeconv-overview.html "PostgreSQL 14 -
10.1. Overview") / [13](/docs/13/typeconv-overview.html "PostgreSQL 13 -
10.1. Overview")

Development Versions: [18](/docs/18/typeconv-overview.html "PostgreSQL 18 -
10.1. Overview") / [devel](/docs/devel/typeconv-overview.html "PostgreSQL
devel - 10.1. Overview")

Unsupported versions: [12](/docs/12/typeconv-overview.html "PostgreSQL 12 -
10.1. Overview") / [11](/docs/11/typeconv-overview.html "PostgreSQL 11 -
10.1. Overview") / [10](/docs/10/typeconv-overview.html "PostgreSQL 10 -
10.1. Overview") / [9.6](/docs/9.6/typeconv-overview.html "PostgreSQL 9.6 -
10.1. Overview") / [9.5](/docs/9.5/typeconv-overview.html "PostgreSQL 9.5 -
10.1. Overview") / [9.4](/docs/9.4/typeconv-overview.html "PostgreSQL 9.4 -
10.1. Overview") / [9.3](/docs/9.3/typeconv-overview.html "PostgreSQL 9.3 -
10.1. Overview") / [9.2](/docs/9.2/typeconv-overview.html "PostgreSQL 9.2 -
10.1. Overview") / [9.1](/docs/9.1/typeconv-overview.html "PostgreSQL 9.1 -
10.1. Overview") / [9.0](/docs/9.0/typeconv-overview.html "PostgreSQL 9.0 -
10.1. Overview") / [8.4](/docs/8.4/typeconv-overview.html "PostgreSQL 8.4 -
10.1. Overview") / [8.3](/docs/8.3/typeconv-overview.html "PostgreSQL 8.3 -
10.1. Overview") / [8.2](/docs/8.2/typeconv-overview.html "PostgreSQL 8.2 -
10.1. Overview") / [7.2](/docs/7.2/typeconv-overview.html "PostgreSQL 7.2 -
10.1. Overview")

__

10.1. Overview  
---  
[Prev](typeconv.html "Chapter 10. Type Conversion")  | [Up](typeconv.html "Chapter 10. Type Conversion") | Chapter 10. Type Conversion | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](typeconv-oper.html "10.2. Operators")  
  
* * *

## 10.1. Overview #

SQL is a strongly typed language. That is, every data item has an associated
data type which determines its behavior and allowed usage. PostgreSQL has an
extensible type system that is more general and flexible than other SQL
implementations. Hence, most type conversion behavior in PostgreSQL is
governed by general rules rather than by ad hoc heuristics. This allows the
use of mixed-type expressions even with user-defined types.

The PostgreSQL scanner/parser divides lexical elements into five fundamental
categories: integers, non-integer numbers, strings, identifiers, and key
words. Constants of most non-numeric types are first classified as strings.
The SQL language definition allows specifying type names with strings, and
this mechanism can be used in PostgreSQL to start the parser down the correct
path. For example, the query:

    
    
    SELECT text 'Origin' AS "label", point '(0,0)' AS "value";
    
     label  | value
    --------+-------
     Origin | (0,0)
    (1 row)
    

has two literal constants, of type `text` and `point`. If a type is not
specified for a string literal, then the placeholder type `unknown` is
assigned initially, to be resolved in later stages as described below.

There are four fundamental SQL constructs requiring distinct type conversion
rules in the PostgreSQL parser:

Function calls

    

Much of the PostgreSQL type system is built around a rich set of functions.
Functions can have one or more arguments. Since PostgreSQL permits function
overloading, the function name alone does not uniquely identify the function
to be called; the parser must select the right function based on the data
types of the supplied arguments.

Operators

    

PostgreSQL allows expressions with prefix (one-argument) operators, as well as
infix (two-argument) operators. Like functions, operators can be overloaded,
so the same problem of selecting the right operator exists.

Value Storage

    

SQL `INSERT` and `UPDATE` statements place the results of expressions into a
table. The expressions in the statement must be matched up with, and perhaps
converted to, the types of the target columns.

`UNION`, `CASE`, and related constructs

    

Since all query results from a unionized `SELECT` statement must appear in a
single set of columns, the types of the results of each `SELECT` clause must
be matched up and converted to a uniform set. Similarly, the result
expressions of a `CASE` construct must be converted to a common type so that
the `CASE` expression as a whole has a known output type. Some other
constructs, such as `ARRAY[]` and the `GREATEST` and `LEAST` functions,
likewise require determination of a common type for several subexpressions.

The system catalogs store information about which conversions, or _casts_ ,
exist between which data types, and how to perform those conversions.
Additional casts can be added by the user with the [CREATE CAST](sql-
createcast.html "CREATE CAST") command. (This is usually done in conjunction
with defining new data types. The set of casts between built-in types has been
carefully crafted and is best not altered.)

An additional heuristic provided by the parser allows improved determination
of the proper casting behavior among groups of types that have implicit casts.
Data types are divided into several basic _type categories_ , including
`boolean`, `numeric`, `string`, `bitstring`, `datetime`, `timespan`,
`geometric`, `network`, and user-defined. (For a list see [Table
53.65](catalog-pg-type.html#CATALOG-TYPCATEGORY-TABLE
"Table 53.65. typcategory Codes"); but note it is also possible to create
custom type categories.) Within each category there can be one or more
_preferred types_ , which are preferred when there is a choice of possible
types. With careful selection of preferred types and available implicit casts,
it is possible to ensure that ambiguous expressions (those with multiple
candidate parsing solutions) can be resolved in a useful way.

All type conversion rules are designed with several principles in mind:

  * Implicit conversions should never have surprising or unpredictable outcomes.

  * There should be no extra overhead in the parser or executor if a query does not need implicit type conversion. That is, if a query is well-formed and the types already match, then the query should execute without spending extra time in the parser and without introducing unnecessary implicit conversion calls in the query.

  * Additionally, if a query usually requires an implicit conversion for a function, and if then the user defines a new function with the correct argument types, the parser should use this new function and no longer do implicit conversion to use the old function.

* * *

[Prev](typeconv.html "Chapter 10. Type Conversion")  | [Up](typeconv.html "Chapter 10. Type Conversion") |  [Next](typeconv-oper.html "10.2. Operators")  
---|---|---  
Chapter 10. Type Conversion  | [Home](index.html "PostgreSQL 16.9 Documentation") |  10.2. Operators  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/typeconv-overview.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

