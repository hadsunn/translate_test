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

Supported Versions: [Current](/docs/current/indexes-intro.html "PostgreSQL 17
- 11.1. Introduction") ([17](/docs/17/indexes-intro.html "PostgreSQL 17 -
11.1. Introduction")) / [16](/docs/16/indexes-intro.html "PostgreSQL 16 -
11.1. Introduction") / [15](/docs/15/indexes-intro.html "PostgreSQL 15 -
11.1. Introduction") / [14](/docs/14/indexes-intro.html "PostgreSQL 14 -
11.1. Introduction") / [13](/docs/13/indexes-intro.html "PostgreSQL 13 -
11.1. Introduction")

Development Versions: [18](/docs/18/indexes-intro.html "PostgreSQL 18 -
11.1. Introduction") / [devel](/docs/devel/indexes-intro.html "PostgreSQL
devel - 11.1. Introduction")

Unsupported versions: [12](/docs/12/indexes-intro.html "PostgreSQL 12 -
11.1. Introduction") / [11](/docs/11/indexes-intro.html "PostgreSQL 11 -
11.1. Introduction") / [10](/docs/10/indexes-intro.html "PostgreSQL 10 -
11.1. Introduction") / [9.6](/docs/9.6/indexes-intro.html "PostgreSQL 9.6 -
11.1. Introduction") / [9.5](/docs/9.5/indexes-intro.html "PostgreSQL 9.5 -
11.1. Introduction") / [9.4](/docs/9.4/indexes-intro.html "PostgreSQL 9.4 -
11.1. Introduction") / [9.3](/docs/9.3/indexes-intro.html "PostgreSQL 9.3 -
11.1. Introduction") / [9.2](/docs/9.2/indexes-intro.html "PostgreSQL 9.2 -
11.1. Introduction") / [9.1](/docs/9.1/indexes-intro.html "PostgreSQL 9.1 -
11.1. Introduction") / [9.0](/docs/9.0/indexes-intro.html "PostgreSQL 9.0 -
11.1. Introduction") / [8.4](/docs/8.4/indexes-intro.html "PostgreSQL 8.4 -
11.1. Introduction") / [8.3](/docs/8.3/indexes-intro.html "PostgreSQL 8.3 -
11.1. Introduction") / [8.2](/docs/8.2/indexes-intro.html "PostgreSQL 8.2 -
11.1. Introduction")

__

11.1. Introduction  
---  
[Prev](indexes.html "Chapter 11. Indexes")  | [Up](indexes.html "Chapter 11. Indexes") | Chapter 11. Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](indexes-types.html "11.2. Index Types")  
  
* * *

## 11.1. Introduction #

Suppose we have a table similar to this:

    
    
    CREATE TABLE test1 (
        id integer,
        content varchar
    );
    

and the application issues many queries of the form:

    
    
    SELECT content FROM test1 WHERE id = _constant_ ;
    

With no advance preparation, the system would have to scan the entire `test1`
table, row by row, to find all matching entries. If there are many rows in
`test1` and only a few rows (perhaps zero or one) that would be returned by
such a query, this is clearly an inefficient method. But if the system has
been instructed to maintain an index on the `id` column, it can use a more
efficient method for locating matching rows. For instance, it might only have
to walk a few levels deep into a search tree.

A similar approach is used in most non-fiction books: terms and concepts that
are frequently looked up by readers are collected in an alphabetic index at
the end of the book. The interested reader can scan the index relatively
quickly and flip to the appropriate page(s), rather than having to read the
entire book to find the material of interest. Just as it is the task of the
author to anticipate the items that readers are likely to look up, it is the
task of the database programmer to foresee which indexes will be useful.

The following command can be used to create an index on the `id` column, as
discussed:

    
    
    CREATE INDEX test1_id_index ON test1 (id);
    

The name `test1_id_index` can be chosen freely, but you should pick something
that enables you to remember later what the index was for.

To remove an index, use the `DROP INDEX` command. Indexes can be added to and
removed from tables at any time.

Once an index is created, no further intervention is required: the system will
update the index when the table is modified, and it will use the index in
queries when it thinks doing so would be more efficient than a sequential
table scan. But you might have to run the `ANALYZE` command regularly to
update statistics to allow the query planner to make educated decisions. See
[Chapter 14](performance-tips.html "Chapter 14. Performance Tips") for
information about how to find out whether an index is used and when and why
the planner might choose _not_ to use an index.

Indexes can also benefit `UPDATE` and `DELETE` commands with search
conditions. Indexes can moreover be used in join searches. Thus, an index
defined on a column that is part of a join condition can also significantly
speed up queries with joins.

In general, PostgreSQL indexes can be used to optimize queries that contain
one or more `WHERE` or `JOIN` clauses of the form

    
    
    _indexed-column_ _indexable-operator_ _comparison-value_
    

Here, the _`indexed-column`_ is whatever column or expression the index has
been defined on. The _`indexable-operator`_ is an operator that is a member of
the index's _operator class_ for the indexed column. (More details about that
appear below.) And the _`comparison-value`_ can be any expression that is not
volatile and does not reference the index's table.

In some cases the query planner can extract an indexable clause of this form
from another SQL construct. A simple example is that if the original clause
was

    
    
    _comparison-value_ _operator_ _indexed-column_
    

then it can be flipped around into indexable form if the original _`operator`_
has a commutator operator that is a member of the index's operator class.

Creating an index on a large table can take a long time. By default,
PostgreSQL allows reads (`SELECT` statements) to occur on the table in
parallel with index creation, but writes (`INSERT`, `UPDATE`, `DELETE`) are
blocked until the index build is finished. In production environments this is
often unacceptable. It is possible to allow writes to occur in parallel with
index creation, but there are several caveats to be aware of — for more
information see [Building Indexes Concurrently](sql-createindex.html#SQL-
CREATEINDEX-CONCURRENTLY "Building Indexes Concurrently").

After an index is created, the system has to keep it synchronized with the
table. This adds overhead to data manipulation operations. Indexes can also
prevent the creation of [heap-only tuples](storage-hot.html "73.7. Heap-Only
Tuples \(HOT\)"). Therefore indexes that are seldom or never used in queries
should be removed.

* * *

[Prev](indexes.html "Chapter 11. Indexes")  | [Up](indexes.html "Chapter 11. Indexes") |  [Next](indexes-types.html "11.2. Index Types")  
---|---|---  
Chapter 11. Indexes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  11.2. Index Types  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/indexes-intro.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

