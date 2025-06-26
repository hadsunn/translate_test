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

Supported Versions: [Current](/docs/current/geqo.html "PostgreSQL 17 -
Chapter 62. Genetic Query Optimizer") ([17](/docs/17/geqo.html "PostgreSQL 17
- Chapter 62. Genetic Query Optimizer")) / [16](/docs/16/geqo.html "PostgreSQL
16 - Chapter 62. Genetic Query Optimizer") / [15](/docs/15/geqo.html
"PostgreSQL 15 - Chapter 62. Genetic Query Optimizer") /
[14](/docs/14/geqo.html "PostgreSQL 14 - Chapter 62. Genetic Query Optimizer")
/ [13](/docs/13/geqo.html "PostgreSQL 13 - Chapter 62. Genetic Query
Optimizer")

Development Versions: [18](/docs/18/geqo.html "PostgreSQL 18 -
Chapter 62. Genetic Query Optimizer") / [devel](/docs/devel/geqo.html
"PostgreSQL devel - Chapter 62. Genetic Query Optimizer")

Unsupported versions: [12](/docs/12/geqo.html "PostgreSQL 12 -
Chapter 62. Genetic Query Optimizer") / [11](/docs/11/geqo.html "PostgreSQL 11
- Chapter 62. Genetic Query Optimizer") / [10](/docs/10/geqo.html "PostgreSQL
10 - Chapter 62. Genetic Query Optimizer") / [9.6](/docs/9.6/geqo.html
"PostgreSQL 9.6 - Chapter 62. Genetic Query Optimizer") /
[9.5](/docs/9.5/geqo.html "PostgreSQL 9.5 - Chapter 62. Genetic Query
Optimizer") / [9.4](/docs/9.4/geqo.html "PostgreSQL 9.4 - Chapter 62. Genetic
Query Optimizer") / [9.3](/docs/9.3/geqo.html "PostgreSQL 9.3 -
Chapter 62. Genetic Query Optimizer") / [9.2](/docs/9.2/geqo.html "PostgreSQL
9.2 - Chapter 62. Genetic Query Optimizer") / [9.1](/docs/9.1/geqo.html
"PostgreSQL 9.1 - Chapter 62. Genetic Query Optimizer") /
[9.0](/docs/9.0/geqo.html "PostgreSQL 9.0 - Chapter 62. Genetic Query
Optimizer") / [8.4](/docs/8.4/geqo.html "PostgreSQL 8.4 - Chapter 62. Genetic
Query Optimizer") / [8.3](/docs/8.3/geqo.html "PostgreSQL 8.3 -
Chapter 62. Genetic Query Optimizer") / [8.2](/docs/8.2/geqo.html "PostgreSQL
8.2 - Chapter 62. Genetic Query Optimizer") / [8.1](/docs/8.1/geqo.html
"PostgreSQL 8.1 - Chapter 62. Genetic Query Optimizer") /
[8.0](/docs/8.0/geqo.html "PostgreSQL 8.0 - Chapter 62. Genetic Query
Optimizer") / [7.4](/docs/7.4/geqo.html "PostgreSQL 7.4 - Chapter 62. Genetic
Query Optimizer") / [7.3](/docs/7.3/geqo.html "PostgreSQL 7.3 -
Chapter 62. Genetic Query Optimizer") / [7.2](/docs/7.2/geqo.html "PostgreSQL
7.2 - Chapter 62. Genetic Query Optimizer") / [7.1](/docs/7.1/geqo.html
"PostgreSQL 7.1 - Chapter 62. Genetic Query Optimizer")

__

Chapter 62. Genetic Query Optimizer  
---  
[Prev](custom-scan-execution.html "61.3. Executing Custom Scans")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](geqo-intro.html "62.1. Query Handling as a Complex Optimization Problem")  
  
* * *

## Chapter 62. Genetic Query Optimizer

**Table of Contents**

[62.1. Query Handling as a Complex Optimization Problem](geqo-intro.html)

[62.2. Genetic Algorithms](geqo-intro2.html)

[62.3. Genetic Query Optimization (GEQO) in PostgreSQL](geqo-pg-intro.html)

    

[62.3.1. Generating Possible Plans with GEQO](geqo-pg-intro.html#GEQO-PG-
INTRO-GEN-POSSIBLE-PLANS)

[62.3.2. Future Implementation Tasks for PostgreSQL GEQO](geqo-pg-
intro.html#GEQO-FUTURE)

[62.4. Further Reading](geqo-biblio.html)

### Author

Written by Martin Utesch (`<[utesch@aut.tu-freiberg.de](mailto:utesch@aut.tu-
freiberg.de)>`) for the Institute of Automatic Control at the University of
Mining and Technology in Freiberg, Germany.

* * *

[Prev](custom-scan-execution.html "61.3. Executing Custom Scans")  | [Up](internals.html "Part VII. Internals") |  [Next](geqo-intro.html "62.1. Query Handling as a Complex Optimization Problem")  
---|---|---  
61.3. Executing Custom Scans  | [Home](index.html "PostgreSQL 16.9 Documentation") |  62.1. Query Handling as a Complex Optimization Problem  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/geqo.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

