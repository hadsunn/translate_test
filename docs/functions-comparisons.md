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

Supported Versions: [Current](/docs/current/functions-comparisons.html
"PostgreSQL 17 - 9.24. Row and Array Comparisons") ([17](/docs/17/functions-
comparisons.html "PostgreSQL 17 - 9.24. Row and Array Comparisons")) /
[16](/docs/16/functions-comparisons.html "PostgreSQL 16 - 9.24. Row and Array
Comparisons") / [15](/docs/15/functions-comparisons.html "PostgreSQL 15 -
9.24. Row and Array Comparisons") / [14](/docs/14/functions-comparisons.html
"PostgreSQL 14 - 9.24. Row and Array Comparisons") / [13](/docs/13/functions-
comparisons.html "PostgreSQL 13 - 9.24. Row and Array Comparisons")

Development Versions: [18](/docs/18/functions-comparisons.html "PostgreSQL 18
- 9.24. Row and Array Comparisons") / [devel](/docs/devel/functions-
comparisons.html "PostgreSQL devel - 9.24. Row and Array Comparisons")

Unsupported versions: [12](/docs/12/functions-comparisons.html "PostgreSQL 12
- 9.24. Row and Array Comparisons") / [11](/docs/11/functions-comparisons.html
"PostgreSQL 11 - 9.24. Row and Array Comparisons") / [10](/docs/10/functions-
comparisons.html "PostgreSQL 10 - 9.24. Row and Array Comparisons") /
[9.6](/docs/9.6/functions-comparisons.html "PostgreSQL 9.6 - 9.24. Row and
Array Comparisons") / [9.5](/docs/9.5/functions-comparisons.html "PostgreSQL
9.5 - 9.24. Row and Array Comparisons") / [9.4](/docs/9.4/functions-
comparisons.html "PostgreSQL 9.4 - 9.24. Row and Array Comparisons") /
[9.3](/docs/9.3/functions-comparisons.html "PostgreSQL 9.3 - 9.24. Row and
Array Comparisons") / [9.2](/docs/9.2/functions-comparisons.html "PostgreSQL
9.2 - 9.24. Row and Array Comparisons") / [9.1](/docs/9.1/functions-
comparisons.html "PostgreSQL 9.1 - 9.24. Row and Array Comparisons") /
[9.0](/docs/9.0/functions-comparisons.html "PostgreSQL 9.0 - 9.24. Row and
Array Comparisons") / [8.4](/docs/8.4/functions-comparisons.html "PostgreSQL
8.4 - 9.24. Row and Array Comparisons") / [8.3](/docs/8.3/functions-
comparisons.html "PostgreSQL 8.3 - 9.24. Row and Array Comparisons") /
[8.2](/docs/8.2/functions-comparisons.html "PostgreSQL 8.2 - 9.24. Row and
Array Comparisons") / [8.1](/docs/8.1/functions-comparisons.html "PostgreSQL
8.1 - 9.24. Row and Array Comparisons") / [8.0](/docs/8.0/functions-
comparisons.html "PostgreSQL 8.0 - 9.24. Row and Array Comparisons") /
[7.4](/docs/7.4/functions-comparisons.html "PostgreSQL 7.4 - 9.24. Row and
Array Comparisons")

__

9.24. Row and Array Comparisons  
---  
[Prev](functions-subquery.html "9.23. Subquery Expressions")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions-srf.html "9.25. Set Returning Functions")  
  
* * *

## 9.24. Row and Array Comparisons #

