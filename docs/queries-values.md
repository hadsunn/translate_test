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

Supported Versions: [Current](/docs/current/queries-values.html "PostgreSQL 17
- 7.7. VALUES Lists") ([17](/docs/17/queries-values.html "PostgreSQL 17 -
7.7. VALUES Lists")) / [16](/docs/16/queries-values.html "PostgreSQL 16 -
7.7. VALUES Lists") / [15](/docs/15/queries-values.html "PostgreSQL 15 -
7.7. VALUES Lists") / [14](/docs/14/queries-values.html "PostgreSQL 14 -
7.7. VALUES Lists") / [13](/docs/13/queries-values.html "PostgreSQL 13 -
7.7. VALUES Lists")

Development Versions: [18](/docs/18/queries-values.html "PostgreSQL 18 -
7.7. VALUES Lists") / [devel](/docs/devel/queries-values.html "PostgreSQL
devel - 7.7. VALUES Lists")

Unsupported versions: [12](/docs/12/queries-values.html "PostgreSQL 12 -
7.7. VALUES Lists") / [11](/docs/11/queries-values.html "PostgreSQL 11 -
7.7. VALUES Lists") / [10](/docs/10/queries-values.html "PostgreSQL 10 -
7.7. VALUES Lists") / [9.6](/docs/9.6/queries-values.html "PostgreSQL 9.6 -
7.7. VALUES Lists") / [9.5](/docs/9.5/queries-values.html "PostgreSQL 9.5 -
7.7. VALUES Lists") / [9.4](/docs/9.4/queries-values.html "PostgreSQL 9.4 -
7.7. VALUES Lists") / [9.3](/docs/9.3/queries-values.html "PostgreSQL 9.3 -
7.7. VALUES Lists") / [9.2](/docs/9.2/queries-values.html "PostgreSQL 9.2 -
7.7. VALUES Lists") / [9.1](/docs/9.1/queries-values.html "PostgreSQL 9.1 -
7.7. VALUES Lists") / [9.0](/docs/9.0/queries-values.html "PostgreSQL 9.0 -
7.7. VALUES Lists") / [8.4](/docs/8.4/queries-values.html "PostgreSQL 8.4 -
7.7. VALUES Lists") / [8.3](/docs/8.3/queries-values.html "PostgreSQL 8.3 -
7.7. VALUES Lists") / [8.2](/docs/8.2/queries-values.html "PostgreSQL 8.2 -
7.7. VALUES Lists")

__

7.7. `VALUES` Lists  
---  
[Prev](queries-limit.html "7.6. LIMIT and OFFSET")  | [Up](queries.html "Chapter 7. Queries") | Chapter 7. Queries | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](queries-with.html "7.8. WITH Queries \(Common Table Expressions\)")  
  
* * *

## 7.7. `VALUES` Lists #

`VALUES` provides a way to generate a “constant table” that can be used in a
query without having to actually create and populate a table on-disk. The
syntax is

    
    
    VALUES ( _expression_ [, ...] ) [, ...]
    

Each parenthesized list of expressions generates a row in the table. The lists
must all have the same number of elements (i.e., the number of columns in the
table), and corresponding entries in each list must have compatible data
types. The actual data type assigned to each column of the result is
determined using the same rules as for `UNION` (see [Section 10.5](typeconv-
union-case.html "10.5. UNION, CASE, and Related Constructs")).

As an example:

    
    
    VALUES (1, 'one'), (2, 'two'), (3, 'three');
    

will return a table of two columns and three rows. It's effectively equivalent
to:

    
    
    SELECT 1 AS column1, 'one' AS column2
    UNION ALL
    SELECT 2, 'two'
    UNION ALL
    SELECT 3, 'three';
    

By default, PostgreSQL assigns the names `column1`, `column2`, etc. to the
columns of a `VALUES` table. The column names are not specified by the SQL
standard and different database systems do it differently, so it's usually
better to override the default names with a table alias list, like this:

    
    
    => SELECT * FROM (VALUES (1, 'one'), (2, 'two'), (3, 'three')) AS t (num,letter);
     num | letter
    -----+--------
       1 | one
       2 | two
       3 | three
    (3 rows)
    

Syntactically, `VALUES` followed by expression lists is treated as equivalent
to:

    
    
    SELECT _select_list_ FROM _table_expression_
    

and can appear anywhere a `SELECT` can. For example, you can use it as part of
a `UNION`, or attach a _`sort_specification`_ (`ORDER BY`, `LIMIT`, and/or
`OFFSET`) to it. `VALUES` is most commonly used as the data source in an
`INSERT` command, and next most commonly as a subquery.

For more information see [VALUES](sql-values.html "VALUES").

* * *

[Prev](queries-limit.html "7.6. LIMIT and OFFSET")  | [Up](queries.html "Chapter 7. Queries") |  [Next](queries-with.html "7.8. WITH Queries \(Common Table Expressions\)")  
---|---|---  
7.6. `LIMIT` and `OFFSET`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  7.8. `WITH` Queries (Common Table Expressions)  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/queries-values.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

