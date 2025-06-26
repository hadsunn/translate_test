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

Supported Versions: [Current](/docs/current/functions-conditional.html
"PostgreSQL 17 - 9.18. Conditional Expressions") ([17](/docs/17/functions-
conditional.html "PostgreSQL 17 - 9.18. Conditional Expressions")) /
[16](/docs/16/functions-conditional.html "PostgreSQL 16 - 9.18. Conditional
Expressions") / [15](/docs/15/functions-conditional.html "PostgreSQL 15 -
9.18. Conditional Expressions") / [14](/docs/14/functions-conditional.html
"PostgreSQL 14 - 9.18. Conditional Expressions") / [13](/docs/13/functions-
conditional.html "PostgreSQL 13 - 9.18. Conditional Expressions")

Development Versions: [18](/docs/18/functions-conditional.html "PostgreSQL 18
- 9.18. Conditional Expressions") / [devel](/docs/devel/functions-
conditional.html "PostgreSQL devel - 9.18. Conditional Expressions")

Unsupported versions: [12](/docs/12/functions-conditional.html "PostgreSQL 12
- 9.18. Conditional Expressions") / [11](/docs/11/functions-conditional.html
"PostgreSQL 11 - 9.18. Conditional Expressions") / [10](/docs/10/functions-
conditional.html "PostgreSQL 10 - 9.18. Conditional Expressions") /
[9.6](/docs/9.6/functions-conditional.html "PostgreSQL 9.6 - 9.18. Conditional
Expressions") / [9.5](/docs/9.5/functions-conditional.html "PostgreSQL 9.5 -
9.18. Conditional Expressions") / [9.4](/docs/9.4/functions-conditional.html
"PostgreSQL 9.4 - 9.18. Conditional Expressions") / [9.3](/docs/9.3/functions-
conditional.html "PostgreSQL 9.3 - 9.18. Conditional Expressions") /
[9.2](/docs/9.2/functions-conditional.html "PostgreSQL 9.2 - 9.18. Conditional
Expressions") / [9.1](/docs/9.1/functions-conditional.html "PostgreSQL 9.1 -
9.18. Conditional Expressions") / [9.0](/docs/9.0/functions-conditional.html
"PostgreSQL 9.0 - 9.18. Conditional Expressions") / [8.4](/docs/8.4/functions-
conditional.html "PostgreSQL 8.4 - 9.18. Conditional Expressions") /
[8.3](/docs/8.3/functions-conditional.html "PostgreSQL 8.3 - 9.18. Conditional
Expressions") / [8.2](/docs/8.2/functions-conditional.html "PostgreSQL 8.2 -
9.18. Conditional Expressions") / [8.1](/docs/8.1/functions-conditional.html
"PostgreSQL 8.1 - 9.18. Conditional Expressions") / [8.0](/docs/8.0/functions-
conditional.html "PostgreSQL 8.0 - 9.18. Conditional Expressions") /
[7.4](/docs/7.4/functions-conditional.html "PostgreSQL 7.4 - 9.18. Conditional
Expressions") / [7.3](/docs/7.3/functions-conditional.html "PostgreSQL 7.3 -
9.18. Conditional Expressions") / [7.2](/docs/7.2/functions-conditional.html
"PostgreSQL 7.2 - 9.18. Conditional Expressions") / [7.1](/docs/7.1/functions-
conditional.html "PostgreSQL 7.1 - 9.18. Conditional Expressions")

__

9.18. Conditional Expressions  
---  
[Prev](functions-sequence.html "9.17. Sequence Manipulation Functions")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions-array.html "9.19. Array Functions and Operators")  
  
* * *

## 9.18. Conditional Expressions #

