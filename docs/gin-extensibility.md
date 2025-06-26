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

Supported Versions: [16](/docs/16/gin-extensibility.html "PostgreSQL 16 -
70.3. Extensibility") / [15](/docs/15/gin-extensibility.html "PostgreSQL 15 -
70.3. Extensibility") / [14](/docs/14/gin-extensibility.html "PostgreSQL 14 -
70.3. Extensibility") / [13](/docs/13/gin-extensibility.html "PostgreSQL 13 -
70.3. Extensibility")

Unsupported versions: [12](/docs/12/gin-extensibility.html "PostgreSQL 12 -
70.3. Extensibility") / [11](/docs/11/gin-extensibility.html "PostgreSQL 11 -
70.3. Extensibility") / [10](/docs/10/gin-extensibility.html "PostgreSQL 10 -
70.3. Extensibility") / [9.6](/docs/9.6/gin-extensibility.html "PostgreSQL 9.6
- 70.3. Extensibility") / [9.5](/docs/9.5/gin-extensibility.html "PostgreSQL
9.5 - 70.3. Extensibility") / [9.4](/docs/9.4/gin-extensibility.html
"PostgreSQL 9.4 - 70.3. Extensibility") / [9.3](/docs/9.3/gin-
extensibility.html "PostgreSQL 9.3 - 70.3. Extensibility") /
[9.2](/docs/9.2/gin-extensibility.html "PostgreSQL 9.2 - 70.3. Extensibility")
/ [9.1](/docs/9.1/gin-extensibility.html "PostgreSQL 9.1 -
70.3. Extensibility") / [9.0](/docs/9.0/gin-extensibility.html "PostgreSQL 9.0
- 70.3. Extensibility") / [8.4](/docs/8.4/gin-extensibility.html "PostgreSQL
8.4 - 70.3. Extensibility") / [8.3](/docs/8.3/gin-extensibility.html
"PostgreSQL 8.3 - 70.3. Extensibility") / [8.2](/docs/8.2/gin-
extensibility.html "PostgreSQL 8.2 - 70.3. Extensibility")

__

70.3. Extensibility  
---  
[Prev](gin-builtin-opclasses.html "70.2. Built-in Operator Classes")  | [Up](gin.html "Chapter 70. GIN Indexes") | Chapter 70. GIN Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](gin-implementation.html "70.4. Implementation")  
  
* * *

## 70.3. Extensibility #

The GIN interface has a high level of abstraction, requiring the access method
implementer only to implement the semantics of the data type being accessed.
The GIN layer itself takes care of concurrency, logging and searching the tree
structure.

All it takes to get a GIN access method working is to implement a few user-
defined methods, which define the behavior of keys in the tree and the
relationships between keys, indexed items, and indexable queries. In short,
GIN combines extensibility with generality, code reuse, and a clean interface.

There are two methods that an operator class for GIN must provide:

`Datum *extractValue(Datum itemValue, int32 *nkeys, bool **nullFlags)`

    

Returns a palloc'd array of keys given an item to be indexed. The number of
returned keys must be stored into `*nkeys`. If any of the keys can be null,
also palloc an array of `*nkeys` `bool` fields, store its address at
`*nullFlags`, and set these null flags as needed. `*nullFlags` can be left
`NULL` (its initial value) if all keys are non-null. The return value can be
`NULL` if the item contains no keys.

`Datum *extractQuery(Datum query, int32 *nkeys, StrategyNumber n, bool
**pmatch, Pointer **extra_data, bool **nullFlags, int32 *searchMode)`

    

Returns a palloc'd array of keys given a value to be queried; that is, `query`
is the value on the right-hand side of an indexable operator whose left-hand
side is the indexed column. `n` is the strategy number of the operator within
the operator class (see [Section 38.16.2](xindex.html#XINDEX-STRATEGIES
"38.16.2. Index Method Strategies")). Often, `extractQuery` will need to
consult `n` to determine the data type of `query` and the method it should use
to extract key values. The number of returned keys must be stored into
`*nkeys`. If any of the keys can be null, also palloc an array of `*nkeys`
`bool` fields, store its address at `*nullFlags`, and set these null flags as
needed. `*nullFlags` can be left `NULL` (its initial value) if all keys are
non-null. The return value can be `NULL` if the `query` contains no keys.

