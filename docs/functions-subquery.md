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

Supported Versions: [Current](/docs/current/functions-subquery.html
"PostgreSQL 17 - 9.23. Subquery Expressions") ([17](/docs/17/functions-
subquery.html "PostgreSQL 17 - 9.23. Subquery Expressions")) /
[16](/docs/16/functions-subquery.html "PostgreSQL 16 - 9.23. Subquery
Expressions") / [15](/docs/15/functions-subquery.html "PostgreSQL 15 -
9.23. Subquery Expressions") / [14](/docs/14/functions-subquery.html
"PostgreSQL 14 - 9.23. Subquery Expressions") / [13](/docs/13/functions-
subquery.html "PostgreSQL 13 - 9.23. Subquery Expressions")

Development Versions: [18](/docs/18/functions-subquery.html "PostgreSQL 18 -
9.23. Subquery Expressions") / [devel](/docs/devel/functions-subquery.html
"PostgreSQL devel - 9.23. Subquery Expressions")

Unsupported versions: [12](/docs/12/functions-subquery.html "PostgreSQL 12 -
9.23. Subquery Expressions") / [11](/docs/11/functions-subquery.html
"PostgreSQL 11 - 9.23. Subquery Expressions") / [10](/docs/10/functions-
subquery.html "PostgreSQL 10 - 9.23. Subquery Expressions") /
[9.6](/docs/9.6/functions-subquery.html "PostgreSQL 9.6 - 9.23. Subquery
Expressions") / [9.5](/docs/9.5/functions-subquery.html "PostgreSQL 9.5 -
9.23. Subquery Expressions") / [9.4](/docs/9.4/functions-subquery.html
"PostgreSQL 9.4 - 9.23. Subquery Expressions") / [9.3](/docs/9.3/functions-
subquery.html "PostgreSQL 9.3 - 9.23. Subquery Expressions") /
[9.2](/docs/9.2/functions-subquery.html "PostgreSQL 9.2 - 9.23. Subquery
Expressions") / [9.1](/docs/9.1/functions-subquery.html "PostgreSQL 9.1 -
9.23. Subquery Expressions") / [9.0](/docs/9.0/functions-subquery.html
"PostgreSQL 9.0 - 9.23. Subquery Expressions") / [8.4](/docs/8.4/functions-
subquery.html "PostgreSQL 8.4 - 9.23. Subquery Expressions") /
[8.3](/docs/8.3/functions-subquery.html "PostgreSQL 8.3 - 9.23. Subquery
Expressions") / [8.2](/docs/8.2/functions-subquery.html "PostgreSQL 8.2 -
9.23. Subquery Expressions") / [8.1](/docs/8.1/functions-subquery.html
"PostgreSQL 8.1 - 9.23. Subquery Expressions") / [8.0](/docs/8.0/functions-
subquery.html "PostgreSQL 8.0 - 9.23. Subquery Expressions") /
[7.4](/docs/7.4/functions-subquery.html "PostgreSQL 7.4 - 9.23. Subquery
Expressions") / [7.3](/docs/7.3/functions-subquery.html "PostgreSQL 7.3 -
9.23. Subquery Expressions") / [7.2](/docs/7.2/functions-subquery.html
"PostgreSQL 7.2 - 9.23. Subquery Expressions")

__

9.23. Subquery Expressions  
---  
[Prev](functions-window.html "9.22. Window Functions")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions-comparisons.html "9.24. Row and Array Comparisons")  
  
* * *

## 9.23. Subquery Expressions #

