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

Supported Versions: [Current](/docs/current/index-cost-estimation.html
"PostgreSQL 17 - 64.6. Index Cost Estimation Functions") ([17](/docs/17/index-
cost-estimation.html "PostgreSQL 17 - 64.6. Index Cost Estimation Functions"))
/ [16](/docs/16/index-cost-estimation.html "PostgreSQL 16 - 64.6. Index Cost
Estimation Functions") / [15](/docs/15/index-cost-estimation.html "PostgreSQL
15 - 64.6. Index Cost Estimation Functions") / [14](/docs/14/index-cost-
estimation.html "PostgreSQL 14 - 64.6. Index Cost Estimation Functions") /
[13](/docs/13/index-cost-estimation.html "PostgreSQL 13 - 64.6. Index Cost
Estimation Functions")

Development Versions: [18](/docs/18/index-cost-estimation.html "PostgreSQL 18
- 64.6. Index Cost Estimation Functions") / [devel](/docs/devel/index-cost-
estimation.html "PostgreSQL devel - 64.6. Index Cost Estimation Functions")

Unsupported versions: [12](/docs/12/index-cost-estimation.html "PostgreSQL 12
- 64.6. Index Cost Estimation Functions") / [11](/docs/11/index-cost-
estimation.html "PostgreSQL 11 - 64.6. Index Cost Estimation Functions") /
[10](/docs/10/index-cost-estimation.html "PostgreSQL 10 - 64.6. Index Cost
Estimation Functions") / [9.6](/docs/9.6/index-cost-estimation.html
"PostgreSQL 9.6 - 64.6. Index Cost Estimation Functions") /
[9.5](/docs/9.5/index-cost-estimation.html "PostgreSQL 9.5 - 64.6. Index Cost
Estimation Functions") / [9.4](/docs/9.4/index-cost-estimation.html
"PostgreSQL 9.4 - 64.6. Index Cost Estimation Functions") /
[9.3](/docs/9.3/index-cost-estimation.html "PostgreSQL 9.3 - 64.6. Index Cost
Estimation Functions") / [9.2](/docs/9.2/index-cost-estimation.html
"PostgreSQL 9.2 - 64.6. Index Cost Estimation Functions") /
[9.1](/docs/9.1/index-cost-estimation.html "PostgreSQL 9.1 - 64.6. Index Cost
Estimation Functions") / [9.0](/docs/9.0/index-cost-estimation.html
"PostgreSQL 9.0 - 64.6. Index Cost Estimation Functions") /
[8.4](/docs/8.4/index-cost-estimation.html "PostgreSQL 8.4 - 64.6. Index Cost
Estimation Functions") / [8.3](/docs/8.3/index-cost-estimation.html
"PostgreSQL 8.3 - 64.6. Index Cost Estimation Functions") /
[8.2](/docs/8.2/index-cost-estimation.html "PostgreSQL 8.2 - 64.6. Index Cost
Estimation Functions") / [8.1](/docs/8.1/index-cost-estimation.html
"PostgreSQL 8.1 - 64.6. Index Cost Estimation Functions")

__

64.6. Index Cost Estimation Functions  
---  
[Prev](index-unique-checks.html "64.5. Index Uniqueness Checks")  | [Up](indexam.html "Chapter 64. Index Access Method Interface Definition") | Chapter 64. Index Access Method Interface Definition | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](generic-wal.html "Chapter 65. Generic WAL Records")  
  
* * *

## 64.6. Index Cost Estimation Functions #

The `amcostestimate` function is given information describing a possible index
scan, including lists of WHERE and ORDER BY clauses that have been determined
to be usable with the index. It must return estimates of the cost of accessing
the index and the selectivity of the WHERE clauses (that is, the fraction of
parent-table rows that will be retrieved during the index scan). For simple
cases, nearly all the work of the cost estimator can be done by calling
standard routines in the optimizer; the point of having an `amcostestimate`
function is to allow index access methods to provide index-type-specific
knowledge, in case it is possible to improve on the standard estimates.

Each `amcostestimate` function must have the signature:

    
    
    void
    amcostestimate (PlannerInfo *root,
                    IndexPath *path,
                    double loop_count,
                    Cost *indexStartupCost,
                    Cost *indexTotalCost,
                    Selectivity *indexSelectivity,
                    double *indexCorrelation,
                    double *indexPages);
    

The first three parameters are inputs:

_`root`_

    

The planner's information about the query being processed.

_`path`_

    

