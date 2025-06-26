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

Supported Versions: [Current](/docs/current/parallel-query.html "PostgreSQL 17
- Chapter 15. Parallel Query") ([17](/docs/17/parallel-query.html "PostgreSQL
17 - Chapter 15. Parallel Query")) / [16](/docs/16/parallel-query.html
"PostgreSQL 16 - Chapter 15. Parallel Query") / [15](/docs/15/parallel-
query.html "PostgreSQL 15 - Chapter 15. Parallel Query") /
[14](/docs/14/parallel-query.html "PostgreSQL 14 - Chapter 15. Parallel
Query") / [13](/docs/13/parallel-query.html "PostgreSQL 13 -
Chapter 15. Parallel Query")

Development Versions: [18](/docs/18/parallel-query.html "PostgreSQL 18 -
Chapter 15. Parallel Query") / [devel](/docs/devel/parallel-query.html
"PostgreSQL devel - Chapter 15. Parallel Query")

Unsupported versions: [12](/docs/12/parallel-query.html "PostgreSQL 12 -
Chapter 15. Parallel Query") / [11](/docs/11/parallel-query.html "PostgreSQL
11 - Chapter 15. Parallel Query") / [10](/docs/10/parallel-query.html
"PostgreSQL 10 - Chapter 15. Parallel Query") / [9.6](/docs/9.6/parallel-
query.html "PostgreSQL 9.6 - Chapter 15. Parallel Query")

__

Chapter 15. Parallel Query  
---  
[Prev](non-durability.html "14.5. Non-Durable Settings")  | [Up](sql.html "Part II. The SQL Language") | Part II. The SQL Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](how-parallel-query-works.html "15.1. How Parallel Query Works")  
  
* * *

## Chapter 15. Parallel Query

**Table of Contents**

[15.1. How Parallel Query Works](how-parallel-query-works.html)

[15.2. When Can Parallel Query Be Used?](when-can-parallel-query-be-used.html)

[15.3. Parallel Plans](parallel-plans.html)

    

[15.3.1. Parallel Scans](parallel-plans.html#PARALLEL-SCANS)

[15.3.2. Parallel Joins](parallel-plans.html#PARALLEL-JOINS)

[15.3.3. Parallel Aggregation](parallel-plans.html#PARALLEL-AGGREGATION)

[15.3.4. Parallel Append](parallel-plans.html#PARALLEL-APPEND)

[15.3.5. Parallel Plan Tips](parallel-plans.html#PARALLEL-PLAN-TIPS)

[15.4. Parallel Safety](parallel-safety.html)

    

[15.4.1. Parallel Labeling for Functions and Aggregates](parallel-
safety.html#PARALLEL-LABELING)

PostgreSQL can devise query plans that can leverage multiple CPUs in order to
answer queries faster. This feature is known as parallel query. Many queries
cannot benefit from parallel query, either due to limitations of the current
implementation or because there is no imaginable query plan that is any faster
than the serial query plan. However, for queries that can benefit, the speedup
from parallel query is often very significant. Many queries can run more than
twice as fast when using parallel query, and some queries can run four times
faster or even more. Queries that touch a large amount of data but return only
a few rows to the user will typically benefit most. This chapter explains some
details of how parallel query works and in which situations it can be used so
that users who wish to make use of it can understand what to expect.

* * *

[Prev](non-durability.html "14.5. Non-Durable Settings")  | [Up](sql.html "Part II. The SQL Language") |  [Next](how-parallel-query-works.html "15.1. How Parallel Query Works")  
---|---|---  
14.5. Non-Durable Settings  | [Home](index.html "PostgreSQL 16.9 Documentation") |  15.1. How Parallel Query Works  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/parallel-query.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