`searchMode` is an output argument that allows `extractQuery` to specify
details about how the search will be done. If `*searchMode` is set to
`GIN_SEARCH_MODE_DEFAULT` (which is the value it is initialized to before
call), only items that match at least one of the returned keys are considered
candidate matches. If `*searchMode` is set to `GIN_SEARCH_MODE_INCLUDE_EMPTY`,
then in addition to items containing at least one matching key, items that
contain no keys at all are considered candidate matches. (This mode is useful
for implementing is-subset-of operators, for example.) If `*searchMode` is set
to `GIN_SEARCH_MODE_ALL`, then all non-null items in the index are considered
candidate matches, whether they match any of the returned keys or not. (This
mode is much slower than the other two choices, since it requires scanning
essentially the entire index, but it may be necessary to implement corner
cases correctly. An operator that needs this mode in most cases is probably
not a good candidate for a GIN operator class.) The symbols to use for setting
this mode are defined in `access/gin.h`.

`pmatch` is an output argument for use when partial match is supported. To use
it, `extractQuery` must allocate an array of `*nkeys` `bool`s and store its
address at `*pmatch`. Each element of the array should be set to true if the
corresponding key requires partial match, false if not. If `*pmatch` is set to
`NULL` then GIN assumes partial match is not required. The variable is
initialized to `NULL` before call, so this argument can simply be ignored by
operator classes that do not support partial match.

`extra_data` is an output argument that allows `extractQuery` to pass
additional data to the `consistent` and `comparePartial` methods. To use it,
`extractQuery` must allocate an array of `*nkeys` pointers and store its
address at `*extra_data`, then store whatever it wants to into the individual
pointers. The variable is initialized to `NULL` before call, so this argument
can simply be ignored by operator classes that do not require extra data. If
`*extra_data` is set, the whole array is passed to the `consistent` method,
and the appropriate element to the `comparePartial` method.

An operator class must also provide a function to check if an indexed item
matches the query. It comes in two flavors, a Boolean `consistent` function,
and a ternary `triConsistent` function. `triConsistent` covers the
functionality of both, so providing `triConsistent` alone is sufficient.
However, if the Boolean variant is significantly cheaper to calculate, it can
be advantageous to provide both. If only the Boolean variant is provided, some
optimizations that depend on refuting index items before fetching all the keys
are disabled.

`bool consistent(bool check[], StrategyNumber n, Datum query, int32 nkeys,
Pointer extra_data[], bool *recheck, Datum queryKeys[], bool nullFlags[])`

    

Returns true if an indexed item satisfies the query operator with strategy
number `n` (or might satisfy it, if the recheck indication is returned). This
function does not have direct access to the indexed item's value, since GIN
does not store items explicitly. Rather, what is available is knowledge about
which key values extracted from the query appear in a given indexed item. The
`check` array has length `nkeys`, which is the same as the number of keys
previously returned by `extractQuery` for this `query` datum. Each element of
the `check` array is true if the indexed item contains the corresponding query
key, i.e., if (check[i] == true) the i-th key of the `extractQuery` result
array is present in the indexed item. The original `query` datum is passed in
case the `consistent` method needs to consult it, and so are the `queryKeys[]`
and `nullFlags[]` arrays previously returned by `extractQuery`. `extra_data`
is the extra-data array returned by `extractQuery`, or `NULL` if none.

When `extractQuery` returns a null key in `queryKeys[]`, the corresponding
`check[]` element is true if the indexed item contains a null key; that is,
the semantics of `check[]` are like `IS NOT DISTINCT FROM`. The `consistent`
function can examine the corresponding `nullFlags[]` element if it needs to
tell the difference between a regular value match and a null match.

On success, `*recheck` should be set to true if the heap tuple needs to be
rechecked against the query operator, or false if the index test is exact.
That is, a false return value guarantees that the heap tuple does not match
the query; a true return value with `*recheck` set to false guarantees that
the heap tuple does match the query; and a true return value with `*recheck`
set to true means that the heap tuple might match the query, so it needs to be
fetched and rechecked by evaluating the query operator directly against the
originally indexed item.

