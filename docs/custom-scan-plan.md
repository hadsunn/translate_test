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

Supported Versions: [Current](/docs/current/custom-scan-plan.html "PostgreSQL
17 - 61.2. Creating Custom Scan Plans") ([17](/docs/17/custom-scan-plan.html
"PostgreSQL 17 - 61.2. Creating Custom Scan Plans")) / [16](/docs/16/custom-
scan-plan.html "PostgreSQL 16 - 61.2. Creating Custom Scan Plans") /
[15](/docs/15/custom-scan-plan.html "PostgreSQL 15 - 61.2. Creating Custom
Scan Plans") / [14](/docs/14/custom-scan-plan.html "PostgreSQL 14 -
61.2. Creating Custom Scan Plans") / [13](/docs/13/custom-scan-plan.html
"PostgreSQL 13 - 61.2. Creating Custom Scan Plans")

Development Versions: [18](/docs/18/custom-scan-plan.html "PostgreSQL 18 -
61.2. Creating Custom Scan Plans") / [devel](/docs/devel/custom-scan-plan.html
"PostgreSQL devel - 61.2. Creating Custom Scan Plans")

Unsupported versions: [12](/docs/12/custom-scan-plan.html "PostgreSQL 12 -
61.2. Creating Custom Scan Plans") / [11](/docs/11/custom-scan-plan.html
"PostgreSQL 11 - 61.2. Creating Custom Scan Plans") / [10](/docs/10/custom-
scan-plan.html "PostgreSQL 10 - 61.2. Creating Custom Scan Plans") /
[9.6](/docs/9.6/custom-scan-plan.html "PostgreSQL 9.6 - 61.2. Creating Custom
Scan Plans") / [9.5](/docs/9.5/custom-scan-plan.html "PostgreSQL 9.5 -
61.2. Creating Custom Scan Plans")

__

61.2. Creating Custom Scan Plans  
---  
[Prev](custom-scan-path.html "61.1. Creating Custom Scan Paths")  | [Up](custom-scan.html "Chapter 61. Writing a Custom Scan Provider") | Chapter 61. Writing a Custom Scan Provider | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](custom-scan-execution.html "61.3. Executing Custom Scans")  
  
* * *

## 61.2. Creating Custom Scan Plans #

[61.2.1. Custom Scan Plan Callbacks](custom-scan-plan.html#CUSTOM-SCAN-PLAN-
CALLBACKS)

A custom scan is represented in a finished plan tree using the following
structure:

    
    
    typedef struct CustomScan
    {
        Scan      scan;
        uint32    flags;
        List     *custom_plans;
        List     *custom_exprs;
        List     *custom_private;
        List     *custom_scan_tlist;
        Bitmapset *custom_relids;
        const CustomScanMethods *methods;
    } CustomScan;
    

`scan` must be initialized as for any other scan, including estimated costs,
target lists, qualifications, and so on. `flags` is a bit mask with the same
meaning as in `CustomPath`. `custom_plans` can be used to store child `Plan`
nodes. `custom_exprs` should be used to store expression trees that will need
to be fixed up by `setrefs.c` and `subselect.c`, while `custom_private` should
be used to store other private data that is only used by the custom scan
provider itself. `custom_scan_tlist` can be NIL when scanning a base relation,
indicating that the custom scan returns scan tuples that match the base
relation's row type. Otherwise it is a target list describing the actual scan
tuples. `custom_scan_tlist` must be provided for joins, and could be provided
for scans if the custom scan provider can compute some non-Var expressions.
`custom_relids` is set by the core code to the set of relations (range table
indexes) that this scan node handles; except when this scan is replacing a
join, it will have only one member. `methods` must point to a (usually
statically allocated) object implementing the required custom scan methods,
which are further detailed below.

When a `CustomScan` scans a single relation, `scan.scanrelid` must be the
range table index of the table to be scanned. When it replaces a join,
`scan.scanrelid` should be zero.

Plan trees must be able to be duplicated using `copyObject`, so all the data
stored within the “custom” fields must consist of nodes that that function can
handle. Furthermore, custom scan providers cannot substitute a larger
structure that embeds a `CustomScan` for the structure itself, as would be
possible for a `CustomPath` or `CustomScanState`.

### 61.2.1. Custom Scan Plan Callbacks #

    
    
    Node *(*CreateCustomScanState) (CustomScan *cscan);
    

Allocate a `CustomScanState` for this `CustomScan`. The actual allocation will
often be larger than required for an ordinary `CustomScanState`, because many
providers will wish to embed that as the first field of a larger structure.
The value returned must have the node tag and `methods` set appropriately, but
other fields should be left as zeroes at this stage; after
`ExecInitCustomScan` performs basic initialization, the `BeginCustomScan`
callback will be invoked to give the custom scan provider a chance to do
whatever else is needed.

* * *

[Prev](custom-scan-path.html "61.1. Creating Custom Scan Paths")  | [Up](custom-scan.html "Chapter 61. Writing a Custom Scan Provider") |  [Next](custom-scan-execution.html "61.3. Executing Custom Scans")  
---|---|---  
61.1. Creating Custom Scan Paths  | [Home](index.html "PostgreSQL 16.9 Documentation") |  61.3. Executing Custom Scans  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/custom-scan-plan.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

