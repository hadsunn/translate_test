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

Supported Versions: [Current](/docs/current/geqo-pg-intro.html "PostgreSQL 17
- 62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL")
([17](/docs/17/geqo-pg-intro.html "PostgreSQL 17 - 62.3. Genetic Query
Optimization \(GEQO\) in PostgreSQL")) / [16](/docs/16/geqo-pg-intro.html
"PostgreSQL 16 - 62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL") /
[15](/docs/15/geqo-pg-intro.html "PostgreSQL 15 - 62.3. Genetic Query
Optimization \(GEQO\) in PostgreSQL") / [14](/docs/14/geqo-pg-intro.html
"PostgreSQL 14 - 62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL") /
[13](/docs/13/geqo-pg-intro.html "PostgreSQL 13 - 62.3. Genetic Query
Optimization \(GEQO\) in PostgreSQL")

Development Versions: [18](/docs/18/geqo-pg-intro.html "PostgreSQL 18 -
62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL") /
[devel](/docs/devel/geqo-pg-intro.html "PostgreSQL devel - 62.3. Genetic Query
Optimization \(GEQO\) in PostgreSQL")

Unsupported versions: [12](/docs/12/geqo-pg-intro.html "PostgreSQL 12 -
62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL") /
[11](/docs/11/geqo-pg-intro.html "PostgreSQL 11 - 62.3. Genetic Query
Optimization \(GEQO\) in PostgreSQL") / [10](/docs/10/geqo-pg-intro.html
"PostgreSQL 10 - 62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL") /
[9.6](/docs/9.6/geqo-pg-intro.html "PostgreSQL 9.6 - 62.3. Genetic Query
Optimization \(GEQO\) in PostgreSQL") / [9.5](/docs/9.5/geqo-pg-intro.html
"PostgreSQL 9.5 - 62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL") /
[9.4](/docs/9.4/geqo-pg-intro.html "PostgreSQL 9.4 - 62.3. Genetic Query
Optimization \(GEQO\) in PostgreSQL") / [9.3](/docs/9.3/geqo-pg-intro.html
"PostgreSQL 9.3 - 62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL") /
[9.2](/docs/9.2/geqo-pg-intro.html "PostgreSQL 9.2 - 62.3. Genetic Query
Optimization \(GEQO\) in PostgreSQL") / [9.1](/docs/9.1/geqo-pg-intro.html
"PostgreSQL 9.1 - 62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL") /
[9.0](/docs/9.0/geqo-pg-intro.html "PostgreSQL 9.0 - 62.3. Genetic Query
Optimization \(GEQO\) in PostgreSQL") / [8.4](/docs/8.4/geqo-pg-intro.html
"PostgreSQL 8.4 - 62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL") /
[8.3](/docs/8.3/geqo-pg-intro.html "PostgreSQL 8.3 - 62.3. Genetic Query
Optimization \(GEQO\) in PostgreSQL") / [8.2](/docs/8.2/geqo-pg-intro.html
"PostgreSQL 8.2 - 62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL") /
[8.1](/docs/8.1/geqo-pg-intro.html "PostgreSQL 8.1 - 62.3. Genetic Query
Optimization \(GEQO\) in PostgreSQL") / [8.0](/docs/8.0/geqo-pg-intro.html
"PostgreSQL 8.0 - 62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL") /
[7.4](/docs/7.4/geqo-pg-intro.html "PostgreSQL 7.4 - 62.3. Genetic Query
Optimization \(GEQO\) in PostgreSQL") / [7.3](/docs/7.3/geqo-pg-intro.html
"PostgreSQL 7.3 - 62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL") /
[7.2](/docs/7.2/geqo-pg-intro.html "PostgreSQL 7.2 - 62.3. Genetic Query
Optimization \(GEQO\) in PostgreSQL") / [7.1](/docs/7.1/geqo-pg-intro.html
"PostgreSQL 7.1 - 62.3. Genetic Query Optimization \(GEQO\) in PostgreSQL")

__

62.3. Genetic Query Optimization (GEQO) in PostgreSQL  
---  
[Prev](geqo-intro2.html "62.2. Genetic Algorithms")  | [Up](geqo.html "Chapter 62. Genetic Query Optimizer") | Chapter 62. Genetic Query Optimizer | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](geqo-biblio.html "62.4. Further Reading")  
  
* * *

## 62.3. Genetic Query Optimization (GEQO) in PostgreSQL #

[62.3.1. Generating Possible Plans with GEQO](geqo-pg-intro.html#GEQO-PG-
INTRO-GEN-POSSIBLE-PLANS)

[62.3.2. Future Implementation Tasks for PostgreSQL GEQO](geqo-pg-
intro.html#GEQO-FUTURE)

The GEQO module approaches the query optimization problem as though it were
the well-known traveling salesman problem (TSP). Possible query plans are
encoded as integer strings. Each string represents the join order from one
relation of the query to the next. For example, the join tree

    
    
       /\
      /\ 2
     /\ 3
    4  1
    

is encoded by the integer string '4-1-3-2', which means, first join relation
'4' and '1', then '3', and then '2', where 1, 2, 3, 4 are relation IDs within
the PostgreSQL optimizer.

Specific characteristics of the GEQO implementation in PostgreSQL are:

  * Usage of a _steady state_ GA (replacement of the least fit individuals in a population, not whole-generational replacement) allows fast convergence towards improved query plans. This is essential for query handling with reasonable time;

  * Usage of _edge recombination crossover_ which is especially suited to keep edge losses low for the solution of the TSP by means of a GA;

  * Mutation as genetic operator is deprecated so that no repair mechanisms are needed to generate legal TSP tours.

Parts of the GEQO module are adapted from D. Whitley's Genitor algorithm.

The GEQO module allows the PostgreSQL query optimizer to support large join
queries effectively through non-exhaustive search.

### 62.3.1. Generating Possible Plans with GEQO #

The GEQO planning process uses the standard planner code to generate plans for
scans of individual relations. Then join plans are developed using the genetic
approach. As shown above, each candidate join plan is represented by a
sequence in which to join the base relations. In the initial stage, the GEQO
code simply generates some possible join sequences at random. For each join
sequence considered, the standard planner code is invoked to estimate the cost
of performing the query using that join sequence. (For each step of the join
sequence, all three possible join strategies are considered; and all the
initially-determined relation scan plans are available. The estimated cost is
the cheapest of these possibilities.) Join sequences with lower estimated cost
are considered “more fit” than those with higher cost. The genetic algorithm
discards the least fit candidates. Then new candidates are generated by
combining genes of more-fit candidates — that is, by using randomly-chosen
portions of known low-cost join sequences to create new sequences for
consideration. This process is repeated until a preset number of join
sequences have been considered; then the best one found at any time during the
search is used to generate the finished plan.

This process is inherently nondeterministic, because of the randomized choices
made during both the initial population selection and subsequent “mutation” of
the best candidates. To avoid surprising changes of the selected plan, each
run of the GEQO algorithm restarts its random number generator with the
current [geqo_seed](runtime-config-query.html#GUC-GEQO-SEED) parameter
setting. As long as `geqo_seed` and the other GEQO parameters are kept fixed,
the same plan will be generated for a given query (and other planner inputs
such as statistics). To experiment with different search paths, try changing
`geqo_seed`.

### 62.3.2. Future Implementation Tasks for PostgreSQL GEQO #

Work is still needed to improve the genetic algorithm parameter settings. In
file `src/backend/optimizer/geqo/geqo_main.c`, routines `gimme_pool_size` and
`gimme_number_generations`, we have to find a compromise for the parameter
settings to satisfy two competing demands:

  * Optimality of the query plan

  * Computing time

In the current implementation, the fitness of each candidate join sequence is
estimated by running the standard planner's join selection and cost estimation
code from scratch. To the extent that different candidates use similar sub-
sequences of joins, a great deal of work will be repeated. This could be made
significantly faster by retaining cost estimates for sub-joins. The problem is
to avoid expending unreasonable amounts of memory on retaining that state.

At a more basic level, it is not clear that solving query optimization with a
GA algorithm designed for TSP is appropriate. In the TSP case, the cost
associated with any substring (partial tour) is independent of the rest of the
tour, but this is certainly not true for query optimization. Thus it is
questionable whether edge recombination crossover is the most effective
mutation procedure.

* * *

[Prev](geqo-intro2.html "62.2. Genetic Algorithms")  | [Up](geqo.html "Chapter 62. Genetic Query Optimizer") |  [Next](geqo-biblio.html "62.4. Further Reading")  
---|---|---  
62.2. Genetic Algorithms  | [Home](index.html "PostgreSQL 16.9 Documentation") |  62.4. Further Reading  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/geqo-pg-intro.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

