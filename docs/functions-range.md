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

Supported Versions: [Current](/docs/current/functions-range.html "PostgreSQL
17 - 9.20. Range/Multirange Functions and Operators")
([17](/docs/17/functions-range.html "PostgreSQL 17 - 9.20. Range/Multirange
Functions and Operators")) / [16](/docs/16/functions-range.html "PostgreSQL 16
- 9.20. Range/Multirange Functions and Operators") / [15](/docs/15/functions-
range.html "PostgreSQL 15 - 9.20. Range/Multirange Functions and Operators") /
[14](/docs/14/functions-range.html "PostgreSQL 14 - 9.20. Range/Multirange
Functions and Operators") / [13](/docs/13/functions-range.html "PostgreSQL 13
- 9.20. Range/Multirange Functions and Operators")

Development Versions: [18](/docs/18/functions-range.html "PostgreSQL 18 -
9.20. Range/Multirange Functions and Operators") /
[devel](/docs/devel/functions-range.html "PostgreSQL devel -
9.20. Range/Multirange Functions and Operators")

Unsupported versions: [12](/docs/12/functions-range.html "PostgreSQL 12 -
9.20. Range/Multirange Functions and Operators") / [11](/docs/11/functions-
range.html "PostgreSQL 11 - 9.20. Range/Multirange Functions and Operators") /
[10](/docs/10/functions-range.html "PostgreSQL 10 - 9.20. Range/Multirange
Functions and Operators") / [9.6](/docs/9.6/functions-range.html "PostgreSQL
9.6 - 9.20. Range/Multirange Functions and Operators") /
[9.5](/docs/9.5/functions-range.html "PostgreSQL 9.5 - 9.20. Range/Multirange
Functions and Operators") / [9.4](/docs/9.4/functions-range.html "PostgreSQL
9.4 - 9.20. Range/Multirange Functions and Operators") /
[9.3](/docs/9.3/functions-range.html "PostgreSQL 9.3 - 9.20. Range/Multirange
Functions and Operators") / [9.2](/docs/9.2/functions-range.html "PostgreSQL
9.2 - 9.20. Range/Multirange Functions and Operators")

__

9.20. Range/Multirange Functions and Operators  
---  
[Prev](functions-array.html "9.19. Array Functions and Operators")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions-aggregate.html "9.21. Aggregate Functions")  
  
* * *

## 9.20. Range/Multirange Functions and Operators #

See [Section 8.17](rangetypes.html "8.17. Range Types") for an overview of
range types.

[Table 9.55](functions-range.html#RANGE-OPERATORS-TABLE "Table 9.55. Range
Operators") shows the specialized operators available for range types. [Table
9.56](functions-range.html#MULTIRANGE-OPERATORS-TABLE "Table 9.56. Multirange
Operators") shows the specialized operators available for multirange types. In
addition to those, the usual comparison operators shown in [Table
9.1](functions-comparison.html#FUNCTIONS-COMPARISON-OP-TABLE
"Table 9.1. Comparison Operators") are available for range and multirange
types. The comparison operators order first by the range lower bounds, and
only if those are equal do they compare the upper bounds. The multirange
operators compare each range until one is unequal. This does not usually
result in a useful overall ordering, but the operators are provided to allow
unique indexes to be constructed on ranges.

**Table  9.55. Range Operators**

Operator Description Example(s)  
---  
`anyrange` `@>` `anyrange` → `boolean` Does the first range contain the
second? `int4range(2,4) @> int4range(2,3)` → `t`  
`anyrange` `@>` `anyelement` → `boolean` Does the range contain the element?
`'[2011-01-01,2011-03-01)'::tsrange @> '2011-01-10'::timestamp` → `t`  
`anyrange` `<@` `anyrange` → `boolean` Is the first range contained by the
second? `int4range(2,4) <@ int4range(1,7)` → `t`  
`anyelement` `<@` `anyrange` → `boolean` Is the element contained in the
range? `42 <@ int4range(1,7)` → `f`  
`anyrange` `&&` `anyrange` → `boolean` Do the ranges overlap, that is, have
any elements in common? `int8range(3,7) && int8range(4,12)` → `t`  
`anyrange` `<<` `anyrange` → `boolean` Is the first range strictly left of the
second? `int8range(1,10) << int8range(100,110)` → `t`  
`anyrange` `>>` `anyrange` → `boolean` Is the first range strictly right of
the second? `int8range(50,60) >> int8range(20,30)` → `t`  
`anyrange` `&<` `anyrange` → `boolean` Does the first range not extend to the
right of the second? `int8range(1,20) &< int8range(18,20)` → `t`  
`anyrange` `&>` `anyrange` → `boolean` Does the first range not extend to the
left of the second? `int8range(7,20) &> int8range(5,10)` → `t`  
`anyrange` `-|-` `anyrange` → `boolean` Are the ranges adjacent?
`numrange(1.1,2.2) -|- numrange(2.2,3.3)` → `t`  
`anyrange` `+` `anyrange` → `anyrange` Computes the union of the ranges. The
ranges must overlap or be adjacent, so that the union is a single range (but
see `range_merge()`). `numrange(5,15) + numrange(10,20)` → `[5,20)`  
`anyrange` `*` `anyrange` → `anyrange` Computes the intersection of the
ranges. `int8range(5,15) * int8range(10,20)` → `[10,15)`  
`anyrange` `-` `anyrange` → `anyrange` Computes the difference of the ranges.
The second range must not be contained in the first in such a way that the
difference would not be a single range. `int8range(5,15) - int8range(10,20)` →
`[5,10)`  
  
  

**Table  9.56. Multirange Operators**

Operator Description Example(s)  
---  
`anymultirange` `@>` `anymultirange` → `boolean` Does the first multirange
contain the second? `'{[2,4)}'::int4multirange @> '{[2,3)}'::int4multirange` →
`t`  
`anymultirange` `@>` `anyrange` → `boolean` Does the multirange contain the
range? `'{[2,4)}'::int4multirange @> int4range(2,3)` → `t`  
`anymultirange` `@>` `anyelement` → `boolean` Does the multirange contain the
element? `'{[2011-01-01,2011-03-01)}'::tsmultirange @>
'2011-01-10'::timestamp` → `t`  
`anyrange` `@>` `anymultirange` → `boolean` Does the range contain the
multirange? `'[2,4)'::int4range @> '{[2,3)}'::int4multirange` → `t`  
`anymultirange` `<@` `anymultirange` → `boolean` Is the first multirange
contained by the second? `'{[2,4)}'::int4multirange <@
'{[1,7)}'::int4multirange` → `t`  
`anymultirange` `<@` `anyrange` → `boolean` Is the multirange contained by the
range? `'{[2,4)}'::int4multirange <@ int4range(1,7)` → `t`  
`anyrange` `<@` `anymultirange` → `boolean` Is the range contained by the
multirange? `int4range(2,4) <@ '{[1,7)}'::int4multirange` → `t`  
`anyelement` `<@` `anymultirange` → `boolean` Is the element contained by the
multirange? `4 <@ '{[1,7)}'::int4multirange` → `t`  
`anymultirange` `&&` `anymultirange` → `boolean` Do the multiranges overlap,
that is, have any elements in common? `'{[3,7)}'::int8multirange &&
'{[4,12)}'::int8multirange` → `t`  
`anymultirange` `&&` `anyrange` → `boolean` Does the multirange overlap the
range? `'{[3,7)}'::int8multirange && int8range(4,12)` → `t`  
`anyrange` `&&` `anymultirange` → `boolean` Does the range overlap the
multirange? `int8range(3,7) && '{[4,12)}'::int8multirange` → `t`  
`anymultirange` `<<` `anymultirange` → `boolean` Is the first multirange
strictly left of the second? `'{[1,10)}'::int8multirange <<
'{[100,110)}'::int8multirange` → `t`  
`anymultirange` `<<` `anyrange` → `boolean` Is the multirange strictly left of
the range? `'{[1,10)}'::int8multirange << int8range(100,110)` → `t`  
`anyrange` `<<` `anymultirange` → `boolean` Is the range strictly left of the
multirange? `int8range(1,10) << '{[100,110)}'::int8multirange` → `t`  
`anymultirange` `>>` `anymultirange` → `boolean` Is the first multirange
strictly right of the second? `'{[50,60)}'::int8multirange >>
'{[20,30)}'::int8multirange` → `t`  
`anymultirange` `>>` `anyrange` → `boolean` Is the multirange strictly right
of the range? `'{[50,60)}'::int8multirange >> int8range(20,30)` → `t`  
`anyrange` `>>` `anymultirange` → `boolean` Is the range strictly right of the
multirange? `int8range(50,60) >> '{[20,30)}'::int8multirange` → `t`  
`anymultirange` `&<` `anymultirange` → `boolean` Does the first multirange not
extend to the right of the second? `'{[1,20)}'::int8multirange &<
'{[18,20)}'::int8multirange` → `t`  
`anymultirange` `&<` `anyrange` → `boolean` Does the multirange not extend to
the right of the range? `'{[1,20)}'::int8multirange &< int8range(18,20)` → `t`  
`anyrange` `&<` `anymultirange` → `boolean` Does the range not extend to the
right of the multirange? `int8range(1,20) &< '{[18,20)}'::int8multirange` →
`t`  
`anymultirange` `&>` `anymultirange` → `boolean` Does the first multirange not
extend to the left of the second? `'{[7,20)}'::int8multirange &>
'{[5,10)}'::int8multirange` → `t`  
`anymultirange` `&>` `anyrange` → `boolean` Does the multirange not extend to
the left of the range? `'{[7,20)}'::int8multirange &> int8range(5,10)` → `t`  
`anyrange` `&>` `anymultirange` → `boolean` Does the range not extend to the
left of the multirange? `int8range(7,20) &> '{[5,10)}'::int8multirange` → `t`  
`anymultirange` `-|-` `anymultirange` → `boolean` Are the multiranges
adjacent? `'{[1.1,2.2)}'::nummultirange -|- '{[2.2,3.3)}'::nummultirange` →
`t`  
`anymultirange` `-|-` `anyrange` → `boolean` Is the multirange adjacent to the
range? `'{[1.1,2.2)}'::nummultirange -|- numrange(2.2,3.3)` → `t`  
`anyrange` `-|-` `anymultirange` → `boolean` Is the range adjacent to the
multirange? `numrange(1.1,2.2) -|- '{[2.2,3.3)}'::nummultirange` → `t`  
`anymultirange` `+` `anymultirange` → `anymultirange` Computes the union of
the multiranges. The multiranges need not overlap or be adjacent.
`'{[5,10)}'::nummultirange + '{[15,20)}'::nummultirange` → `{[5,10), [15,20)}`  
`anymultirange` `*` `anymultirange` → `anymultirange` Computes the
intersection of the multiranges. `'{[5,15)}'::int8multirange *
'{[10,20)}'::int8multirange` → `{[10,15)}`  
`anymultirange` `-` `anymultirange` → `anymultirange` Computes the difference
of the multiranges. `'{[5,20)}'::int8multirange - '{[10,15)}'::int8multirange`
→ `{[5,10), [15,20)}`  
  
  

The left-of/right-of/adjacent operators always return false when an empty
range or multirange is involved; that is, an empty range is not considered to
be either before or after any other range.

Elsewhere empty ranges and multiranges are treated as the additive identity:
anything unioned with an empty value is itself. Anything minus an empty value
is itself. An empty multirange has exactly the same points as an empty range.
Every range contains the empty range. Every multirange contains as many empty
ranges as you like.

The range union and difference operators will fail if the resulting range
would need to contain two disjoint sub-ranges, as such a range cannot be
represented. There are separate operators for union and difference that take
multirange parameters and return a multirange, and they do not fail even if
their arguments are disjoint. So if you need a union or difference operation
for ranges that may be disjoint, you can avoid errors by first casting your
ranges to multiranges.

[Table 9.57](functions-range.html#RANGE-FUNCTIONS-TABLE "Table 9.57. Range
Functions") shows the functions available for use with range types. [Table
9.58](functions-range.html#MULTIRANGE-FUNCTIONS-TABLE "Table 9.58. Multirange
Functions") shows the functions available for use with multirange types.

**Table  9.57. Range Functions**

Function Description Example(s)  
---  
`lower` ( `anyrange` ) → `anyelement` Extracts the lower bound of the range
(`NULL` if the range is empty or has no lower bound).
`lower(numrange(1.1,2.2))` → `1.1`  
`upper` ( `anyrange` ) → `anyelement` Extracts the upper bound of the range
(`NULL` if the range is empty or has no upper bound).
`upper(numrange(1.1,2.2))` → `2.2`  
`isempty` ( `anyrange` ) → `boolean` Is the range empty?
`isempty(numrange(1.1,2.2))` → `f`  
`lower_inc` ( `anyrange` ) → `boolean` Is the range's lower bound inclusive?
`lower_inc(numrange(1.1,2.2))` → `t`  
`upper_inc` ( `anyrange` ) → `boolean` Is the range's upper bound inclusive?
`upper_inc(numrange(1.1,2.2))` → `f`  
`lower_inf` ( `anyrange` ) → `boolean` Does the range have no lower bound? (A
lower bound of `-Infinity` returns false.) `lower_inf('(,)'::daterange)` → `t`  
`upper_inf` ( `anyrange` ) → `boolean` Does the range have no upper bound? (An
upper bound of `Infinity` returns false.) `upper_inf('(,)'::daterange)` → `t`  
`range_merge` ( `anyrange`, `anyrange` ) → `anyrange` Computes the smallest
range that includes both of the given ranges. `range_merge('[1,2)'::int4range,
'[3,4)'::int4range)` → `[1,4)`  
  
  

**Table  9.58. Multirange Functions**

Function Description Example(s)  
---  
`lower` ( `anymultirange` ) → `anyelement` Extracts the lower bound of the
multirange (`NULL` if the multirange is empty has no lower bound).
`lower('{[1.1,2.2)}'::nummultirange)` → `1.1`  
`upper` ( `anymultirange` ) → `anyelement` Extracts the upper bound of the
multirange (`NULL` if the multirange is empty or has no upper bound).
`upper('{[1.1,2.2)}'::nummultirange)` → `2.2`  
`isempty` ( `anymultirange` ) → `boolean` Is the multirange empty?
`isempty('{[1.1,2.2)}'::nummultirange)` → `f`  
`lower_inc` ( `anymultirange` ) → `boolean` Is the multirange's lower bound
inclusive? `lower_inc('{[1.1,2.2)}'::nummultirange)` → `t`  
`upper_inc` ( `anymultirange` ) → `boolean` Is the multirange's upper bound
inclusive? `upper_inc('{[1.1,2.2)}'::nummultirange)` → `f`  
`lower_inf` ( `anymultirange` ) → `boolean` Does the multirange have no lower
bound? (A lower bound of `-Infinity` returns false.)
`lower_inf('{(,)}'::datemultirange)` → `t`  
`upper_inf` ( `anymultirange` ) → `boolean` Does the multirange have no upper
bound? (An upper bound of `Infinity` returns false.)
`upper_inf('{(,)}'::datemultirange)` → `t`  
`range_merge` ( `anymultirange` ) → `anyrange` Computes the smallest range
that includes the entire multirange. `range_merge('{[1,2),
[3,4)}'::int4multirange)` → `[1,4)`  
`multirange` ( `anyrange` ) → `anymultirange` Returns a multirange containing
just the given range. `multirange('[1,2)'::int4range)` → `{[1,2)}`  
`unnest` ( `anymultirange` ) → `setof anyrange` Expands a multirange into a
set of ranges. The ranges are read out in storage order (ascending).
`unnest('{[1,2), [3,4)}'::int4multirange)` →

    
    
     [1,2)
     [3,4)
      
  
  

The `lower_inc`, `upper_inc`, `lower_inf`, and `upper_inf` functions all
return false for an empty range or multirange.

* * *

[Prev](functions-array.html "9.19. Array Functions and Operators")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](functions-aggregate.html "9.21. Aggregate Functions")  
---|---|---  
9.19. Array Functions and Operators  | [Home](index.html "PostgreSQL 16.9 Documentation") |  9.21. Aggregate Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-range.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