The index access path being considered. All fields except cost and selectivity
values are valid.

_`loop_count`_

    

The number of repetitions of the index scan that should be factored into the
cost estimates. This will typically be greater than one when considering a
parameterized scan for use in the inside of a nestloop join. Note that the
cost estimates should still be for just one scan; a larger _`loop_count`_
means that it may be appropriate to allow for some caching effects across
multiple scans.

The last five parameters are pass-by-reference outputs:

_`*indexStartupCost`_

    

Set to cost of index start-up processing

_`*indexTotalCost`_

    

Set to total cost of index processing

_`*indexSelectivity`_

    

Set to index selectivity

_`*indexCorrelation`_

    

Set to correlation coefficient between index scan order and underlying table's
order

_`*indexPages`_

    

Set to number of index leaf pages

Note that cost estimate functions must be written in C, not in SQL or any
available procedural language, because they must access internal data
structures of the planner/optimizer.

The index access costs should be computed using the parameters used by
`src/backend/optimizer/path/costsize.c`: a sequential disk block fetch has
cost `seq_page_cost`, a nonsequential fetch has cost `random_page_cost`, and
the cost of processing one index row should usually be taken as
`cpu_index_tuple_cost`. In addition, an appropriate multiple of
`cpu_operator_cost` should be charged for any comparison operators invoked
during index processing (especially evaluation of the indexquals themselves).

The access costs should include all disk and CPU costs associated with
scanning the index itself, but _not_ the costs of retrieving or processing the
parent-table rows that are identified by the index.

The “start-up cost” is the part of the total scan cost that must be expended
before we can begin to fetch the first row. For most indexes this can be taken
as zero, but an index type with a high start-up cost might want to set it
nonzero.

The _`indexSelectivity`_ should be set to the estimated fraction of the parent
table rows that will be retrieved during the index scan. In the case of a
lossy query, this will typically be higher than the fraction of rows that
actually pass the given qual conditions.

The _`indexCorrelation`_ should be set to the correlation (ranging between
-1.0 and 1.0) between the index order and the table order. This is used to
adjust the estimate for the cost of fetching rows from the parent table.

The _`indexPages`_ should be set to the number of leaf pages. This is used to
estimate the number of workers for parallel index scan.

When _`loop_count`_ is greater than one, the returned numbers should be
averages expected for any one scan of the index.

**Cost Estimation**

A typical cost estimator will proceed as follows:

  1. Estimate and return the fraction of parent-table rows that will be visited based on the given qual conditions. In the absence of any index-type-specific knowledge, use the standard optimizer function `clauselist_selectivity()`:
         
         *indexSelectivity = clauselist_selectivity(root, path->indexquals,
                                                    path->indexinfo->rel->relid,
                                                    JOIN_INNER, NULL);
         

  2. Estimate the number of index rows that will be visited during the scan. For many index types this is the same as _`indexSelectivity`_ times the number of rows in the index, but it might be more. (Note that the index's size in pages and rows is available from the `path->indexinfo` struct.)

  3. Estimate the number of index pages that will be retrieved during the scan. This might be just _`indexSelectivity`_ times the index's size in pages.

  4. Compute the index access cost. A generic estimator might do this:
         
         /*
          * Our generic assumption is that the index pages will be read
          * sequentially, so they cost seq_page_cost each, not random_page_cost.
          * Also, we charge for evaluation of the indexquals at each index row.
          * All the costs are assumed to be paid incrementally during the scan.
          */
         cost_qual_eval(&index_qual_cost, path->indexquals, root);
         *indexStartupCost = index_qual_cost.startup;
         *indexTotalCost = seq_page_cost * numIndexPages +
             (cpu_index_tuple_cost + index_qual_cost.per_tuple) * numIndexTuples;
         

However, the above does not account for amortization of index reads across
repeated index scans.

  5. Estimate the index correlation. For a simple ordered index on a single field, this can be retrieved from pg_statistic. If the correlation is not known, the conservative estimate is zero (no correlation).

Examples of cost estimator functions can be found in
`src/backend/utils/adt/selfuncs.c`.

* * *

[Prev](index-unique-checks.html "64.5. Index Uniqueness Checks")  | [Up](indexam.html "Chapter 64. Index Access Method Interface Definition") |  [Next](generic-wal.html "Chapter 65. Generic WAL Records")  
---|---|---  
64.5. Index Uniqueness Checks  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 65. Generic WAL Records  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/index-cost-estimation.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

