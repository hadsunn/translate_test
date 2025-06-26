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

Supported Versions: [Current](/docs/current/geqo-intro.html "PostgreSQL 17 -
62.1. Query Handling as a Complex Optimization Problem") ([17](/docs/17/geqo-
intro.html "PostgreSQL 17 - 62.1. Query Handling as a Complex Optimization
Problem")) / [16](/docs/16/geqo-intro.html "PostgreSQL 16 - 62.1. Query
Handling as a Complex Optimization Problem") / [15](/docs/15/geqo-intro.html
"PostgreSQL 15 - 62.1. Query Handling as a Complex Optimization Problem") /
[14](/docs/14/geqo-intro.html "PostgreSQL 14 - 62.1. Query Handling as a
Complex Optimization Problem") / [13](/docs/13/geqo-intro.html "PostgreSQL 13
- 62.1. Query Handling as a Complex Optimization Problem")

Development Versions: [18](/docs/18/geqo-intro.html "PostgreSQL 18 -
62.1. Query Handling as a Complex Optimization Problem") /
[devel](/docs/devel/geqo-intro.html "PostgreSQL devel - 62.1. Query Handling
as a Complex Optimization Problem")

Unsupported versions: [12](/docs/12/geqo-intro.html "PostgreSQL 12 -
62.1. Query Handling as a Complex Optimization Problem") / [11](/docs/11/geqo-
intro.html "PostgreSQL 11 - 62.1. Query Handling as a Complex Optimization
Problem") / [10](/docs/10/geqo-intro.html "PostgreSQL 10 - 62.1. Query
Handling as a Complex Optimization Problem") / [9.6](/docs/9.6/geqo-intro.html
"PostgreSQL 9.6 - 62.1. Query Handling as a Complex Optimization Problem") /
[9.5](/docs/9.5/geqo-intro.html "PostgreSQL 9.5 - 62.1. Query Handling as a
Complex Optimization Problem") / [9.4](/docs/9.4/geqo-intro.html "PostgreSQL
9.4 - 62.1. Query Handling as a Complex Optimization Problem") /
[9.3](/docs/9.3/geqo-intro.html "PostgreSQL 9.3 - 62.1. Query Handling as a
Complex Optimization Problem") / [9.2](/docs/9.2/geqo-intro.html "PostgreSQL
9.2 - 62.1. Query Handling as a Complex Optimization Problem") /
[9.1](/docs/9.1/geqo-intro.html "PostgreSQL 9.1 - 62.1. Query Handling as a
Complex Optimization Problem") / [9.0](/docs/9.0/geqo-intro.html "PostgreSQL
9.0 - 62.1. Query Handling as a Complex Optimization Problem") /
[8.4](/docs/8.4/geqo-intro.html "PostgreSQL 8.4 - 62.1. Query Handling as a
Complex Optimization Problem") / [8.3](/docs/8.3/geqo-intro.html "PostgreSQL
8.3 - 62.1. Query Handling as a Complex Optimization Problem") /
[8.2](/docs/8.2/geqo-intro.html "PostgreSQL 8.2 - 62.1. Query Handling as a
Complex Optimization Problem")

__

62.1. Query Handling as a Complex Optimization Problem  
---  
[Prev](geqo.html "Chapter 62. Genetic Query Optimizer")  | [Up](geqo.html "Chapter 62. Genetic Query Optimizer") | Chapter 62. Genetic Query Optimizer | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](geqo-intro2.html "62.2. Genetic Algorithms")  
  
* * *

## 62.1. Query Handling as a Complex Optimization Problem #

Among all relational operators the most difficult one to process and optimize
is the _join_. The number of possible query plans grows exponentially with the
number of joins in the query. Further optimization effort is caused by the
support of a variety of _join methods_ (e.g., nested loop, hash join, merge
join in PostgreSQL) to process individual joins and a diversity of _indexes_
(e.g., B-tree, hash, GiST and GIN in PostgreSQL) as access paths for
relations.

The normal PostgreSQL query optimizer performs a _near-exhaustive search_ over
the space of alternative strategies. This algorithm, first introduced in IBM's
System R database, produces a near-optimal join order, but can take an
enormous amount of time and memory space when the number of joins in the query
grows large. This makes the ordinary PostgreSQL query optimizer inappropriate
for queries that join a large number of tables.

The Institute of Automatic Control at the University of Mining and Technology,
in Freiberg, Germany, encountered some problems when it wanted to use
PostgreSQL as the backend for a decision support knowledge based system for
the maintenance of an electrical power grid. The DBMS needed to handle large
join queries for the inference machine of the knowledge based system. The
number of joins in these queries made using the normal query optimizer
infeasible.

In the following we describe the implementation of a _genetic algorithm_ to
solve the join ordering problem in a manner that is efficient for queries
involving large numbers of joins.

* * *

[Prev](geqo.html "Chapter 62. Genetic Query Optimizer")  | [Up](geqo.html "Chapter 62. Genetic Query Optimizer") |  [Next](geqo-intro2.html "62.2. Genetic Algorithms")  
---|---|---  
Chapter 62. Genetic Query Optimizer  | [Home](index.html "PostgreSQL 16.9 Documentation") |  62.2. Genetic Algorithms  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/geqo-intro.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