[9.24.1. `IN`](functions-comparisons.html#FUNCTIONS-COMPARISONS-IN-SCALAR)

[9.24.2. `NOT IN`](functions-comparisons.html#FUNCTIONS-COMPARISONS-NOT-IN)

[9.24.3. `ANY`/`SOME` (array)](functions-comparisons.html#FUNCTIONS-
COMPARISONS-ANY-SOME)

[9.24.4. `ALL` (array)](functions-comparisons.html#FUNCTIONS-COMPARISONS-ALL)

[9.24.5. Row Constructor Comparison](functions-comparisons.html#ROW-WISE-
COMPARISON)

[9.24.6. Composite Type Comparison](functions-comparisons.html#COMPOSITE-TYPE-
COMPARISON)

This section describes several specialized constructs for making multiple
comparisons between groups of values. These forms are syntactically related to
the subquery forms of the previous section, but do not involve subqueries. The
forms involving array subexpressions are PostgreSQL extensions; the rest are
SQL-compliant. All of the expression forms documented in this section return
Boolean (true/false) results.

### 9.24.1. `IN` #

    
    
    _expression_ IN (_value_ [, ...])
    

The right-hand side is a parenthesized list of expressions. The result is
“true” if the left-hand expression's result is equal to any of the right-hand
expressions. This is a shorthand notation for

    
    
    _expression_ = _value1_
    OR
    _expression_ = _value2_
    OR
    ...
    

Note that if the left-hand expression yields null, or if there are no equal
right-hand values and at least one right-hand expression yields null, the
result of the `IN` construct will be null, not false. This is in accordance
with SQL's normal rules for Boolean combinations of null values.

### 9.24.2. `NOT IN` #

    
    
    _expression_ NOT IN (_value_ [, ...])
    

The right-hand side is a parenthesized list of expressions. The result is
“true” if the left-hand expression's result is unequal to all of the right-
hand expressions. This is a shorthand notation for

    
    
    _expression_ <> _value1_
    AND
    _expression_ <> _value2_
    AND
    ...
    

Note that if the left-hand expression yields null, or if there are no equal
right-hand values and at least one right-hand expression yields null, the
result of the `NOT IN` construct will be null, not true as one might naively
expect. This is in accordance with SQL's normal rules for Boolean combinations
of null values.

### Tip

`x NOT IN y` is equivalent to `NOT (x IN y)` in all cases. However, null
values are much more likely to trip up the novice when working with `NOT IN`
than when working with `IN`. It is best to express your condition positively
if possible.

### 9.24.3. `ANY`/`SOME` (array) #

    
    
    _expression_ _operator_ ANY (_array expression_)
    _expression_ _operator_ SOME (_array expression_)
    

The right-hand side is a parenthesized expression, which must yield an array
value. The left-hand expression is evaluated and compared to each element of
the array using the given _`operator`_ , which must yield a Boolean result.
The result of `ANY` is “true” if any true result is obtained. The result is
“false” if no true result is found (including the case where the array has
zero elements).

If the array expression yields a null array, the result of `ANY` will be null.
If the left-hand expression yields null, the result of `ANY` is ordinarily
null (though a non-strict comparison operator could possibly yield a different
result). Also, if the right-hand array contains any null elements and no true
comparison result is obtained, the result of `ANY` will be null, not false
(again, assuming a strict comparison operator). This is in accordance with
SQL's normal rules for Boolean combinations of null values.

`SOME` is a synonym for `ANY`.

### 9.24.4. `ALL` (array) #

    
    
    _expression_ _operator_ ALL (_array expression_)
    

The right-hand side is a parenthesized expression, which must yield an array
value. The left-hand expression is evaluated and compared to each element of
the array using the given _`operator`_ , which must yield a Boolean result.
The result of `ALL` is “true” if all comparisons yield true (including the
case where the array has zero elements). The result is “false” if any false
result is found.

If the array expression yields a null array, the result of `ALL` will be null.
If the left-hand expression yields null, the result of `ALL` is ordinarily
null (though a non-strict comparison operator could possibly yield a different
result). Also, if the right-hand array contains any null elements and no false
comparison result is obtained, the result of `ALL` will be null, not true
(again, assuming a strict comparison operator). This is in accordance with
SQL's normal rules for Boolean combinations of null values.

### 9.24.5. Row Constructor Comparison #

    
    
    _row_constructor_ _operator_ _row_constructor_
    

Each side is a row constructor, as described in [Section 4.2.13](sql-
expressions.html#SQL-SYNTAX-ROW-CONSTRUCTORS "4.2.13. Row Constructors"). The
two row constructors must have the same number of fields. The given
_`operator`_ is applied to each pair of corresponding fields. (Since the
fields could be of different types, this means that a different specific
operator could be selected for each pair.) All the selected operators must be
members of some B-tree operator class, or be the negator of an `=` member of a
B-tree operator class, meaning that row constructor comparison is only
possible when the _`operator`_ is `=`, `<>`, `<`, `<=`, `>`, or `>=`, or has
semantics similar to one of these.

The `=` and `<>` cases work slightly differently from the others. Two rows are
considered equal if all their corresponding members are non-null and equal;
the rows are unequal if any corresponding members are non-null and unequal;
otherwise the result of the row comparison is unknown (null).

For the `<`, `<=`, `>` and `>=` cases, the row elements are compared left-to-
right, stopping as soon as an unequal or null pair of elements is found. If
either of this pair of elements is null, the result of the row comparison is
unknown (null); otherwise comparison of this pair of elements determines the
result. For example, `ROW(1,2,NULL) < ROW(1,3,0)` yields true, not null,
because the third pair of elements are not considered.

    
    
    _row_constructor_ IS DISTINCT FROM _row_constructor_
    

This construct is similar to a `<>` row comparison, but it does not yield null
for null inputs. Instead, any null value is considered unequal to (distinct
from) any non-null value, and any two nulls are considered equal (not
distinct). Thus the result will either be true or false, never null.

    
    
    _row_constructor_ IS NOT DISTINCT FROM _row_constructor_
    

This construct is similar to a `=` row comparison, but it does not yield null
for null inputs. Instead, any null value is considered unequal to (distinct
from) any non-null value, and any two nulls are considered equal (not
distinct). Thus the result will always be either true or false, never null.

### 9.24.6. Composite Type Comparison #

    
    
    _record_ _operator_ _record_
    

The SQL specification requires row-wise comparison to return NULL if the
result depends on comparing two NULL values or a NULL and a non-NULL.
PostgreSQL does this only when comparing the results of two row constructors
(as in [Section 9.24.5](functions-comparisons.html#ROW-WISE-COMPARISON
"9.24.5. Row Constructor Comparison")) or comparing a row constructor to the
output of a subquery (as in [Section 9.23](functions-subquery.html
"9.23. Subquery Expressions")). In other contexts where two composite-type
values are compared, two NULL field values are considered equal, and a NULL is
considered larger than a non-NULL. This is necessary in order to have
consistent sorting and indexing behavior for composite types.

Each side is evaluated and they are compared row-wise. Composite type
comparisons are allowed when the _`operator`_ is `=`, `<>`, `<`, `<=`, `>` or
`>=`, or has semantics similar to one of these. (To be specific, an operator
can be a row comparison operator if it is a member of a B-tree operator class,
or is the negator of the `=` member of a B-tree operator class.) The default
behavior of the above operators is the same as for `IS [ NOT ] DISTINCT FROM`
for row constructors (see [Section 9.24.5](functions-comparisons.html#ROW-
WISE-COMPARISON "9.24.5. Row Constructor Comparison")).

To support matching of rows which include elements without a default B-tree
operator class, the following operators are defined for composite type
comparison: `*=`, `*<>`, `*<`, `*<=`, `*>`, and `*>=`. These operators compare
the internal binary representation of the two rows. Two rows might have a
different binary representation even though comparisons of the two rows with
the equality operator is true. The ordering of rows under these comparison
operators is deterministic but not otherwise meaningful. These operators are
used internally for materialized views and might be useful for other
specialized purposes such as replication and B-Tree deduplication (see
[Section 67.4.3](btree-implementation.html#BTREE-DEDUPLICATION
"67.4.3. Deduplication")). They are not intended to be generally useful for
writing queries, though.

* * *

[Prev](functions-subquery.html "9.23. Subquery Expressions")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](functions-srf.html "9.25. Set Returning Functions")  
---|---|---  
9.23. Subquery Expressions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  9.25. Set Returning Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-comparisons.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

