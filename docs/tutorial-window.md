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

Supported Versions: [Current](/docs/current/tutorial-window.html "PostgreSQL
17 - 3.5. Window Functions") ([17](/docs/17/tutorial-window.html "PostgreSQL
17 - 3.5. Window Functions")) / [16](/docs/16/tutorial-window.html "PostgreSQL
16 - 3.5. Window Functions") / [15](/docs/15/tutorial-window.html "PostgreSQL
15 - 3.5. Window Functions") / [14](/docs/14/tutorial-window.html "PostgreSQL
14 - 3.5. Window Functions") / [13](/docs/13/tutorial-window.html "PostgreSQL
13 - 3.5. Window Functions")

Development Versions: [18](/docs/18/tutorial-window.html "PostgreSQL 18 -
3.5. Window Functions") / [devel](/docs/devel/tutorial-window.html "PostgreSQL
devel - 3.5. Window Functions")

Unsupported versions: [12](/docs/12/tutorial-window.html "PostgreSQL 12 -
3.5. Window Functions") / [11](/docs/11/tutorial-window.html "PostgreSQL 11 -
3.5. Window Functions") / [10](/docs/10/tutorial-window.html "PostgreSQL 10 -
3.5. Window Functions") / [9.6](/docs/9.6/tutorial-window.html "PostgreSQL 9.6
- 3.5. Window Functions") / [9.5](/docs/9.5/tutorial-window.html "PostgreSQL
9.5 - 3.5. Window Functions") / [9.4](/docs/9.4/tutorial-window.html
"PostgreSQL 9.4 - 3.5. Window Functions") / [9.3](/docs/9.3/tutorial-
window.html "PostgreSQL 9.3 - 3.5. Window Functions") /
[9.2](/docs/9.2/tutorial-window.html "PostgreSQL 9.2 - 3.5. Window Functions")
/ [9.1](/docs/9.1/tutorial-window.html "PostgreSQL 9.1 - 3.5. Window
Functions") / [9.0](/docs/9.0/tutorial-window.html "PostgreSQL 9.0 -
3.5. Window Functions") / [8.4](/docs/8.4/tutorial-window.html "PostgreSQL 8.4
- 3.5. Window Functions")

__

3.5. Window Functions  
---  
[Prev](tutorial-transactions.html "3.4. Transactions")  | [Up](tutorial-advanced.html "Chapter 3. Advanced Features") | Chapter 3. Advanced Features | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-inheritance.html "3.6. Inheritance")  
  
* * *

## 3.5. Window Functions #

A _window function_ performs a calculation across a set of table rows that are
somehow related to the current row. This is comparable to the type of
calculation that can be done with an aggregate function. However, window
functions do not cause rows to become grouped into a single output row like
non-window aggregate calls would. Instead, the rows retain their separate
identities. Behind the scenes, the window function is able to access more than
just the current row of the query result.

Here is an example that shows how to compare each employee's salary with the
average salary in his or her department:

    
    
    SELECT depname, empno, salary, avg(salary) OVER (PARTITION BY depname) FROM empsalary;
    
    
    
      depname  | empno | salary |          avg
    -----------+-------+--------+-----------------------
     develop   |    11 |   5200 | 5020.0000000000000000
     develop   |     7 |   4200 | 5020.0000000000000000
     develop   |     9 |   4500 | 5020.0000000000000000
     develop   |     8 |   6000 | 5020.0000000000000000
     develop   |    10 |   5200 | 5020.0000000000000000
     personnel |     5 |   3500 | 3700.0000000000000000
     personnel |     2 |   3900 | 3700.0000000000000000
     sales     |     3 |   4800 | 4866.6666666666666667
     sales     |     1 |   5000 | 4866.6666666666666667
     sales     |     4 |   4800 | 4866.6666666666666667
    (10 rows)
    

The first three output columns come directly from the table `empsalary`, and
there is one output row for each row in the table. The fourth column
represents an average taken across all the table rows that have the same
`depname` value as the current row. (This actually is the same function as the
non-window `avg` aggregate, but the `OVER` clause causes it to be treated as a
window function and computed across the window frame.)

A window function call always contains an `OVER` clause directly following the
window function's name and argument(s). This is what syntactically
distinguishes it from a normal function or non-window aggregate. The `OVER`
clause determines exactly how the rows of the query are split up for
processing by the window function. The `PARTITION BY` clause within `OVER`
divides the rows into groups, or partitions, that share the same values of the
`PARTITION BY` expression(s). For each row, the window function is computed
across the rows that fall into the same partition as the current row.

You can also control the order in which rows are processed by window functions
using `ORDER BY` within `OVER`. (The window `ORDER BY` does not even have to
match the order in which the rows are output.) Here is an example:

    
    
    SELECT depname, empno, salary,
           rank() OVER (PARTITION BY depname ORDER BY salary DESC)
    FROM empsalary;
    
    
    
      depname  | empno | salary | rank
    -----------+-------+--------+------
     develop   |     8 |   6000 |    1
     develop   |    10 |   5200 |    2
     develop   |    11 |   5200 |    2
     develop   |     9 |   4500 |    4
     develop   |     7 |   4200 |    5
     personnel |     2 |   3900 |    1
     personnel |     5 |   3500 |    2
     sales     |     1 |   5000 |    1
     sales     |     4 |   4800 |    2
     sales     |     3 |   4800 |    2
    (10 rows)
    

As shown here, the `rank` function produces a numerical rank for each distinct
`ORDER BY` value in the current row's partition, using the order defined by
the `ORDER BY` clause. `rank` needs no explicit parameter, because its
behavior is entirely determined by the `OVER` clause.

The rows considered by a window function are those of the “virtual table”
produced by the query's `FROM` clause as filtered by its `WHERE`, `GROUP BY`,
and `HAVING` clauses if any. For example, a row removed because it does not
meet the `WHERE` condition is not seen by any window function. A query can
contain multiple window functions that slice up the data in different ways
using different `OVER` clauses, but they all act on the same collection of
rows defined by this virtual table.

We already saw that `ORDER BY` can be omitted if the ordering of rows is not
important. It is also possible to omit `PARTITION BY`, in which case there is
a single partition containing all rows.

There is another important concept associated with window functions: for each
row, there is a set of rows within its partition called its _window frame_.
Some window functions act only on the rows of the window frame, rather than of
the whole partition. By default, if `ORDER BY` is supplied then the frame
consists of all rows from the start of the partition up through the current
row, plus any following rows that are equal to the current row according to
the `ORDER BY` clause. When `ORDER BY` is omitted the default frame consists
of all rows in the partition. [5] Here is an example using `sum`:

    
    
    SELECT salary, sum(salary) OVER () FROM empsalary;
    
    
    
     salary |  sum
    --------+-------
       5200 | 47100
       5000 | 47100
       3500 | 47100
       4800 | 47100
       3900 | 47100
       4200 | 47100
       4500 | 47100
       4800 | 47100
       6000 | 47100
       5200 | 47100
    (10 rows)
    

Above, since there is no `ORDER BY` in the `OVER` clause, the window frame is
the same as the partition, which for lack of `PARTITION BY` is the whole
table; in other words each sum is taken over the whole table and so we get the
same result for each output row. But if we add an `ORDER BY` clause, we get
very different results:

    
    
    SELECT salary, sum(salary) OVER (ORDER BY salary) FROM empsalary;
    
    
    
     salary |  sum
    --------+-------
       3500 |  3500
       3900 |  7400
       4200 | 11600
       4500 | 16100
       4800 | 25700
       4800 | 25700
       5000 | 30700
       5200 | 41100
       5200 | 41100
       6000 | 47100
    (10 rows)
    

Here the sum is taken from the first (lowest) salary up through the current
one, including any duplicates of the current one (notice the results for the
duplicated salaries).

Window functions are permitted only in the `SELECT` list and the `ORDER BY`
clause of the query. They are forbidden elsewhere, such as in `GROUP BY`,
`HAVING` and `WHERE` clauses. This is because they logically execute after the
processing of those clauses. Also, window functions execute after non-window
aggregate functions. This means it is valid to include an aggregate function
call in the arguments of a window function, but not vice versa.

If there is a need to filter or group rows after the window calculations are
performed, you can use a sub-select. For example:

    
    
    SELECT depname, empno, salary, enroll_date
    FROM
      (SELECT depname, empno, salary, enroll_date,
              rank() OVER (PARTITION BY depname ORDER BY salary DESC, empno) AS pos
         FROM empsalary
      ) AS ss
    WHERE pos < 3;
    

The above query only shows the rows from the inner query having `rank` less
than 3.

When a query involves multiple window functions, it is possible to write out
each one with a separate `OVER` clause, but this is duplicative and error-
prone if the same windowing behavior is wanted for several functions. Instead,
each windowing behavior can be named in a `WINDOW` clause and then referenced
in `OVER`. For example:

    
    
    SELECT sum(salary) OVER w, avg(salary) OVER w
      FROM empsalary
      WINDOW w AS (PARTITION BY depname ORDER BY salary DESC);
    

More details about window functions can be found in [Section 4.2.8](sql-
expressions.html#SYNTAX-WINDOW-FUNCTIONS "4.2.8. Window Function Calls"),
[Section 9.22](functions-window.html "9.22. Window Functions"), [Section
7.2.5](queries-table-expressions.html#QUERIES-WINDOW "7.2.5. Window Function
Processing"), and the [SELECT](sql-select.html "SELECT") reference page.

  

* * *

[5] There are options to define the window frame in other ways, but this
tutorial does not cover them. See [Section 4.2.8](sql-expressions.html#SYNTAX-
WINDOW-FUNCTIONS "4.2.8. Window Function Calls") for details.

* * *

[Prev](tutorial-transactions.html "3.4. Transactions")  | [Up](tutorial-advanced.html "Chapter 3. Advanced Features") |  [Next](tutorial-inheritance.html "3.6. Inheritance")  
---|---|---  
3.4. Transactions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  3.6. Inheritance  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-window.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

