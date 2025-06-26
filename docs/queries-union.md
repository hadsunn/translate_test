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

Supported Versions: [Current](/docs/current/queries-union.html "PostgreSQL 17
- 7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)")
([17](/docs/17/queries-union.html "PostgreSQL 17 - 7.4. Combining Queries
\(UNION, INTERSECT, EXCEPT\)")) / [16](/docs/16/queries-union.html "PostgreSQL
16 - 7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)") /
[15](/docs/15/queries-union.html "PostgreSQL 15 - 7.4. Combining Queries
\(UNION, INTERSECT, EXCEPT\)") / [14](/docs/14/queries-union.html "PostgreSQL
14 - 7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)") /
[13](/docs/13/queries-union.html "PostgreSQL 13 - 7.4. Combining Queries
\(UNION, INTERSECT, EXCEPT\)")

Development Versions: [18](/docs/18/queries-union.html "PostgreSQL 18 -
7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)") /
[devel](/docs/devel/queries-union.html "PostgreSQL devel - 7.4. Combining
Queries \(UNION, INTERSECT, EXCEPT\)")

Unsupported versions: [12](/docs/12/queries-union.html "PostgreSQL 12 -
7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)") / [11](/docs/11/queries-
union.html "PostgreSQL 11 - 7.4. Combining Queries \(UNION, INTERSECT,
EXCEPT\)") / [10](/docs/10/queries-union.html "PostgreSQL 10 - 7.4. Combining
Queries \(UNION, INTERSECT, EXCEPT\)") / [9.6](/docs/9.6/queries-union.html
"PostgreSQL 9.6 - 7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)") /
[9.5](/docs/9.5/queries-union.html "PostgreSQL 9.5 - 7.4. Combining Queries
\(UNION, INTERSECT, EXCEPT\)") / [9.4](/docs/9.4/queries-union.html
"PostgreSQL 9.4 - 7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)") /
[9.3](/docs/9.3/queries-union.html "PostgreSQL 9.3 - 7.4. Combining Queries
\(UNION, INTERSECT, EXCEPT\)") / [9.2](/docs/9.2/queries-union.html
"PostgreSQL 9.2 - 7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)") /
[9.1](/docs/9.1/queries-union.html "PostgreSQL 9.1 - 7.4. Combining Queries
\(UNION, INTERSECT, EXCEPT\)") / [9.0](/docs/9.0/queries-union.html
"PostgreSQL 9.0 - 7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)") /
[8.4](/docs/8.4/queries-union.html "PostgreSQL 8.4 - 7.4. Combining Queries
\(UNION, INTERSECT, EXCEPT\)") / [8.3](/docs/8.3/queries-union.html
"PostgreSQL 8.3 - 7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)") /
[8.2](/docs/8.2/queries-union.html "PostgreSQL 8.2 - 7.4. Combining Queries
\(UNION, INTERSECT, EXCEPT\)") / [8.1](/docs/8.1/queries-union.html
"PostgreSQL 8.1 - 7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)") /
[8.0](/docs/8.0/queries-union.html "PostgreSQL 8.0 - 7.4. Combining Queries
\(UNION, INTERSECT, EXCEPT\)") / [7.4](/docs/7.4/queries-union.html
"PostgreSQL 7.4 - 7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)") /
[7.3](/docs/7.3/queries-union.html "PostgreSQL 7.3 - 7.4. Combining Queries
\(UNION, INTERSECT, EXCEPT\)") / [7.2](/docs/7.2/queries-union.html
"PostgreSQL 7.2 - 7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)") /
[7.1](/docs/7.1/queries-union.html "PostgreSQL 7.1 - 7.4. Combining Queries
\(UNION, INTERSECT, EXCEPT\)")

__

7.4. Combining Queries (`UNION`, `INTERSECT`, `EXCEPT`)  
---  
[Prev](queries-select-lists.html "7.3. Select Lists")  | [Up](queries.html "Chapter 7. Queries") | Chapter 7. Queries | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](queries-order.html "7.5. Sorting Rows \(ORDER BY\)")  
  
* * *

## 7.4. Combining Queries (`UNION`, `INTERSECT`, `EXCEPT`) #

The results of two queries can be combined using the set operations union,
intersection, and difference. The syntax is

    
    
    _query1_ UNION [ALL] _query2_
    _query1_ INTERSECT [ALL] _query2_
    _query1_ EXCEPT [ALL] _query2_
    

where _`query1`_ and _`query2`_ are queries that can use any of the features
discussed up to this point.

`UNION` effectively appends the result of _`query2`_ to the result of
_`query1`_ (although there is no guarantee that this is the order in which the
rows are actually returned). Furthermore, it eliminates duplicate rows from
its result, in the same way as `DISTINCT`, unless `UNION ALL` is used.

`INTERSECT` returns all rows that are both in the result of _`query1`_ and in
the result of _`query2`_. Duplicate rows are eliminated unless `INTERSECT ALL`
is used.

`EXCEPT` returns all rows that are in the result of _`query1`_ but not in the
result of _`query2`_. (This is sometimes called the _difference_ between two
queries.) Again, duplicates are eliminated unless `EXCEPT ALL` is used.

In order to calculate the union, intersection, or difference of two queries,
the two queries must be “union compatible”, which means that they return the
same number of columns and the corresponding columns have compatible data
types, as described in [Section 10.5](typeconv-union-case.html "10.5. UNION,
CASE, and Related Constructs").

Set operations can be combined, for example

    
    
    _query1_ UNION _query2_ EXCEPT _query3_
    

which is equivalent to

    
    
    (_query1_ UNION _query2_) EXCEPT _query3_
    

As shown here, you can use parentheses to control the order of evaluation.
Without parentheses, `UNION` and `EXCEPT` associate left-to-right, but
`INTERSECT` binds more tightly than those two operators. Thus

    
    
    _query1_ UNION _query2_ INTERSECT _query3_
    

means

    
    
    _query1_ UNION (_query2_ INTERSECT _query3_)
    

You can also surround an individual _`query`_ with parentheses. This is
important if the _`query`_ needs to use any of the clauses discussed in
following sections, such as `LIMIT`. Without parentheses, you'll get a syntax
error, or else the clause will be understood as applying to the output of the
set operation rather than one of its inputs. For example,

    
    
    SELECT a FROM b UNION SELECT x FROM y LIMIT 10
    

is accepted, but it means

    
    
    (SELECT a FROM b UNION SELECT x FROM y) LIMIT 10
    

not

    
    
    SELECT a FROM b UNION (SELECT x FROM y LIMIT 10)
    

* * *

[Prev](queries-select-lists.html "7.3. Select Lists")  | [Up](queries.html "Chapter 7. Queries") |  [Next](queries-order.html "7.5. Sorting Rows \(ORDER BY\)")  
---|---|---  
7.3. Select Lists  | [Home](index.html "PostgreSQL 16.9 Documentation") |  7.5. Sorting Rows (`ORDER BY`)  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/queries-union.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

