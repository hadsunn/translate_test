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

Supported Versions: [Current](/docs/current/queries-order.html "PostgreSQL 17
- 7.5. Sorting Rows \(ORDER BY\)") ([17](/docs/17/queries-order.html
"PostgreSQL 17 - 7.5. Sorting Rows \(ORDER BY\)")) / [16](/docs/16/queries-
order.html "PostgreSQL 16 - 7.5. Sorting Rows \(ORDER BY\)") /
[15](/docs/15/queries-order.html "PostgreSQL 15 - 7.5. Sorting Rows \(ORDER
BY\)") / [14](/docs/14/queries-order.html "PostgreSQL 14 - 7.5. Sorting Rows
\(ORDER BY\)") / [13](/docs/13/queries-order.html "PostgreSQL 13 -
7.5. Sorting Rows \(ORDER BY\)")

Development Versions: [18](/docs/18/queries-order.html "PostgreSQL 18 -
7.5. Sorting Rows \(ORDER BY\)") / [devel](/docs/devel/queries-order.html
"PostgreSQL devel - 7.5. Sorting Rows \(ORDER BY\)")

Unsupported versions: [12](/docs/12/queries-order.html "PostgreSQL 12 -
7.5. Sorting Rows \(ORDER BY\)") / [11](/docs/11/queries-order.html
"PostgreSQL 11 - 7.5. Sorting Rows \(ORDER BY\)") / [10](/docs/10/queries-
order.html "PostgreSQL 10 - 7.5. Sorting Rows \(ORDER BY\)") /
[9.6](/docs/9.6/queries-order.html "PostgreSQL 9.6 - 7.5. Sorting Rows \(ORDER
BY\)") / [9.5](/docs/9.5/queries-order.html "PostgreSQL 9.5 - 7.5. Sorting
Rows \(ORDER BY\)") / [9.4](/docs/9.4/queries-order.html "PostgreSQL 9.4 -
7.5. Sorting Rows \(ORDER BY\)") / [9.3](/docs/9.3/queries-order.html
"PostgreSQL 9.3 - 7.5. Sorting Rows \(ORDER BY\)") / [9.2](/docs/9.2/queries-
order.html "PostgreSQL 9.2 - 7.5. Sorting Rows \(ORDER BY\)") /
[9.1](/docs/9.1/queries-order.html "PostgreSQL 9.1 - 7.5. Sorting Rows \(ORDER
BY\)") / [9.0](/docs/9.0/queries-order.html "PostgreSQL 9.0 - 7.5. Sorting
Rows \(ORDER BY\)") / [8.4](/docs/8.4/queries-order.html "PostgreSQL 8.4 -
7.5. Sorting Rows \(ORDER BY\)") / [8.3](/docs/8.3/queries-order.html
"PostgreSQL 8.3 - 7.5. Sorting Rows \(ORDER BY\)") / [8.2](/docs/8.2/queries-
order.html "PostgreSQL 8.2 - 7.5. Sorting Rows \(ORDER BY\)") /
[8.1](/docs/8.1/queries-order.html "PostgreSQL 8.1 - 7.5. Sorting Rows \(ORDER
BY\)") / [8.0](/docs/8.0/queries-order.html "PostgreSQL 8.0 - 7.5. Sorting
Rows \(ORDER BY\)") / [7.4](/docs/7.4/queries-order.html "PostgreSQL 7.4 -
7.5. Sorting Rows \(ORDER BY\)") / [7.3](/docs/7.3/queries-order.html
"PostgreSQL 7.3 - 7.5. Sorting Rows \(ORDER BY\)") / [7.2](/docs/7.2/queries-
order.html "PostgreSQL 7.2 - 7.5. Sorting Rows \(ORDER BY\)") /
[7.1](/docs/7.1/queries-order.html "PostgreSQL 7.1 - 7.5. Sorting Rows \(ORDER
BY\)")

__

7.5. Sorting Rows (`ORDER BY`)  
---  
[Prev](queries-union.html "7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)")  | [Up](queries.html "Chapter 7. Queries") | Chapter 7. Queries | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](queries-limit.html "7.6. LIMIT and OFFSET")  
  
* * *

## 7.5. Sorting Rows (`ORDER BY`) #

After a query has produced an output table (after the select list has been
processed) it can optionally be sorted. If sorting is not chosen, the rows
will be returned in an unspecified order. The actual order in that case will
depend on the scan and join plan types and the order on disk, but it must not
be relied on. A particular output ordering can only be guaranteed if the sort
step is explicitly chosen.

The `ORDER BY` clause specifies the sort order:

    
    
    SELECT _select_list_
        FROM _table_expression_
        ORDER BY _sort_expression1_ [ASC | DESC] [NULLS { FIRST | LAST }]
                 [, _sort_expression2_ [ASC | DESC] [NULLS { FIRST | LAST }] ...]
    

The sort expression(s) can be any expression that would be valid in the
query's select list. An example is:

    
    
    SELECT a, b FROM table1 ORDER BY a + b, c;
    

When more than one expression is specified, the later values are used to sort
rows that are equal according to the earlier values. Each expression can be
followed by an optional `ASC` or `DESC` keyword to set the sort direction to
ascending or descending. `ASC` order is the default. Ascending order puts
smaller values first, where “smaller” is defined in terms of the `<` operator.
Similarly, descending order is determined with the `>` operator. [6]

The `NULLS FIRST` and `NULLS LAST` options can be used to determine whether
nulls appear before or after non-null values in the sort ordering. By default,
null values sort as if larger than any non-null value; that is, `NULLS FIRST`
is the default for `DESC` order, and `NULLS LAST` otherwise.

Note that the ordering options are considered independently for each sort
column. For example `ORDER BY x, y DESC` means `ORDER BY x ASC, y DESC`, which
is not the same as `ORDER BY x DESC, y DESC`.

A _`sort_expression`_ can also be the column label or number of an output
column, as in:

    
    
    SELECT a + b AS sum, c FROM table1 ORDER BY sum;
    SELECT a, max(b) FROM table1 GROUP BY a ORDER BY 1;
    

both of which sort by the first output column. Note that an output column name
has to stand alone, that is, it cannot be used in an expression — for example,
this is _not_ correct:

    
    
    SELECT a + b AS sum, c FROM table1 ORDER BY sum + c;          -- wrong
    

This restriction is made to reduce ambiguity. There is still ambiguity if an
`ORDER BY` item is a simple name that could match either an output column name
or a column from the table expression. The output column is used in such
cases. This would only cause confusion if you use `AS` to rename an output
column to match some other table column's name.

`ORDER BY` can be applied to the result of a `UNION`, `INTERSECT`, or `EXCEPT`
combination, but in this case it is only permitted to sort by output column
names or numbers, not by expressions.

  

* * *

[6] Actually, PostgreSQL uses the _default B-tree operator class_ for the
expression's data type to determine the sort ordering for `ASC` and `DESC`.
Conventionally, data types will be set up so that the `<` and `>` operators
correspond to this sort ordering, but a user-defined data type's designer
could choose to do something different.

* * *

[Prev](queries-union.html "7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)")  | [Up](queries.html "Chapter 7. Queries") |  [Next](queries-limit.html "7.6. LIMIT and OFFSET")  
---|---|---  
7.4. Combining Queries (`UNION`, `INTERSECT`, `EXCEPT`)  | [Home](index.html "PostgreSQL 16.9 Documentation") |  7.6. `LIMIT` and `OFFSET`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/queries-order.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

