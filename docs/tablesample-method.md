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

Supported Versions: [Current](/docs/current/tablesample-method.html
"PostgreSQL 17 - Chapter 60. Writing a Table Sampling Method")
([17](/docs/17/tablesample-method.html "PostgreSQL 17 - Chapter 60. Writing a
Table Sampling Method")) / [16](/docs/16/tablesample-method.html "PostgreSQL
16 - Chapter 60. Writing a Table Sampling Method") /
[15](/docs/15/tablesample-method.html "PostgreSQL 15 - Chapter 60. Writing a
Table Sampling Method") / [14](/docs/14/tablesample-method.html "PostgreSQL 14
- Chapter 60. Writing a Table Sampling Method") / [13](/docs/13/tablesample-
method.html "PostgreSQL 13 - Chapter 60. Writing a Table Sampling Method")

Development Versions: [18](/docs/18/tablesample-method.html "PostgreSQL 18 -
Chapter 60. Writing a Table Sampling Method") /
[devel](/docs/devel/tablesample-method.html "PostgreSQL devel -
Chapter 60. Writing a Table Sampling Method")

Unsupported versions: [12](/docs/12/tablesample-method.html "PostgreSQL 12 -
Chapter 60. Writing a Table Sampling Method") / [11](/docs/11/tablesample-
method.html "PostgreSQL 11 - Chapter 60. Writing a Table Sampling Method") /
[10](/docs/10/tablesample-method.html "PostgreSQL 10 - Chapter 60. Writing a
Table Sampling Method") / [9.6](/docs/9.6/tablesample-method.html "PostgreSQL
9.6 - Chapter 60. Writing a Table Sampling Method") /
[9.5](/docs/9.5/tablesample-method.html "PostgreSQL 9.5 - Chapter 60. Writing
a Table Sampling Method")

__

Chapter 60. Writing a Table Sampling Method  
---  
[Prev](fdw-row-locking.html "59.5. Row Locking in Foreign Data Wrappers")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tablesample-support-functions.html "60.1. Sampling Method Support Functions")  
  
* * *

## Chapter 60. Writing a Table Sampling Method

**Table of Contents**

[60.1. Sampling Method Support Functions](tablesample-support-functions.html)

PostgreSQL's implementation of the `TABLESAMPLE` clause supports custom table
sampling methods, in addition to the `BERNOULLI` and `SYSTEM` methods that are
required by the SQL standard. The sampling method determines which rows of the
table will be selected when the `TABLESAMPLE` clause is used.

At the SQL level, a table sampling method is represented by a single SQL
function, typically implemented in C, having the signature

    
    
    method_name(internal) RETURNS tsm_handler
    

The name of the function is the same method name appearing in the
`TABLESAMPLE` clause. The `internal` argument is a dummy (always having value
zero) that simply serves to prevent this function from being called directly
from an SQL command. The result of the function must be a palloc'd struct of
type `TsmRoutine`, which contains pointers to support functions for the
sampling method. These support functions are plain C functions and are not
visible or callable at the SQL level. The support functions are described in
[Section 60.1](tablesample-support-functions.html "60.1. Sampling Method
Support Functions").

In addition to function pointers, the `TsmRoutine` struct must provide these
additional fields:

`List *parameterTypes`

    

This is an OID list containing the data type OIDs of the parameter(s) that
will be accepted by the `TABLESAMPLE` clause when this sampling method is
used. For example, for the built-in methods, this list contains a single item
with value `FLOAT4OID`, which represents the sampling percentage. Custom
sampling methods can have more or different parameters.

`bool repeatable_across_queries`

    

If `true`, the sampling method can deliver identical samples across successive
queries, if the same parameters and `REPEATABLE` seed value are supplied each
time and the table contents have not changed. When this is `false`, the
`REPEATABLE` clause is not accepted for use with the sampling method.

`bool repeatable_across_scans`

    

If `true`, the sampling method can deliver identical samples across successive
scans in the same query (assuming unchanging parameters, seed value, and
snapshot). When this is `false`, the planner will not select plans that would
require scanning the sampled table more than once, since that might result in
inconsistent query output.

The `TsmRoutine` struct type is declared in `src/include/access/tsmapi.h`,
which see for additional details.

The table sampling methods included in the standard distribution are good
references when trying to write your own. Look into the
`src/backend/access/tablesample` subdirectory of the source tree for the
built-in sampling methods, and into the `contrib` subdirectory for add-on
methods.

* * *

[Prev](fdw-row-locking.html "59.5. Row Locking in Foreign Data Wrappers")  | [Up](internals.html "Part VII. Internals") |  [Next](tablesample-support-functions.html "60.1. Sampling Method Support Functions")  
---|---|---  
59.5. Row Locking in Foreign Data Wrappers  | [Home](index.html "PostgreSQL 16.9 Documentation") |  60.1. Sampling Method Support Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tablesample-method.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