`GinTernaryValue triConsistent(GinTernaryValue check[], StrategyNumber n,
Datum query, int32 nkeys, Pointer extra_data[], Datum queryKeys[], bool
nullFlags[])`

    

`triConsistent` is similar to `consistent`, but instead of Booleans in the
`check` vector, there are three possible values for each key: `GIN_TRUE`,
`GIN_FALSE` and `GIN_MAYBE`. `GIN_FALSE` and `GIN_TRUE` have the same meaning
as regular Boolean values, while `GIN_MAYBE` means that the presence of that
key is not known. When `GIN_MAYBE` values are present, the function should
only return `GIN_TRUE` if the item certainly matches whether or not the index
item contains the corresponding query keys. Likewise, the function must return
`GIN_FALSE` only if the item certainly does not match, whether or not it
contains the `GIN_MAYBE` keys. If the result depends on the `GIN_MAYBE`
entries, i.e., the match cannot be confirmed or refuted based on the known
query keys, the function must return `GIN_MAYBE`.

When there are no `GIN_MAYBE` values in the `check` vector, a `GIN_MAYBE`
return value is the equivalent of setting the `recheck` flag in the Boolean
`consistent` function.

In addition, GIN must have a way to sort the key values stored in the index.
The operator class can define the sort ordering by specifying a comparison
method:

`int compare(Datum a, Datum b)`

    

Compares two keys (not indexed items!) and returns an integer less than zero,
zero, or greater than zero, indicating whether the first key is less than,
equal to, or greater than the second. Null keys are never passed to this
function.

Alternatively, if the operator class does not provide a `compare` method, GIN
will look up the default btree operator class for the index key data type, and
use its comparison function. It is recommended to specify the comparison
function in a GIN operator class that is meant for just one data type, as
looking up the btree operator class costs a few cycles. However, polymorphic
GIN operator classes (such as `array_ops`) typically cannot specify a single
comparison function.

An operator class for GIN can optionally supply the following methods:

`int comparePartial(Datum partial_key, Datum key, StrategyNumber n, Pointer
extra_data)`

    

Compare a partial-match query key to an index key. Returns an integer whose
sign indicates the result: less than zero means the index key does not match
the query, but the index scan should continue; zero means that the index key
does match the query; greater than zero indicates that the index scan should
stop because no more matches are possible. The strategy number `n` of the
operator that generated the partial match query is provided, in case its
semantics are needed to determine when to end the scan. Also, `extra_data` is
the corresponding element of the extra-data array made by `extractQuery`, or
`NULL` if none. Null keys are never passed to this function.

`void options(local_relopts *relopts)`

    

Defines a set of user-visible parameters that control operator class behavior.

The `options` function is passed a pointer to a `local_relopts` struct, which
needs to be filled with a set of operator class specific options. The options
can be accessed from other support functions using the
`PG_HAS_OPCLASS_OPTIONS()` and `PG_GET_OPCLASS_OPTIONS()` macros.

Since both key extraction of indexed values and representation of the key in
GIN are flexible, they may depend on user-specified parameters.

To support “partial match” queries, an operator class must provide the
`comparePartial` method, and its `extractQuery` method must set the `pmatch`
parameter when a partial-match query is encountered. See [Section 70.4.2](gin-
implementation.html#GIN-PARTIAL-MATCH "70.4.2. Partial Match Algorithm") for
details.

The actual data types of the various `Datum` values mentioned above vary
depending on the operator class. The item values passed to `extractValue` are
always of the operator class's input type, and all key values must be of the
class's `STORAGE` type. The type of the `query` argument passed to
`extractQuery`, `consistent` and `triConsistent` is whatever is the right-hand
input type of the class member operator identified by the strategy number.
This need not be the same as the indexed type, so long as key values of the
correct type can be extracted from it. However, it is recommended that the SQL
declarations of these three support functions use the opclass's indexed data
type for the `query` argument, even though the actual type might be something
else depending on the operator.

* * *

[Prev](gin-builtin-opclasses.html "70.2. Built-in Operator Classes")  | [Up](gin.html "Chapter 70. GIN Indexes") |  [Next](gin-implementation.html "70.4. Implementation")  
---|---|---  
70.2. Built-in Operator Classes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  70.4. Implementation  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/gin-extensibility.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

