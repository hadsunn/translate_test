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

Supported Versions: [16](/docs/16/gin-tips.html "PostgreSQL 16 - 70.5. GIN
Tips and Tricks") / [15](/docs/15/gin-tips.html "PostgreSQL 15 - 70.5. GIN
Tips and Tricks") / [14](/docs/14/gin-tips.html "PostgreSQL 14 - 70.5. GIN
Tips and Tricks") / [13](/docs/13/gin-tips.html "PostgreSQL 13 - 70.5. GIN
Tips and Tricks")

Unsupported versions: [12](/docs/12/gin-tips.html "PostgreSQL 12 - 70.5. GIN
Tips and Tricks") / [11](/docs/11/gin-tips.html "PostgreSQL 11 - 70.5. GIN
Tips and Tricks") / [10](/docs/10/gin-tips.html "PostgreSQL 10 - 70.5. GIN
Tips and Tricks") / [9.6](/docs/9.6/gin-tips.html "PostgreSQL 9.6 - 70.5. GIN
Tips and Tricks") / [9.5](/docs/9.5/gin-tips.html "PostgreSQL 9.5 - 70.5. GIN
Tips and Tricks") / [9.4](/docs/9.4/gin-tips.html "PostgreSQL 9.4 - 70.5. GIN
Tips and Tricks") / [9.3](/docs/9.3/gin-tips.html "PostgreSQL 9.3 - 70.5. GIN
Tips and Tricks") / [9.2](/docs/9.2/gin-tips.html "PostgreSQL 9.2 - 70.5. GIN
Tips and Tricks") / [9.1](/docs/9.1/gin-tips.html "PostgreSQL 9.1 - 70.5. GIN
Tips and Tricks") / [9.0](/docs/9.0/gin-tips.html "PostgreSQL 9.0 - 70.5. GIN
Tips and Tricks") / [8.4](/docs/8.4/gin-tips.html "PostgreSQL 8.4 - 70.5. GIN
Tips and Tricks") / [8.3](/docs/8.3/gin-tips.html "PostgreSQL 8.3 - 70.5. GIN
Tips and Tricks") / [8.2](/docs/8.2/gin-tips.html "PostgreSQL 8.2 - 70.5. GIN
Tips and Tricks")

__

70.5. GIN Tips and Tricks  
---  
[Prev](gin-implementation.html "70.4. Implementation")  | [Up](gin.html "Chapter 70. GIN Indexes") | Chapter 70. GIN Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](gin-limit.html "70.6. Limitations")  
  
* * *

## 70.5. GIN Tips and Tricks #

Create vs. insert

    

Insertion into a GIN index can be slow due to the likelihood of many keys
being inserted for each item. So, for bulk insertions into a table it is
advisable to drop the GIN index and recreate it after finishing bulk
insertion.

When `fastupdate` is enabled for GIN (see [Section 70.4.1](gin-
implementation.html#GIN-FAST-UPDATE "70.4.1. GIN Fast Update Technique") for
details), the penalty is less than when it is not. But for very large updates
it may still be best to drop and recreate the index.

[maintenance_work_mem](runtime-config-resource.html#GUC-MAINTENANCE-WORK-MEM)

    

Build time for a GIN index is very sensitive to the `maintenance_work_mem`
setting; it doesn't pay to skimp on work memory during index creation.

[gin_pending_list_limit](runtime-config-client.html#GUC-GIN-PENDING-LIST-
LIMIT)

    

During a series of insertions into an existing GIN index that has `fastupdate`
enabled, the system will clean up the pending-entry list whenever the list
grows larger than `gin_pending_list_limit`. To avoid fluctuations in observed
response time, it's desirable to have pending-list cleanup occur in the
background (i.e., via autovacuum). Foreground cleanup operations can be
avoided by increasing `gin_pending_list_limit` or making autovacuum more
aggressive. However, enlarging the threshold of the cleanup operation means
that if a foreground cleanup does occur, it will take even longer.

`gin_pending_list_limit` can be overridden for individual GIN indexes by
changing storage parameters, which allows each GIN index to have its own
cleanup threshold. For example, it's possible to increase the threshold only
for the GIN index which can be updated heavily, and decrease it otherwise.

[gin_fuzzy_search_limit](runtime-config-client.html#GUC-GIN-FUZZY-SEARCH-
LIMIT)

    

The primary goal of developing GIN indexes was to create support for highly
scalable full-text search in PostgreSQL, and there are often situations when a
full-text search returns a very large set of results. Moreover, this often
happens when the query contains very frequent words, so that the large result
set is not even useful. Since reading many tuples from the disk and sorting
them could take a lot of time, this is unacceptable for production. (Note that
the index search itself is very fast.)

To facilitate controlled execution of such queries, GIN has a configurable
soft upper limit on the number of rows returned: the `gin_fuzzy_search_limit`
configuration parameter. It is set to 0 (meaning no limit) by default. If a
non-zero limit is set, then the returned set is a subset of the whole result
set, chosen at random.

“Soft” means that the actual number of returned results could differ somewhat
from the specified limit, depending on the query and the quality of the
system's random number generator.

From experience, values in the thousands (e.g., 5000 — 20000) work well.

* * *

[Prev](gin-implementation.html "70.4. Implementation")  | [Up](gin.html "Chapter 70. GIN Indexes") |  [Next](gin-limit.html "70.6. Limitations")  
---|---|---  
70.4. Implementation  | [Home](index.html "PostgreSQL 16.9 Documentation") |  70.6. Limitations  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/gin-tips.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

