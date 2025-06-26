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

Supported Versions: [Current](/docs/current/bloom.html "PostgreSQL 17 -
F.7. bloom — bloom filter index access method") ([17](/docs/17/bloom.html
"PostgreSQL 17 - F.7. bloom — bloom filter index access method")) /
[16](/docs/16/bloom.html "PostgreSQL 16 - F.7. bloom — bloom filter index
access method") / [15](/docs/15/bloom.html "PostgreSQL 15 - F.7. bloom — bloom
filter index access method") / [14](/docs/14/bloom.html "PostgreSQL 14 -
F.7. bloom — bloom filter index access method") / [13](/docs/13/bloom.html
"PostgreSQL 13 - F.7. bloom — bloom filter index access method")

Development Versions: [18](/docs/18/bloom.html "PostgreSQL 18 - F.7. bloom —
bloom filter index access method") / [devel](/docs/devel/bloom.html
"PostgreSQL devel - F.7. bloom — bloom filter index access method")

Unsupported versions: [12](/docs/12/bloom.html "PostgreSQL 12 - F.7. bloom —
bloom filter index access method") / [11](/docs/11/bloom.html "PostgreSQL 11 -
F.7. bloom — bloom filter index access method") / [10](/docs/10/bloom.html
"PostgreSQL 10 - F.7. bloom — bloom filter index access method") /
[9.6](/docs/9.6/bloom.html "PostgreSQL 9.6 - F.7. bloom — bloom filter index
access method")

__

F.7. bloom — bloom filter index access method  
---  
[Prev](basic-archive.html "F.6. basic_archive — an example WAL archive module")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](btree-gin.html "F.8. btree_gin — GIN operator classes with B-tree behavior")  
  
* * *

## F.7. bloom — bloom filter index access method #

