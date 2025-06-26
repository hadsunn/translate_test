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

Supported Versions: [Current](/docs/current/geqo-intro2.html "PostgreSQL 17 -
62.2. Genetic Algorithms") ([17](/docs/17/geqo-intro2.html "PostgreSQL 17 -
62.2. Genetic Algorithms")) / [16](/docs/16/geqo-intro2.html "PostgreSQL 16 -
62.2. Genetic Algorithms") / [15](/docs/15/geqo-intro2.html "PostgreSQL 15 -
62.2. Genetic Algorithms") / [14](/docs/14/geqo-intro2.html "PostgreSQL 14 -
62.2. Genetic Algorithms") / [13](/docs/13/geqo-intro2.html "PostgreSQL 13 -
62.2. Genetic Algorithms")

Development Versions: [18](/docs/18/geqo-intro2.html "PostgreSQL 18 -
62.2. Genetic Algorithms") / [devel](/docs/devel/geqo-intro2.html "PostgreSQL
devel - 62.2. Genetic Algorithms")

Unsupported versions: [12](/docs/12/geqo-intro2.html "PostgreSQL 12 -
62.2. Genetic Algorithms") / [11](/docs/11/geqo-intro2.html "PostgreSQL 11 -
62.2. Genetic Algorithms") / [10](/docs/10/geqo-intro2.html "PostgreSQL 10 -
62.2. Genetic Algorithms") / [9.6](/docs/9.6/geqo-intro2.html "PostgreSQL 9.6
- 62.2. Genetic Algorithms") / [9.5](/docs/9.5/geqo-intro2.html "PostgreSQL
9.5 - 62.2. Genetic Algorithms") / [9.4](/docs/9.4/geqo-intro2.html
"PostgreSQL 9.4 - 62.2. Genetic Algorithms") / [9.3](/docs/9.3/geqo-
intro2.html "PostgreSQL 9.3 - 62.2. Genetic Algorithms") /
[9.2](/docs/9.2/geqo-intro2.html "PostgreSQL 9.2 - 62.2. Genetic Algorithms")
/ [9.1](/docs/9.1/geqo-intro2.html "PostgreSQL 9.1 - 62.2. Genetic
Algorithms") / [9.0](/docs/9.0/geqo-intro2.html "PostgreSQL 9.0 -
62.2. Genetic Algorithms") / [8.4](/docs/8.4/geqo-intro2.html "PostgreSQL 8.4
- 62.2. Genetic Algorithms") / [8.3](/docs/8.3/geqo-intro2.html "PostgreSQL
8.3 - 62.2. Genetic Algorithms") / [8.2](/docs/8.2/geqo-intro2.html
"PostgreSQL 8.2 - 62.2. Genetic Algorithms") / [8.1](/docs/8.1/geqo-
intro2.html "PostgreSQL 8.1 - 62.2. Genetic Algorithms") /
[8.0](/docs/8.0/geqo-intro2.html "PostgreSQL 8.0 - 62.2. Genetic Algorithms")
/ [7.4](/docs/7.4/geqo-intro2.html "PostgreSQL 7.4 - 62.2. Genetic
Algorithms") / [7.3](/docs/7.3/geqo-intro2.html "PostgreSQL 7.3 -
62.2. Genetic Algorithms") / [7.2](/docs/7.2/geqo-intro2.html "PostgreSQL 7.2
- 62.2. Genetic Algorithms") / [7.1](/docs/7.1/geqo-intro2.html "PostgreSQL
7.1 - 62.2. Genetic Algorithms")

__

62.2. Genetic Algorithms  
---  
[Prev](geqo-intro.html "62.1. Query Handling as a Complex Optimization Problem")  | [Up](geqo.html "Chapter 62. Genetic Query Optimizer") | Chapter 62. Genetic Query Optimizer | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](geqo-pg-intro.html "62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL")  
  
* * *

## 62.2. Genetic Algorithms #

The genetic algorithm (GA) is a heuristic optimization method which operates
through randomized search. The set of possible solutions for the optimization
problem is considered as a _population_ of _individuals_. The degree of
adaptation of an individual to its environment is specified by its _fitness_.

The coordinates of an individual in the search space are represented by
_chromosomes_ , in essence a set of character strings. A _gene_ is a
subsection of a chromosome which encodes the value of a single parameter being
optimized. Typical encodings for a gene could be _binary_ or _integer_.

Through simulation of the evolutionary operations _recombination_ , _mutation_
, and _selection_ new generations of search points are found that show a
higher average fitness than their ancestors. [Figure 62.1](geqo-
intro2.html#GEQO-FIGURE "Figure 62.1. Structure of a Genetic Algorithm")
illustrates these steps.

**Figure  62.1. Structure of a Genetic Algorithm**

  

According to the comp.ai.genetic FAQ it cannot be stressed too strongly that a
GA is not a pure random search for a solution to a problem. A GA uses
stochastic processes, but the result is distinctly non-random (better than
random).

* * *

[Prev](geqo-intro.html "62.1. Query Handling as a Complex Optimization Problem")  | [Up](geqo.html "Chapter 62. Genetic Query Optimizer") |  [Next](geqo-pg-intro.html "62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL")  
---|---|---  
62.1. Query Handling as a Complex Optimization Problem  | [Home](index.html "PostgreSQL 16.9 Documentation") |  62.3. Genetic Query Optimization (GEQO) in PostgreSQL  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/geqo-intro2.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

