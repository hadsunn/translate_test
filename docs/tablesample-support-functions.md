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

Supported Versions: [Current](/docs/current/tablesample-support-functions.html
"PostgreSQL 17 - 60.1. Sampling Method Support Functions")
([17](/docs/17/tablesample-support-functions.html "PostgreSQL 17 -
60.1. Sampling Method Support Functions")) / [16](/docs/16/tablesample-
support-functions.html "PostgreSQL 16 - 60.1. Sampling Method Support
Functions") / [15](/docs/15/tablesample-support-functions.html "PostgreSQL 15
- 60.1. Sampling Method Support Functions") / [14](/docs/14/tablesample-
support-functions.html "PostgreSQL 14 - 60.1. Sampling Method Support
Functions") / [13](/docs/13/tablesample-support-functions.html "PostgreSQL 13
- 60.1. Sampling Method Support Functions")

Development Versions: [18](/docs/18/tablesample-support-functions.html
"PostgreSQL 18 - 60.1. Sampling Method Support Functions") /
[devel](/docs/devel/tablesample-support-functions.html "PostgreSQL devel -
60.1. Sampling Method Support Functions")

Unsupported versions: [12](/docs/12/tablesample-support-functions.html
"PostgreSQL 12 - 60.1. Sampling Method Support Functions") /
[11](/docs/11/tablesample-support-functions.html "PostgreSQL 11 -
60.1. Sampling Method Support Functions") / [10](/docs/10/tablesample-support-
functions.html "PostgreSQL 10 - 60.1. Sampling Method Support Functions") /
[9.6](/docs/9.6/tablesample-support-functions.html "PostgreSQL 9.6 -
60.1. Sampling Method Support Functions") / [9.5](/docs/9.5/tablesample-
support-functions.html "PostgreSQL 9.5 - 60.1. Sampling Method Support
Functions")

__

60.1. Sampling Method Support Functions  
---  
[Prev](tablesample-method.html "Chapter 60. Writing a Table Sampling Method")  | [Up](tablesample-method.html "Chapter 60. Writing a Table Sampling Method") | Chapter 60. Writing a Table Sampling Method | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](custom-scan.html "Chapter 61. Writing a Custom Scan Provider")  
  
* * *

## 60.1. Sampling Method Support Functions #

The TSM handler function returns a palloc'd `TsmRoutine` struct containing
pointers to the support functions described below. Most of the functions are
required, but some are optional, and those pointers can be NULL.

    
    
    void
    SampleScanGetSampleSize (PlannerInfo *root,
                             RelOptInfo *baserel,
                             List *paramexprs,
                             BlockNumber *pages,
                             double *tuples);
    

This function is called during planning. It must estimate the number of
relation pages that will be read during a sample scan, and the number of
tuples that will be selected by the scan. (For example, these might be
determined by estimating the sampling fraction, and then multiplying the
`baserel->pages` and `baserel->tuples` numbers by that, being sure to round
the results to integral values.) The `paramexprs` list holds the expression(s)
that are parameters to the `TABLESAMPLE` clause. It is recommended to use
`estimate_expression_value()` to try to reduce these expressions to constants,
if their values are needed for estimation purposes; but the function must
provide size estimates even if they cannot be reduced, and it should not fail
even if the values appear invalid (remember that they're only estimates of
what the run-time values will be). The `pages` and `tuples` parameters are
outputs.

    
    
    void
    InitSampleScan (SampleScanState *node,
                    int eflags);
    

Initialize for execution of a SampleScan plan node. This is called during
executor startup. It should perform any initialization needed before
processing can start. The `SampleScanState` node has already been created, but
its `tsm_state` field is NULL. The `InitSampleScan` function can palloc
whatever internal state data is needed by the sampling method, and store a
pointer to it in `node->tsm_state`. Information about the table to scan is
accessible through other fields of the `SampleScanState` node (but note that
the `node->ss.ss_currentScanDesc` scan descriptor is not set up yet). `eflags`
contains flag bits describing the executor's operating mode for this plan
node.

When `(eflags & EXEC_FLAG_EXPLAIN_ONLY)` is true, the scan will not actually
be performed, so this function should only do the minimum required to make the
node state valid for `EXPLAIN` and `EndSampleScan`.

This function can be omitted (set the pointer to NULL), in which case
`BeginSampleScan` must perform all initialization needed by the sampling
method.

    
    
    void
    BeginSampleScan (SampleScanState *node,
                     Datum *params,
                     int nparams,
                     uint32 seed);
    

Begin execution of a sampling scan. This is called just before the first
attempt to fetch a tuple, and may be called again if the scan needs to be
restarted. Information about the table to scan is accessible through fields of
the `SampleScanState` node (but note that the `node->ss.ss_currentScanDesc`
scan descriptor is not set up yet). The `params` array, of length `nparams`,
contains the values of the parameters supplied in the `TABLESAMPLE` clause.
These will have the number and types specified in the sampling method's
`parameterTypes` list, and have been checked to not be null. `seed` contains a
seed to use for any random numbers generated within the sampling method; it is
either a hash derived from the `REPEATABLE` value if one was given, or the
result of `random()` if not.

This function may adjust the fields `node->use_bulkread` and
`node->use_pagemode`. If `node->use_bulkread` is `true`, which it is by
default, the scan will use a buffer access strategy that encourages recycling
buffers after use. It might be reasonable to set this to `false` if the scan
will visit only a small fraction of the table's pages. If `node->use_pagemode`
is `true`, which it is by default, the scan will perform visibility checking
in a single pass for all tuples on each visited page. It might be reasonable
to set this to `false` if the scan will select only a small fraction of the
tuples on each visited page. That will result in fewer tuple visibility checks
being performed, though each one will be more expensive because it will
require more locking.

If the sampling method is marked `repeatable_across_scans`, it must be able to
select the same set of tuples during a rescan as it did originally, that is a
fresh call of `BeginSampleScan` must lead to selecting the same tuples as
before (if the `TABLESAMPLE` parameters and seed don't change).

    
    
    BlockNumber
    NextSampleBlock (SampleScanState *node, BlockNumber nblocks);
    

Returns the block number of the next page to be scanned, or
`InvalidBlockNumber` if no pages remain to be scanned.

This function can be omitted (set the pointer to NULL), in which case the core
code will perform a sequential scan of the entire relation. Such a scan can
use synchronized scanning, so that the sampling method cannot assume that the
relation pages are visited in the same order on each scan.

    
    
    OffsetNumber
    NextSampleTuple (SampleScanState *node,
                     BlockNumber blockno,
                     OffsetNumber maxoffset);
    

Returns the offset number of the next tuple to be sampled on the specified
page, or `InvalidOffsetNumber` if no tuples remain to be sampled. `maxoffset`
is the largest offset number in use on the page.

### Note

`NextSampleTuple` is not explicitly told which of the offset numbers in the
range `1 .. maxoffset` actually contain valid tuples. This is not normally a
problem since the core code ignores requests to sample missing or invisible
tuples; that should not result in any bias in the sample. However, if
necessary, the function can use `node->donetuples` to examine how many of the
tuples it returned were valid and visible.

### Note

`NextSampleTuple` must _not_ assume that `blockno` is the same page number
returned by the most recent `NextSampleBlock` call. It was returned by some
previous `NextSampleBlock` call, but the core code is allowed to call
`NextSampleBlock` in advance of actually scanning pages, so as to support
prefetching. It is OK to assume that once sampling of a given page begins,
successive `NextSampleTuple` calls all refer to the same page until
`InvalidOffsetNumber` is returned.

    
    
    void
    EndSampleScan (SampleScanState *node);
    

End the scan and release resources. It is normally not important to release
palloc'd memory, but any externally-visible resources should be cleaned up.
This function can be omitted (set the pointer to NULL) in the common case
where no such resources exist.

* * *

[Prev](tablesample-method.html "Chapter 60. Writing a Table Sampling Method")  | [Up](tablesample-method.html "Chapter 60. Writing a Table Sampling Method") |  [Next](custom-scan.html "Chapter 61. Writing a Custom Scan Provider")  
---|---|---  
Chapter 60. Writing a Table Sampling Method  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 61. Writing a Custom Scan Provider  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tablesample-support-
functions.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

