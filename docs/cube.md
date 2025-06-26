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

Supported Versions: [Current](/docs/current/cube.html "PostgreSQL 17 -
F.11. cube — a multi-dimensional cube data type") ([17](/docs/17/cube.html
"PostgreSQL 17 - F.11. cube — a multi-dimensional cube data type")) /
[16](/docs/16/cube.html "PostgreSQL 16 - F.11. cube — a multi-dimensional cube
data type") / [15](/docs/15/cube.html "PostgreSQL 15 - F.11. cube — a multi-
dimensional cube data type") / [14](/docs/14/cube.html "PostgreSQL 14 -
F.11. cube — a multi-dimensional cube data type") / [13](/docs/13/cube.html
"PostgreSQL 13 - F.11. cube — a multi-dimensional cube data type")

Development Versions: [18](/docs/18/cube.html "PostgreSQL 18 - F.11. cube — a
multi-dimensional cube data type") / [devel](/docs/devel/cube.html "PostgreSQL
devel - F.11. cube — a multi-dimensional cube data type")

Unsupported versions: [12](/docs/12/cube.html "PostgreSQL 12 - F.11. cube — a
multi-dimensional cube data type") / [11](/docs/11/cube.html "PostgreSQL 11 -
F.11. cube — a multi-dimensional cube data type") / [10](/docs/10/cube.html
"PostgreSQL 10 - F.11. cube — a multi-dimensional cube data type") /
[9.6](/docs/9.6/cube.html "PostgreSQL 9.6 - F.11. cube — a multi-dimensional
cube data type") / [9.5](/docs/9.5/cube.html "PostgreSQL 9.5 - F.11. cube — a
multi-dimensional cube data type") / [9.4](/docs/9.4/cube.html "PostgreSQL 9.4
- F.11. cube — a multi-dimensional cube data type") /
[9.3](/docs/9.3/cube.html "PostgreSQL 9.3 - F.11. cube — a multi-dimensional
cube data type") / [9.2](/docs/9.2/cube.html "PostgreSQL 9.2 - F.11. cube — a
multi-dimensional cube data type") / [9.1](/docs/9.1/cube.html "PostgreSQL 9.1
- F.11. cube — a multi-dimensional cube data type") /
[9.0](/docs/9.0/cube.html "PostgreSQL 9.0 - F.11. cube — a multi-dimensional
cube data type") / [8.4](/docs/8.4/cube.html "PostgreSQL 8.4 - F.11. cube — a
multi-dimensional cube data type") / [8.3](/docs/8.3/cube.html "PostgreSQL 8.3
- F.11. cube — a multi-dimensional cube data type")

__

F.11. cube — a multi-dimensional cube data type  
---  
[Prev](citext.html "F.10. citext — a case-insensitive character string type")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](dblink.html "F.12. dblink — connect to other PostgreSQL databases")  
  
* * *

## F.11. cube — a multi-dimensional cube data type #

[F.11.1. Syntax](cube.html#CUBE-SYNTAX)

[F.11.2. Precision](cube.html#CUBE-PRECISION)

[F.11.3. Usage](cube.html#CUBE-USAGE)

[F.11.4. Defaults](cube.html#CUBE-DEFAULTS)

[F.11.5. Notes](cube.html#CUBE-NOTES)

[F.11.6. Credits](cube.html#CUBE-CREDITS)

This module implements a data type `cube` for representing multidimensional
cubes.

This module is considered “trusted”, that is, it can be installed by non-
superusers who have `CREATE` privilege on the current database.

### F.11.1. Syntax #

[Table F.2](cube.html#CUBE-REPR-TABLE "Table F.2. Cube External
Representations") shows the valid external representations for the `cube`
type. _`x`_ , _`y`_ , etc. denote floating-point numbers.

**Table  F.2. Cube External Representations**

External Syntax | Meaning  
---|---  
`_`x`_` | A one-dimensional point (or, zero-length one-dimensional interval)  
`(_`x`_)` | Same as above  
`_`x1`_ ,_`x2`_ ,...,_`xn`_` | A point in n-dimensional space, represented internally as a zero-volume cube  
`(_`x1`_ ,_`x2`_ ,...,_`xn`_)` | Same as above  
`(_`x`_),(_`y`_)` | A one-dimensional interval starting at _`x`_ and ending at _`y`_ or vice versa; the order does not matter  
`[(_`x`_),(_`y`_)]` | Same as above  
`(_`x1`_ ,...,_`xn`_),(_`y1`_ ,...,_`yn`_)` | An n-dimensional cube represented by a pair of its diagonally opposite corners  
`[(_`x1`_ ,...,_`xn`_),(_`y1`_ ,...,_`yn`_)]` | Same as above  
  
  

It does not matter which order the opposite corners of a cube are entered in.
The `cube` functions automatically swap values if needed to create a uniform
“lower left — upper right” internal representation. When the corners coincide,
`cube` stores only one corner along with an “is point” flag to avoid wasting
space.

White space is ignored on input, so `[(_`x`_),(_`y`_)]` is the same as `[ (
_`x`_ ), ( _`y`_ ) ]`.

### F.11.2. Precision #

Values are stored internally as 64-bit floating point numbers. This means that
numbers with more than about 16 significant digits will be truncated.

### F.11.3. Usage #

[Table F.3](cube.html#CUBE-OPERATORS-TABLE "Table F.3. Cube Operators") shows
the specialized operators provided for type `cube`.

**Table  F.3. Cube Operators**

Operator Description  
---  
`cube` `&&` `cube` → `boolean` Do the cubes overlap?  
`cube` `@>` `cube` → `boolean` Does the first cube contain the second?  
`cube` `<@` `cube` → `boolean` Is the first cube contained in the second?  
`cube` `->` `integer` → `float8` Extracts the _`n`_ -th coordinate of the cube
(counting from 1).  
`cube` `~>` `integer` → `float8` Extracts the _`n`_ -th coordinate of the
cube, counting in the following way: _`n`_ = 2 * _`k`_ \- 1 means lower bound
of _`k`_ -th dimension, _`n`_ = 2 * _`k`_ means upper bound of _`k`_ -th
dimension. Negative _`n`_ denotes the inverse value of the corresponding
positive coordinate. This operator is designed for KNN-GiST support.  
`cube` `<->` `cube` → `float8` Computes the Euclidean distance between the two
cubes.  
`cube` `<#>` `cube` → `float8` Computes the taxicab (L-1 metric) distance
between the two cubes.  
`cube` `<=>` `cube` → `float8` Computes the Chebyshev (L-inf metric) distance
between the two cubes.  
  
  

In addition to the above operators, the usual comparison operators shown in
[Table 9.1](functions-comparison.html#FUNCTIONS-COMPARISON-OP-TABLE
"Table 9.1. Comparison Operators") are available for type `cube`. These
operators first compare the first coordinates, and if those are equal, compare
the second coordinates, etc. They exist mainly to support the b-tree index
operator class for `cube`, which can be useful for example if you would like a
UNIQUE constraint on a `cube` column. Otherwise, this ordering is not of much
practical use.

The `cube` module also provides a GiST index operator class for `cube` values.
A `cube` GiST index can be used to search for values using the `=`, `&&`,
`@>`, and `<@` operators in `WHERE` clauses.

In addition, a `cube` GiST index can be used to find nearest neighbors using
the metric operators `<->`, `<#>`, and `<=>` in `ORDER BY` clauses. For
example, the nearest neighbor of the 3-D point (0.5, 0.5, 0.5) could be found
efficiently with:

    
    
    SELECT c FROM test ORDER BY c <-> cube(array[0.5,0.5,0.5]) LIMIT 1;
    

The `~>` operator can also be used in this way to efficiently retrieve the
first few values sorted by a selected coordinate. For example, to get the
first few cubes ordered by the first coordinate (lower left corner) ascending
one could use the following query:

    
    
    SELECT c FROM test ORDER BY c ~> 1 LIMIT 5;
    

And to get 2-D cubes ordered by the first coordinate of the upper right corner
descending:

    
    
    SELECT c FROM test ORDER BY c ~> 3 DESC LIMIT 5;
    

[Table F.4](cube.html#CUBE-FUNCTIONS-TABLE "Table F.4. Cube Functions") shows
the available functions.

**Table  F.4. Cube Functions**

Function Description Example(s)  
---  
`cube` ( `float8` ) → `cube` Makes a one dimensional cube with both
coordinates the same. `cube(1)` → `(1)`  
`cube` ( `float8`, `float8` ) → `cube` Makes a one dimensional cube. `cube(1,
2)` → `(1),(2)`  
`cube` ( `float8[]` ) → `cube` Makes a zero-volume cube using the coordinates
defined by the array. `cube(ARRAY[1,2,3])` → `(1, 2, 3)`  
`cube` ( `float8[]`, `float8[]` ) → `cube` Makes a cube with upper right and
lower left coordinates as defined by the two arrays, which must be of the same
length. `cube(ARRAY[1,2], ARRAY[3,4])` → `(1, 2),(3, 4)`  
`cube` ( `cube`, `float8` ) → `cube` Makes a new cube by adding a dimension on
to an existing cube, with the same values for both endpoints of the new
coordinate. This is useful for building cubes piece by piece from calculated
values. `cube('(1,2),(3,4)'::cube, 5)` → `(1, 2, 5),(3, 4, 5)`  
`cube` ( `cube`, `float8`, `float8` ) → `cube` Makes a new cube by adding a
dimension on to an existing cube. This is useful for building cubes piece by
piece from calculated values. `cube('(1,2),(3,4)'::cube, 5, 6)` → `(1, 2,
5),(3, 4, 6)`  
`cube_dim` ( `cube` ) → `integer` Returns the number of dimensions of the
cube. `cube_dim('(1,2),(3,4)')` → `2`  
`cube_ll_coord` ( `cube`, `integer` ) → `float8` Returns the _`n`_ -th
coordinate value for the lower left corner of the cube.
`cube_ll_coord('(1,2),(3,4)', 2)` → `2`  
`cube_ur_coord` ( `cube`, `integer` ) → `float8` Returns the _`n`_ -th
coordinate value for the upper right corner of the cube.
`cube_ur_coord('(1,2),(3,4)', 2)` → `4`  
`cube_is_point` ( `cube` ) → `boolean` Returns true if the cube is a point,
that is, the two defining corners are the same. `cube_is_point(cube(1,1))` →
`t`  
`cube_distance` ( `cube`, `cube` ) → `float8` Returns the distance between two
cubes. If both cubes are points, this is the normal distance function.
`cube_distance('(1,2)', '(3,4)')` → `2.8284271247461903`  
`cube_subset` ( `cube`, `integer[]` ) → `cube` Makes a new cube from an
existing cube, using a list of dimension indexes from an array. Can be used to
extract the endpoints of a single dimension, or to drop dimensions, or to
reorder them as desired. `cube_subset(cube('(1,3,5),(6,7,8)'), ARRAY[2])` →
`(3),(7)` `cube_subset(cube('(1,3,5),(6,7,8)'), ARRAY[3,2,1,1])` → `(5, 3, 1,
1),(8, 7, 6, 6)`  
`cube_union` ( `cube`, `cube` ) → `cube` Produces the union of two cubes.
`cube_union('(1,2)', '(3,4)')` → `(1, 2),(3, 4)`  
`cube_inter` ( `cube`, `cube` ) → `cube` Produces the intersection of two
cubes. `cube_inter('(1,2)', '(3,4)')` → `(3, 4),(1, 2)`  
`cube_enlarge` ( _`c`_ `cube`, _`r`_ `double`, _`n`_ `integer` ) → `cube`
Increases the size of the cube by the specified radius _`r`_ in at least _`n`_
dimensions. If the radius is negative the cube is shrunk instead. All defined
dimensions are changed by the radius _`r`_. Lower-left coordinates are
decreased by _`r`_ and upper-right coordinates are increased by _`r`_. If a
lower-left coordinate is increased to more than the corresponding upper-right
coordinate (this can only happen when _`r`_ < 0) than both coordinates are set
to their average. If _`n`_ is greater than the number of defined dimensions
and the cube is being enlarged (_`r`_ > 0), then extra dimensions are added to
make _`n`_ altogether; 0 is used as the initial value for the extra
coordinates. This function is useful for creating bounding boxes around a
point for searching for nearby points. `cube_enlarge('(1,2),(3,4)', 0.5, 3)` →
`(0.5, 1.5, -0.5),(3.5, 4.5, 0.5)`  
  
  

### F.11.4. Defaults #

This union:

    
    
    select cube_union('(0,5,2),(2,3,1)', '0');
    cube_union
    -------------------
    (0, 0, 0),(2, 5, 2)
    (1 row)
    

does not contradict common sense, neither does the intersection:

    
    
    select cube_inter('(0,-1),(1,1)', '(-2),(2)');
    cube_inter
    -------------
    (0, 0),(1, 0)
    (1 row)
    

In all binary operations on differently-dimensioned cubes, the lower-
dimensional one is assumed to be a Cartesian projection, i. e., having zeroes
in place of coordinates omitted in the string representation. The above
examples are equivalent to:

    
    
    cube_union('(0,5,2),(2,3,1)','(0,0,0),(0,0,0)');
    cube_inter('(0,-1),(1,1)','(-2,0),(2,0)');
    

The following containment predicate uses the point syntax, while in fact the
second argument is internally represented by a box. This syntax makes it
unnecessary to define a separate point type and functions for (box,point)
predicates.

    
    
    select cube_contains('(0,0),(1,1)', '0.5,0.5');
    cube_contains
    --------------
    t
    (1 row)
    

### F.11.5. Notes #

For examples of usage, see the regression test `sql/cube.sql`.

To make it harder for people to break things, there is a limit of 100 on the
number of dimensions of cubes. This is set in `cubedata.h` if you need
something bigger.

### F.11.6. Credits #

Original author: Gene Selkov, Jr.
`<[selkovjr@mcs.anl.gov](mailto:selkovjr@mcs.anl.gov)>`, Mathematics and
Computer Science Division, Argonne National Laboratory.

My thanks are primarily to Prof. Joe Hellerstein
(<https://dsf.berkeley.edu/jmh/>) for elucidating the gist of the GiST
(<http://gist.cs.berkeley.edu/>), and to his former student Andy Dong for his
example written for Illustra. I am also grateful to all Postgres developers,
present and past, for enabling myself to create my own world and live
undisturbed in it. And I would like to acknowledge my gratitude to Argonne Lab
and to the U.S. Department of Energy for the years of faithful support of my
database research.

Minor updates to this package were made by Bruno Wolff III
`<[bruno@wolff.to](mailto:bruno@wolff.to)>` in August/September of 2002. These
include changing the precision from single precision to double precision and
adding some new functions.

Additional updates were made by Joshua Reich
`<[josh@root.net](mailto:josh@root.net)>` in July 2006. These include
`cube(float8[], float8[])` and cleaning up the code to use the V1 call
protocol instead of the deprecated V0 protocol.

* * *

[Prev](citext.html "F.10. citext — a case-insensitive character string type")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](dblink.html "F.12. dblink — connect to other PostgreSQL databases")  
---|---|---  
F.10. citext — a case-insensitive character string type  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.12. dblink — connect to other PostgreSQL databases  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/cube.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

