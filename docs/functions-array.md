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

Supported Versions: [Current](/docs/current/functions-array.html "PostgreSQL
17 - 9.19. Array Functions and Operators") ([17](/docs/17/functions-array.html
"PostgreSQL 17 - 9.19. Array Functions and Operators")) /
[16](/docs/16/functions-array.html "PostgreSQL 16 - 9.19. Array Functions and
Operators") / [15](/docs/15/functions-array.html "PostgreSQL 15 - 9.19. Array
Functions and Operators") / [14](/docs/14/functions-array.html "PostgreSQL 14
- 9.19. Array Functions and Operators") / [13](/docs/13/functions-array.html
"PostgreSQL 13 - 9.19. Array Functions and Operators")

Development Versions: [18](/docs/18/functions-array.html "PostgreSQL 18 -
9.19. Array Functions and Operators") / [devel](/docs/devel/functions-
array.html "PostgreSQL devel - 9.19. Array Functions and Operators")

Unsupported versions: [12](/docs/12/functions-array.html "PostgreSQL 12 -
9.19. Array Functions and Operators") / [11](/docs/11/functions-array.html
"PostgreSQL 11 - 9.19. Array Functions and Operators") /
[10](/docs/10/functions-array.html "PostgreSQL 10 - 9.19. Array Functions and
Operators") / [9.6](/docs/9.6/functions-array.html "PostgreSQL 9.6 -
9.19. Array Functions and Operators") / [9.5](/docs/9.5/functions-array.html
"PostgreSQL 9.5 - 9.19. Array Functions and Operators") /
[9.4](/docs/9.4/functions-array.html "PostgreSQL 9.4 - 9.19. Array Functions
and Operators") / [9.3](/docs/9.3/functions-array.html "PostgreSQL 9.3 -
9.19. Array Functions and Operators") / [9.2](/docs/9.2/functions-array.html
"PostgreSQL 9.2 - 9.19. Array Functions and Operators") /
[9.1](/docs/9.1/functions-array.html "PostgreSQL 9.1 - 9.19. Array Functions
and Operators") / [9.0](/docs/9.0/functions-array.html "PostgreSQL 9.0 -
9.19. Array Functions and Operators") / [8.4](/docs/8.4/functions-array.html
"PostgreSQL 8.4 - 9.19. Array Functions and Operators") /
[8.3](/docs/8.3/functions-array.html "PostgreSQL 8.3 - 9.19. Array Functions
and Operators") / [8.2](/docs/8.2/functions-array.html "PostgreSQL 8.2 -
9.19. Array Functions and Operators") / [8.1](/docs/8.1/functions-array.html
"PostgreSQL 8.1 - 9.19. Array Functions and Operators") /
[8.0](/docs/8.0/functions-array.html "PostgreSQL 8.0 - 9.19. Array Functions
and Operators") / [7.4](/docs/7.4/functions-array.html "PostgreSQL 7.4 -
9.19. Array Functions and Operators")

__

9.19. Array Functions and Operators  
---  
[Prev](functions-conditional.html "9.18. Conditional Expressions")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions-range.html "9.20. Range/Multirange Functions and Operators")  
  
* * *

## 9.19. Array Functions and Operators #

