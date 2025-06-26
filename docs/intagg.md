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

Supported Versions: [Current](/docs/current/intagg.html "PostgreSQL 17 -
F.19. intagg — integer aggregator and enumerator") ([17](/docs/17/intagg.html
"PostgreSQL 17 - F.19. intagg — integer aggregator and enumerator")) /
[16](/docs/16/intagg.html "PostgreSQL 16 - F.19. intagg — integer aggregator
and enumerator") / [15](/docs/15/intagg.html "PostgreSQL 15 - F.19. intagg —
integer aggregator and enumerator") / [14](/docs/14/intagg.html "PostgreSQL 14
- F.19. intagg — integer aggregator and enumerator") /
[13](/docs/13/intagg.html "PostgreSQL 13 - F.19. intagg — integer aggregator
and enumerator")

Development Versions: [18](/docs/18/intagg.html "PostgreSQL 18 - F.19. intagg
— integer aggregator and enumerator") / [devel](/docs/devel/intagg.html
"PostgreSQL devel - F.19. intagg — integer aggregator and enumerator")

Unsupported versions: [12](/docs/12/intagg.html "PostgreSQL 12 - F.19. intagg
— integer aggregator and enumerator") / [11](/docs/11/intagg.html "PostgreSQL
11 - F.19. intagg — integer aggregator and enumerator") /
[10](/docs/10/intagg.html "PostgreSQL 10 - F.19. intagg — integer aggregator
and enumerator") / [9.6](/docs/9.6/intagg.html "PostgreSQL 9.6 - F.19. intagg
— integer aggregator and enumerator") / [9.5](/docs/9.5/intagg.html
"PostgreSQL 9.5 - F.19. intagg — integer aggregator and enumerator") /
[9.4](/docs/9.4/intagg.html "PostgreSQL 9.4 - F.19. intagg — integer
aggregator and enumerator") / [9.3](/docs/9.3/intagg.html "PostgreSQL 9.3 -
F.19. intagg — integer aggregator and enumerator") /
[9.2](/docs/9.2/intagg.html "PostgreSQL 9.2 - F.19. intagg — integer
aggregator and enumerator") / [9.1](/docs/9.1/intagg.html "PostgreSQL 9.1 -
F.19. intagg — integer aggregator and enumerator") /
[9.0](/docs/9.0/intagg.html "PostgreSQL 9.0 - F.19. intagg — integer
aggregator and enumerator") / [8.4](/docs/8.4/intagg.html "PostgreSQL 8.4 -
F.19. intagg — integer aggregator and enumerator") /
[8.3](/docs/8.3/intagg.html "PostgreSQL 8.3 - F.19. intagg — integer
aggregator and enumerator")

__

F.19. intagg — integer aggregator and enumerator  
---  
[Prev](hstore.html "F.18. hstore — hstore key/value datatype")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](intarray.html "F.20. intarray — manipulate arrays of integers")  
  
* * *

## F.19. intagg — integer aggregator and enumerator #

[F.19.1. Functions](intagg.html#INTAGG-FUNCTIONS)

[F.19.2. Sample Uses](intagg.html#INTAGG-SAMPLES)

The `intagg` module provides an integer aggregator and an enumerator. `intagg`
is now obsolete, because there are built-in functions that provide a superset
of its capabilities. However, the module is still provided as a compatibility
wrapper around the built-in functions.

### F.19.1. Functions #

The aggregator is an aggregate function `int_array_aggregate(integer)` that
produces an integer array containing exactly the integers it is fed. This is a
wrapper around `array_agg`, which does the same thing for any array type.

The enumerator is a function `int_array_enum(integer[])` that returns `setof
integer`. It is essentially the reverse operation of the aggregator: given an
array of integers, expand it into a set of rows. This is a wrapper around
`unnest`, which does the same thing for any array type.

### F.19.2. Sample Uses #

Many database systems have the notion of a one to many table. Such a table
usually sits between two indexed tables, for example:

    
    
    CREATE TABLE left (id INT PRIMARY KEY, ...);
    CREATE TABLE right (id INT PRIMARY KEY, ...);
    CREATE TABLE one_to_many(left INT REFERENCES left, right INT REFERENCES right);
    

It is typically used like this:

    
    
    SELECT right.* from right JOIN one_to_many ON (right.id = one_to_many.right)
      WHERE one_to_many.left = _item_ ;
    

This will return all the items in the right hand table for an entry in the
left hand table. This is a very common construct in SQL.

Now, this methodology can be cumbersome with a very large number of entries in
the `one_to_many` table. Often, a join like this would result in an index scan
and a fetch for each right hand entry in the table for a particular left hand
entry. If you have a very dynamic system, there is not much you can do.
However, if you have some data which is fairly static, you can create a
summary table with the aggregator.

    
    
    CREATE TABLE summary AS
      SELECT left, int_array_aggregate(right) AS right
      FROM one_to_many
      GROUP BY left;
    

This will create a table with one row per left item, and an array of right
items. Now this is pretty useless without some way of using the array; that's
why there is an array enumerator. You can do

    
    
    SELECT left, int_array_enum(right) FROM summary WHERE left = _item_ ;
    

The above query using `int_array_enum` produces the same results as

    
    
    SELECT left, right FROM one_to_many WHERE left = _item_ ;
    

The difference is that the query against the summary table has to get only one
row from the table, whereas the direct query against `one_to_many` must index
scan and fetch a row for each entry.

On one system, an `EXPLAIN` showed a query with a cost of 8488 was reduced to
a cost of 329. The original query was a join involving the `one_to_many`
table, which was replaced by:

    
    
    SELECT right, count(right) FROM
      ( SELECT left, int_array_enum(right) AS right
        FROM summary JOIN (SELECT left FROM left_table WHERE left = _item_) AS lefts
             ON (summary.left = lefts.left)
      ) AS list
      GROUP BY right
      ORDER BY count DESC;
    

* * *

[Prev](hstore.html "F.18. hstore — hstore key/value datatype")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](intarray.html "F.20. intarray — manipulate arrays of integers")  
---|---|---  
F.18. hstore — hstore key/value datatype  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.20. intarray — manipulate arrays of integers  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/intagg.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

