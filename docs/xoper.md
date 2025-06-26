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

Supported Versions: [Current](/docs/current/xoper.html "PostgreSQL 17 -
38.14. User-Defined Operators") ([17](/docs/17/xoper.html "PostgreSQL 17 -
38.14. User-Defined Operators")) / [16](/docs/16/xoper.html "PostgreSQL 16 -
38.14. User-Defined Operators") / [15](/docs/15/xoper.html "PostgreSQL 15 -
38.14. User-Defined Operators") / [14](/docs/14/xoper.html "PostgreSQL 14 -
38.14. User-Defined Operators") / [13](/docs/13/xoper.html "PostgreSQL 13 -
38.14. User-Defined Operators")

Development Versions: [18](/docs/18/xoper.html "PostgreSQL 18 - 38.14. User-
Defined Operators") / [devel](/docs/devel/xoper.html "PostgreSQL devel -
38.14. User-Defined Operators")

Unsupported versions: [12](/docs/12/xoper.html "PostgreSQL 12 - 38.14. User-
Defined Operators") / [11](/docs/11/xoper.html "PostgreSQL 11 - 38.14. User-
Defined Operators") / [10](/docs/10/xoper.html "PostgreSQL 10 - 38.14. User-
Defined Operators") / [9.6](/docs/9.6/xoper.html "PostgreSQL 9.6 -
38.14. User-Defined Operators") / [9.5](/docs/9.5/xoper.html "PostgreSQL 9.5 -
38.14. User-Defined Operators") / [9.4](/docs/9.4/xoper.html "PostgreSQL 9.4 -
38.14. User-Defined Operators") / [9.3](/docs/9.3/xoper.html "PostgreSQL 9.3 -
38.14. User-Defined Operators") / [9.2](/docs/9.2/xoper.html "PostgreSQL 9.2 -
38.14. User-Defined Operators") / [9.1](/docs/9.1/xoper.html "PostgreSQL 9.1 -
38.14. User-Defined Operators") / [9.0](/docs/9.0/xoper.html "PostgreSQL 9.0 -
38.14. User-Defined Operators") / [8.4](/docs/8.4/xoper.html "PostgreSQL 8.4 -
38.14. User-Defined Operators") / [8.3](/docs/8.3/xoper.html "PostgreSQL 8.3 -
38.14. User-Defined Operators") / [8.2](/docs/8.2/xoper.html "PostgreSQL 8.2 -
38.14. User-Defined Operators") / [8.1](/docs/8.1/xoper.html "PostgreSQL 8.1 -
38.14. User-Defined Operators") / [8.0](/docs/8.0/xoper.html "PostgreSQL 8.0 -
38.14. User-Defined Operators") / [7.4](/docs/7.4/xoper.html "PostgreSQL 7.4 -
38.14. User-Defined Operators") / [7.3](/docs/7.3/xoper.html "PostgreSQL 7.3 -
38.14. User-Defined Operators") / [7.2](/docs/7.2/xoper.html "PostgreSQL 7.2 -
38.14. User-Defined Operators") / [7.1](/docs/7.1/xoper.html "PostgreSQL 7.1 -
38.14. User-Defined Operators")

__

38.14. User-Defined Operators  
---  
[Prev](xtypes.html "38.13. User-Defined Types")  | [Up](extend.html "Chapter 38. Extending SQL") | Chapter 38. Extending SQL | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](xoper-optimization.html "38.15. Operator Optimization Information")  
  
* * *

## 38.14. User-Defined Operators #

Every operator is “syntactic sugar” for a call to an underlying function that
does the real work; so you must first create the underlying function before
you can create the operator. However, an operator is _not merely_ syntactic
sugar, because it carries additional information that helps the query planner
optimize queries that use the operator. The next section will be devoted to
explaining that additional information.

PostgreSQL supports prefix and infix operators. Operators can be overloaded;
that is, the same operator name can be used for different operators that have
different numbers and types of operands. When a query is executed, the system
determines the operator to call from the number and types of the provided
operands.

Here is an example of creating an operator for adding two complex numbers. We
assume we've already created the definition of type `complex` (see [Section
38.13](xtypes.html "38.13. User-Defined Types")). First we need a function
that does the work, then we can define the operator:

    
    
    CREATE FUNCTION complex_add(complex, complex)
        RETURNS complex
        AS '_filename_ ', 'complex_add'
        LANGUAGE C IMMUTABLE STRICT;
    
    CREATE OPERATOR + (
        leftarg = complex,
        rightarg = complex,
        function = complex_add,
        commutator = +
    );
    

Now we could execute a query like this:

    
    
    SELECT (a + b) AS c FROM test_complex;
    
            c
    -----------------
     (5.2,6.05)
     (133.42,144.95)
    

We've shown how to create a binary operator here. To create a prefix operator,
just omit the `leftarg`. The `function` clause and the argument clauses are
the only required items in `CREATE OPERATOR`. The `commutator` clause shown in
the example is an optional hint to the query optimizer. Further details about
`commutator` and other optimizer hints appear in the next section.

* * *

[Prev](xtypes.html "38.13. User-Defined Types")  | [Up](extend.html "Chapter 38. Extending SQL") |  [Next](xoper-optimization.html "38.15. Operator Optimization Information")  
---|---|---  
38.13. User-Defined Types  | [Home](index.html "PostgreSQL 16.9 Documentation") |  38.15. Operator Optimization Information  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/xoper.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