[Table 9.53](functions-array.html#ARRAY-OPERATORS-TABLE "Table 9.53. Array
Operators") shows the specialized operators available for array types. In
addition to those, the usual comparison operators shown in [Table
9.1](functions-comparison.html#FUNCTIONS-COMPARISON-OP-TABLE
"Table 9.1. Comparison Operators") are available for arrays. The comparison
operators compare the array contents element-by-element, using the default
B-tree comparison function for the element data type, and sort based on the
first difference. In multidimensional arrays the elements are visited in row-
major order (last subscript varies most rapidly). If the contents of two
arrays are equal but the dimensionality is different, the first difference in
the dimensionality information determines the sort order.

**Table  9.53. Array Operators**

Operator Description Example(s)  
---  
`anyarray` `@>` `anyarray` → `boolean` Does the first array contain the
second, that is, does each element appearing in the second array equal some
element of the first array? (Duplicates are not treated specially, thus
`ARRAY[1]` and `ARRAY[1,1]` are each considered to contain the other.)
`ARRAY[1,4,3] @> ARRAY[3,1,3]` → `t`  
`anyarray` `<@` `anyarray` → `boolean` Is the first array contained by the
second? `ARRAY[2,2,7] <@ ARRAY[1,7,4,2,6]` → `t`  
`anyarray` `&&` `anyarray` → `boolean` Do the arrays overlap, that is, have
any elements in common? `ARRAY[1,4,3] && ARRAY[2,1]` → `t`  
`anycompatiblearray` `||` `anycompatiblearray` → `anycompatiblearray`
Concatenates the two arrays. Concatenating a null or empty array is a no-op;
otherwise the arrays must have the same number of dimensions (as illustrated
by the first example) or differ in number of dimensions by one (as illustrated
by the second). If the arrays are not of identical element types, they will be
coerced to a common type (see [Section 10.5](typeconv-union-case.html
"10.5. UNION, CASE, and Related Constructs")). `ARRAY[1,2,3] ||
ARRAY[4,5,6,7]` → `{1,2,3,4,5,6,7}` `ARRAY[1,2,3] || ARRAY[[4,5,6],[7,8,9.9]]`
→ `{{1,2,3},{4,5,6},{7,8,9.9}}`  
`anycompatible` `||` `anycompatiblearray` → `anycompatiblearray` Concatenates
an element onto the front of an array (which must be empty or one-
dimensional). `3 || ARRAY[4,5,6]` → `{3,4,5,6}`  
`anycompatiblearray` `||` `anycompatible` → `anycompatiblearray` Concatenates
an element onto the end of an array (which must be empty or one-dimensional).
`ARRAY[4,5,6] || 7` → `{4,5,6,7}`  
  
  

See [Section 8.15](arrays.html "8.15. Arrays") for more details about array
operator behavior. See [Section 11.2](indexes-types.html "11.2. Index Types")
for more details about which operators support indexed operations.

[Table 9.54](functions-array.html#ARRAY-FUNCTIONS-TABLE "Table 9.54. Array
Functions") shows the functions available for use with array types. See
[Section 8.15](arrays.html "8.15. Arrays") for more information and examples
of the use of these functions.

**Table  9.54. Array Functions**

Function Description Example(s)  
---  
`array_append` ( `anycompatiblearray`, `anycompatible` ) →
`anycompatiblearray` Appends an element to the end of an array (same as the
`anycompatiblearray` `||` `anycompatible` operator). `array_append(ARRAY[1,2],
3)` → `{1,2,3}`  
`array_cat` ( `anycompatiblearray`, `anycompatiblearray` ) →
`anycompatiblearray` Concatenates two arrays (same as the `anycompatiblearray`
`||` `anycompatiblearray` operator). `array_cat(ARRAY[1,2,3], ARRAY[4,5])` →
`{1,2,3,4,5}`  
`array_dims` ( `anyarray` ) → `text` Returns a text representation of the
array's dimensions. `array_dims(ARRAY[[1,2,3], [4,5,6]])` → `[1:2][1:3]`  
`array_fill` ( `anyelement`, `integer[]` [, `integer[]` ] ) → `anyarray`
Returns an array filled with copies of the given value, having dimensions of
the lengths specified by the second argument. The optional third argument
supplies lower-bound values for each dimension (which default to all `1`).
`array_fill(11, ARRAY[2,3])` → `{{11,11,11},{11,11,11}}` `array_fill(7,
ARRAY[3], ARRAY[2])` → `[2:4]={7,7,7}`  
`array_length` ( `anyarray`, `integer` ) → `integer` Returns the length of the
requested array dimension. (Produces NULL instead of 0 for empty or missing
array dimensions.) `array_length(array[1,2,3], 1)` → `3`
`array_length(array[]::int[], 1)` → `NULL` `array_length(array['text'], 2)` →
`NULL`  
`array_lower` ( `anyarray`, `integer` ) → `integer` Returns the lower bound of
the requested array dimension. `array_lower('[0:2]={1,2,3}'::integer[], 1)` →
`0`  
`array_ndims` ( `anyarray` ) → `integer` Returns the number of dimensions of
the array. `array_ndims(ARRAY[[1,2,3], [4,5,6]])` → `2`  
`array_position` ( `anycompatiblearray`, `anycompatible` [, `integer` ] ) →
`integer` Returns the subscript of the first occurrence of the second argument
in the array, or `NULL` if it's not present. If the third argument is given,
the search begins at that subscript. The array must be one-dimensional.
Comparisons are done using `IS NOT DISTINCT FROM` semantics, so it is possible
to search for `NULL`. `array_position(ARRAY['sun', 'mon', 'tue', 'wed', 'thu',
'fri', 'sat'], 'mon')` → `2`  
`array_positions` ( `anycompatiblearray`, `anycompatible` ) → `integer[]`
Returns an array of the subscripts of all occurrences of the second argument
in the array given as first argument. The array must be one-dimensional.
Comparisons are done using `IS NOT DISTINCT FROM` semantics, so it is possible
to search for `NULL`. `NULL` is returned only if the array is `NULL`; if the
value is not found in the array, an empty array is returned.
`array_positions(ARRAY['A','A','B','A'], 'A')` → `{1,2,4}`  
`array_prepend` ( `anycompatible`, `anycompatiblearray` ) →
`anycompatiblearray` Prepends an element to the beginning of an array (same as
the `anycompatible` `||` `anycompatiblearray` operator). `array_prepend(1,
ARRAY[2,3])` → `{1,2,3}`  
`array_remove` ( `anycompatiblearray`, `anycompatible` ) →
`anycompatiblearray` Removes all elements equal to the given value from the
array. The array must be one-dimensional. Comparisons are done using `IS NOT
DISTINCT FROM` semantics, so it is possible to remove `NULL`s.
`array_remove(ARRAY[1,2,3,2], 2)` → `{1,3}`  
`array_replace` ( `anycompatiblearray`, `anycompatible`, `anycompatible` ) →
`anycompatiblearray` Replaces each array element equal to the second argument
with the third argument. `array_replace(ARRAY[1,2,5,4], 5, 3)` → `{1,2,3,4}`  
`array_sample` ( _`array`_ `anyarray`, _`n`_ `integer` ) → `anyarray` Returns
an array of _`n`_ items randomly selected from _`array`_. _`n`_ may not exceed
the length of _`array`_ 's first dimension. If _`array`_ is multi-dimensional,
an “item” is a slice having a given first subscript.
`array_sample(ARRAY[1,2,3,4,5,6], 3)` → `{2,6,1}`
`array_sample(ARRAY[[1,2],[3,4],[5,6]], 2)` → `{{5,6},{1,2}}`  
`array_shuffle` ( `anyarray` ) → `anyarray` Randomly shuffles the first
dimension of the array. `array_shuffle(ARRAY[[1,2],[3,4],[5,6]])` →
`{{5,6},{1,2},{3,4}}`  
`array_to_string` ( _`array`_ `anyarray`, _`delimiter`_ `text` [,
_`null_string`_ `text` ] ) → `text` Converts each array element to its text
representation, and concatenates those separated by the _`delimiter`_ string.
If _`null_string`_ is given and is not `NULL`, then `NULL` array entries are
represented by that string; otherwise, they are omitted. See also
[`string_to_array`](functions-string.html#FUNCTION-STRING-TO-ARRAY).
`array_to_string(ARRAY[1, 2, 3, NULL, 5], ',', '*')` → `1,2,3,*,5`  
`array_upper` ( `anyarray`, `integer` ) → `integer` Returns the upper bound of
the requested array dimension. `array_upper(ARRAY[1,8,3,7], 1)` → `4`  
`cardinality` ( `anyarray` ) → `integer` Returns the total number of elements
in the array, or 0 if the array is empty. `cardinality(ARRAY[[1,2],[3,4]])` →
`4`  
`trim_array` ( _`array`_ `anyarray`, _`n`_ `integer` ) → `anyarray` Trims an
array by removing the last _`n`_ elements. If the array is multidimensional,
only the first dimension is trimmed. `trim_array(ARRAY[1,2,3,4,5,6], 2)` →
`{1,2,3,4}`  
`unnest` ( `anyarray` ) → `setof anyelement` Expands an array into a set of
rows. The array's elements are read out in storage order. `unnest(ARRAY[1,2])`
→

    
    
     1
     2
    

`unnest(ARRAY[['foo','bar'],['baz','quux']])` →

    
    
     foo
     bar
     baz
     quux
      
  
`unnest` ( `anyarray`, `anyarray` [, ... ] ) → `setof anyelement, anyelement
[, ... ]` Expands multiple arrays (possibly of different data types) into a
set of rows. If the arrays are not all the same length then the shorter ones
are padded with `NULL`s. This form is only allowed in a query's FROM clause;
see [Section 7.2.1.4](queries-table-expressions.html#QUERIES-TABLEFUNCTIONS
"7.2.1.4. Table Functions"). `select * from unnest(ARRAY[1,2],
ARRAY['foo','bar','baz']) as x(a,b)` →

    
    
     a |  b
    ---+-----
     1 | foo
     2 | bar
       | baz
      
  
  

See also [Section 9.21](functions-aggregate.html "9.21. Aggregate Functions")
about the aggregate function `array_agg` for use with arrays.

* * *

[Prev](functions-conditional.html "9.18. Conditional Expressions")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](functions-range.html "9.20. Range/Multirange Functions and Operators")  
---|---|---  
9.18. Conditional Expressions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  9.20. Range/Multirange Functions and Operators  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-array.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

