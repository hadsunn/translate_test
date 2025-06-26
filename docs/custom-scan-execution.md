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

Supported Versions: [Current](/docs/current/custom-scan-execution.html
"PostgreSQL 17 - 61.3. Executing Custom Scans") ([17](/docs/17/custom-scan-
execution.html "PostgreSQL 17 - 61.3. Executing Custom Scans")) /
[16](/docs/16/custom-scan-execution.html "PostgreSQL 16 - 61.3. Executing
Custom Scans") / [15](/docs/15/custom-scan-execution.html "PostgreSQL 15 -
61.3. Executing Custom Scans") / [14](/docs/14/custom-scan-execution.html
"PostgreSQL 14 - 61.3. Executing Custom Scans") / [13](/docs/13/custom-scan-
execution.html "PostgreSQL 13 - 61.3. Executing Custom Scans")

Development Versions: [18](/docs/18/custom-scan-execution.html "PostgreSQL 18
- 61.3. Executing Custom Scans") / [devel](/docs/devel/custom-scan-
execution.html "PostgreSQL devel - 61.3. Executing Custom Scans")

Unsupported versions: [12](/docs/12/custom-scan-execution.html "PostgreSQL 12
- 61.3. Executing Custom Scans") / [11](/docs/11/custom-scan-execution.html
"PostgreSQL 11 - 61.3. Executing Custom Scans") / [10](/docs/10/custom-scan-
execution.html "PostgreSQL 10 - 61.3. Executing Custom Scans") /
[9.6](/docs/9.6/custom-scan-execution.html "PostgreSQL 9.6 - 61.3. Executing
Custom Scans") / [9.5](/docs/9.5/custom-scan-execution.html "PostgreSQL 9.5 -
61.3. Executing Custom Scans")

__

61.3. Executing Custom Scans  
---  
[Prev](custom-scan-plan.html "61.2. Creating Custom Scan Plans")  | [Up](custom-scan.html "Chapter 61. Writing a Custom Scan Provider") | Chapter 61. Writing a Custom Scan Provider | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](geqo.html "Chapter 62. Genetic Query Optimizer")  
  
* * *

## 61.3. Executing Custom Scans #

[61.3.1. Custom Scan Execution Callbacks](custom-scan-execution.html#CUSTOM-
SCAN-EXECUTION-CALLBACKS)

When a `CustomScan` is executed, its execution state is represented by a
`CustomScanState`, which is declared as follows:

    
    
    typedef struct CustomScanState
    {
        ScanState ss;
        uint32    flags;
        const CustomExecMethods *methods;
    } CustomScanState;
    

`ss` is initialized as for any other scan state, except that if the scan is
for a join rather than a base relation, `ss.ss_currentRelation` is left NULL.
`flags` is a bit mask with the same meaning as in `CustomPath` and
`CustomScan`. `methods` must point to a (usually statically allocated) object
implementing the required custom scan state methods, which are further
detailed below. Typically, a `CustomScanState`, which need not support
`copyObject`, will actually be a larger structure embedding the above as its
first member.

### 61.3.1. Custom Scan Execution Callbacks #

    
    
    void (*BeginCustomScan) (CustomScanState *node,
                             EState *estate,
                             int eflags);
    

Complete initialization of the supplied `CustomScanState`. Standard fields
have been initialized by `ExecInitCustomScan`, but any private fields should
be initialized here.

    
    
    TupleTableSlot *(*ExecCustomScan) (CustomScanState *node);
    

Fetch the next scan tuple. If any tuples remain, it should fill
`ps_ResultTupleSlot` with the next tuple in the current scan direction, and
then return the tuple slot. If not, `NULL` or an empty slot should be
returned.

    
    
    void (*EndCustomScan) (CustomScanState *node);
    

Clean up any private data associated with the `CustomScanState`. This method
is required, but it does not need to do anything if there is no associated
data or it will be cleaned up automatically.

    
    
    void (*ReScanCustomScan) (CustomScanState *node);
    

Rewind the current scan to the beginning and prepare to rescan the relation.

    
    
    void (*MarkPosCustomScan) (CustomScanState *node);
    

Save the current scan position so that it can subsequently be restored by the
`RestrPosCustomScan` callback. This callback is optional, and need only be
supplied if the `CUSTOMPATH_SUPPORT_MARK_RESTORE` flag is set.

    
    
    void (*RestrPosCustomScan) (CustomScanState *node);
    

Restore the previous scan position as saved by the `MarkPosCustomScan`
callback. This callback is optional, and need only be supplied if the
`CUSTOMPATH_SUPPORT_MARK_RESTORE` flag is set.

    
    
    Size (*EstimateDSMCustomScan) (CustomScanState *node,
                                   ParallelContext *pcxt);
    

Estimate the amount of dynamic shared memory that will be required for
parallel operation. This may be higher than the amount that will actually be
used, but it must not be lower. The return value is in bytes. This callback is
optional, and need only be supplied if this custom scan provider supports
parallel execution.

    
    
    void (*InitializeDSMCustomScan) (CustomScanState *node,
                                     ParallelContext *pcxt,
                                     void *coordinate);
    

Initialize the dynamic shared memory that will be required for parallel
operation. `coordinate` points to a shared memory area of size equal to the
return value of `EstimateDSMCustomScan`. This callback is optional, and need
only be supplied if this custom scan provider supports parallel execution.

    
    
    void (*ReInitializeDSMCustomScan) (CustomScanState *node,
                                       ParallelContext *pcxt,
                                       void *coordinate);
    

Re-initialize the dynamic shared memory required for parallel operation when
the custom-scan plan node is about to be re-scanned. This callback is
optional, and need only be supplied if this custom scan provider supports
parallel execution. Recommended practice is that this callback reset only
shared state, while the `ReScanCustomScan` callback resets only local state.
Currently, this callback will be called before `ReScanCustomScan`, but it's
best not to rely on that ordering.

    
    
    void (*InitializeWorkerCustomScan) (CustomScanState *node,
                                        shm_toc *toc,
                                        void *coordinate);
    

Initialize a parallel worker's local state based on the shared state set up by
the leader during `InitializeDSMCustomScan`. This callback is optional, and
need only be supplied if this custom scan provider supports parallel
execution.

    
    
    void (*ShutdownCustomScan) (CustomScanState *node);
    

Release resources when it is anticipated the node will not be executed to
completion. This is not called in all cases; sometimes, `EndCustomScan` may be
called without this function having been called first. Since the DSM segment
used by parallel query is destroyed just after this callback is invoked,
custom scan providers that wish to take some action before the DSM segment
goes away should implement this method.

    
    
    void (*ExplainCustomScan) (CustomScanState *node,
                               List *ancestors,
                               ExplainState *es);
    

Output additional information for `EXPLAIN` of a custom-scan plan node. This
callback is optional. Common data stored in the `ScanState`, such as the
target list and scan relation, will be shown even without this callback, but
the callback allows the display of additional, private state.

* * *

[Prev](custom-scan-plan.html "61.2. Creating Custom Scan Plans")  | [Up](custom-scan.html "Chapter 61. Writing a Custom Scan Provider") |  [Next](geqo.html "Chapter 62. Genetic Query Optimizer")  
---|---|---  
61.2. Creating Custom Scan Plans  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 62. Genetic Query Optimizer  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/custom-scan-execution.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

