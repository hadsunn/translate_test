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

Supported Versions: [Current](/docs/current/tutorial-select.html "PostgreSQL
17 - 2.5. Querying a Table") ([17](/docs/17/tutorial-select.html "PostgreSQL
17 - 2.5. Querying a Table")) / [16](/docs/16/tutorial-select.html "PostgreSQL
16 - 2.5. Querying a Table") / [15](/docs/15/tutorial-select.html "PostgreSQL
15 - 2.5. Querying a Table") / [14](/docs/14/tutorial-select.html "PostgreSQL
14 - 2.5. Querying a Table") / [13](/docs/13/tutorial-select.html "PostgreSQL
13 - 2.5. Querying a Table")

Development Versions: [18](/docs/18/tutorial-select.html "PostgreSQL 18 -
2.5. Querying a Table") / [devel](/docs/devel/tutorial-select.html "PostgreSQL
devel - 2.5. Querying a Table")

Unsupported versions: [12](/docs/12/tutorial-select.html "PostgreSQL 12 -
2.5. Querying a Table") / [11](/docs/11/tutorial-select.html "PostgreSQL 11 -
2.5. Querying a Table") / [10](/docs/10/tutorial-select.html "PostgreSQL 10 -
2.5. Querying a Table") / [9.6](/docs/9.6/tutorial-select.html "PostgreSQL 9.6
- 2.5. Querying a Table") / [9.5](/docs/9.5/tutorial-select.html "PostgreSQL
9.5 - 2.5. Querying a Table") / [9.4](/docs/9.4/tutorial-select.html
"PostgreSQL 9.4 - 2.5. Querying a Table") / [9.3](/docs/9.3/tutorial-
select.html "PostgreSQL 9.3 - 2.5. Querying a Table") /
[9.2](/docs/9.2/tutorial-select.html "PostgreSQL 9.2 - 2.5. Querying a Table")
/ [9.1](/docs/9.1/tutorial-select.html "PostgreSQL 9.1 - 2.5. Querying a
Table") / [9.0](/docs/9.0/tutorial-select.html "PostgreSQL 9.0 - 2.5. Querying
a Table") / [8.4](/docs/8.4/tutorial-select.html "PostgreSQL 8.4 -
2.5. Querying a Table") / [8.3](/docs/8.3/tutorial-select.html "PostgreSQL 8.3
- 2.5. Querying a Table") / [8.2](/docs/8.2/tutorial-select.html "PostgreSQL
8.2 - 2.5. Querying a Table") / [8.1](/docs/8.1/tutorial-select.html
"PostgreSQL 8.1 - 2.5. Querying a Table") / [8.0](/docs/8.0/tutorial-
select.html "PostgreSQL 8.0 - 2.5. Querying a Table") /
[7.4](/docs/7.4/tutorial-select.html "PostgreSQL 7.4 - 2.5. Querying a Table")
/ [7.3](/docs/7.3/tutorial-select.html "PostgreSQL 7.3 - 2.5. Querying a
Table") / [7.2](/docs/7.2/tutorial-select.html "PostgreSQL 7.2 - 2.5. Querying
a Table")

__

2.5. Querying a Table  
---  
[Prev](tutorial-populate.html "2.4. Populating a Table With Rows")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") | Chapter 2. The SQL Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-join.html "2.6. Joins Between Tables")  
  
* * *

## 2.5. Querying a Table #

To retrieve data from a table, the table is _queried_. An SQL `SELECT`
statement is used to do this. The statement is divided into a select list (the
part that lists the columns to be returned), a table list (the part that lists
the tables from which to retrieve the data), and an optional qualification
(the part that specifies any restrictions). For example, to retrieve all the
rows of table `weather`, type:

    
    
    SELECT * FROM weather;
    

Here `*` is a shorthand for “all columns”. [2] So the same result would be had
with:

    
    
    SELECT city, temp_lo, temp_hi, prcp, date FROM weather;
    

The output should be:

    
    
         city      | temp_lo | temp_hi | prcp |    date
    ---------------+---------+---------+------+------------
     San Francisco |      46 |      50 | 0.25 | 1994-11-27
     San Francisco |      43 |      57 |    0 | 1994-11-29
     Hayward       |      37 |      54 |      | 1994-11-29
    (3 rows)
    

You can write expressions, not just simple column references, in the select
list. For example, you can do:

    
    
    SELECT city, (temp_hi+temp_lo)/2 AS temp_avg, date FROM weather;
    

This should give:

    
    
         city      | temp_avg |    date
    ---------------+----------+------------
     San Francisco |       48 | 1994-11-27
     San Francisco |       50 | 1994-11-29
     Hayward       |       45 | 1994-11-29
    (3 rows)
    

Notice how the `AS` clause is used to relabel the output column. (The `AS`
clause is optional.)

A query can be “qualified” by adding a `WHERE` clause that specifies which
rows are wanted. The `WHERE` clause contains a Boolean (truth value)
expression, and only rows for which the Boolean expression is true are
returned. The usual Boolean operators (`AND`, `OR`, and `NOT`) are allowed in
the qualification. For example, the following retrieves the weather of San
Francisco on rainy days:

    
    
    SELECT * FROM weather
        WHERE city = 'San Francisco' AND prcp > 0.0;
    

Result:

    
    
         city      | temp_lo | temp_hi | prcp |    date
    ---------------+---------+---------+------+------------
     San Francisco |      46 |      50 | 0.25 | 1994-11-27
    (1 row)
    

You can request that the results of a query be returned in sorted order:

    
    
    SELECT * FROM weather
        ORDER BY city;
    
    
    
         city      | temp_lo | temp_hi | prcp |    date
    ---------------+---------+---------+------+------------
     Hayward       |      37 |      54 |      | 1994-11-29
     San Francisco |      43 |      57 |    0 | 1994-11-29
     San Francisco |      46 |      50 | 0.25 | 1994-11-27
    

In this example, the sort order isn't fully specified, and so you might get
the San Francisco rows in either order. But you'd always get the results shown
above if you do:

    
    
    SELECT * FROM weather
        ORDER BY city, temp_lo;
    

You can request that duplicate rows be removed from the result of a query:

    
    
    SELECT DISTINCT city
        FROM weather;
    
    
    
         city
    ---------------
     Hayward
     San Francisco
    (2 rows)
    

Here again, the result row ordering might vary. You can ensure consistent
results by using `DISTINCT` and `ORDER BY` together: [3]

    
    
    SELECT DISTINCT city
        FROM weather
        ORDER BY city;
    

  

* * *

[2] While `SELECT *` is useful for off-the-cuff queries, it is widely
considered bad style in production code, since adding a column to the table
would change the results.

[3] In some database systems, including older versions of PostgreSQL, the
implementation of `DISTINCT` automatically orders the rows and so `ORDER BY`
is unnecessary. But this is not required by the SQL standard, and current
PostgreSQL does not guarantee that `DISTINCT` causes the rows to be ordered.

* * *

[Prev](tutorial-populate.html "2.4. Populating a Table With Rows")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") |  [Next](tutorial-join.html "2.6. Joins Between Tables")  
---|---|---  
2.4. Populating a Table With Rows  | [Home](index.html "PostgreSQL 16.9 Documentation") |  2.6. Joins Between Tables  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-select.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