[9.23.1. `EXISTS`](functions-subquery.html#FUNCTIONS-SUBQUERY-EXISTS)

[9.23.2. `IN`](functions-subquery.html#FUNCTIONS-SUBQUERY-IN)

[9.23.3. `NOT IN`](functions-subquery.html#FUNCTIONS-SUBQUERY-NOTIN)

[9.23.4. `ANY`/`SOME`](functions-subquery.html#FUNCTIONS-SUBQUERY-ANY-SOME)

[9.23.5. `ALL`](functions-subquery.html#FUNCTIONS-SUBQUERY-ALL)

[9.23.6. Single-Row Comparison](functions-subquery.html#FUNCTIONS-SUBQUERY-
SINGLE-ROW-COMP)

This section describes the SQL-compliant subquery expressions available in
PostgreSQL. All of the expression forms documented in this section return
Boolean (true/false) results.

### 9.23.1. `EXISTS` #

    
    
    EXISTS (_subquery_)
    

The argument of `EXISTS` is an arbitrary `SELECT` statement, or _subquery_.
The subquery is evaluated to determine whether it returns any rows. If it
returns at least one row, the result of `EXISTS` is “true”; if the subquery
returns no rows, the result of `EXISTS` is “false”.

The subquery can refer to variables from the surrounding query, which will act
as constants during any one evaluation of the subquery.

The subquery will generally only be executed long enough to determine whether
at least one row is returned, not all the way to completion. It is unwise to
write a subquery that has side effects (such as calling sequence functions);
whether the side effects occur might be unpredictable.

Since the result depends only on whether any rows are returned, and not on the
contents of those rows, the output list of the subquery is normally
unimportant. A common coding convention is to write all `EXISTS` tests in the
form `EXISTS(SELECT 1 WHERE ...)`. There are exceptions to this rule however,
such as subqueries that use `INTERSECT`.

This simple example is like an inner join on `col2`, but it produces at most
one output row for each `tab1` row, even if there are several matching `tab2`
rows:

    
    
    SELECT col1
    FROM tab1
    WHERE EXISTS (SELECT 1 FROM tab2 WHERE col2 = tab1.col2);
    

### 9.23.2. `IN` #

    
    
    _expression_ IN (_subquery_)
    

The right-hand side is a parenthesized subquery, which must return exactly one
column. The left-hand expression is evaluated and compared to each row of the
subquery result. The result of `IN` is “true” if any equal subquery row is
found. The result is “false” if no equal row is found (including the case
where the subquery returns no rows).

Note that if the left-hand expression yields null, or if there are no equal
right-hand values and at least one right-hand row yields null, the result of
the `IN` construct will be null, not false. This is in accordance with SQL's
normal rules for Boolean combinations of null values.

As with `EXISTS`, it's unwise to assume that the subquery will be evaluated
completely.

    
    
    _row_constructor_ IN (_subquery_)
    

The left-hand side of this form of `IN` is a row constructor, as described in
[Section 4.2.13](sql-expressions.html#SQL-SYNTAX-ROW-CONSTRUCTORS "4.2.13. Row
Constructors"). The right-hand side is a parenthesized subquery, which must
return exactly as many columns as there are expressions in the left-hand row.
The left-hand expressions are evaluated and compared row-wise to each row of
the subquery result. The result of `IN` is “true” if any equal subquery row is
found. The result is “false” if no equal row is found (including the case
where the subquery returns no rows).

As usual, null values in the rows are combined per the normal rules of SQL
Boolean expressions. Two rows are considered equal if all their corresponding
members are non-null and equal; the rows are unequal if any corresponding
members are non-null and unequal; otherwise the result of that row comparison
is unknown (null). If all the per-row results are either unequal or null, with
at least one null, then the result of `IN` is null.

### 9.23.3. `NOT IN` #

    
    
    _expression_ NOT IN (_subquery_)
    

The right-hand side is a parenthesized subquery, which must return exactly one
column. The left-hand expression is evaluated and compared to each row of the
subquery result. The result of `NOT IN` is “true” if only unequal subquery
rows are found (including the case where the subquery returns no rows). The
result is “false” if any equal row is found.

Note that if the left-hand expression yields null, or if there are no equal
right-hand values and at least one right-hand row yields null, the result of
the `NOT IN` construct will be null, not true. This is in accordance with
SQL's normal rules for Boolean combinations of null values.

As with `EXISTS`, it's unwise to assume that the subquery will be evaluated
completely.

    
    
    _row_constructor_ NOT IN (_subquery_)
    

The left-hand side of this form of `NOT IN` is a row constructor, as described
in [Section 4.2.13](sql-expressions.html#SQL-SYNTAX-ROW-CONSTRUCTORS
"4.2.13. Row Constructors"). The right-hand side is a parenthesized subquery,
which must return exactly as many columns as there are expressions in the
left-hand row. The left-hand expressions are evaluated and compared row-wise
to each row of the subquery result. The result of `NOT IN` is “true” if only
unequal subquery rows are found (including the case where the subquery returns
no rows). The result is “false” if any equal row is found.

As usual, null values in the rows are combined per the normal rules of SQL
Boolean expressions. Two rows are considered equal if all their corresponding
members are non-null and equal; the rows are unequal if any corresponding
members are non-null and unequal; otherwise the result of that row comparison
is unknown (null). If all the per-row results are either unequal or null, with
at least one null, then the result of `NOT IN` is null.

### 9.23.4. `ANY`/`SOME` #

    
    
    _expression_ _operator_ ANY (_subquery_)
    _expression_ _operator_ SOME (_subquery_)
    

The right-hand side is a parenthesized subquery, which must return exactly one
column. The left-hand expression is evaluated and compared to each row of the
subquery result using the given _`operator`_ , which must yield a Boolean
result. The result of `ANY` is “true” if any true result is obtained. The
result is “false” if no true result is found (including the case where the
subquery returns no rows).

`SOME` is a synonym for `ANY`. `IN` is equivalent to `= ANY`.

Note that if there are no successes and at least one right-hand row yields
null for the operator's result, the result of the `ANY` construct will be
null, not false. This is in accordance with SQL's normal rules for Boolean
combinations of null values.

As with `EXISTS`, it's unwise to assume that the subquery will be evaluated
completely.

    
    
    _row_constructor_ _operator_ ANY (_subquery_)
    _row_constructor_ _operator_ SOME (_subquery_)
    

The left-hand side of this form of `ANY` is a row constructor, as described in
[Section 4.2.13](sql-expressions.html#SQL-SYNTAX-ROW-CONSTRUCTORS "4.2.13. Row
Constructors"). The right-hand side is a parenthesized subquery, which must
return exactly as many columns as there are expressions in the left-hand row.
The left-hand expressions are evaluated and compared row-wise to each row of
the subquery result, using the given _`operator`_. The result of `ANY` is
“true” if the comparison returns true for any subquery row. The result is
“false” if the comparison returns false for every subquery row (including the
case where the subquery returns no rows). The result is NULL if no comparison
with a subquery row returns true, and at least one comparison returns NULL.

See [Section 9.24.5](functions-comparisons.html#ROW-WISE-COMPARISON
"9.24.5. Row Constructor Comparison") for details about the meaning of a row
constructor comparison.

### 9.23.5. `ALL` #

    
    
    _expression_ _operator_ ALL (_subquery_)
    

The right-hand side is a parenthesized subquery, which must return exactly one
column. The left-hand expression is evaluated and compared to each row of the
subquery result using the given _`operator`_ , which must yield a Boolean
result. The result of `ALL` is “true” if all rows yield true (including the
case where the subquery returns no rows). The result is “false” if any false
result is found. The result is NULL if no comparison with a subquery row
returns false, and at least one comparison returns NULL.

`NOT IN` is equivalent to `<> ALL`.

As with `EXISTS`, it's unwise to assume that the subquery will be evaluated
completely.

    
    
    _row_constructor_ _operator_ ALL (_subquery_)
    

The left-hand side of this form of `ALL` is a row constructor, as described in
[Section 4.2.13](sql-expressions.html#SQL-SYNTAX-ROW-CONSTRUCTORS "4.2.13. Row
Constructors"). The right-hand side is a parenthesized subquery, which must
return exactly as many columns as there are expressions in the left-hand row.
The left-hand expressions are evaluated and compared row-wise to each row of
the subquery result, using the given _`operator`_. The result of `ALL` is
“true” if the comparison returns true for all subquery rows (including the
case where the subquery returns no rows). The result is “false” if the
comparison returns false for any subquery row. The result is NULL if no
comparison with a subquery row returns false, and at least one comparison
returns NULL.

See [Section 9.24.5](functions-comparisons.html#ROW-WISE-COMPARISON
"9.24.5. Row Constructor Comparison") for details about the meaning of a row
constructor comparison.

### 9.23.6. Single-Row Comparison #

    
    
    _row_constructor_ _operator_ (_subquery_)
    

The left-hand side is a row constructor, as described in [Section 4.2.13](sql-
expressions.html#SQL-SYNTAX-ROW-CONSTRUCTORS "4.2.13. Row Constructors"). The
right-hand side is a parenthesized subquery, which must return exactly as many
columns as there are expressions in the left-hand row. Furthermore, the
subquery cannot return more than one row. (If it returns zero rows, the result
is taken to be null.) The left-hand side is evaluated and compared row-wise to
the single subquery result row.

See [Section 9.24.5](functions-comparisons.html#ROW-WISE-COMPARISON
"9.24.5. Row Constructor Comparison") for details about the meaning of a row
constructor comparison.

* * *

[Prev](functions-window.html "9.22. Window Functions")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](functions-comparisons.html "9.24. Row and Array Comparisons")  
---|---|---  
9.22. Window Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  9.24. Row and Array Comparisons  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-subquery.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