[F.7.1. Parameters](bloom.html#BLOOM-PARAMETERS)

[F.7.2. Examples](bloom.html#BLOOM-EXAMPLES)

[F.7.3. Operator Class Interface](bloom.html#BLOOM-OPERATOR-CLASS-INTERFACE)

[F.7.4. Limitations](bloom.html#BLOOM-LIMITATIONS)

[F.7.5. Authors](bloom.html#BLOOM-AUTHORS)

`bloom` provides an index access method based on [Bloom
filters](https://en.wikipedia.org/wiki/Bloom_filter).

A Bloom filter is a space-efficient data structure that is used to test
whether an element is a member of a set. In the case of an index access
method, it allows fast exclusion of non-matching tuples via signatures whose
size is determined at index creation.

A signature is a lossy representation of the indexed attribute(s), and as such
is prone to reporting false positives; that is, it may be reported that an
element is in the set, when it is not. So index search results must always be
rechecked using the actual attribute values from the heap entry. Larger
signatures reduce the odds of a false positive and thus reduce the number of
useless heap visits, but of course also make the index larger and hence slower
to scan.

This type of index is most useful when a table has many attributes and queries
test arbitrary combinations of them. A traditional btree index is faster than
a bloom index, but it can require many btree indexes to support all possible
queries where one needs only a single bloom index. Note however that bloom
indexes only support equality queries, whereas btree indexes can also perform
inequality and range searches.

### F.7.1. Parameters #

A `bloom` index accepts the following parameters in its `WITH` clause:

`length`

    

Length of each signature (index entry) in bits. It is rounded up to the
nearest multiple of `16`. The default is `80` bits and the maximum is `4096`.

`col1 — col32`

    

Number of bits generated for each index column. Each parameter's name refers
to the number of the index column that it controls. The default is `2` bits
and the maximum is `4095`. Parameters for index columns not actually used are
ignored.

### F.7.2. Examples #

This is an example of creating a bloom index:

    
    
    CREATE INDEX bloomidx ON tbloom USING bloom (i1,i2,i3)
           WITH (length=80, col1=2, col2=2, col3=4);
    

The index is created with a signature length of 80 bits, with attributes i1
and i2 mapped to 2 bits, and attribute i3 mapped to 4 bits. We could have
omitted the `length`, `col1`, and `col2` specifications since those have the
default values.

Here is a more complete example of bloom index definition and usage, as well
as a comparison with equivalent btree indexes. The bloom index is considerably
smaller than the btree index, and can perform better.

    
    
    =# CREATE TABLE tbloom AS
       SELECT
         (random() * 1000000)::int as i1,
         (random() * 1000000)::int as i2,
         (random() * 1000000)::int as i3,
         (random() * 1000000)::int as i4,
         (random() * 1000000)::int as i5,
         (random() * 1000000)::int as i6
       FROM
      generate_series(1,10000000);
    SELECT 10000000
    

A sequential scan over this large table takes a long time:

    
    
    =# EXPLAIN ANALYZE SELECT * FROM tbloom WHERE i2 = 898732 AND i5 = 123451;
                                                  QUERY PLAN
    -------------------------------------------------------------------​-----------------------------------
     Seq Scan on tbloom  (cost=0.00..213744.00 rows=250 width=24) (actual time=357.059..357.059 rows=0 loops=1)
       Filter: ((i2 = 898732) AND (i5 = 123451))
       Rows Removed by Filter: 10000000
     Planning Time: 0.346 ms
     Execution Time: 357.076 ms
    (5 rows)
    

Even with the btree index defined the result will still be a sequential scan:

    
    
    =# CREATE INDEX btreeidx ON tbloom (i1, i2, i3, i4, i5, i6);
    CREATE INDEX
    =# SELECT pg_size_pretty(pg_relation_size('btreeidx'));
     pg_size_pretty
    ----------------
     386 MB
    (1 row)
    =# EXPLAIN ANALYZE SELECT * FROM tbloom WHERE i2 = 898732 AND i5 = 123451;
                                                  QUERY PLAN
    -------------------------------------------------------------------​-----------------------------------
     Seq Scan on tbloom  (cost=0.00..213744.00 rows=2 width=24) (actual time=351.016..351.017 rows=0 loops=1)
       Filter: ((i2 = 898732) AND (i5 = 123451))
       Rows Removed by Filter: 10000000
     Planning Time: 0.138 ms
     Execution Time: 351.035 ms
    (5 rows)
    

Having the bloom index defined on the table is better than btree in handling
this type of search:

    
    
    =# CREATE INDEX bloomidx ON tbloom USING bloom (i1, i2, i3, i4, i5, i6);
    CREATE INDEX
    =# SELECT pg_size_pretty(pg_relation_size('bloomidx'));
     pg_size_pretty
    ----------------
     153 MB
    (1 row)
    =# EXPLAIN ANALYZE SELECT * FROM tbloom WHERE i2 = 898732 AND i5 = 123451;
                                                         QUERY PLAN
    -------------------------------------------------------------------​--------------------------------------------------
     Bitmap Heap Scan on tbloom  (cost=1792.00..1799.69 rows=2 width=24) (actual time=22.605..22.606 rows=0 loops=1)
       Recheck Cond: ((i2 = 898732) AND (i5 = 123451))
       Rows Removed by Index Recheck: 2300
       Heap Blocks: exact=2256
       ->  Bitmap Index Scan on bloomidx  (cost=0.00..178436.00 rows=1 width=0) (actual time=20.005..20.005 rows=2300 loops=1)
             Index Cond: ((i2 = 898732) AND (i5 = 123451))
     Planning Time: 0.099 ms
     Execution Time: 22.632 ms
    (8 rows)
    

Now, the main problem with the btree search is that btree is inefficient when
the search conditions do not constrain the leading index column(s). A better
strategy for btree is to create a separate index on each column. Then the
planner will choose something like this:

    
    
    =# CREATE INDEX btreeidx1 ON tbloom (i1);
    CREATE INDEX
    =# CREATE INDEX btreeidx2 ON tbloom (i2);
    CREATE INDEX
    =# CREATE INDEX btreeidx3 ON tbloom (i3);
    CREATE INDEX
    =# CREATE INDEX btreeidx4 ON tbloom (i4);
    CREATE INDEX
    =# CREATE INDEX btreeidx5 ON tbloom (i5);
    CREATE INDEX
    =# CREATE INDEX btreeidx6 ON tbloom (i6);
    CREATE INDEX
    =# EXPLAIN ANALYZE SELECT * FROM tbloom WHERE i2 = 898732 AND i5 = 123451;
                                                            QUERY PLAN
    -------------------------------------------------------------------​--------------------------------------------------------
     Bitmap Heap Scan on tbloom  (cost=9.29..13.30 rows=1 width=24) (actual time=0.032..0.033 rows=0 loops=1)
       Recheck Cond: ((i5 = 123451) AND (i2 = 898732))
       ->  BitmapAnd  (cost=9.29..9.29 rows=1 width=0) (actual time=0.047..0.047 rows=0 loops=1)
             ->  Bitmap Index Scan on btreeidx5  (cost=0.00..4.52 rows=11 width=0) (actual time=0.026..0.026 rows=7 loops=1)
                   Index Cond: (i5 = 123451)
             ->  Bitmap Index Scan on btreeidx2  (cost=0.00..4.52 rows=11 width=0) (actual time=0.007..0.007 rows=8 loops=1)
                   Index Cond: (i2 = 898732)
     Planning Time: 0.264 ms
     Execution Time: 0.047 ms
    (9 rows)
    

Although this query runs much faster than with either of the single indexes,
we pay a penalty in index size. Each of the single-column btree indexes
occupies 88.5 MB, so the total space needed is 531 MB, over three times the
space used by the bloom index.

### F.7.3. Operator Class Interface #

An operator class for bloom indexes requires only a hash function for the
indexed data type and an equality operator for searching. This example shows
the operator class definition for the `text` data type:

    
    
    CREATE OPERATOR CLASS text_ops
    DEFAULT FOR TYPE text USING bloom AS
        OPERATOR    1   =(text, text),
        FUNCTION    1   hashtext(text);
    

### F.7.4. Limitations #

  * Only operator classes for `int4` and `text` are included with the module.

  * Only the `=` operator is supported for search. But it is possible to add support for arrays with union and intersection operations in the future.

  * `bloom` access method doesn't support `UNIQUE` indexes.

  * `bloom` access method doesn't support searching for `NULL` values.

### F.7.5. Authors #

Teodor Sigaev `<[teodor@postgrespro.ru](mailto:teodor@postgrespro.ru)>`,
Postgres Professional, Moscow, Russia

Alexander Korotkov
`<[a.korotkov@postgrespro.ru](mailto:a.korotkov@postgrespro.ru)>`, Postgres
Professional, Moscow, Russia

Oleg Bartunov `<[obartunov@postgrespro.ru](mailto:obartunov@postgrespro.ru)>`,
Postgres Professional, Moscow, Russia

* * *

[Prev](basic-archive.html "F.6. basic_archive — an example WAL archive module")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](btree-gin.html "F.8. btree_gin — GIN operator classes with B-tree behavior")  
---|---|---  
F.6. basic_archive — an example WAL archive module  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.8. btree_gin — GIN operator classes with B-tree behavior  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/bloom.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

