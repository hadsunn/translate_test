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

Supported Versions: [Current](/docs/current/functions-geometry.html
"PostgreSQL 17 - 9.11. Geometric Functions and Operators")
([17](/docs/17/functions-geometry.html "PostgreSQL 17 - 9.11. Geometric
Functions and Operators")) / [16](/docs/16/functions-geometry.html "PostgreSQL
16 - 9.11. Geometric Functions and Operators") / [15](/docs/15/functions-
geometry.html "PostgreSQL 15 - 9.11. Geometric Functions and Operators") /
[14](/docs/14/functions-geometry.html "PostgreSQL 14 - 9.11. Geometric
Functions and Operators") / [13](/docs/13/functions-geometry.html "PostgreSQL
13 - 9.11. Geometric Functions and Operators")

Development Versions: [18](/docs/18/functions-geometry.html "PostgreSQL 18 -
9.11. Geometric Functions and Operators") / [devel](/docs/devel/functions-
geometry.html "PostgreSQL devel - 9.11. Geometric Functions and Operators")

Unsupported versions: [12](/docs/12/functions-geometry.html "PostgreSQL 12 -
9.11. Geometric Functions and Operators") / [11](/docs/11/functions-
geometry.html "PostgreSQL 11 - 9.11. Geometric Functions and Operators") /
[10](/docs/10/functions-geometry.html "PostgreSQL 10 - 9.11. Geometric
Functions and Operators") / [9.6](/docs/9.6/functions-geometry.html
"PostgreSQL 9.6 - 9.11. Geometric Functions and Operators") /
[9.5](/docs/9.5/functions-geometry.html "PostgreSQL 9.5 - 9.11. Geometric
Functions and Operators") / [9.4](/docs/9.4/functions-geometry.html
"PostgreSQL 9.4 - 9.11. Geometric Functions and Operators") /
[9.3](/docs/9.3/functions-geometry.html "PostgreSQL 9.3 - 9.11. Geometric
Functions and Operators") / [9.2](/docs/9.2/functions-geometry.html
"PostgreSQL 9.2 - 9.11. Geometric Functions and Operators") /
[9.1](/docs/9.1/functions-geometry.html "PostgreSQL 9.1 - 9.11. Geometric
Functions and Operators") / [9.0](/docs/9.0/functions-geometry.html
"PostgreSQL 9.0 - 9.11. Geometric Functions and Operators") /
[8.4](/docs/8.4/functions-geometry.html "PostgreSQL 8.4 - 9.11. Geometric
Functions and Operators") / [8.3](/docs/8.3/functions-geometry.html
"PostgreSQL 8.3 - 9.11. Geometric Functions and Operators") /
[8.2](/docs/8.2/functions-geometry.html "PostgreSQL 8.2 - 9.11. Geometric
Functions and Operators") / [8.1](/docs/8.1/functions-geometry.html
"PostgreSQL 8.1 - 9.11. Geometric Functions and Operators") /
[8.0](/docs/8.0/functions-geometry.html "PostgreSQL 8.0 - 9.11. Geometric
Functions and Operators") / [7.4](/docs/7.4/functions-geometry.html
"PostgreSQL 7.4 - 9.11. Geometric Functions and Operators") /
[7.3](/docs/7.3/functions-geometry.html "PostgreSQL 7.3 - 9.11. Geometric
Functions and Operators") / [7.2](/docs/7.2/functions-geometry.html
"PostgreSQL 7.2 - 9.11. Geometric Functions and Operators") /
[7.1](/docs/7.1/functions-geometry.html "PostgreSQL 7.1 - 9.11. Geometric
Functions and Operators")

__

9.11. Geometric Functions and Operators  
---  
[Prev](functions-enum.html "9.10. Enum Support Functions")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions-net.html "9.12. Network Address Functions and Operators")  
  
* * *

## 9.11. Geometric Functions and Operators #

The geometric types `point`, `box`, `lseg`, `line`, `path`, `polygon`, and
`circle` have a large set of native support functions and operators, shown in
[Table 9.36](functions-geometry.html#FUNCTIONS-GEOMETRY-OP-TABLE
"Table 9.36. Geometric Operators"), [Table 9.37](functions-
geometry.html#FUNCTIONS-GEOMETRY-FUNC-TABLE "Table 9.37. Geometric
Functions"), and [Table 9.38](functions-geometry.html#FUNCTIONS-GEOMETRY-CONV-
TABLE "Table 9.38. Geometric Type Conversion Functions").

**Table  9.36. Geometric Operators**

Operator Description Example(s)  
---  
_`geometric_type`_ `+` `point` → `_`geometric_type`_` Adds the coordinates of
the second `point` to those of each point of the first argument, thus
performing translation. Available for `point`, `box`, `path`, `circle`. `box
'(1,1),(0,0)' + point '(2,0)'` → `(3,1),(2,0)`  
`path` `+` `path` → `path` Concatenates two open paths (returns NULL if either
path is closed). `path '[(0,0),(1,1)]' + path '[(2,2),(3,3),(4,4)]'` →
`[(0,0),(1,1),(2,2),(3,3),(4,4)]`  
_`geometric_type`_ `-` `point` → `_`geometric_type`_` Subtracts the
coordinates of the second `point` from those of each point of the first
argument, thus performing translation. Available for `point`, `box`, `path`,
`circle`. `box '(1,1),(0,0)' - point '(2,0)'` → `(-1,1),(-2,0)`  
_`geometric_type`_ `*` `point` → `_`geometric_type`_` Multiplies each point of
the first argument by the second `point` (treating a point as being a complex
number represented by real and imaginary parts, and performing standard
complex multiplication). If one interprets the second `point` as a vector,
this is equivalent to scaling the object's size and distance from the origin
by the length of the vector, and rotating it counterclockwise around the
origin by the vector's angle from the _`x`_ axis. Available for `point`,
`box`,[a] `path`, `circle`. `path '((0,0),(1,0),(1,1))' * point '(3.0,0)'` →
`((0,0),(3,0),(3,3))` `path '((0,0),(1,0),(1,1))' * point(cosd(45), sind(45))`
→ `((0,0),​(0.7071067811865475,0.7071067811865475),​(0,1.414213562373095))`  
_`geometric_type`_ `/` `point` → `_`geometric_type`_` Divides each point of
the first argument by the second `point` (treating a point as being a complex
number represented by real and imaginary parts, and performing standard
complex division). If one interprets the second `point` as a vector, this is
equivalent to scaling the object's size and distance from the origin down by
the length of the vector, and rotating it clockwise around the origin by the
vector's angle from the _`x`_ axis. Available for `point`,
`box`,[[a]](functions-geometry.html#ftn.FUNCTIONS-GEOMETRY-ROTATION-FN)
`path`, `circle`. `path '((0,0),(1,0),(1,1))' / point '(2.0,0)'` →
`((0,0),(0.5,0),(0.5,0.5))` `path '((0,0),(1,0),(1,1))' / point(cosd(45),
sind(45))` →
`((0,0),​(0.7071067811865476,-0.7071067811865476),​(1.4142135623730951,0))`  
`@-@` _`geometric_type`_ → `double precision` Computes the total length.
Available for `lseg`, `path`. `@-@ path '[(0,0),(1,0),(1,1)]'` → `2`  
`@@` _`geometric_type`_ → `point` Computes the center point. Available for
`box`, `lseg`, `polygon`, `circle`. `@@ box '(2,2),(0,0)'` → `(1,1)`  
`#` _`geometric_type`_ → `integer` Returns the number of points. Available for
`path`, `polygon`. `# path '((1,0),(0,1),(-1,0))'` → `3`  
_`geometric_type`_ `#` _`geometric_type`_ → `point` Computes the point of
intersection, or NULL if there is none. Available for `lseg`, `line`. `lseg
'[(0,0),(1,1)]' # lseg '[(1,0),(0,1)]'` → `(0.5,0.5)`  
`box` `#` `box` → `box` Computes the intersection of two boxes, or NULL if
there is none. `box '(2,2),(-1,-1)' # box '(1,1),(-2,-2)'` → `(1,1),(-1,-1)`  
_`geometric_type`_ `##` _`geometric_type`_ → `point` Computes the closest
point to the first object on the second object. Available for these pairs of
types: (`point`, `box`), (`point`, `lseg`), (`point`, `line`), (`lseg`,
`box`), (`lseg`, `lseg`), (`line`, `lseg`). `point '(0,0)' ## lseg
'[(2,0),(0,2)]'` → `(1,1)`  
_`geometric_type`_ `<->` _`geometric_type`_ → `double precision` Computes the
distance between the objects. Available for all seven geometric types, for all
combinations of `point` with another geometric type, and for these additional
pairs of types: (`box`, `lseg`), (`lseg`, `line`), (`polygon`, `circle`) (and
the commutator cases). `circle '<(0,0),1>' <-> circle '<(5,0),1>'` → `3`  
_`geometric_type`_ `@>` _`geometric_type`_ → `boolean` Does first object
contain second? Available for these pairs of types: (`box`, `point`), (`box`,
`box`), (`path`, `point`), (`polygon`, `point`), (`polygon`, `polygon`),
(`circle`, `point`), (`circle`, `circle`). `circle '<(0,0),2>' @> point
'(1,1)'` → `t`  
_`geometric_type`_ `<@` _`geometric_type`_ → `boolean` Is first object
contained in or on second? Available for these pairs of types: (`point`,
`box`), (`point`, `lseg`), (`point`, `line`), (`point`, `path`), (`point`,
`polygon`), (`point`, `circle`), (`box`, `box`), (`lseg`, `box`), (`lseg`,
`line`), (`polygon`, `polygon`), (`circle`, `circle`). `point '(1,1)' <@
circle '<(0,0),2>'` → `t`  
_`geometric_type`_ `&&` _`geometric_type`_ → `boolean` Do these objects
overlap? (One point in common makes this true.) Available for `box`,
`polygon`, `circle`. `box '(1,1),(0,0)' && box '(2,2),(0,0)'` → `t`  
_`geometric_type`_ `<<` _`geometric_type`_ → `boolean` Is first object
strictly left of second? Available for `point`, `box`, `polygon`, `circle`.
`circle '<(0,0),1>' << circle '<(5,0),1>'` → `t`  
_`geometric_type`_ `>>` _`geometric_type`_ → `boolean` Is first object
strictly right of second? Available for `point`, `box`, `polygon`, `circle`.
`circle '<(5,0),1>' >> circle '<(0,0),1>'` → `t`  
_`geometric_type`_ `&<` _`geometric_type`_ → `boolean` Does first object not
extend to the right of second? Available for `box`, `polygon`, `circle`. `box
'(1,1),(0,0)' &< box '(2,2),(0,0)'` → `t`  
_`geometric_type`_ `&>` _`geometric_type`_ → `boolean` Does first object not
extend to the left of second? Available for `box`, `polygon`, `circle`. `box
'(3,3),(0,0)' &> box '(2,2),(0,0)'` → `t`  
_`geometric_type`_ `<<|` _`geometric_type`_ → `boolean` Is first object
strictly below second? Available for `point`, `box`, `polygon`, `circle`. `box
'(3,3),(0,0)' <<| box '(5,5),(3,4)'` → `t`  
_`geometric_type`_ `|>>` _`geometric_type`_ → `boolean` Is first object
strictly above second? Available for `point`, `box`, `polygon`, `circle`. `box
'(5,5),(3,4)' |>> box '(3,3),(0,0)'` → `t`  
_`geometric_type`_ `&<|` _`geometric_type`_ → `boolean` Does first object not
extend above second? Available for `box`, `polygon`, `circle`. `box
'(1,1),(0,0)' &<| box '(2,2),(0,0)'` → `t`  
_`geometric_type`_ `|&>` _`geometric_type`_ → `boolean` Does first object not
extend below second? Available for `box`, `polygon`, `circle`. `box
'(3,3),(0,0)' |&> box '(2,2),(0,0)'` → `t`  
`box` `<^` `box` → `boolean` Is first object below second (allows edges to
touch)? `box '((1,1),(0,0))' <^ box '((2,2),(1,1))'` → `t`  
`box` `>^` `box` → `boolean` Is first object above second (allows edges to
touch)? `box '((2,2),(1,1))' >^ box '((1,1),(0,0))'` → `t`  
_`geometric_type`_ `?#` _`geometric_type`_ → `boolean` Do these objects
intersect? Available for these pairs of types: (`box`, `box`), (`lseg`,
`box`), (`lseg`, `lseg`), (`lseg`, `line`), (`line`, `box`), (`line`, `line`),
(`path`, `path`). `lseg '[(-1,0),(1,0)]' ?# box '(2,2),(-2,-2)'` → `t`  
`?-` `line` → `boolean` `?-` `lseg` → `boolean` Is line horizontal? `?- lseg
'[(-1,0),(1,0)]'` → `t`  
`point` `?-` `point` → `boolean` Are points horizontally aligned (that is,
have same y coordinate)? `point '(1,0)' ?- point '(0,0)'` → `t`  
`?|` `line` → `boolean` `?|` `lseg` → `boolean` Is line vertical? `?| lseg
'[(-1,0),(1,0)]'` → `f`  
`point` `?|` `point` → `boolean` Are points vertically aligned (that is, have
same x coordinate)? `point '(0,1)' ?| point '(0,0)'` → `t`  
`line` `?-|` `line` → `boolean` `lseg` `?-|` `lseg` → `boolean` Are lines
perpendicular? `lseg '[(0,0),(0,1)]' ?-| lseg '[(0,0),(1,0)]'` → `t`  
`line` `?||` `line` → `boolean` `lseg` `?||` `lseg` → `boolean` Are lines
parallel? `lseg '[(-1,0),(1,0)]' ?|| lseg '[(-1,2),(1,2)]'` → `t`  
_`geometric_type`_ `~=` _`geometric_type`_ → `boolean` Are these objects the
same? Available for `point`, `box`, `polygon`, `circle`. `polygon
'((0,0),(1,1))' ~= polygon '((1,1),(0,0))'` → `t`  
[a] “Rotating” a box with these operators only moves its corner points: the
box is still considered to have sides parallel to the axes. Hence the box's
size is not preserved, as a true rotation would do.  
  
  

### Caution

Note that the “same as” operator, `~=`, represents the usual notion of
equality for the `point`, `box`, `polygon`, and `circle` types. Some of the
geometric types also have an `=` operator, but `=` compares for equal _areas_
only. The other scalar comparison operators (`<=` and so on), where available
for these types, likewise compare areas.

### Note

Before PostgreSQL 14, the point is strictly below/above comparison operators
`point` `<<|` `point` and `point` `|>>` `point` were respectively called `<^`
and `>^`. These names are still available, but are deprecated and will
eventually be removed.

**Table  9.37. Geometric Functions**

Function Description Example(s)  
---  
`area` ( _`geometric_type`_ ) → `double precision` Computes area. Available
for `box`, `path`, `circle`. A `path` input must be closed, else NULL is
returned. Also, if the `path` is self-intersecting, the result may be
meaningless. `area(box '(2,2),(0,0)')` → `4`  
`center` ( _`geometric_type`_ ) → `point` Computes center point. Available for
`box`, `circle`. `center(box '(1,2),(0,0)')` → `(0.5,1)`  
`diagonal` ( `box` ) → `lseg` Extracts box's diagonal as a line segment (same
as `lseg(box)`). `diagonal(box '(1,2),(0,0)')` → `[(1,2),(0,0)]`  
`diameter` ( `circle` ) → `double precision` Computes diameter of circle.
`diameter(circle '<(0,0),2>')` → `4`  
`height` ( `box` ) → `double precision` Computes vertical size of box.
`height(box '(1,2),(0,0)')` → `2`  
`isclosed` ( `path` ) → `boolean` Is path closed? `isclosed(path
'((0,0),(1,1),(2,0))')` → `t`  
`isopen` ( `path` ) → `boolean` Is path open? `isopen(path
'[(0,0),(1,1),(2,0)]')` → `t`  
`length` ( _`geometric_type`_ ) → `double precision` Computes the total
length. Available for `lseg`, `path`. `length(path '((-1,0),(1,0))')` → `4`  
`npoints` ( _`geometric_type`_ ) → `integer` Returns the number of points.
Available for `path`, `polygon`. `npoints(path '[(0,0),(1,1),(2,0)]')` → `3`  
`pclose` ( `path` ) → `path` Converts path to closed form. `pclose(path
'[(0,0),(1,1),(2,0)]')` → `((0,0),(1,1),(2,0))`  
`popen` ( `path` ) → `path` Converts path to open form. `popen(path
'((0,0),(1,1),(2,0))')` → `[(0,0),(1,1),(2,0)]`  
`radius` ( `circle` ) → `double precision` Computes radius of circle.
`radius(circle '<(0,0),2>')` → `2`  
`slope` ( `point`, `point` ) → `double precision` Computes slope of a line
drawn through the two points. `slope(point '(0,0)', point '(2,1)')` → `0.5`  
`width` ( `box` ) → `double precision` Computes horizontal size of box.
`width(box '(1,2),(0,0)')` → `1`  
  
  

**Table  9.38. Geometric Type Conversion Functions**

Function Description Example(s)  
---  
`box` ( `circle` ) → `box` Computes box inscribed within the circle.
`box(circle '<(0,0),2>')` →
`(1.414213562373095,1.414213562373095),​(-1.414213562373095,-1.414213562373095)`  
`box` ( `point` ) → `box` Converts point to empty box. `box(point '(1,0)')` →
`(1,0),(1,0)`  
`box` ( `point`, `point` ) → `box` Converts any two corner points to box.
`box(point '(0,1)', point '(1,0)')` → `(1,1),(0,0)`  
`box` ( `polygon` ) → `box` Computes bounding box of polygon. `box(polygon
'((0,0),(1,1),(2,0))')` → `(2,1),(0,0)`  
`bound_box` ( `box`, `box` ) → `box` Computes bounding box of two boxes.
`bound_box(box '(1,1),(0,0)', box '(4,4),(3,3)')` → `(4,4),(0,0)`  
`circle` ( `box` ) → `circle` Computes smallest circle enclosing box.
`circle(box '(1,1),(0,0)')` → `<(0.5,0.5),0.7071067811865476>`  
`circle` ( `point`, `double precision` ) → `circle` Constructs circle from
center and radius. `circle(point '(0,0)', 2.0)` → `<(0,0),2>`  
`circle` ( `polygon` ) → `circle` Converts polygon to circle. The circle's
center is the mean of the positions of the polygon's points, and the radius is
the average distance of the polygon's points from that center. `circle(polygon
'((0,0),(1,3),(2,0))')` → `<(1,1),1.6094757082487299>`  
`line` ( `point`, `point` ) → `line` Converts two points to the line through
them. `line(point '(-1,0)', point '(1,0)')` → `{0,-1,0}`  
`lseg` ( `box` ) → `lseg` Extracts box's diagonal as a line segment. `lseg(box
'(1,0),(-1,0)')` → `[(1,0),(-1,0)]`  
`lseg` ( `point`, `point` ) → `lseg` Constructs line segment from two
endpoints. `lseg(point '(-1,0)', point '(1,0)')` → `[(-1,0),(1,0)]`  
`path` ( `polygon` ) → `path` Converts polygon to a closed path with the same
list of points. `path(polygon '((0,0),(1,1),(2,0))')` → `((0,0),(1,1),(2,0))`  
`point` ( `double precision`, `double precision` ) → `point` Constructs point
from its coordinates. `point(23.4, -44.5)` → `(23.4,-44.5)`  
`point` ( `box` ) → `point` Computes center of box. `point(box
'(1,0),(-1,0)')` → `(0,0)`  
`point` ( `circle` ) → `point` Computes center of circle. `point(circle
'<(0,0),2>')` → `(0,0)`  
`point` ( `lseg` ) → `point` Computes center of line segment. `point(lseg
'[(-1,0),(1,0)]')` → `(0,0)`  
`point` ( `polygon` ) → `point` Computes center of polygon (the mean of the
positions of the polygon's points). `point(polygon '((0,0),(1,1),(2,0))')` →
`(1,0.3333333333333333)`  
`polygon` ( `box` ) → `polygon` Converts box to a 4-point polygon.
`polygon(box '(1,1),(0,0)')` → `((0,0),(0,1),(1,1),(1,0))`  
`polygon` ( `circle` ) → `polygon` Converts circle to a 12-point polygon.
`polygon(circle '<(0,0),2>')` →
`((-2,0),​(-1.7320508075688774,0.9999999999999999),​(-1.0000000000000002,1.7320508075688772),​(-1.2246063538223773e-16,2),​(0.9999999999999996,1.7320508075688774),​(1.732050807568877,1.0000000000000007),​(2,2.4492127076447545e-16),​(1.7320508075688776,-0.9999999999999994),​(1.0000000000000009,-1.7320508075688767),​(3.673819061467132e-16,-2),​(-0.9999999999999987,-1.732050807568878),​(-1.7320508075688767,-1.0000000000000009))`  
`polygon` ( `integer`, `circle` ) → `polygon` Converts circle to an _`n`_
-point polygon. `polygon(4, circle '<(3,0),1>')` →
`((2,0),​(3,1),​(4,1.2246063538223773e-16),​(3,-1))`  
`polygon` ( `path` ) → `polygon` Converts closed path to a polygon with the
same list of points. `polygon(path '((0,0),(1,1),(2,0))')` →
`((0,0),(1,1),(2,0))`  
  
  

It is possible to access the two component numbers of a `point` as though the
point were an array with indexes 0 and 1. For example, if `t.p` is a `point`
column then `SELECT p[0] FROM t` retrieves the X coordinate and `UPDATE t SET
p[1] = ...` changes the Y coordinate. In the same way, a value of type `box`
or `lseg` can be treated as an array of two `point` values.

* * *

[Prev](functions-enum.html "9.10. Enum Support Functions")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](functions-net.html "9.12. Network Address Functions and Operators")  
---|---|---  
9.10. Enum Support Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  9.12. Network Address Functions and Operators  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-geometry.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

