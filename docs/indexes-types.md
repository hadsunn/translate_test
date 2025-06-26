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

Supported Versions: [Current](/docs/current/indexes-types.html "PostgreSQL 17
- 11.2. Index Types") ([17](/docs/17/indexes-types.html "PostgreSQL 17 -
11.2. Index Types")) / [16](/docs/16/indexes-types.html "PostgreSQL 16 -
11.2. Index Types") / [15](/docs/15/indexes-types.html "PostgreSQL 15 -
11.2. Index Types") / [14](/docs/14/indexes-types.html "PostgreSQL 14 -
11.2. Index Types") / [13](/docs/13/indexes-types.html "PostgreSQL 13 -
11.2. Index Types")

Development Versions: [18](/docs/18/indexes-types.html "PostgreSQL 18 -
11.2. Index Types") / [devel](/docs/devel/indexes-types.html "PostgreSQL devel
- 11.2. Index Types")

Unsupported versions: [12](/docs/12/indexes-types.html "PostgreSQL 12 -
11.2. Index Types") / [11](/docs/11/indexes-types.html "PostgreSQL 11 -
11.2. Index Types") / [10](/docs/10/indexes-types.html "PostgreSQL 10 -
11.2. Index Types") / [9.6](/docs/9.6/indexes-types.html "PostgreSQL 9.6 -
11.2. Index Types") / [9.5](/docs/9.5/indexes-types.html "PostgreSQL 9.5 -
11.2. Index Types") / [9.4](/docs/9.4/indexes-types.html "PostgreSQL 9.4 -
11.2. Index Types") / [9.3](/docs/9.3/indexes-types.html "PostgreSQL 9.3 -
11.2. Index Types") / [9.2](/docs/9.2/indexes-types.html "PostgreSQL 9.2 -
11.2. Index Types") / [9.1](/docs/9.1/indexes-types.html "PostgreSQL 9.1 -
11.2. Index Types") / [9.0](/docs/9.0/indexes-types.html "PostgreSQL 9.0 -
11.2. Index Types") / [8.4](/docs/8.4/indexes-types.html "PostgreSQL 8.4 -
11.2. Index Types") / [8.3](/docs/8.3/indexes-types.html "PostgreSQL 8.3 -
11.2. Index Types") / [8.2](/docs/8.2/indexes-types.html "PostgreSQL 8.2 -
11.2. Index Types") / [8.1](/docs/8.1/indexes-types.html "PostgreSQL 8.1 -
11.2. Index Types") / [8.0](/docs/8.0/indexes-types.html "PostgreSQL 8.0 -
11.2. Index Types") / [7.4](/docs/7.4/indexes-types.html "PostgreSQL 7.4 -
11.2. Index Types") / [7.3](/docs/7.3/indexes-types.html "PostgreSQL 7.3 -
11.2. Index Types") / [7.2](/docs/7.2/indexes-types.html "PostgreSQL 7.2 -
11.2. Index Types")

__

11.2. Index Types  
---  
[Prev](indexes-intro.html "11.1. Introduction")  | [Up](indexes.html "Chapter 11. Indexes") | Chapter 11. Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](indexes-multicolumn.html "11.3. Multicolumn Indexes")  
  
* * *

## 11.2. Index Types #

[11.2.1. B-Tree](indexes-types.html#INDEXES-TYPES-BTREE)

[11.2.2. Hash](indexes-types.html#INDEXES-TYPES-HASH)

[11.2.3. GiST](indexes-types.html#INDEXES-TYPE-GIST)

[11.2.4. SP-GiST](indexes-types.html#INDEXES-TYPE-SPGIST)

[11.2.5. GIN](indexes-types.html#INDEXES-TYPES-GIN)

[11.2.6. BRIN](indexes-types.html#INDEXES-TYPES-BRIN)

PostgreSQL provides several index types: B-tree, Hash, GiST, SP-GiST, GIN,
BRIN, and the extension [bloom](bloom.html "F.7. bloom — bloom filter index
access method"). Each index type uses a different algorithm that is best
suited to different types of indexable clauses. By default, the [`CREATE
INDEX`](sql-createindex.html "CREATE INDEX") command creates B-tree indexes,
which fit the most common situations. The other index types are selected by
writing the keyword `USING` followed by the index type name. For example, to
create a Hash index:

    
    
    CREATE INDEX _name_ ON _table_ USING HASH (_column_);
    

### 11.2.1. B-Tree #

B-trees can handle equality and range queries on data that can be sorted into
some ordering. In particular, the PostgreSQL query planner will consider using
a B-tree index whenever an indexed column is involved in a comparison using
one of these operators:

    
    
    <   <=   =   >=   >
    

Constructs equivalent to combinations of these operators, such as `BETWEEN`
and `IN`, can also be implemented with a B-tree index search. Also, an `IS
NULL` or `IS NOT NULL` condition on an index column can be used with a B-tree
index.

The optimizer can also use a B-tree index for queries involving the pattern
matching operators `LIKE` and `~` _if_ the pattern is a constant and is
anchored to the beginning of the string — for example, `col LIKE 'foo%'` or
`col ~ '^foo'`, but not `col LIKE '%bar'`. However, if your database does not
use the C locale you will need to create the index with a special operator
class to support indexing of pattern-matching queries; see [Section
11.10](indexes-opclass.html "11.10. Operator Classes and Operator Families")
below. It is also possible to use B-tree indexes for `ILIKE` and `~*`, but
only if the pattern starts with non-alphabetic characters, i.e., characters
that are not affected by upper/lower case conversion.

B-tree indexes can also be used to retrieve data in sorted order. This is not
always faster than a simple scan and sort, but it is often helpful.

### 11.2.2. Hash #

Hash indexes store a 32-bit hash code derived from the value of the indexed
column. Hence, such indexes can only handle simple equality comparisons. The
query planner will consider using a hash index whenever an indexed column is
involved in a comparison using the equal operator:

    
    
    =
    

### 11.2.3. GiST #

GiST indexes are not a single kind of index, but rather an infrastructure
within which many different indexing strategies can be implemented.
Accordingly, the particular operators with which a GiST index can be used vary
depending on the indexing strategy (the _operator class_). As an example, the
standard distribution of PostgreSQL includes GiST operator classes for several
two-dimensional geometric data types, which support indexed queries using
these operators:

    
    
    <<   &<   &>   >>   <<|   &<|   |&>   |>>   @>   <@   ~=   &&
    

(See [Section 9.11](functions-geometry.html "9.11. Geometric Functions and
Operators") for the meaning of these operators.) The GiST operator classes
included in the standard distribution are documented in [Table 68.1](gist-
builtin-opclasses.html#GIST-BUILTIN-OPCLASSES-TABLE "Table 68.1. Built-in GiST
Operator Classes"). Many other GiST operator classes are available in the
`contrib` collection or as separate projects. For more information see
[Chapter 68](gist.html "Chapter 68. GiST Indexes").

GiST indexes are also capable of optimizing “nearest-neighbor” searches, such
as

    
    
    SELECT * FROM places ORDER BY location <-> point '(101,456)' LIMIT 10;
    
    

which finds the ten places closest to a given target point. The ability to do
this is again dependent on the particular operator class being used. In [Table
68.1](gist-builtin-opclasses.html#GIST-BUILTIN-OPCLASSES-TABLE
"Table 68.1. Built-in GiST Operator Classes"), operators that can be used in
this way are listed in the column “Ordering Operators”.

### 11.2.4. SP-GiST #

SP-GiST indexes, like GiST indexes, offer an infrastructure that supports
various kinds of searches. SP-GiST permits implementation of a wide range of
different non-balanced disk-based data structures, such as quadtrees, k-d
trees, and radix trees (tries). As an example, the standard distribution of
PostgreSQL includes SP-GiST operator classes for two-dimensional points, which
support indexed queries using these operators:

    
    
    <<   >>   ~=   <@   <<|   |>>
    

(See [Section 9.11](functions-geometry.html "9.11. Geometric Functions and
Operators") for the meaning of these operators.) The SP-GiST operator classes
included in the standard distribution are documented in [Table 69.1](spgist-
builtin-opclasses.html#SPGIST-BUILTIN-OPCLASSES-TABLE "Table 69.1. Built-in
SP-GiST Operator Classes"). For more information see [Chapter 69](spgist.html
"Chapter 69. SP-GiST Indexes").

Like GiST, SP-GiST supports “nearest-neighbor” searches. For SP-GiST operator
classes that support distance ordering, the corresponding operator is listed
in the “Ordering Operators” column in [Table 69.1](spgist-builtin-
opclasses.html#SPGIST-BUILTIN-OPCLASSES-TABLE "Table 69.1. Built-in SP-GiST
Operator Classes").

### 11.2.5. GIN #

GIN indexes are “inverted indexes” which are appropriate for data values that
contain multiple component values, such as arrays. An inverted index contains
a separate entry for each component value, and can efficiently handle queries
that test for the presence of specific component values.

Like GiST and SP-GiST, GIN can support many different user-defined indexing
strategies, and the particular operators with which a GIN index can be used
vary depending on the indexing strategy. As an example, the standard
distribution of PostgreSQL includes a GIN operator class for arrays, which
supports indexed queries using these operators:

    
    
    <@   @>   =   &&
    

(See [Section 9.19](functions-array.html "9.19. Array Functions and
Operators") for the meaning of these operators.) The GIN operator classes
included in the standard distribution are documented in [Table 70.1](gin-
builtin-opclasses.html#GIN-BUILTIN-OPCLASSES-TABLE "Table 70.1. Built-in GIN
Operator Classes"). Many other GIN operator classes are available in the
`contrib` collection or as separate projects. For more information see
[Chapter 70](gin.html "Chapter 70. GIN Indexes").

### 11.2.6. BRIN #

BRIN indexes (a shorthand for Block Range INdexes) store summaries about the
values stored in consecutive physical block ranges of a table. Thus, they are
most effective for columns whose values are well-correlated with the physical
order of the table rows. Like GiST, SP-GiST and GIN, BRIN can support many
different indexing strategies, and the particular operators with which a BRIN
index can be used vary depending on the indexing strategy. For data types that
have a linear sort order, the indexed data corresponds to the minimum and
maximum values of the values in the column for each block range. This supports
indexed queries using these operators:

    
    
    <   <=   =   >=   >
    

The BRIN operator classes included in the standard distribution are documented
in [Table 71.1](brin-builtin-opclasses.html#BRIN-BUILTIN-OPCLASSES-TABLE
"Table 71.1. Built-in BRIN Operator Classes"). For more information see
[Chapter 71](brin.html "Chapter 71. BRIN Indexes").

* * *

[Prev](indexes-intro.html "11.1. Introduction")  | [Up](indexes.html "Chapter 11. Indexes") |  [Next](indexes-multicolumn.html "11.3. Multicolumn Indexes")  
---|---|---  
11.1. Introduction  | [Home](index.html "PostgreSQL 16.9 Documentation") |  11.3. Multicolumn Indexes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/indexes-types.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

