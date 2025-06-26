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

Supported Versions: [Current](/docs/current/btree-gin.html "PostgreSQL 17 -
F.8. btree_gin — GIN operator classes with B-tree behavior")
([17](/docs/17/btree-gin.html "PostgreSQL 17 - F.8. btree_gin — GIN operator
classes with B-tree behavior")) / [16](/docs/16/btree-gin.html "PostgreSQL 16
- F.8. btree_gin — GIN operator classes with B-tree behavior") /
[15](/docs/15/btree-gin.html "PostgreSQL 15 - F.8. btree_gin — GIN operator
classes with B-tree behavior") / [14](/docs/14/btree-gin.html "PostgreSQL 14 -
F.8. btree_gin — GIN operator classes with B-tree behavior") /
[13](/docs/13/btree-gin.html "PostgreSQL 13 - F.8. btree_gin — GIN operator
classes with B-tree behavior")

Development Versions: [18](/docs/18/btree-gin.html "PostgreSQL 18 -
F.8. btree_gin — GIN operator classes with B-tree behavior") /
[devel](/docs/devel/btree-gin.html "PostgreSQL devel - F.8. btree_gin — GIN
operator classes with B-tree behavior")

Unsupported versions: [12](/docs/12/btree-gin.html "PostgreSQL 12 -
F.8. btree_gin — GIN operator classes with B-tree behavior") /
[11](/docs/11/btree-gin.html "PostgreSQL 11 - F.8. btree_gin — GIN operator
classes with B-tree behavior") / [10](/docs/10/btree-gin.html "PostgreSQL 10 -
F.8. btree_gin — GIN operator classes with B-tree behavior") /
[9.6](/docs/9.6/btree-gin.html "PostgreSQL 9.6 - F.8. btree_gin — GIN operator
classes with B-tree behavior") / [9.5](/docs/9.5/btree-gin.html "PostgreSQL
9.5 - F.8. btree_gin — GIN operator classes with B-tree behavior") /
[9.4](/docs/9.4/btree-gin.html "PostgreSQL 9.4 - F.8. btree_gin — GIN operator
classes with B-tree behavior") / [9.3](/docs/9.3/btree-gin.html "PostgreSQL
9.3 - F.8. btree_gin — GIN operator classes with B-tree behavior") /
[9.2](/docs/9.2/btree-gin.html "PostgreSQL 9.2 - F.8. btree_gin — GIN operator
classes with B-tree behavior") / [9.1](/docs/9.1/btree-gin.html "PostgreSQL
9.1 - F.8. btree_gin — GIN operator classes with B-tree behavior") /
[9.0](/docs/9.0/btree-gin.html "PostgreSQL 9.0 - F.8. btree_gin — GIN operator
classes with B-tree behavior") / [8.4](/docs/8.4/btree-gin.html "PostgreSQL
8.4 - F.8. btree_gin — GIN operator classes with B-tree behavior")

__

F.8. btree_gin — GIN operator classes with B-tree behavior  
---  
[Prev](bloom.html "F.7. bloom — bloom filter index access method")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](btree-gist.html "F.9. btree_gist — GiST operator classes with B-tree behavior")  
  
* * *

## F.8. btree_gin — GIN operator classes with B-tree behavior #

[F.8.1. Example Usage](btree-gin.html#BTREE-GIN-EXAMPLE-USAGE)

[F.8.2. Authors](btree-gin.html#BTREE-GIN-AUTHORS)

`btree_gin` provides GIN operator classes that implement B-tree equivalent
behavior for the data types `int2`, `int4`, `int8`, `float4`, `float8`,
`timestamp with time zone`, `timestamp without time zone`, `time with time
zone`, `time without time zone`, `date`, `interval`, `oid`, `money`, `"char"`,
`varchar`, `text`, `bytea`, `bit`, `varbit`, `macaddr`, `macaddr8`, `inet`,
`cidr`, `uuid`, `name`, `bool`, `bpchar`, and all `enum` types.

In general, these operator classes will not outperform the equivalent standard
B-tree index methods, and they lack one major feature of the standard B-tree
code: the ability to enforce uniqueness. However, they are useful for GIN
testing and as a base for developing other GIN operator classes. Also, for
queries that test both a GIN-indexable column and a B-tree-indexable column,
it might be more efficient to create a multicolumn GIN index that uses one of
these operator classes than to create two separate indexes that would have to
be combined via bitmap ANDing.

This module is considered “trusted”, that is, it can be installed by non-
superusers who have `CREATE` privilege on the current database.

### F.8.1. Example Usage #

    
    
    CREATE TABLE test (a int4);
    -- create index
    CREATE INDEX testidx ON test USING GIN (a);
    -- query
    SELECT * FROM test WHERE a < 10;
    

### F.8.2. Authors #

Teodor Sigaev (`<[teodor@stack.net](mailto:teodor@stack.net)>`) and Oleg
Bartunov (`<[oleg@sai.msu.su](mailto:oleg@sai.msu.su)>`). See
<http://www.sai.msu.su/~megera/oddmuse/index.cgi/Gin> for additional
information.

* * *

[Prev](bloom.html "F.7. bloom — bloom filter index access method")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](btree-gist.html "F.9. btree_gist — GiST operator classes with B-tree behavior")  
---|---|---  
F.7. bloom — bloom filter index access method  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.9. btree_gist — GiST operator classes with B-tree behavior  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/btree-gin.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

