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

Supported Versions: [Current](/docs/current/functions-comparison.html
"PostgreSQL 17 - 9.2. Comparison Functions and Operators")
([17](/docs/17/functions-comparison.html "PostgreSQL 17 - 9.2. Comparison
Functions and Operators")) / [16](/docs/16/functions-comparison.html
"PostgreSQL 16 - 9.2. Comparison Functions and Operators") /
[15](/docs/15/functions-comparison.html "PostgreSQL 15 - 9.2. Comparison
Functions and Operators") / [14](/docs/14/functions-comparison.html
"PostgreSQL 14 - 9.2. Comparison Functions and Operators") /
[13](/docs/13/functions-comparison.html "PostgreSQL 13 - 9.2. Comparison
Functions and Operators")

Development Versions: [18](/docs/18/functions-comparison.html "PostgreSQL 18 -
9.2. Comparison Functions and Operators") / [devel](/docs/devel/functions-
comparison.html "PostgreSQL devel - 9.2. Comparison Functions and Operators")

Unsupported versions: [12](/docs/12/functions-comparison.html "PostgreSQL 12 -
9.2. Comparison Functions and Operators") / [11](/docs/11/functions-
comparison.html "PostgreSQL 11 - 9.2. Comparison Functions and Operators") /
[10](/docs/10/functions-comparison.html "PostgreSQL 10 - 9.2. Comparison
Functions and Operators") / [9.6](/docs/9.6/functions-comparison.html
"PostgreSQL 9.6 - 9.2. Comparison Functions and Operators") /
[9.5](/docs/9.5/functions-comparison.html "PostgreSQL 9.5 - 9.2. Comparison
Functions and Operators") / [9.4](/docs/9.4/functions-comparison.html
"PostgreSQL 9.4 - 9.2. Comparison Functions and Operators") /
[9.3](/docs/9.3/functions-comparison.html "PostgreSQL 9.3 - 9.2. Comparison
Functions and Operators") / [9.2](/docs/9.2/functions-comparison.html
"PostgreSQL 9.2 - 9.2. Comparison Functions and Operators") /
[9.1](/docs/9.1/functions-comparison.html "PostgreSQL 9.1 - 9.2. Comparison
Functions and Operators") / [9.0](/docs/9.0/functions-comparison.html
"PostgreSQL 9.0 - 9.2. Comparison Functions and Operators") /
[8.4](/docs/8.4/functions-comparison.html "PostgreSQL 8.4 - 9.2. Comparison
Functions and Operators") / [8.3](/docs/8.3/functions-comparison.html
"PostgreSQL 8.3 - 9.2. Comparison Functions and Operators") /
[8.2](/docs/8.2/functions-comparison.html "PostgreSQL 8.2 - 9.2. Comparison
Functions and Operators") / [8.1](/docs/8.1/functions-comparison.html
"PostgreSQL 8.1 - 9.2. Comparison Functions and Operators") /
[8.0](/docs/8.0/functions-comparison.html "PostgreSQL 8.0 - 9.2. Comparison
Functions and Operators") / [7.4](/docs/7.4/functions-comparison.html
"PostgreSQL 7.4 - 9.2. Comparison Functions and Operators") /
[7.3](/docs/7.3/functions-comparison.html "PostgreSQL 7.3 - 9.2. Comparison
Functions and Operators") / [7.2](/docs/7.2/functions-comparison.html
"PostgreSQL 7.2 - 9.2. Comparison Functions and Operators") /
[7.1](/docs/7.1/functions-comparison.html "PostgreSQL 7.1 - 9.2. Comparison
Functions and Operators")

__

9.2. Comparison Functions and Operators  
---  
[Prev](functions-logical.html "9.1. Logical Operators")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions-math.html "9.3. Mathematical Functions and Operators")  
  
* * *

## 9.2. Comparison Functions and Operators #

The usual comparison operators are available, as shown in [Table
9.1](functions-comparison.html#FUNCTIONS-COMPARISON-OP-TABLE
"Table 9.1. Comparison Operators").

**Table  9.1. Comparison Operators**

Operator | Description  
---|---  
_`datatype`_ `<` _`datatype`_ → `boolean` | Less than  
_`datatype`_ `>` _`datatype`_ → `boolean` | Greater than  
_`datatype`_ `<=` _`datatype`_ → `boolean` | Less than or equal to  
_`datatype`_ `>=` _`datatype`_ → `boolean` | Greater than or equal to  
_`datatype`_ `=` _`datatype`_ → `boolean` | Equal  
_`datatype`_ `<>` _`datatype`_ → `boolean` | Not equal  
_`datatype`_ `!=` _`datatype`_ → `boolean` | Not equal  
  
  

### Note

`<>` is the standard SQL notation for “not equal”. `!=` is an alias, which is
converted to `<>` at a very early stage of parsing. Hence, it is not possible
to implement `!=` and `<>` operators that do different things.

These comparison operators are available for all built-in data types that have
a natural ordering, including numeric, string, and date/time types. In
addition, arrays, composite types, and ranges can be compared if their
component data types are comparable.

It is usually possible to compare values of related data types as well; for
example `integer` `>` `bigint` will work. Some cases of this sort are
implemented directly by “cross-type” comparison operators, but if no such
operator is available, the parser will coerce the less-general type to the
more-general type and apply the latter's comparison operator.

As shown above, all comparison operators are binary operators that return
values of type `boolean`. Thus, expressions like `1 < 2 < 3` are not valid
(because there is no `<` operator to compare a Boolean value with `3`). Use
the `BETWEEN` predicates shown below to perform range tests.

There are also some comparison predicates, as shown in [Table 9.2](functions-
comparison.html#FUNCTIONS-COMPARISON-PRED-TABLE "Table 9.2. Comparison
Predicates"). These behave much like operators, but have special syntax
mandated by the SQL standard.

**Table  9.2. Comparison Predicates**

Predicate Description Example(s)  
---  
_`datatype`_ `BETWEEN` _`datatype`_ `AND` _`datatype`_ → `boolean` Between
(inclusive of the range endpoints). `2 BETWEEN 1 AND 3` → `t` `2 BETWEEN 3 AND
1` → `f`  
_`datatype`_ `NOT BETWEEN` _`datatype`_ `AND` _`datatype`_ → `boolean` Not
between (the negation of `BETWEEN`). `2 NOT BETWEEN 1 AND 3` → `f`  
_`datatype`_ `BETWEEN SYMMETRIC` _`datatype`_ `AND` _`datatype`_ → `boolean`
Between, after sorting the two endpoint values. `2 BETWEEN SYMMETRIC 3 AND 1`
→ `t`  
_`datatype`_ `NOT BETWEEN SYMMETRIC` _`datatype`_ `AND` _`datatype`_ →
`boolean` Not between, after sorting the two endpoint values. `2 NOT BETWEEN
SYMMETRIC 3 AND 1` → `f`  
_`datatype`_ `IS DISTINCT FROM` _`datatype`_ → `boolean` Not equal, treating
null as a comparable value. `1 IS DISTINCT FROM NULL` → `t` (rather than
`NULL`) `NULL IS DISTINCT FROM NULL` → `f` (rather than `NULL`)  
_`datatype`_ `IS NOT DISTINCT FROM` _`datatype`_ → `boolean` Equal, treating
null as a comparable value. `1 IS NOT DISTINCT FROM NULL` → `f` (rather than
`NULL`) `NULL IS NOT DISTINCT FROM NULL` → `t` (rather than `NULL`)  
_`datatype`_ `IS NULL` → `boolean` Test whether value is null. `1.5 IS NULL` →
`f`  
_`datatype`_ `IS NOT NULL` → `boolean` Test whether value is not null. `'null'
IS NOT NULL` → `t`  
_`datatype`_ `ISNULL` → `boolean` Test whether value is null (nonstandard
syntax).  
_`datatype`_ `NOTNULL` → `boolean` Test whether value is not null (nonstandard
syntax).  
`boolean` `IS TRUE` → `boolean` Test whether boolean expression yields true.
`true IS TRUE` → `t` `NULL::boolean IS TRUE` → `f` (rather than `NULL`)  
`boolean` `IS NOT TRUE` → `boolean` Test whether boolean expression yields
false or unknown. `true IS NOT TRUE` → `f` `NULL::boolean IS NOT TRUE` → `t`
(rather than `NULL`)  
`boolean` `IS FALSE` → `boolean` Test whether boolean expression yields false.
`true IS FALSE` → `f` `NULL::boolean IS FALSE` → `f` (rather than `NULL`)  
`boolean` `IS NOT FALSE` → `boolean` Test whether boolean expression yields
true or unknown. `true IS NOT FALSE` → `t` `NULL::boolean IS NOT FALSE` → `t`
(rather than `NULL`)  
`boolean` `IS UNKNOWN` → `boolean` Test whether boolean expression yields
unknown. `true IS UNKNOWN` → `f` `NULL::boolean IS UNKNOWN` → `t` (rather than
`NULL`)  
`boolean` `IS NOT UNKNOWN` → `boolean` Test whether boolean expression yields
true or false. `true IS NOT UNKNOWN` → `t` `NULL::boolean IS NOT UNKNOWN` →
`f` (rather than `NULL`)  
  
  

The `BETWEEN` predicate simplifies range tests:

    
    
    _a_ BETWEEN _x_ AND _y_
    

is equivalent to

    
    
    _a_ >= _x_ AND _a_ <= _y_
    

Notice that `BETWEEN` treats the endpoint values as included in the range.
`BETWEEN SYMMETRIC` is like `BETWEEN` except there is no requirement that the
argument to the left of `AND` be less than or equal to the argument on the
right. If it is not, those two arguments are automatically swapped, so that a
nonempty range is always implied.

The various variants of `BETWEEN` are implemented in terms of the ordinary
comparison operators, and therefore will work for any data type(s) that can be
compared.

### Note

The use of `AND` in the `BETWEEN` syntax creates an ambiguity with the use of
`AND` as a logical operator. To resolve this, only a limited set of expression
types are allowed as the second argument of a `BETWEEN` clause. If you need to
write a more complex sub-expression in `BETWEEN`, write parentheses around the
sub-expression.

Ordinary comparison operators yield null (signifying “unknown”), not true or
false, when either input is null. For example, `7 = NULL` yields null, as does
`7 <> NULL`. When this behavior is not suitable, use the `IS [ NOT ] DISTINCT
FROM` predicates:

    
    
    _a_ IS DISTINCT FROM _b_
    _a_ IS NOT DISTINCT FROM _b_
    

For non-null inputs, `IS DISTINCT FROM` is the same as the `<>` operator.
However, if both inputs are null it returns false, and if only one input is
null it returns true. Similarly, `IS NOT DISTINCT FROM` is identical to `=`
for non-null inputs, but it returns true when both inputs are null, and false
when only one input is null. Thus, these predicates effectively act as though
null were a normal data value, rather than “unknown”.

To check whether a value is or is not null, use the predicates:

    
    
    _expression_ IS NULL
    _expression_ IS NOT NULL
    

or the equivalent, but nonstandard, predicates:

    
    
    _expression_ ISNULL
    _expression_ NOTNULL
    

Do _not_ write `_`expression`_ = NULL` because `NULL` is not “equal to”
`NULL`. (The null value represents an unknown value, and it is not known
whether two unknown values are equal.)

### Tip

Some applications might expect that `_`expression`_ = NULL` returns true if
_`expression`_ evaluates to the null value. It is highly recommended that
these applications be modified to comply with the SQL standard. However, if
that cannot be done the [transform_null_equals](runtime-config-
compatible.html#GUC-TRANSFORM-NULL-EQUALS) configuration variable is
available. If it is enabled, PostgreSQL will convert `x = NULL` clauses to `x
IS NULL`.

If the _`expression`_ is row-valued, then `IS NULL` is true when the row
expression itself is null or when all the row's fields are null, while `IS NOT
NULL` is true when the row expression itself is non-null and all the row's
fields are non-null. Because of this behavior, `IS NULL` and `IS NOT NULL` do
not always return inverse results for row-valued expressions; in particular, a
row-valued expression that contains both null and non-null fields will return
false for both tests. In some cases, it may be preferable to write _`row`_ `IS
DISTINCT FROM NULL` or _`row`_ `IS NOT DISTINCT FROM NULL`, which will simply
check whether the overall row value is null without any additional tests on
the row fields.

Boolean values can also be tested using the predicates

    
    
    _boolean_expression_ IS TRUE
    _boolean_expression_ IS NOT TRUE
    _boolean_expression_ IS FALSE
    _boolean_expression_ IS NOT FALSE
    _boolean_expression_ IS UNKNOWN
    _boolean_expression_ IS NOT UNKNOWN
    

These will always return true or false, never a null value, even when the
operand is null. A null input is treated as the logical value “unknown”.
Notice that `IS UNKNOWN` and `IS NOT UNKNOWN` are effectively the same as `IS
NULL` and `IS NOT NULL`, respectively, except that the input expression must
be of Boolean type.

Some comparison-related functions are also available, as shown in [Table
9.3](functions-comparison.html#FUNCTIONS-COMPARISON-FUNC-TABLE
"Table 9.3. Comparison Functions").

**Table  9.3. Comparison Functions**

Function Description Example(s)  
---  
`num_nonnulls` ( `VARIADIC` `"any"` ) → `integer` Returns the number of non-
null arguments. `num_nonnulls(1, NULL, 2)` → `2`  
`num_nulls` ( `VARIADIC` `"any"` ) → `integer` Returns the number of null
arguments. `num_nulls(1, NULL, 2)` → `1`  
  
  

* * *

[Prev](functions-logical.html "9.1. Logical Operators")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](functions-math.html "9.3. Mathematical Functions and Operators")  
---|---|---  
9.1. Logical Operators  | [Home](index.html "PostgreSQL 16.9 Documentation") |  9.3. Mathematical Functions and Operators  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-comparison.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

