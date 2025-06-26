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

Supported Versions: [Current](/docs/current/btree-gist.html "PostgreSQL 17 -
F.9. btree_gist — GiST operator classes with B-tree behavior")
([17](/docs/17/btree-gist.html "PostgreSQL 17 - F.9. btree_gist — GiST
operator classes with B-tree behavior")) / [16](/docs/16/btree-gist.html
"PostgreSQL 16 - F.9. btree_gist — GiST operator classes with B-tree
behavior") / [15](/docs/15/btree-gist.html "PostgreSQL 15 - F.9. btree_gist —
GiST operator classes with B-tree behavior") / [14](/docs/14/btree-gist.html
"PostgreSQL 14 - F.9. btree_gist — GiST operator classes with B-tree
behavior") / [13](/docs/13/btree-gist.html "PostgreSQL 13 - F.9. btree_gist —
GiST operator classes with B-tree behavior")

Development Versions: [18](/docs/18/btree-gist.html "PostgreSQL 18 -
F.9. btree_gist — GiST operator classes with B-tree behavior") /
[devel](/docs/devel/btree-gist.html "PostgreSQL devel - F.9. btree_gist — GiST
operator classes with B-tree behavior")

Unsupported versions: [12](/docs/12/btree-gist.html "PostgreSQL 12 -
F.9. btree_gist — GiST operator classes with B-tree behavior") /
[11](/docs/11/btree-gist.html "PostgreSQL 11 - F.9. btree_gist — GiST operator
classes with B-tree behavior") / [10](/docs/10/btree-gist.html "PostgreSQL 10
- F.9. btree_gist — GiST operator classes with B-tree behavior") /
[9.6](/docs/9.6/btree-gist.html "PostgreSQL 9.6 - F.9. btree_gist — GiST
operator classes with B-tree behavior") / [9.5](/docs/9.5/btree-gist.html
"PostgreSQL 9.5 - F.9. btree_gist — GiST operator classes with B-tree
behavior") / [9.4](/docs/9.4/btree-gist.html "PostgreSQL 9.4 - F.9. btree_gist
— GiST operator classes with B-tree behavior") / [9.3](/docs/9.3/btree-
gist.html "PostgreSQL 9.3 - F.9. btree_gist — GiST operator classes with
B-tree behavior") / [9.2](/docs/9.2/btree-gist.html "PostgreSQL 9.2 -
F.9. btree_gist — GiST operator classes with B-tree behavior") /
[9.1](/docs/9.1/btree-gist.html "PostgreSQL 9.1 - F.9. btree_gist — GiST
operator classes with B-tree behavior") / [9.0](/docs/9.0/btree-gist.html
"PostgreSQL 9.0 - F.9. btree_gist — GiST operator classes with B-tree
behavior") / [8.4](/docs/8.4/btree-gist.html "PostgreSQL 8.4 - F.9. btree_gist
— GiST operator classes with B-tree behavior") / [8.3](/docs/8.3/btree-
gist.html "PostgreSQL 8.3 - F.9. btree_gist — GiST operator classes with
B-tree behavior")

__

F.9. btree_gist — GiST operator classes with B-tree behavior  
---  
[Prev](btree-gin.html "F.8. btree_gin — GIN operator classes with B-tree behavior")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](citext.html "F.10. citext — a case-insensitive character string type")  
  
* * *

## F.9. btree_gist — GiST operator classes with B-tree behavior #

[F.9.1. Example Usage](btree-gist.html#BTREE-GIST-EXAMPLE-USAGE)

[F.9.2. Authors](btree-gist.html#BTREE-GIST-AUTHORS)

`btree_gist` provides GiST index operator classes that implement B-tree
equivalent behavior for the data types `int2`, `int4`, `int8`, `float4`,
`float8`, `numeric`, `timestamp with time zone`, `timestamp without time
zone`, `time with time zone`, `time without time zone`, `date`, `interval`,
`oid`, `money`, `char`, `varchar`, `text`, `bytea`, `bit`, `varbit`,
`macaddr`, `macaddr8`, `inet`, `cidr`, `uuid`, `bool` and all `enum` types.

In general, these operator classes will not outperform the equivalent standard
B-tree index methods, and they lack one major feature of the standard B-tree
code: the ability to enforce uniqueness. However, they provide some other
features that are not available with a B-tree index, as described below. Also,
these operator classes are useful when a multicolumn GiST index is needed,
wherein some of the columns are of data types that are only indexable with
GiST but other columns are just simple data types. Lastly, these operator
classes are useful for GiST testing and as a base for developing other GiST
operator classes.

In addition to the typical B-tree search operators, `btree_gist` also provides
index support for `<>` (“not equals”). This may be useful in combination with
an [exclusion constraint](sql-createtable.html#SQL-CREATETABLE-EXCLUDE), as
described below.

Also, for data types for which there is a natural distance metric,
`btree_gist` defines a distance operator `<->`, and provides GiST index
support for nearest-neighbor searches using this operator. Distance operators
are provided for `int2`, `int4`, `int8`, `float4`, `float8`, `timestamp with
time zone`, `timestamp without time zone`, `time without time zone`, `date`,
`interval`, `oid`, and `money`.

This module is considered “trusted”, that is, it can be installed by non-
superusers who have `CREATE` privilege on the current database.

### F.9.1. Example Usage #

Simple example using `btree_gist` instead of `btree`:

    
    
    CREATE TABLE test (a int4);
    -- create index
    CREATE INDEX testidx ON test USING GIST (a);
    -- query
    SELECT * FROM test WHERE a < 10;
    -- nearest-neighbor search: find the ten entries closest to "42"
    SELECT *, a <-> 42 AS dist FROM test ORDER BY a <-> 42 LIMIT 10;
    

Use an [exclusion constraint](sql-createtable.html#SQL-CREATETABLE-EXCLUDE) to
enforce the rule that a cage at a zoo can contain only one kind of animal:

    
    
    => CREATE TABLE zoo (
      cage   INTEGER,
      animal TEXT,
      EXCLUDE USING GIST (cage WITH =, animal WITH <>)
    );
    
    => INSERT INTO zoo VALUES(123, 'zebra');
    INSERT 0 1
    => INSERT INTO zoo VALUES(123, 'zebra');
    INSERT 0 1
    => INSERT INTO zoo VALUES(123, 'lion');
    ERROR:  conflicting key value violates exclusion constraint "zoo_cage_animal_excl"
    DETAIL:  Key (cage, animal)=(123, lion) conflicts with existing key (cage, animal)=(123, zebra).
    => INSERT INTO zoo VALUES(124, 'lion');
    INSERT 0 1
    

### F.9.2. Authors #

Teodor Sigaev (`<[teodor@stack.net](mailto:teodor@stack.net)>`), Oleg Bartunov
(`<[oleg@sai.msu.su](mailto:oleg@sai.msu.su)>`), Janko Richter
(`<[jankorichter@yahoo.de](mailto:jankorichter@yahoo.de)>`), and Paul
Jungwirth
(`<[pj@illuminatedcomputing.com](mailto:pj@illuminatedcomputing.com)>`). See
<http://www.sai.msu.su/~megera/postgres/gist/> for additional information.

* * *

[Prev](btree-gin.html "F.8. btree_gin — GIN operator classes with B-tree behavior")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](citext.html "F.10. citext — a case-insensitive character string type")  
---|---|---  
F.8. btree_gin — GIN operator classes with B-tree behavior  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.10. citext — a case-insensitive character string type  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/btree-gist.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

