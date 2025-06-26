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

Supported Versions: [Current](/docs/current/tutorial-agg.html "PostgreSQL 17 -
2.7. Aggregate Functions") ([17](/docs/17/tutorial-agg.html "PostgreSQL 17 -
2.7. Aggregate Functions")) / [16](/docs/16/tutorial-agg.html "PostgreSQL 16 -
2.7. Aggregate Functions") / [15](/docs/15/tutorial-agg.html "PostgreSQL 15 -
2.7. Aggregate Functions") / [14](/docs/14/tutorial-agg.html "PostgreSQL 14 -
2.7. Aggregate Functions") / [13](/docs/13/tutorial-agg.html "PostgreSQL 13 -
2.7. Aggregate Functions")

Development Versions: [18](/docs/18/tutorial-agg.html "PostgreSQL 18 -
2.7. Aggregate Functions") / [devel](/docs/devel/tutorial-agg.html "PostgreSQL
devel - 2.7. Aggregate Functions")

Unsupported versions: [12](/docs/12/tutorial-agg.html "PostgreSQL 12 -
2.7. Aggregate Functions") / [11](/docs/11/tutorial-agg.html "PostgreSQL 11 -
2.7. Aggregate Functions") / [10](/docs/10/tutorial-agg.html "PostgreSQL 10 -
2.7. Aggregate Functions") / [9.6](/docs/9.6/tutorial-agg.html "PostgreSQL 9.6
- 2.7. Aggregate Functions") / [9.5](/docs/9.5/tutorial-agg.html "PostgreSQL
9.5 - 2.7. Aggregate Functions") / [9.4](/docs/9.4/tutorial-agg.html
"PostgreSQL 9.4 - 2.7. Aggregate Functions") / [9.3](/docs/9.3/tutorial-
agg.html "PostgreSQL 9.3 - 2.7. Aggregate Functions") /
[9.2](/docs/9.2/tutorial-agg.html "PostgreSQL 9.2 - 2.7. Aggregate Functions")
/ [9.1](/docs/9.1/tutorial-agg.html "PostgreSQL 9.1 - 2.7. Aggregate
Functions") / [9.0](/docs/9.0/tutorial-agg.html "PostgreSQL 9.0 -
2.7. Aggregate Functions") / [8.4](/docs/8.4/tutorial-agg.html "PostgreSQL 8.4
- 2.7. Aggregate Functions") / [8.3](/docs/8.3/tutorial-agg.html "PostgreSQL
8.3 - 2.7. Aggregate Functions") / [8.2](/docs/8.2/tutorial-agg.html
"PostgreSQL 8.2 - 2.7. Aggregate Functions") / [8.1](/docs/8.1/tutorial-
agg.html "PostgreSQL 8.1 - 2.7. Aggregate Functions") /
[8.0](/docs/8.0/tutorial-agg.html "PostgreSQL 8.0 - 2.7. Aggregate Functions")
/ [7.4](/docs/7.4/tutorial-agg.html "PostgreSQL 7.4 - 2.7. Aggregate
Functions") / [7.3](/docs/7.3/tutorial-agg.html "PostgreSQL 7.3 -
2.7. Aggregate Functions") / [7.2](/docs/7.2/tutorial-agg.html "PostgreSQL 7.2
- 2.7. Aggregate Functions")

__

2.7. Aggregate Functions  
---  
[Prev](tutorial-join.html "2.6. Joins Between Tables")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") | Chapter 2. The SQL Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-update.html "2.8. Updates")  
  
* * *

## 2.7. Aggregate Functions #

Like most other relational database products, PostgreSQL supports _aggregate
functions_. An aggregate function computes a single result from multiple input
rows. For example, there are aggregates to compute the `count`, `sum`, `avg`
(average), `max` (maximum) and `min` (minimum) over a set of rows.

As an example, we can find the highest low-temperature reading anywhere with:

    
    
    SELECT max(temp_lo) FROM weather;
    
    
    
     max
    -----
      46
    (1 row)
    

If we wanted to know what city (or cities) that reading occurred in, we might
try:

    
    
    SELECT city FROM weather WHERE temp_lo = max(temp_lo);     _WRONG_
    

but this will not work since the aggregate `max` cannot be used in the `WHERE`
clause. (This restriction exists because the `WHERE` clause determines which
rows will be included in the aggregate calculation; so obviously it has to be
evaluated before aggregate functions are computed.) However, as is often the
case the query can be restated to accomplish the desired result, here by using
a _subquery_ :

    
    
    SELECT city FROM weather
        WHERE temp_lo = (SELECT max(temp_lo) FROM weather);
    
    
    
         city
    ---------------
     San Francisco
    (1 row)
    

This is OK because the subquery is an independent computation that computes
its own aggregate separately from what is happening in the outer query.

Aggregates are also very useful in combination with `GROUP BY` clauses. For
example, we can get the number of readings and the maximum low temperature
observed in each city with:

    
    
    SELECT city, count(*), max(temp_lo)
        FROM weather
        GROUP BY city;
    
    
    
         city      | count | max
    ---------------+-------+-----
     Hayward       |     1 |  37
     San Francisco |     2 |  46
    (2 rows)
    

which gives us one output row per city. Each aggregate result is computed over
the table rows matching that city. We can filter these grouped rows using
`HAVING`:

    
    
    SELECT city, count(*), max(temp_lo)
        FROM weather
        GROUP BY city
        HAVING max(temp_lo) < 40;
    
    
    
      city   | count | max
    ---------+-------+-----
     Hayward |     1 |  37
    (1 row)
    

which gives us the same results for only the cities that have all `temp_lo`
values below 40. Finally, if we only care about cities whose names begin with
“`S`”, we might do:

    
    
    SELECT city, count(*), max(temp_lo)
        FROM weather
        WHERE city LIKE 'S%'            -- (1)
        GROUP BY city;
    
    
    
         city      | count | max
    ---------------+-------+-----
     San Francisco |     2 |  46
    (1 row)
    

(1) |  The `LIKE` operator does pattern matching and is explained in [Section 9.7](functions-matching.html "9.7. Pattern Matching").  
---|---  
  
It is important to understand the interaction between aggregates and SQL's
`WHERE` and `HAVING` clauses. The fundamental difference between `WHERE` and
`HAVING` is this: `WHERE` selects input rows before groups and aggregates are
computed (thus, it controls which rows go into the aggregate computation),
whereas `HAVING` selects group rows after groups and aggregates are computed.
Thus, the `WHERE` clause must not contain aggregate functions; it makes no
sense to try to use an aggregate to determine which rows will be inputs to the
aggregates. On the other hand, the `HAVING` clause always contains aggregate
functions. (Strictly speaking, you are allowed to write a `HAVING` clause that
doesn't use aggregates, but it's seldom useful. The same condition could be
used more efficiently at the `WHERE` stage.)

In the previous example, we can apply the city name restriction in `WHERE`,
since it needs no aggregate. This is more efficient than adding the
restriction to `HAVING`, because we avoid doing the grouping and aggregate
calculations for all rows that fail the `WHERE` check.

Another way to select the rows that go into an aggregate computation is to use
`FILTER`, which is a per-aggregate option:

    
    
    SELECT city, count(*) FILTER (WHERE temp_lo < 45), max(temp_lo)
        FROM weather
        GROUP BY city;
    
    
    
         city      | count | max
    ---------------+-------+-----
     Hayward       |     1 |  37
     San Francisco |     1 |  46
    (2 rows)
    

`FILTER` is much like `WHERE`, except that it removes rows only from the input
of the particular aggregate function that it is attached to. Here, the `count`
aggregate counts only rows with `temp_lo` below 45; but the `max` aggregate is
still applied to all rows, so it still finds the reading of 46.

* * *

[Prev](tutorial-join.html "2.6. Joins Between Tables")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") |  [Next](tutorial-update.html "2.8. Updates")  
---|---|---  
2.6. Joins Between Tables  | [Home](index.html "PostgreSQL 16.9 Documentation") |  2.8. Updates  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-agg.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