[9.18.1. `CASE`](functions-conditional.html#FUNCTIONS-CASE)

[9.18.2. `COALESCE`](functions-conditional.html#FUNCTIONS-COALESCE-NVL-IFNULL)

[9.18.3. `NULLIF`](functions-conditional.html#FUNCTIONS-NULLIF)

[9.18.4. `GREATEST` and `LEAST`](functions-conditional.html#FUNCTIONS-
GREATEST-LEAST)

This section describes the SQL-compliant conditional expressions available in
PostgreSQL.

### Tip

If your needs go beyond the capabilities of these conditional expressions, you
might want to consider writing a server-side function in a more expressive
programming language.

### Note

Although `COALESCE`, `GREATEST`, and `LEAST` are syntactically similar to
functions, they are not ordinary functions, and thus cannot be used with
explicit `VARIADIC` array arguments.

### 9.18.1. `CASE` #

The SQL `CASE` expression is a generic conditional expression, similar to
if/else statements in other programming languages:

    
    
    CASE WHEN _condition_ THEN _result_
         [WHEN ...]
         [ELSE _result_]
    END
    

`CASE` clauses can be used wherever an expression is valid. Each _`condition`_
is an expression that returns a `boolean` result. If the condition's result is
true, the value of the `CASE` expression is the _`result`_ that follows the
condition, and the remainder of the `CASE` expression is not processed. If the
condition's result is not true, any subsequent `WHEN` clauses are examined in
the same manner. If no `WHEN` _`condition`_ yields true, the value of the
`CASE` expression is the _`result`_ of the `ELSE` clause. If the `ELSE` clause
is omitted and no condition is true, the result is null.

An example:

    
    
    SELECT * FROM test;
    
     a
    ---
     1
     2
     3
    
    
    SELECT a,
           CASE WHEN a=1 THEN 'one'
                WHEN a=2 THEN 'two'
                ELSE 'other'
           END
        FROM test;
    
     a | case
    ---+-------
     1 | one
     2 | two
     3 | other
    

The data types of all the _`result`_ expressions must be convertible to a
single output type. See [Section 10.5](typeconv-union-case.html "10.5. UNION,
CASE, and Related Constructs") for more details.

There is a “simple” form of `CASE` expression that is a variant of the general
form above:

    
    
    CASE _expression_
        WHEN _value_ THEN _result_
        [WHEN ...]
        [ELSE _result_]
    END
    

The first _`expression`_ is computed, then compared to each of the _`value`_
expressions in the `WHEN` clauses until one is found that is equal to it. If
no match is found, the _`result`_ of the `ELSE` clause (or a null value) is
returned. This is similar to the `switch` statement in C.

The example above can be written using the simple `CASE` syntax:

    
    
    SELECT a,
           CASE a WHEN 1 THEN 'one'
                  WHEN 2 THEN 'two'
                  ELSE 'other'
           END
        FROM test;
    
     a | case
    ---+-------
     1 | one
     2 | two
     3 | other
    

A `CASE` expression does not evaluate any subexpressions that are not needed
to determine the result. For example, this is a possible way of avoiding a
division-by-zero failure:

    
    
    SELECT ... WHERE CASE WHEN x <> 0 THEN y/x > 1.5 ELSE false END;
    

### Note

As described in [Section 4.2.14](sql-expressions.html#SYNTAX-EXPRESS-EVAL
"4.2.14. Expression Evaluation Rules"), there are various situations in which
subexpressions of an expression are evaluated at different times, so that the
principle that “`CASE` evaluates only necessary subexpressions” is not
ironclad. For example a constant `1/0` subexpression will usually result in a
division-by-zero failure at planning time, even if it's within a `CASE` arm
that would never be entered at run time.

### 9.18.2. `COALESCE` #

    
    
    COALESCE(_value_ [, ...])
    

The `COALESCE` function returns the first of its arguments that is not null.
Null is returned only if all arguments are null. It is often used to
substitute a default value for null values when data is retrieved for display,
for example:

    
    
    SELECT COALESCE(description, short_description, '(none)') ...
    

This returns `description` if it is not null, otherwise `short_description` if
it is not null, otherwise `(none)`.

The arguments must all be convertible to a common data type, which will be the
type of the result (see [Section 10.5](typeconv-union-case.html "10.5. UNION,
CASE, and Related Constructs") for details).

Like a `CASE` expression, `COALESCE` only evaluates the arguments that are
needed to determine the result; that is, arguments to the right of the first
non-null argument are not evaluated. This SQL-standard function provides
capabilities similar to `NVL` and `IFNULL`, which are used in some other
database systems.

### 9.18.3. `NULLIF` #

    
    
    NULLIF(_value1_ , _value2_)
    

The `NULLIF` function returns a null value if _`value1`_ equals _`value2`_ ;
otherwise it returns _`value1`_. This can be used to perform the inverse
operation of the `COALESCE` example given above:

    
    
    SELECT NULLIF(value, '(none)') ...
    

In this example, if `value` is `(none)`, null is returned, otherwise the value
of `value` is returned.

The two arguments must be of comparable types. To be specific, they are
compared exactly as if you had written `_`value1`_ = _`value2`_`, so there
must be a suitable `=` operator available.

The result has the same type as the first argument — but there is a subtlety.
What is actually returned is the first argument of the implied `=` operator,
and in some cases that will have been promoted to match the second argument's
type. For example, `NULLIF(1, 2.2)` yields `numeric`, because there is no
`integer` `=` `numeric` operator, only `numeric` `=` `numeric`.

### 9.18.4. `GREATEST` and `LEAST` #

    
    
    GREATEST(_value_ [, ...])
    
    
    
    LEAST(_value_ [, ...])
    

The `GREATEST` and `LEAST` functions select the largest or smallest value from
a list of any number of expressions. The expressions must all be convertible
to a common data type, which will be the type of the result (see [Section
10.5](typeconv-union-case.html "10.5. UNION, CASE, and Related Constructs")
for details).

NULL values in the argument list are ignored. The result will be NULL only if
all the expressions evaluate to NULL. (This is a deviation from the SQL
standard. According to the standard, the return value is NULL if any argument
is NULL. Some other databases behave this way.)

* * *

[Prev](functions-sequence.html "9.17. Sequence Manipulation Functions")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](functions-array.html "9.19. Array Functions and Operators")  
---|---|---  
9.17. Sequence Manipulation Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  9.19. Array Functions and Operators  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-conditional.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

