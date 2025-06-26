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

Supported Versions: [Current](/docs/current/overview.html "PostgreSQL 17 -
Chapter 52. Overview of PostgreSQL Internals") ([17](/docs/17/overview.html
"PostgreSQL 17 - Chapter 52. Overview of PostgreSQL Internals")) /
[16](/docs/16/overview.html "PostgreSQL 16 - Chapter 52. Overview of
PostgreSQL Internals") / [15](/docs/15/overview.html "PostgreSQL 15 -
Chapter 52. Overview of PostgreSQL Internals") / [14](/docs/14/overview.html
"PostgreSQL 14 - Chapter 52. Overview of PostgreSQL Internals") /
[13](/docs/13/overview.html "PostgreSQL 13 - Chapter 52. Overview of
PostgreSQL Internals")

Development Versions: [18](/docs/18/overview.html "PostgreSQL 18 -
Chapter 52. Overview of PostgreSQL Internals") /
[devel](/docs/devel/overview.html "PostgreSQL devel - Chapter 52. Overview of
PostgreSQL Internals")

Unsupported versions: [12](/docs/12/overview.html "PostgreSQL 12 -
Chapter 52. Overview of PostgreSQL Internals") / [11](/docs/11/overview.html
"PostgreSQL 11 - Chapter 52. Overview of PostgreSQL Internals") /
[10](/docs/10/overview.html "PostgreSQL 10 - Chapter 52. Overview of
PostgreSQL Internals") / [9.6](/docs/9.6/overview.html "PostgreSQL 9.6 -
Chapter 52. Overview of PostgreSQL Internals") / [9.5](/docs/9.5/overview.html
"PostgreSQL 9.5 - Chapter 52. Overview of PostgreSQL Internals") /
[9.4](/docs/9.4/overview.html "PostgreSQL 9.4 - Chapter 52. Overview of
PostgreSQL Internals") / [9.3](/docs/9.3/overview.html "PostgreSQL 9.3 -
Chapter 52. Overview of PostgreSQL Internals") / [9.2](/docs/9.2/overview.html
"PostgreSQL 9.2 - Chapter 52. Overview of PostgreSQL Internals") /
[9.1](/docs/9.1/overview.html "PostgreSQL 9.1 - Chapter 52. Overview of
PostgreSQL Internals") / [9.0](/docs/9.0/overview.html "PostgreSQL 9.0 -
Chapter 52. Overview of PostgreSQL Internals") / [8.4](/docs/8.4/overview.html
"PostgreSQL 8.4 - Chapter 52. Overview of PostgreSQL Internals") /
[8.3](/docs/8.3/overview.html "PostgreSQL 8.3 - Chapter 52. Overview of
PostgreSQL Internals") / [8.2](/docs/8.2/overview.html "PostgreSQL 8.2 -
Chapter 52. Overview of PostgreSQL Internals") / [8.1](/docs/8.1/overview.html
"PostgreSQL 8.1 - Chapter 52. Overview of PostgreSQL Internals") /
[8.0](/docs/8.0/overview.html "PostgreSQL 8.0 - Chapter 52. Overview of
PostgreSQL Internals") / [7.4](/docs/7.4/overview.html "PostgreSQL 7.4 -
Chapter 52. Overview of PostgreSQL Internals") / [7.3](/docs/7.3/overview.html
"PostgreSQL 7.3 - Chapter 52. Overview of PostgreSQL Internals") /
[7.2](/docs/7.2/overview.html "PostgreSQL 7.2 - Chapter 52. Overview of
PostgreSQL Internals") / [7.1](/docs/7.1/overview.html "PostgreSQL 7.1 -
Chapter 52. Overview of PostgreSQL Internals")

__

Chapter 52. Overview of PostgreSQL Internals  
---  
[Prev](internals.html "Part VII. Internals")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](query-path.html "52.1. The Path of a Query")  
  
* * *

## Chapter 52. Overview of PostgreSQL Internals

**Table of Contents**

[52.1. The Path of a Query](query-path.html)

[52.2. How Connections Are Established](connect-estab.html)

[52.3. The Parser Stage](parser-stage.html)

    

[52.3.1. Parser](parser-stage.html#PARSER-STAGE-PARSER)

[52.3.2. Transformation Process](parser-stage.html#PARSER-STAGE-
TRANSFORMATION-PROCESS)

[52.4. The PostgreSQL Rule System](rule-system.html)

[52.5. Planner/Optimizer](planner-optimizer.html)

    

[52.5.1. Generating Possible Plans](planner-optimizer.html#PLANNER-OPTIMIZER-
GENERATING-POSSIBLE-PLANS)

[52.6. Executor](executor.html)

### Author

This chapter originated as part of [[sim98]](biblio.html#SIM98 "Enhancement of
the ANSI SQL Implementation of PostgreSQL") Stefan Simkovics' Master's Thesis
prepared at Vienna University of Technology under the direction of
O.Univ.Prof.Dr. Georg Gottlob and Univ.Ass. Mag. Katrin Seyr.

This chapter gives an overview of the internal structure of the backend of
PostgreSQL. After having read the following sections you should have an idea
of how a query is processed. This chapter is intended to help the reader
understand the general sequence of operations that occur within the backend
from the point at which a query is received, to the point at which the results
are returned to the client.

* * *

[Prev](internals.html "Part VII. Internals")  | [Up](internals.html "Part VII. Internals") |  [Next](query-path.html "52.1. The Path of a Query")  
---|---|---  
Part VII. Internals  | [Home](index.html "PostgreSQL 16.9 Documentation") |  52.1. The Path of a Query  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/overview.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

