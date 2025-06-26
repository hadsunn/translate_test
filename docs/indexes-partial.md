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

Supported Versions: [Current](/docs/current/indexes-partial.html "PostgreSQL
17 - 11.8. Partial Indexes") ([17](/docs/17/indexes-partial.html "PostgreSQL
17 - 11.8. Partial Indexes")) / [16](/docs/16/indexes-partial.html "PostgreSQL
16 - 11.8. Partial Indexes") / [15](/docs/15/indexes-partial.html "PostgreSQL
15 - 11.8. Partial Indexes") / [14](/docs/14/indexes-partial.html "PostgreSQL
14 - 11.8. Partial Indexes") / [13](/docs/13/indexes-partial.html "PostgreSQL
13 - 11.8. Partial Indexes")

Development Versions: [18](/docs/18/indexes-partial.html "PostgreSQL 18 -
11.8. Partial Indexes") / [devel](/docs/devel/indexes-partial.html "PostgreSQL
devel - 11.8. Partial Indexes")

Unsupported versions: [12](/docs/12/indexes-partial.html "PostgreSQL 12 -
11.8. Partial Indexes") / [11](/docs/11/indexes-partial.html "PostgreSQL 11 -
11.8. Partial Indexes") / [10](/docs/10/indexes-partial.html "PostgreSQL 10 -
11.8. Partial Indexes") / [9.6](/docs/9.6/indexes-partial.html "PostgreSQL 9.6
- 11.8. Partial Indexes") / [9.5](/docs/9.5/indexes-partial.html "PostgreSQL
9.5 - 11.8. Partial Indexes") / [9.4](/docs/9.4/indexes-partial.html
"PostgreSQL 9.4 - 11.8. Partial Indexes") / [9.3](/docs/9.3/indexes-
partial.html "PostgreSQL 9.3 - 11.8. Partial Indexes") /
[9.2](/docs/9.2/indexes-partial.html "PostgreSQL 9.2 - 11.8. Partial Indexes")
/ [9.1](/docs/9.1/indexes-partial.html "PostgreSQL 9.1 - 11.8. Partial
Indexes") / [9.0](/docs/9.0/indexes-partial.html "PostgreSQL 9.0 -
11.8. Partial Indexes") / [8.4](/docs/8.4/indexes-partial.html "PostgreSQL 8.4
- 11.8. Partial Indexes") / [8.3](/docs/8.3/indexes-partial.html "PostgreSQL
8.3 - 11.8. Partial Indexes") / [8.2](/docs/8.2/indexes-partial.html
"PostgreSQL 8.2 - 11.8. Partial Indexes") / [8.1](/docs/8.1/indexes-
partial.html "PostgreSQL 8.1 - 11.8. Partial Indexes") /
[8.0](/docs/8.0/indexes-partial.html "PostgreSQL 8.0 - 11.8. Partial Indexes")
/ [7.4](/docs/7.4/indexes-partial.html "PostgreSQL 7.4 - 11.8. Partial
Indexes") / [7.3](/docs/7.3/indexes-partial.html "PostgreSQL 7.3 -
11.8. Partial Indexes") / [7.2](/docs/7.2/indexes-partial.html "PostgreSQL 7.2
- 11.8. Partial Indexes")

__

11.8. Partial Indexes  
---  
[Prev](indexes-expressional.html "11.7. Indexes on Expressions")  | [Up](indexes.html "Chapter 11. Indexes") | Chapter 11. Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](indexes-index-only-scans.html "11.9. Index-Only Scans and Covering Indexes")  
  
* * *

## 11.8. Partial Indexes #

A _partial index_ is an index built over a subset of a table; the subset is
defined by a conditional expression (called the _predicate_ of the partial
index). The index contains entries only for those table rows that satisfy the
predicate. Partial indexes are a specialized feature, but there are several
situations in which they are useful.

One major reason for using a partial index is to avoid indexing common values.
Since a query searching for a common value (one that accounts for more than a
few percent of all the table rows) will not use the index anyway, there is no
point in keeping those rows in the index at all. This reduces the size of the
index, which will speed up those queries that do use the index. It will also
speed up many table update operations because the index does not need to be
updated in all cases. [Example 11.1](indexes-partial.html#INDEXES-PARTIAL-EX1
"Example 11.1. Setting up a Partial Index to Exclude Common Values") shows a
possible application of this idea.

**Example  11.1. Setting up a Partial Index to Exclude Common Values**

Suppose you are storing web server access logs in a database. Most accesses
originate from the IP address range of your organization but some are from
elsewhere (say, employees on dial-up connections). If your searches by IP are
primarily for outside accesses, you probably do not need to index the IP range
that corresponds to your organization's subnet.

Assume a table like this:

    
    
    CREATE TABLE access_log (
        url varchar,
        client_ip inet,
        ...
    );
    

To create a partial index that suits our example, use a command such as this:

    
    
    CREATE INDEX access_log_client_ip_ix ON access_log (client_ip)
    WHERE NOT (client_ip > inet '192.168.100.0' AND
               client_ip < inet '192.168.100.255');
    

A typical query that can use this index would be:

    
    
    SELECT *
    FROM access_log
    WHERE url = '/index.html' AND client_ip = inet '212.78.10.32';
    

Here the query's IP address is covered by the partial index. The following
query cannot use the partial index, as it uses an IP address that is excluded
from the index:

    
    
    SELECT *
    FROM access_log
    WHERE url = '/index.html' AND client_ip = inet '192.168.100.23';
    

Observe that this kind of partial index requires that the common values be
predetermined, so such partial indexes are best used for data distributions
that do not change. Such indexes can be recreated occasionally to adjust for
new data distributions, but this adds maintenance effort.

  

Another possible use for a partial index is to exclude values from the index
that the typical query workload is not interested in; this is shown in
[Example 11.2](indexes-partial.html#INDEXES-PARTIAL-EX2 "Example 11.2. Setting
up a Partial Index to Exclude Uninteresting Values"). This results in the same
advantages as listed above, but it prevents the “uninteresting” values from
being accessed via that index, even if an index scan might be profitable in
that case. Obviously, setting up partial indexes for this kind of scenario
will require a lot of care and experimentation.

**Example  11.2. Setting up a Partial Index to Exclude Uninteresting Values**

If you have a table that contains both billed and unbilled orders, where the
unbilled orders take up a small fraction of the total table and yet those are
the most-accessed rows, you can improve performance by creating an index on
just the unbilled rows. The command to create the index would look like this:

    
    
    CREATE INDEX orders_unbilled_index ON orders (order_nr)
        WHERE billed is not true;
    

A possible query to use this index would be:

    
    
    SELECT * FROM orders WHERE billed is not true AND order_nr < 10000;
    

However, the index can also be used in queries that do not involve `order_nr`
at all, e.g.:

    
    
    SELECT * FROM orders WHERE billed is not true AND amount > 5000.00;
    

This is not as efficient as a partial index on the `amount` column would be,
since the system has to scan the entire index. Yet, if there are relatively
few unbilled orders, using this partial index just to find the unbilled orders
could be a win.

Note that this query cannot use this index:

    
    
    SELECT * FROM orders WHERE order_nr = 3501;
    

The order 3501 might be among the billed or unbilled orders.

  

[Example 11.2](indexes-partial.html#INDEXES-PARTIAL-EX2 "Example 11.2. Setting
up a Partial Index to Exclude Uninteresting Values") also illustrates that the
indexed column and the column used in the predicate do not need to match.
PostgreSQL supports partial indexes with arbitrary predicates, so long as only
columns of the table being indexed are involved. However, keep in mind that
the predicate must match the conditions used in the queries that are supposed
to benefit from the index. To be precise, a partial index can be used in a
query only if the system can recognize that the `WHERE` condition of the query
mathematically implies the predicate of the index. PostgreSQL does not have a
sophisticated theorem prover that can recognize mathematically equivalent
expressions that are written in different forms. (Not only is such a general
theorem prover extremely difficult to create, it would probably be too slow to
be of any real use.) The system can recognize simple inequality implications,
for example “x < 1” implies “x < 2”; otherwise the predicate condition must
exactly match part of the query's `WHERE` condition or the index will not be
recognized as usable. Matching takes place at query planning time, not at run
time. As a result, parameterized query clauses do not work with a partial
index. For example a prepared query with a parameter might specify “x < ?”
which will never imply “x < 2” for all possible values of the parameter.

A third possible use for partial indexes does not require the index to be used
in queries at all. The idea here is to create a unique index over a subset of
a table, as in [Example 11.3](indexes-partial.html#INDEXES-PARTIAL-EX3
"Example 11.3. Setting up a Partial Unique Index"). This enforces uniqueness
among the rows that satisfy the index predicate, without constraining those
that do not.

**Example  11.3. Setting up a Partial Unique Index**

Suppose that we have a table describing test outcomes. We wish to ensure that
there is only one “successful” entry for a given subject and target
combination, but there might be any number of “unsuccessful” entries. Here is
one way to do it:

    
    
    CREATE TABLE tests (
        subject text,
        target text,
        success boolean,
        ...
    );
    
    CREATE UNIQUE INDEX tests_success_constraint ON tests (subject, target)
        WHERE success;
    

This is a particularly efficient approach when there are few successful tests
and many unsuccessful ones. It is also possible to allow only one null in a
column by creating a unique partial index with an `IS NULL` restriction.

  

Finally, a partial index can also be used to override the system's query plan
choices. Also, data sets with peculiar distributions might cause the system to
use an index when it really should not. In that case the index can be set up
so that it is not available for the offending query. Normally, PostgreSQL
makes reasonable choices about index usage (e.g., it avoids them when
retrieving common values, so the earlier example really only saves index size,
it is not required to avoid index usage), and grossly incorrect plan choices
are cause for a bug report.

Keep in mind that setting up a partial index indicates that you know at least
as much as the query planner knows, in particular you know when an index might
be profitable. Forming this knowledge requires experience and understanding of
how indexes in PostgreSQL work. In most cases, the advantage of a partial
index over a regular index will be minimal. There are cases where they are
quite counterproductive, as in [Example 11.4](indexes-partial.html#INDEXES-
PARTIAL-EX4 "Example 11.4. Do Not Use Partial Indexes as a Substitute for
Partitioning").

**Example  11.4. Do Not Use Partial Indexes as a Substitute for Partitioning**

You might be tempted to create a large set of non-overlapping partial indexes,
for example

    
    
    CREATE INDEX mytable_cat_1 ON mytable (data) WHERE category = 1;
    CREATE INDEX mytable_cat_2 ON mytable (data) WHERE category = 2;
    CREATE INDEX mytable_cat_3 ON mytable (data) WHERE category = 3;
    ...
    CREATE INDEX mytable_cat__N_ ON mytable (data) WHERE category = _N_ ;
    

This is a bad idea! Almost certainly, you'll be better off with a single non-
partial index, declared like

    
    
    CREATE INDEX mytable_cat_data ON mytable (category, data);
    

(Put the category column first, for the reasons described in [Section
11.3](indexes-multicolumn.html "11.3. Multicolumn Indexes").) While a search
in this larger index might have to descend through a couple more tree levels
than a search in a smaller index, that's almost certainly going to be cheaper
than the planner effort needed to select the appropriate one of the partial
indexes. The core of the problem is that the system does not understand the
relationship among the partial indexes, and will laboriously test each one to
see if it's applicable to the current query.

If your table is large enough that a single index really is a bad idea, you
should look into using partitioning instead (see [Section 5.11](ddl-
partitioning.html "5.11. Table Partitioning")). With that mechanism, the
system does understand that the tables and indexes are non-overlapping, so far
better performance is possible.

  

More information about partial indexes can be found in
[[ston89b]](biblio.html#STON89B), [[olson93]](biblio.html#OLSON93 "Partial
indexing in POSTGRES: research project"), and
[[seshadri95]](biblio.html#SESHADRI95).

* * *

[Prev](indexes-expressional.html "11.7. Indexes on Expressions")  | [Up](indexes.html "Chapter 11. Indexes") |  [Next](indexes-index-only-scans.html "11.9. Index-Only Scans and Covering Indexes")  
---|---|---  
11.7. Indexes on Expressions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  11.9. Index-Only Scans and Covering Indexes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/indexes-partial.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

