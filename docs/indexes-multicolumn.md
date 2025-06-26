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

Supported Versions: [Current](/docs/current/indexes-multicolumn.html
"PostgreSQL 17 - 11.3. Multicolumn Indexes") ([17](/docs/17/indexes-
multicolumn.html "PostgreSQL 17 - 11.3. Multicolumn Indexes")) /
[16](/docs/16/indexes-multicolumn.html "PostgreSQL 16 - 11.3. Multicolumn
Indexes") / [15](/docs/15/indexes-multicolumn.html "PostgreSQL 15 -
11.3. Multicolumn Indexes") / [14](/docs/14/indexes-multicolumn.html
"PostgreSQL 14 - 11.3. Multicolumn Indexes") / [13](/docs/13/indexes-
multicolumn.html "PostgreSQL 13 - 11.3. Multicolumn Indexes")

Development Versions: [18](/docs/18/indexes-multicolumn.html "PostgreSQL 18 -
11.3. Multicolumn Indexes") / [devel](/docs/devel/indexes-multicolumn.html
"PostgreSQL devel - 11.3. Multicolumn Indexes")

Unsupported versions: [12](/docs/12/indexes-multicolumn.html "PostgreSQL 12 -
11.3. Multicolumn Indexes") / [11](/docs/11/indexes-multicolumn.html
"PostgreSQL 11 - 11.3. Multicolumn Indexes") / [10](/docs/10/indexes-
multicolumn.html "PostgreSQL 10 - 11.3. Multicolumn Indexes") /
[9.6](/docs/9.6/indexes-multicolumn.html "PostgreSQL 9.6 - 11.3. Multicolumn
Indexes") / [9.5](/docs/9.5/indexes-multicolumn.html "PostgreSQL 9.5 -
11.3. Multicolumn Indexes") / [9.4](/docs/9.4/indexes-multicolumn.html
"PostgreSQL 9.4 - 11.3. Multicolumn Indexes") / [9.3](/docs/9.3/indexes-
multicolumn.html "PostgreSQL 9.3 - 11.3. Multicolumn Indexes") /
[9.2](/docs/9.2/indexes-multicolumn.html "PostgreSQL 9.2 - 11.3. Multicolumn
Indexes") / [9.1](/docs/9.1/indexes-multicolumn.html "PostgreSQL 9.1 -
11.3. Multicolumn Indexes") / [9.0](/docs/9.0/indexes-multicolumn.html
"PostgreSQL 9.0 - 11.3. Multicolumn Indexes") / [8.4](/docs/8.4/indexes-
multicolumn.html "PostgreSQL 8.4 - 11.3. Multicolumn Indexes") /
[8.3](/docs/8.3/indexes-multicolumn.html "PostgreSQL 8.3 - 11.3. Multicolumn
Indexes") / [8.2](/docs/8.2/indexes-multicolumn.html "PostgreSQL 8.2 -
11.3. Multicolumn Indexes") / [8.1](/docs/8.1/indexes-multicolumn.html
"PostgreSQL 8.1 - 11.3. Multicolumn Indexes") / [8.0](/docs/8.0/indexes-
multicolumn.html "PostgreSQL 8.0 - 11.3. Multicolumn Indexes") /
[7.4](/docs/7.4/indexes-multicolumn.html "PostgreSQL 7.4 - 11.3. Multicolumn
Indexes") / [7.3](/docs/7.3/indexes-multicolumn.html "PostgreSQL 7.3 -
11.3. Multicolumn Indexes") / [7.2](/docs/7.2/indexes-multicolumn.html
"PostgreSQL 7.2 - 11.3. Multicolumn Indexes")

__

11.3. Multicolumn Indexes  
---  
[Prev](indexes-types.html "11.2. Index Types")  | [Up](indexes.html "Chapter 11. Indexes") | Chapter 11. Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](indexes-ordering.html "11.4. Indexes and ORDER BY")  
  
* * *

## 11.3. Multicolumn Indexes #

An index can be defined on more than one column of a table. For example, if
you have a table of this form:

    
    
    CREATE TABLE test2 (
      major int,
      minor int,
      name varchar
    );
    

(say, you keep your `/dev` directory in a database...) and you frequently
issue queries like:

    
    
    SELECT name FROM test2 WHERE major = _constant_ AND minor = _constant_ ;
    

then it might be appropriate to define an index on the columns `major` and
`minor` together, e.g.:

    
    
    CREATE INDEX test2_mm_idx ON test2 (major, minor);
    

Currently, only the B-tree, GiST, GIN, and BRIN index types support multiple-
key-column indexes. Whether there can be multiple key columns is independent
of whether `INCLUDE` columns can be added to the index. Indexes can have up to
32 columns, including `INCLUDE` columns. (This limit can be altered when
building PostgreSQL; see the file `pg_config_manual.h`.)

A multicolumn B-tree index can be used with query conditions that involve any
subset of the index's columns, but the index is most efficient when there are
constraints on the leading (leftmost) columns. The exact rule is that equality
constraints on leading columns, plus any inequality constraints on the first
column that does not have an equality constraint, will be used to limit the
portion of the index that is scanned. Constraints on columns to the right of
these columns are checked in the index, so they save visits to the table
proper, but they do not reduce the portion of the index that has to be
scanned. For example, given an index on `(a, b, c)` and a query condition
`WHERE a = 5 AND b >= 42 AND c < 77`, the index would have to be scanned from
the first entry with `a` = 5 and `b` = 42 up through the last entry with `a` =
5. Index entries with `c` >= 77 would be skipped, but they'd still have to be
scanned through. This index could in principle be used for queries that have
constraints on `b` and/or `c` with no constraint on `a` — but the entire index
would have to be scanned, so in most cases the planner would prefer a
sequential table scan over using the index.

A multicolumn GiST index can be used with query conditions that involve any
subset of the index's columns. Conditions on additional columns restrict the
entries returned by the index, but the condition on the first column is the
most important one for determining how much of the index needs to be scanned.
A GiST index will be relatively ineffective if its first column has only a few
distinct values, even if there are many distinct values in additional columns.

A multicolumn GIN index can be used with query conditions that involve any
subset of the index's columns. Unlike B-tree or GiST, index search
effectiveness is the same regardless of which index column(s) the query
conditions use.

A multicolumn BRIN index can be used with query conditions that involve any
subset of the index's columns. Like GIN and unlike B-tree or GiST, index
search effectiveness is the same regardless of which index column(s) the query
conditions use. The only reason to have multiple BRIN indexes instead of one
multicolumn BRIN index on a single table is to have a different
`pages_per_range` storage parameter.

Of course, each column must be used with operators appropriate to the index
type; clauses that involve other operators will not be considered.

Multicolumn indexes should be used sparingly. In most situations, an index on
a single column is sufficient and saves space and time. Indexes with more than
three columns are unlikely to be helpful unless the usage of the table is
extremely stylized. See also [Section 11.5](indexes-bitmap-scans.html
"11.5. Combining Multiple Indexes") and [Section 11.9](indexes-index-only-
scans.html "11.9. Index-Only Scans and Covering Indexes") for some discussion
of the merits of different index configurations.

* * *

[Prev](indexes-types.html "11.2. Index Types")  | [Up](indexes.html "Chapter 11. Indexes") |  [Next](indexes-ordering.html "11.4. Indexes and ORDER BY")  
---|---|---  
11.2. Index Types  | [Home](index.html "PostgreSQL 16.9 Documentation") |  11.4. Indexes and `ORDER BY`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/indexes-multicolumn.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

