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

Supported Versions: [Current](/docs/current/queries.html "PostgreSQL 17 -
Chapter 7. Queries") ([17](/docs/17/queries.html "PostgreSQL 17 -
Chapter 7. Queries")) / [16](/docs/16/queries.html "PostgreSQL 16 -
Chapter 7. Queries") / [15](/docs/15/queries.html "PostgreSQL 15 -
Chapter 7. Queries") / [14](/docs/14/queries.html "PostgreSQL 14 -
Chapter 7. Queries") / [13](/docs/13/queries.html "PostgreSQL 13 -
Chapter 7. Queries")

Development Versions: [18](/docs/18/queries.html "PostgreSQL 18 -
Chapter 7. Queries") / [devel](/docs/devel/queries.html "PostgreSQL devel -
Chapter 7. Queries")

Unsupported versions: [12](/docs/12/queries.html "PostgreSQL 12 -
Chapter 7. Queries") / [11](/docs/11/queries.html "PostgreSQL 11 -
Chapter 7. Queries") / [10](/docs/10/queries.html "PostgreSQL 10 -
Chapter 7. Queries") / [9.6](/docs/9.6/queries.html "PostgreSQL 9.6 -
Chapter 7. Queries") / [9.5](/docs/9.5/queries.html "PostgreSQL 9.5 -
Chapter 7. Queries") / [9.4](/docs/9.4/queries.html "PostgreSQL 9.4 -
Chapter 7. Queries") / [9.3](/docs/9.3/queries.html "PostgreSQL 9.3 -
Chapter 7. Queries") / [9.2](/docs/9.2/queries.html "PostgreSQL 9.2 -
Chapter 7. Queries") / [9.1](/docs/9.1/queries.html "PostgreSQL 9.1 -
Chapter 7. Queries") / [9.0](/docs/9.0/queries.html "PostgreSQL 9.0 -
Chapter 7. Queries") / [8.4](/docs/8.4/queries.html "PostgreSQL 8.4 -
Chapter 7. Queries") / [8.3](/docs/8.3/queries.html "PostgreSQL 8.3 -
Chapter 7. Queries") / [8.2](/docs/8.2/queries.html "PostgreSQL 8.2 -
Chapter 7. Queries") / [8.1](/docs/8.1/queries.html "PostgreSQL 8.1 -
Chapter 7. Queries") / [8.0](/docs/8.0/queries.html "PostgreSQL 8.0 -
Chapter 7. Queries") / [7.4](/docs/7.4/queries.html "PostgreSQL 7.4 -
Chapter 7. Queries") / [7.3](/docs/7.3/queries.html "PostgreSQL 7.3 -
Chapter 7. Queries") / [7.2](/docs/7.2/queries.html "PostgreSQL 7.2 -
Chapter 7. Queries") / [7.1](/docs/7.1/queries.html "PostgreSQL 7.1 -
Chapter 7. Queries")

__

Chapter 7. Queries  
---  
[Prev](dml-returning.html "6.4. Returning Data from Modified Rows")  | [Up](sql.html "Part II. The SQL Language") | Part II. The SQL Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](queries-overview.html "7.1. Overview")  
  
* * *

## Chapter 7. Queries

**Table of Contents**

[7.1. Overview](queries-overview.html)

[7.2. Table Expressions](queries-table-expressions.html)

    

[7.2.1. The `FROM` Clause](queries-table-expressions.html#QUERIES-FROM)

[7.2.2. The `WHERE` Clause](queries-table-expressions.html#QUERIES-WHERE)

[7.2.3. The `GROUP BY` and `HAVING` Clauses](queries-table-
expressions.html#QUERIES-GROUP)

[7.2.4. `GROUPING SETS`, `CUBE`, and `ROLLUP`](queries-table-
expressions.html#QUERIES-GROUPING-SETS)

[7.2.5. Window Function Processing](queries-table-expressions.html#QUERIES-
WINDOW)

[7.3. Select Lists](queries-select-lists.html)

    

[7.3.1. Select-List Items](queries-select-lists.html#QUERIES-SELECT-LIST-
ITEMS)

[7.3.2. Column Labels](queries-select-lists.html#QUERIES-COLUMN-LABELS)

[7.3.3. `DISTINCT`](queries-select-lists.html#QUERIES-DISTINCT)

[7.4. Combining Queries (`UNION`, `INTERSECT`, `EXCEPT`)](queries-union.html)

[7.5. Sorting Rows (`ORDER BY`)](queries-order.html)

[7.6. `LIMIT` and `OFFSET`](queries-limit.html)

[7.7. `VALUES` Lists](queries-values.html)

[7.8. `WITH` Queries (Common Table Expressions)](queries-with.html)

    

[7.8.1. `SELECT` in `WITH`](queries-with.html#QUERIES-WITH-SELECT)

[7.8.2. Recursive Queries](queries-with.html#QUERIES-WITH-RECURSIVE)

[7.8.3. Common Table Expression Materialization](queries-with.html#QUERIES-
WITH-CTE-MATERIALIZATION)

[7.8.4. Data-Modifying Statements in `WITH`](queries-with.html#QUERIES-WITH-
MODIFYING)

The previous chapters explained how to create tables, how to fill them with
data, and how to manipulate that data. Now we finally discuss how to retrieve
the data from the database.

* * *

[Prev](dml-returning.html "6.4. Returning Data from Modified Rows")  | [Up](sql.html "Part II. The SQL Language") |  [Next](queries-overview.html "7.1. Overview")  
---|---|---  
6.4. Returning Data from Modified Rows  | [Home](index.html "PostgreSQL 16.9 Documentation") |  7.1. Overview  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/queries.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

