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

Supported Versions: [Current](/docs/current/tutorial-join.html "PostgreSQL 17
- 2.6. Joins Between Tables") ([17](/docs/17/tutorial-join.html "PostgreSQL 17
- 2.6. Joins Between Tables")) / [16](/docs/16/tutorial-join.html "PostgreSQL
16 - 2.6. Joins Between Tables") / [15](/docs/15/tutorial-join.html
"PostgreSQL 15 - 2.6. Joins Between Tables") / [14](/docs/14/tutorial-
join.html "PostgreSQL 14 - 2.6. Joins Between Tables") /
[13](/docs/13/tutorial-join.html "PostgreSQL 13 - 2.6. Joins Between Tables")

Development Versions: [18](/docs/18/tutorial-join.html "PostgreSQL 18 -
2.6. Joins Between Tables") / [devel](/docs/devel/tutorial-join.html
"PostgreSQL devel - 2.6. Joins Between Tables")

Unsupported versions: [12](/docs/12/tutorial-join.html "PostgreSQL 12 -
2.6. Joins Between Tables") / [11](/docs/11/tutorial-join.html "PostgreSQL 11
- 2.6. Joins Between Tables") / [10](/docs/10/tutorial-join.html "PostgreSQL
10 - 2.6. Joins Between Tables") / [9.6](/docs/9.6/tutorial-join.html
"PostgreSQL 9.6 - 2.6. Joins Between Tables") / [9.5](/docs/9.5/tutorial-
join.html "PostgreSQL 9.5 - 2.6. Joins Between Tables") /
[9.4](/docs/9.4/tutorial-join.html "PostgreSQL 9.4 - 2.6. Joins Between
Tables") / [9.3](/docs/9.3/tutorial-join.html "PostgreSQL 9.3 - 2.6. Joins
Between Tables") / [9.2](/docs/9.2/tutorial-join.html "PostgreSQL 9.2 -
2.6. Joins Between Tables") / [9.1](/docs/9.1/tutorial-join.html "PostgreSQL
9.1 - 2.6. Joins Between Tables") / [9.0](/docs/9.0/tutorial-join.html
"PostgreSQL 9.0 - 2.6. Joins Between Tables") / [8.4](/docs/8.4/tutorial-
join.html "PostgreSQL 8.4 - 2.6. Joins Between Tables") /
[8.3](/docs/8.3/tutorial-join.html "PostgreSQL 8.3 - 2.6. Joins Between
Tables") / [8.2](/docs/8.2/tutorial-join.html "PostgreSQL 8.2 - 2.6. Joins
Between Tables") / [8.1](/docs/8.1/tutorial-join.html "PostgreSQL 8.1 -
2.6. Joins Between Tables") / [8.0](/docs/8.0/tutorial-join.html "PostgreSQL
8.0 - 2.6. Joins Between Tables") / [7.4](/docs/7.4/tutorial-join.html
"PostgreSQL 7.4 - 2.6. Joins Between Tables") / [7.3](/docs/7.3/tutorial-
join.html "PostgreSQL 7.3 - 2.6. Joins Between Tables") /
[7.2](/docs/7.2/tutorial-join.html "PostgreSQL 7.2 - 2.6. Joins Between
Tables")

__

2.6. Joins Between Tables  
---  
[Prev](tutorial-select.html "2.5. Querying a Table")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") | Chapter 2. The SQL Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-agg.html "2.7. Aggregate Functions")  
  
* * *

## 2.6. Joins Between Tables #

Thus far, our queries have only accessed one table at a time. Queries can
access multiple tables at once, or access the same table in such a way that
multiple rows of the table are being processed at the same time. Queries that
access multiple tables (or multiple instances of the same table) at one time
are called _join_ queries. They combine rows from one table with rows from a
second table, with an expression specifying which rows are to be paired. For
example, to return all the weather records together with the location of the
associated city, the database needs to compare the `city` column of each row
of the `weather` table with the `name` column of all rows in the `cities`
table, and select the pairs of rows where these values match.[4] This would be
accomplished by the following query:

    
    
    SELECT * FROM weather JOIN cities ON city = name;
    
    
    
         city      | temp_lo | temp_hi | prcp |    date    |     name      | location
    ---------------+---------+---------+------+------------+---------------+-----------
     San Francisco |      46 |      50 | 0.25 | 1994-11-27 | San Francisco | (-194,53)
     San Francisco |      43 |      57 |    0 | 1994-11-29 | San Francisco | (-194,53)
    (2 rows)
    

Observe two things about the result set:

  * There is no result row for the city of Hayward. This is because there is no matching entry in the `cities` table for Hayward, so the join ignores the unmatched rows in the `weather` table. We will see shortly how this can be fixed.

  * There are two columns containing the city name. This is correct because the lists of columns from the `weather` and `cities` tables are concatenated. In practice this is undesirable, though, so you will probably want to list the output columns explicitly rather than using `*`:
        
        SELECT city, temp_lo, temp_hi, prcp, date, location
            FROM weather JOIN cities ON city = name;
        

Since the columns all had different names, the parser automatically found
which table they belong to. If there were duplicate column names in the two
tables you'd need to _qualify_ the column names to show which one you meant,
as in:

    
    
    SELECT weather.city, weather.temp_lo, weather.temp_hi,
           weather.prcp, weather.date, cities.location
        FROM weather JOIN cities ON weather.city = cities.name;
    

It is widely considered good style to qualify all column names in a join
query, so that the query won't fail if a duplicate column name is later added
to one of the tables.

Join queries of the kind seen thus far can also be written in this form:

    
    
    SELECT *
        FROM weather, cities
        WHERE city = name;
    

This syntax pre-dates the `JOIN`/`ON` syntax, which was introduced in SQL-92.
The tables are simply listed in the `FROM` clause, and the comparison
expression is added to the `WHERE` clause. The results from this older
implicit syntax and the newer explicit `JOIN`/`ON` syntax are identical. But
for a reader of the query, the explicit syntax makes its meaning easier to
understand: The join condition is introduced by its own key word whereas
previously the condition was mixed into the `WHERE` clause together with other
conditions.

Now we will figure out how we can get the Hayward records back in. What we
want the query to do is to scan the `weather` table and for each row to find
the matching `cities` row(s). If no matching row is found we want some “empty
values” to be substituted for the `cities` table's columns. This kind of query
is called an _outer join_. (The joins we have seen so far are _inner joins_.)
The command looks like this:

    
    
    SELECT *
        FROM weather LEFT OUTER JOIN cities ON weather.city = cities.name;
    
    
    
         city      | temp_lo | temp_hi | prcp |    date    |     name      | location
    ---------------+---------+---------+------+------------+---------------+-----------
     Hayward       |      37 |      54 |      | 1994-11-29 |               |
     San Francisco |      46 |      50 | 0.25 | 1994-11-27 | San Francisco | (-194,53)
     San Francisco |      43 |      57 |    0 | 1994-11-29 | San Francisco | (-194,53)
    (3 rows)
    

This query is called a _left outer join_ because the table mentioned on the
left of the join operator will have each of its rows in the output at least
once, whereas the table on the right will only have those rows output that
match some row of the left table. When outputting a left-table row for which
there is no right-table match, empty (null) values are substituted for the
right-table columns.

**Exercise:  ** There are also right outer joins and full outer joins. Try to
find out what those do.

We can also join a table against itself. This is called a _self join_. As an
example, suppose we wish to find all the weather records that are in the
temperature range of other weather records. So we need to compare the
`temp_lo` and `temp_hi` columns of each `weather` row to the `temp_lo` and
`temp_hi` columns of all other `weather` rows. We can do this with the
following query:

    
    
    SELECT w1.city, w1.temp_lo AS low, w1.temp_hi AS high,
           w2.city, w2.temp_lo AS low, w2.temp_hi AS high
        FROM weather w1 JOIN weather w2
            ON w1.temp_lo < w2.temp_lo AND w1.temp_hi > w2.temp_hi;
    
    
    
         city      | low | high |     city      | low | high
    ---------------+-----+------+---------------+-----+------
     San Francisco |  43 |   57 | San Francisco |  46 |   50
     Hayward       |  37 |   54 | San Francisco |  46 |   50
    (2 rows)
    

Here we have relabeled the weather table as `w1` and `w2` to be able to
distinguish the left and right side of the join. You can also use these kinds
of aliases in other queries to save some typing, e.g.:

    
    
    SELECT *
        FROM weather w JOIN cities c ON w.city = c.name;
    

You will encounter this style of abbreviating quite frequently.

  

* * *

[4] This is only a conceptual model. The join is usually performed in a more
efficient manner than actually comparing each possible pair of rows, but this
is invisible to the user.

* * *

[Prev](tutorial-select.html "2.5. Querying a Table")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") |  [Next](tutorial-agg.html "2.7. Aggregate Functions")  
---|---|---  
2.5. Querying a Table  | [Home](index.html "PostgreSQL 16.9 Documentation") |  2.7. Aggregate Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-join.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

