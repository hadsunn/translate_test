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

Supported Versions: [Current](/docs/current/intarray.html "PostgreSQL 17 -
F.20. intarray — manipulate arrays of integers") ([17](/docs/17/intarray.html
"PostgreSQL 17 - F.20. intarray — manipulate arrays of integers")) /
[16](/docs/16/intarray.html "PostgreSQL 16 - F.20. intarray — manipulate
arrays of integers") / [15](/docs/15/intarray.html "PostgreSQL 15 -
F.20. intarray — manipulate arrays of integers") / [14](/docs/14/intarray.html
"PostgreSQL 14 - F.20. intarray — manipulate arrays of integers") /
[13](/docs/13/intarray.html "PostgreSQL 13 - F.20. intarray — manipulate
arrays of integers")

Development Versions: [18](/docs/18/intarray.html "PostgreSQL 18 -
F.20. intarray — manipulate arrays of integers") /
[devel](/docs/devel/intarray.html "PostgreSQL devel - F.20. intarray —
manipulate arrays of integers")

Unsupported versions: [12](/docs/12/intarray.html "PostgreSQL 12 -
F.20. intarray — manipulate arrays of integers") / [11](/docs/11/intarray.html
"PostgreSQL 11 - F.20. intarray — manipulate arrays of integers") /
[10](/docs/10/intarray.html "PostgreSQL 10 - F.20. intarray — manipulate
arrays of integers") / [9.6](/docs/9.6/intarray.html "PostgreSQL 9.6 -
F.20. intarray — manipulate arrays of integers") /
[9.5](/docs/9.5/intarray.html "PostgreSQL 9.5 - F.20. intarray — manipulate
arrays of integers") / [9.4](/docs/9.4/intarray.html "PostgreSQL 9.4 -
F.20. intarray — manipulate arrays of integers") /
[9.3](/docs/9.3/intarray.html "PostgreSQL 9.3 - F.20. intarray — manipulate
arrays of integers") / [9.2](/docs/9.2/intarray.html "PostgreSQL 9.2 -
F.20. intarray — manipulate arrays of integers") /
[9.1](/docs/9.1/intarray.html "PostgreSQL 9.1 - F.20. intarray — manipulate
arrays of integers") / [9.0](/docs/9.0/intarray.html "PostgreSQL 9.0 -
F.20. intarray — manipulate arrays of integers") /
[8.4](/docs/8.4/intarray.html "PostgreSQL 8.4 - F.20. intarray — manipulate
arrays of integers") / [8.3](/docs/8.3/intarray.html "PostgreSQL 8.3 -
F.20. intarray — manipulate arrays of integers")

__

F.20. intarray — manipulate arrays of integers  
---  
[Prev](intagg.html "F.19. intagg — integer aggregator and enumerator")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](isn.html "F.21. isn — data types for international standard numbers \(ISBN, EAN, UPC, etc.\)")  
  
* * *

## F.20. intarray — manipulate arrays of integers #

[F.20.1. `intarray` Functions and Operators](intarray.html#INTARRAY-FUNCS-OPS)

[F.20.2. Index Support](intarray.html#INTARRAY-INDEX)

[F.20.3. Example](intarray.html#INTARRAY-EXAMPLE)

[F.20.4. Benchmark](intarray.html#INTARRAY-BENCHMARK)

[F.20.5. Authors](intarray.html#INTARRAY-AUTHORS)

The `intarray` module provides a number of useful functions and operators for
manipulating null-free arrays of integers. There is also support for indexed
searches using some of the operators.

All of these operations will throw an error if a supplied array contains any
NULL elements.

Many of these operations are only sensible for one-dimensional arrays.
Although they will accept input arrays of more dimensions, the data is treated
as though it were a linear array in storage order.

This module is considered “trusted”, that is, it can be installed by non-
superusers who have `CREATE` privilege on the current database.

### F.20.1. `intarray` Functions and Operators #

The functions provided by the `intarray` module are shown in [Table
F.9](intarray.html#INTARRAY-FUNC-TABLE "Table F.9. intarray Functions"), the
operators in [Table F.10](intarray.html#INTARRAY-OP-TABLE
"Table F.10. intarray Operators").

**Table  F.9. `intarray` Functions**

Function Description Example(s)  
---  
`icount` ( `integer[]` ) → `integer` Returns the number of elements in the
array. `icount('{1,2,3}'::integer[])` → `3`  
`sort` ( `integer[]`, _`dir`_ `text` ) → `integer[]` Sorts the array in either
ascending or descending order. _`dir`_ must be `asc` or `desc`.
`sort('{1,3,2}'::integer[], 'desc')` → `{3,2,1}`  
`sort` ( `integer[]` ) → `integer[]` `sort_asc` ( `integer[]` ) → `integer[]`
Sorts in ascending order. `sort(array[11,77,44])` → `{11,44,77}`  
`sort_desc` ( `integer[]` ) → `integer[]` Sorts in descending order.
`sort_desc(array[11,77,44])` → `{77,44,11}`  
`uniq` ( `integer[]` ) → `integer[]` Removes adjacent duplicates. Often used
with `sort` to remove all duplicates. `uniq('{1,2,2,3,1,1}'::integer[])` →
`{1,2,3,1}` `uniq(sort('{1,2,3,2,1}'::integer[]))` → `{1,2,3}`  
`idx` ( `integer[]`, _`item`_ `integer` ) → `integer` Returns index of the
first array element matching _`item`_ , or 0 if no match.
`idx(array[11,22,33,22,11], 22)` → `2`  
`subarray` ( `integer[]`, _`start`_ `integer`, _`len`_ `integer` ) →
`integer[]` Extracts the portion of the array starting at position _`start`_ ,
with _`len`_ elements. `subarray('{1,2,3,2,1}'::integer[], 2, 3)` → `{2,3,2}`  
`subarray` ( `integer[]`, _`start`_ `integer` ) → `integer[]` Extracts the
portion of the array starting at position _`start`_.
`subarray('{1,2,3,2,1}'::integer[], 2)` → `{2,3,2,1}`  
`intset` ( `integer` ) → `integer[]` Makes a single-element array.
`intset(42)` → `{42}`  
  
  

**Table  F.10. `intarray` Operators**

Operator Description  
---  
`integer[]` `&&` `integer[]` → `boolean` Do arrays overlap (have at least one
element in common)?  
`integer[]` `@>` `integer[]` → `boolean` Does left array contain right array?  
`integer[]` `<@` `integer[]` → `boolean` Is left array contained in right
array?  
`#` `integer[]` → `integer` Returns the number of elements in the array.  
`integer[]` `#` `integer` → `integer` Returns index of the first array element
matching the right argument, or 0 if no match. (Same as `idx` function.)  
`integer[]` `+` `integer` → `integer[]` Adds element to end of array.  
`integer[]` `+` `integer[]` → `integer[]` Concatenates the arrays.  
`integer[]` `-` `integer` → `integer[]` Removes entries matching the right
argument from the array.  
`integer[]` `-` `integer[]` → `integer[]` Removes elements of the right array
from the left array.  
`integer[]` `|` `integer` → `integer[]` Computes the union of the arguments.  
`integer[]` `|` `integer[]` → `integer[]` Computes the union of the arguments.  
`integer[]` `&` `integer[]` → `integer[]` Computes the intersection of the
arguments.  
`integer[]` `@@` `query_int` → `boolean` Does array satisfy query? (see below)  
`query_int` `~~` `integer[]` → `boolean` Does array satisfy query? (commutator
of `@@`)  
  
  

The operators `&&`, `@>` and `<@` are equivalent to PostgreSQL's built-in
operators of the same names, except that they work only on integer arrays that
do not contain nulls, while the built-in operators work for any array type.
This restriction makes them faster than the built-in operators in many cases.

The `@@` and `~~` operators test whether an array satisfies a _query_ , which
is expressed as a value of a specialized data type `query_int`. A _query_
consists of integer values that are checked against the elements of the array,
possibly combined using the operators `&` (AND), `|` (OR), and `!` (NOT).
Parentheses can be used as needed. For example, the query `1&(2|3)` matches
arrays that contain 1 and also contain either 2 or 3.

### F.20.2. Index Support #

`intarray` provides index support for the `&&`, `@>`, and `@@` operators, as
well as regular array equality.

Two parameterized GiST index operator classes are provided: `gist__int_ops`
(used by default) is suitable for small- to medium-size data sets, while
`gist__intbig_ops` uses a larger signature and is more suitable for indexing
large data sets (i.e., columns containing a large number of distinct array
values). The implementation uses an RD-tree data structure with built-in lossy
compression.

`gist__int_ops` approximates an integer set as an array of integer ranges. Its
optional integer parameter `numranges` determines the maximum number of ranges
in one index key. The default value of `numranges` is 100. Valid values are
between 1 and 253. Using larger arrays as GiST index keys leads to a more
precise search (scanning a smaller fraction of the index and fewer heap
pages), at the cost of a larger index.

`gist__intbig_ops` approximates an integer set as a bitmap signature. Its
optional integer parameter `siglen` determines the signature length in bytes.
The default signature length is 16 bytes. Valid values of signature length are
between 1 and 2024 bytes. Longer signatures lead to a more precise search
(scanning a smaller fraction of the index and fewer heap pages), at the cost
of a larger index.

There is also a non-default GIN operator class `gin__int_ops`, which supports
these operators as well as `<@`.

The choice between GiST and GIN indexing depends on the relative performance
characteristics of GiST and GIN, which are discussed elsewhere.

### F.20.3. Example #

    
    
    -- a message can be in one or more “sections”
    CREATE TABLE message (mid INT PRIMARY KEY, sections INT[], ...);
    
    -- create specialized index with signature length of 32 bytes
    CREATE INDEX message_rdtree_idx ON message USING GIST (sections gist__intbig_ops (siglen = 32));
    
    -- select messages in section 1 OR 2 - OVERLAP operator
    SELECT message.mid FROM message WHERE message.sections && '{1,2}';
    
    -- select messages in sections 1 AND 2 - CONTAINS operator
    SELECT message.mid FROM message WHERE message.sections @> '{1,2}';
    
    -- the same, using QUERY operator
    SELECT message.mid FROM message WHERE message.sections @@ '1&2'::query_int;
    

### F.20.4. Benchmark #

The source directory `contrib/intarray/bench` contains a benchmark test suite,
which can be run against an installed PostgreSQL server. (It also requires
`DBD::Pg` to be installed.) To run:

    
    
    cd .../contrib/intarray/bench
    createdb TEST
    psql -c "CREATE EXTENSION intarray" TEST
    ./create_test.pl | psql TEST
    ./bench.pl
    

The `bench.pl` script has numerous options, which are displayed when it is run
without any arguments.

### F.20.5. Authors #

All work was done by Teodor Sigaev
(`<[teodor@sigaev.ru](mailto:teodor@sigaev.ru)>`) and Oleg Bartunov
(`<[oleg@sai.msu.su](mailto:oleg@sai.msu.su)>`). See
<http://www.sai.msu.su/~megera/postgres/gist/> for additional information.
Andrey Oktyabrski did a great work on adding new functions and operations.

* * *

[Prev](intagg.html "F.19. intagg — integer aggregator and enumerator")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](isn.html "F.21. isn — data types for international standard numbers \(ISBN, EAN, UPC, etc.\)")  
---|---|---  
F.19. intagg — integer aggregator and enumerator  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.21. isn — data types for international standard numbers (ISBN, EAN, UPC, etc.)  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/intarray.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

