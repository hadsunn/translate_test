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

Supported Versions: [Current](/docs/current/functions-json.html "PostgreSQL 17
- 9.16. JSON Functions and Operators") ([17](/docs/17/functions-json.html
"PostgreSQL 17 - 9.16. JSON Functions and Operators")) /
[16](/docs/16/functions-json.html "PostgreSQL 16 - 9.16. JSON Functions and
Operators") / [15](/docs/15/functions-json.html "PostgreSQL 15 - 9.16. JSON
Functions and Operators") / [14](/docs/14/functions-json.html "PostgreSQL 14 -
9.16. JSON Functions and Operators") / [13](/docs/13/functions-json.html
"PostgreSQL 13 - 9.16. JSON Functions and Operators")

Development Versions: [18](/docs/18/functions-json.html "PostgreSQL 18 -
9.16. JSON Functions and Operators") / [devel](/docs/devel/functions-json.html
"PostgreSQL devel - 9.16. JSON Functions and Operators")

Unsupported versions: [12](/docs/12/functions-json.html "PostgreSQL 12 -
9.16. JSON Functions and Operators") / [11](/docs/11/functions-json.html
"PostgreSQL 11 - 9.16. JSON Functions and Operators") /
[10](/docs/10/functions-json.html "PostgreSQL 10 - 9.16. JSON Functions and
Operators") / [9.6](/docs/9.6/functions-json.html "PostgreSQL 9.6 - 9.16. JSON
Functions and Operators") / [9.5](/docs/9.5/functions-json.html "PostgreSQL
9.5 - 9.16. JSON Functions and Operators") / [9.4](/docs/9.4/functions-
json.html "PostgreSQL 9.4 - 9.16. JSON Functions and Operators") /
[9.3](/docs/9.3/functions-json.html "PostgreSQL 9.3 - 9.16. JSON Functions and
Operators") / [9.2](/docs/9.2/functions-json.html "PostgreSQL 9.2 - 9.16. JSON
Functions and Operators")

__

9.16. JSON Functions and Operators  
---  
[Prev](functions-xml.html "9.15. XML Functions")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions-sequence.html "9.17. Sequence Manipulation Functions")  
  
* * *

## 9.16. JSON Functions and Operators #

[9.16.1. Processing and Creating JSON Data](functions-json.html#FUNCTIONS-
JSON-PROCESSING)

[9.16.2. The SQL/JSON Path Language](functions-json.html#FUNCTIONS-SQLJSON-
PATH)

This section describes:

  * functions and operators for processing and creating JSON data

  * the SQL/JSON path language

To provide native support for JSON data types within the SQL environment,
PostgreSQL implements the _SQL/JSON data model_. This model comprises
sequences of items. Each item can hold SQL scalar values, with an additional
SQL/JSON null value, and composite data structures that use JSON arrays and
objects. The model is a formalization of the implied data model in the JSON
specification [RFC 7159](https://datatracker.ietf.org/doc/html/rfc7159).

SQL/JSON allows you to handle JSON data alongside regular SQL data, with
transaction support, including:

  * Uploading JSON data into the database and storing it in regular SQL columns as character or binary strings.

  * Generating JSON objects and arrays from relational data.

  * Querying JSON data using SQL/JSON query functions and SQL/JSON path language expressions.

To learn more about the SQL/JSON standard, see
[[sqltr-19075-6]](biblio.html#SQLTR-19075-6 "SQL Technical Report"). For
details on JSON types supported in PostgreSQL, see [Section 8.14](datatype-
json.html "8.14. JSON Types").

### 9.16.1. Processing and Creating JSON Data #

[Table 9.45](functions-json.html#FUNCTIONS-JSON-OP-TABLE "Table 9.45. json and
jsonb Operators") shows the operators that are available for use with JSON
data types (see [Section 8.14](datatype-json.html "8.14. JSON Types")). In
addition, the usual comparison operators shown in [Table 9.1](functions-
comparison.html#FUNCTIONS-COMPARISON-OP-TABLE "Table 9.1. Comparison
Operators") are available for `jsonb`, though not for `json`. The comparison
operators follow the ordering rules for B-tree operations outlined in [Section
8.14.4](datatype-json.html#JSON-INDEXING "8.14.4. jsonb Indexing"). See also
[Section 9.21](functions-aggregate.html "9.21. Aggregate Functions") for the
aggregate function `json_agg` which aggregates record values as JSON, the
aggregate function `json_object_agg` which aggregates pairs of values into a
JSON object, and their `jsonb` equivalents, `jsonb_agg` and
`jsonb_object_agg`.

**Table  9.45. `json` and `jsonb` Operators**

Operator Description Example(s)  
---  
`json` `->` `integer` → `json` `jsonb` `->` `integer` → `jsonb` Extracts _`n`_
'th element of JSON array (array elements are indexed from zero, but negative
integers count from the end). `'[{"a":"foo"},{"b":"bar"},{"c":"baz"}]'::json
-> 2` → `{"c":"baz"}` `'[{"a":"foo"},{"b":"bar"},{"c":"baz"}]'::json -> -3` →
`{"a":"foo"}`  
`json` `->` `text` → `json` `jsonb` `->` `text` → `jsonb` Extracts JSON object
field with the given key. `'{"a": {"b":"foo"}}'::json -> 'a'` → `{"b":"foo"}`  
`json` `->>` `integer` → `text` `jsonb` `->>` `integer` → `text` Extracts
_`n`_ 'th element of JSON array, as `text`. `'[1,2,3]'::json ->> 2` → `3`  
`json` `->>` `text` → `text` `jsonb` `->>` `text` → `text` Extracts JSON
object field with the given key, as `text`. `'{"a":1,"b":2}'::json ->> 'b'` →
`2`  
`json` `#>` `text[]` → `json` `jsonb` `#>` `text[]` → `jsonb` Extracts JSON
sub-object at the specified path, where path elements can be either field keys
or array indexes. `'{"a": {"b": ["foo","bar"]}}'::json #> '{a,b,1}'` → `"bar"`  
`json` `#>>` `text[]` → `text` `jsonb` `#>>` `text[]` → `text` Extracts JSON
sub-object at the specified path as `text`. `'{"a": {"b":
["foo","bar"]}}'::json #>> '{a,b,1}'` → `bar`  
  
  

### Note

The field/element/path extraction operators return NULL, rather than failing,
if the JSON input does not have the right structure to match the request; for
example if no such key or array element exists.

Some further operators exist only for `jsonb`, as shown in [Table
9.46](functions-json.html#FUNCTIONS-JSONB-OP-TABLE "Table 9.46. Additional
jsonb Operators"). [Section 8.14.4](datatype-json.html#JSON-INDEXING
"8.14.4. jsonb Indexing") describes how these operators can be used to
effectively search indexed `jsonb` data.

**Table  9.46. Additional `jsonb` Operators**

Operator Description Example(s)  
---  
`jsonb` `@>` `jsonb` → `boolean` Does the first JSON value contain the second?
(See [Section 8.14.3](datatype-json.html#JSON-CONTAINMENT "8.14.3. jsonb
Containment and Existence") for details about containment.) `'{"a":1,
"b":2}'::jsonb @> '{"b":2}'::jsonb` → `t`  
`jsonb` `<@` `jsonb` → `boolean` Is the first JSON value contained in the
second? `'{"b":2}'::jsonb <@ '{"a":1, "b":2}'::jsonb` → `t`  
`jsonb` `?` `text` → `boolean` Does the text string exist as a top-level key
or array element within the JSON value? `'{"a":1, "b":2}'::jsonb ? 'b'` → `t`
`'["a", "b", "c"]'::jsonb ? 'b'` → `t`  
`jsonb` `?|` `text[]` → `boolean` Do any of the strings in the text array
exist as top-level keys or array elements? `'{"a":1, "b":2, "c":3}'::jsonb ?|
array['b', 'd']` → `t`  
`jsonb` `?&` `text[]` → `boolean` Do all of the strings in the text array
exist as top-level keys or array elements? `'["a", "b", "c"]'::jsonb ?&
array['a', 'b']` → `t`  
`jsonb` `||` `jsonb` → `jsonb` Concatenates two `jsonb` values. Concatenating
two arrays generates an array containing all the elements of each input.
Concatenating two objects generates an object containing the union of their
keys, taking the second object's value when there are duplicate keys. All
other cases are treated by converting a non-array input into a single-element
array, and then proceeding as for two arrays. Does not operate recursively:
only the top-level array or object structure is merged. `'["a", "b"]'::jsonb
|| '["a", "d"]'::jsonb` → `["a", "b", "a", "d"]` `'{"a": "b"}'::jsonb ||
'{"c": "d"}'::jsonb` → `{"a": "b", "c": "d"}` `'[1, 2]'::jsonb || '3'::jsonb`
→ `[1, 2, 3]` `'{"a": "b"}'::jsonb || '42'::jsonb` → `[{"a": "b"}, 42]` To
append an array to another array as a single entry, wrap it in an additional
layer of array, for example: `'[1, 2]'::jsonb || jsonb_build_array('[3,
4]'::jsonb)` → `[1, 2, [3, 4]]`  
`jsonb` `-` `text` → `jsonb` Deletes a key (and its value) from a JSON object,
or matching string value(s) from a JSON array. `'{"a": "b", "c": "d"}'::jsonb
- 'a'` → `{"c": "d"}` `'["a", "b", "c", "b"]'::jsonb - 'b'` → `["a", "c"]`  
`jsonb` `-` `text[]` → `jsonb` Deletes all matching keys or array elements
from the left operand. `'{"a": "b", "c": "d"}'::jsonb - '{a,c}'::text[]` →
`{}`  
`jsonb` `-` `integer` → `jsonb` Deletes the array element with specified index
(negative integers count from the end). Throws an error if JSON value is not
an array. `'["a", "b"]'::jsonb - 1` → `["a"]`  
`jsonb` `#-` `text[]` → `jsonb` Deletes the field or array element at the
specified path, where path elements can be either field keys or array indexes.
`'["a", {"b":1}]'::jsonb #- '{1,b}'` → `["a", {}]`  
`jsonb` `@?` `jsonpath` → `boolean` Does JSON path return any item for the
specified JSON value? `'{"a":[1,2,3,4,5]}'::jsonb @? '$.a[*] ? (@ > 2)'` → `t`  
`jsonb` `@@` `jsonpath` → `boolean` Returns the result of a JSON path
predicate check for the specified JSON value. Only the first item of the
result is taken into account. If the result is not Boolean, then `NULL` is
returned. `'{"a":[1,2,3,4,5]}'::jsonb @@ '$.a[*] > 2'` → `t`  
  
  

### Note

The `jsonpath` operators `@?` and `@@` suppress the following errors: missing
object field or array element, unexpected JSON item type, datetime and numeric
errors. The `jsonpath`-related functions described below can also be told to
suppress these types of errors. This behavior might be helpful when searching
JSON document collections of varying structure.

[Table 9.47](functions-json.html#FUNCTIONS-JSON-CREATION-TABLE
"Table 9.47. JSON Creation Functions") shows the functions that are available
for constructing `json` and `jsonb` values. Some functions in this table have
a `RETURNING` clause, which specifies the data type returned. It must be one
of `json`, `jsonb`, `bytea`, a character string type (`text`, `char`, or
`varchar`), or a type that can be cast to `json`. By default, the `json` type
is returned.

**Table  9.47. JSON Creation Functions**

Function Description Example(s)  
---  
`to_json` ( `anyelement` ) → `json` `to_jsonb` ( `anyelement` ) → `jsonb`
Converts any SQL value to `json` or `jsonb`. Arrays and composites are
converted recursively to arrays and objects (multidimensional arrays become
arrays of arrays in JSON). Otherwise, if there is a cast from the SQL data
type to `json`, the cast function will be used to perform the conversion;[a]
otherwise, a scalar JSON value is produced. For any scalar other than a
number, a Boolean, or a null value, the text representation will be used, with
escaping as necessary to make it a valid JSON string value. `to_json('Fred
said "Hi."'::text)` → `"Fred said \"Hi.\""` `to_jsonb(row(42, 'Fred said
"Hi."'::text))` → `{"f1": 42, "f2": "Fred said \"Hi.\""}`  
`array_to_json` ( `anyarray` [, `boolean` ] ) → `json` Converts an SQL array
to a JSON array. The behavior is the same as `to_json` except that line feeds
will be added between top-level array elements if the optional boolean
parameter is true. `array_to_json('{{1,5},{99,100}}'::int[])` →
`[[1,5],[99,100]]`  
`json_array` ( [ { _`value_expression`_ [ `FORMAT JSON` ] } [, ...] ] [ { `NULL` | `ABSENT` } `ON NULL` ] [ `RETURNING` _`data_type`_ [ `FORMAT JSON` [ `ENCODING UTF8` ] ] ]) `json_array` ( [ _`query_expression`_ ] [ `RETURNING` _`data_type`_ [ `FORMAT JSON` [ `ENCODING UTF8` ] ] ]) Constructs a JSON array from either a series of _`value_expression`_ parameters or from the results of _`query_expression`_ , which must be a SELECT query returning a single column. If `ABSENT ON NULL` is specified, NULL values are ignored. This is always the case if a _`query_expression`_ is used. `json_array(1,true,json '{"a":null}')` → `[1, true, {"a":null}]` `json_array(SELECT * FROM (VALUES(1),(2)) t)` → `[1, 2]`  
`row_to_json` ( `record` [, `boolean` ] ) → `json` Converts an SQL composite
value to a JSON object. The behavior is the same as `to_json` except that line
feeds will be added between top-level elements if the optional boolean
parameter is true. `row_to_json(row(1,'foo'))` → `{"f1":1,"f2":"foo"}`  
`json_build_array` ( `VARIADIC` `"any"` ) → `json` `jsonb_build_array` (
`VARIADIC` `"any"` ) → `jsonb` Builds a possibly-heterogeneously-typed JSON
array out of a variadic argument list. Each argument is converted as per
`to_json` or `to_jsonb`. `json_build_array(1, 2, 'foo', 4, 5)` → `[1, 2,
"foo", 4, 5]`  
`json_build_object` ( `VARIADIC` `"any"` ) → `json` `jsonb_build_object` (
`VARIADIC` `"any"` ) → `jsonb` Builds a JSON object out of a variadic argument
list. By convention, the argument list consists of alternating keys and
values. Key arguments are coerced to text; value arguments are converted as
per `to_json` or `to_jsonb`. `json_build_object('foo', 1, 2, row(3,'bar'))` →
`{"foo" : 1, "2" : {"f1":3,"f2":"bar"}}`  
`json_object` ( [ { _`key_expression`_ { `VALUE` | ':' } _`value_expression`_ [ `FORMAT JSON` [ `ENCODING UTF8` ] ] }[, ...] ] [ { `NULL` | `ABSENT` } `ON NULL` ] [ { `WITH` | `WITHOUT` } `UNIQUE` [ `KEYS` ] ] [ `RETURNING` _`data_type`_ [ `FORMAT JSON` [ `ENCODING UTF8` ] ] ]) Constructs a JSON object of all the key/value pairs given, or an empty object if none are given. _`key_expression`_ is a scalar expression defining the JSON key, which is converted to the `text` type. It cannot be `NULL` nor can it belong to a type that has a cast to the `json` type. If `WITH UNIQUE KEYS` is specified, there must not be any duplicate _`key_expression`_. Any pair for which the _`value_expression`_ evaluates to `NULL` is omitted from the output if `ABSENT ON NULL` is specified; if `NULL ON NULL` is specified or the clause omitted, the key is included with value `NULL`. `json_object('code' VALUE 'P123', 'title': 'Jaws')` → `{"code" : "P123", "title" : "Jaws"}`  
`json_object` ( `text[]` ) → `json` `jsonb_object` ( `text[]` ) → `jsonb`
Builds a JSON object out of a text array. The array must have either exactly
one dimension with an even number of members, in which case they are taken as
alternating key/value pairs, or two dimensions such that each inner array has
exactly two elements, which are taken as a key/value pair. All values are
converted to JSON strings. `json_object('{a, 1, b, "def", c, 3.5}')` → `{"a" :
"1", "b" : "def", "c" : "3.5"}` `json_object('{{a, 1}, {b, "def"}, {c,
3.5}}')` → `{"a" : "1", "b" : "def", "c" : "3.5"}`  
`json_object` ( _`keys`_ `text[]`, _`values`_ `text[]` ) → `json`
`jsonb_object` ( _`keys`_ `text[]`, _`values`_ `text[]` ) → `jsonb` This form
of `json_object` takes keys and values pairwise from separate text arrays.
Otherwise it is identical to the one-argument form. `json_object('{a,b}',
'{1,2}')` → `{"a": "1", "b": "2"}`  
[a] For example, the [hstore](hstore.html "F.18. hstore — hstore key/value
datatype") extension has a cast from `hstore` to `json`, so that `hstore`
values converted via the JSON creation functions will be represented as JSON
objects, not as primitive string values.  
  
  

[Table 9.48](functions-json.html#FUNCTIONS-SQLJSON-MISC "Table 9.48. SQL/JSON
Testing Functions") details SQL/JSON facilities for testing JSON.

**Table  9.48. SQL/JSON Testing Functions**

Function signature Description Example(s)  
---  
_`expression`_ `IS` [ `NOT` ] `JSON` [ { `VALUE` | `SCALAR` | `ARRAY` | `OBJECT` } ] [ { `WITH` | `WITHOUT` } `UNIQUE` [ `KEYS` ] ] This predicate tests whether _`expression`_ can be parsed as JSON, possibly of a specified type. If `SCALAR` or `ARRAY` or `OBJECT` is specified, the test is whether or not the JSON is of that particular type. If `WITH UNIQUE KEYS` is specified, then any object in the _`expression`_ is also tested to see if it has duplicate keys.
    
    
    SELECT js,
      js IS JSON "json?",
      js IS JSON SCALAR "scalar?",
      js IS JSON OBJECT "object?",
      js IS JSON ARRAY "array?"
    FROM (VALUES
          ('123'), ('"abc"'), ('{"a": "b"}'), ('[1,2]'),('abc')) foo(js);
         js     | json? | scalar? | object? | array?
    ------------+-------+---------+---------+--------
     123        | t     | t       | f       | f
     "abc"      | t     | t       | f       | f
     {"a": "b"} | t     | f       | t       | f
     [1,2]      | t     | f       | f       | t
     abc        | f     | f       | f       | f
    
    
    
    SELECT js,
      js IS JSON OBJECT "object?",
      js IS JSON ARRAY "array?",
      js IS JSON ARRAY WITH UNIQUE KEYS "array w. UK?",
      js IS JSON ARRAY WITHOUT UNIQUE KEYS "array w/o UK?"
    FROM (VALUES ('[{"a":"1"},
     {"b":"2","b":"3"}]')) foo(js);
    -[ RECORD 1 ]-+--------------------
    js            | [{"a":"1"},        +
                  |  {"b":"2","b":"3"}]
    object?       | f
    array?        | t
    array w. UK?  | f
    array w/o UK? | t
      
  
  

[Table 9.49](functions-json.html#FUNCTIONS-JSON-PROCESSING-TABLE
"Table 9.49. JSON Processing Functions") shows the functions that are
available for processing `json` and `jsonb` values.

**Table  9.49. JSON Processing Functions**

Function Description Example(s)  
---  
`json_array_elements` ( `json` ) → `setof json` `jsonb_array_elements` (
`jsonb` ) → `setof jsonb` Expands the top-level JSON array into a set of JSON
values. `select * from json_array_elements('[1,true, [2,false]]')` →

    
    
       value
    -----------
     1
     true
     [2,false]
      
  
`json_array_elements_text` ( `json` ) → `setof text`
`jsonb_array_elements_text` ( `jsonb` ) → `setof text` Expands the top-level
JSON array into a set of `text` values. `select * from
json_array_elements_text('["foo", "bar"]')` →

    
    
       value
    -----------
     foo
     bar
      
  
`json_array_length` ( `json` ) → `integer` `jsonb_array_length` ( `jsonb` ) →
`integer` Returns the number of elements in the top-level JSON array.
`json_array_length('[1,2,3,{"f1":1,"f2":[5,6]},4]')` → `5`
`jsonb_array_length('[]')` → `0`  
`json_each` ( `json` ) → `setof record` ( _`key`_ `text`, _`value`_ `json` )
`jsonb_each` ( `jsonb` ) → `setof record` ( _`key`_ `text`, _`value`_ `jsonb`
) Expands the top-level JSON object into a set of key/value pairs. `select *
from json_each('{"a":"foo", "b":"bar"}')` →

    
    
     key | value
    -----+-------
     a   | "foo"
     b   | "bar"
      
  
`json_each_text` ( `json` ) → `setof record` ( _`key`_ `text`, _`value`_
`text` ) `jsonb_each_text` ( `jsonb` ) → `setof record` ( _`key`_ `text`,
_`value`_ `text` ) Expands the top-level JSON object into a set of key/value
pairs. The returned _`value`_ s will be of type `text`. `select * from
json_each_text('{"a":"foo", "b":"bar"}')` →

    
    
     key | value
    -----+-------
     a   | foo
     b   | bar
      
  
`json_extract_path` ( _`from_json`_ `json`, `VARIADIC` _`path_elems`_ `text[]`
) → `json` `jsonb_extract_path` ( _`from_json`_ `jsonb`, `VARIADIC`
_`path_elems`_ `text[]` ) → `jsonb` Extracts JSON sub-object at the specified
path. (This is functionally equivalent to the `#>` operator, but writing the
path out as a variadic list can be more convenient in some cases.)
`json_extract_path('{"f2":{"f3":1},"f4":{"f5":99,"f6":"foo"}}', 'f4', 'f6')` →
`"foo"`  
`json_extract_path_text` ( _`from_json`_ `json`, `VARIADIC` _`path_elems`_
`text[]` ) → `text` `jsonb_extract_path_text` ( _`from_json`_ `jsonb`,
`VARIADIC` _`path_elems`_ `text[]` ) → `text` Extracts JSON sub-object at the
specified path as `text`. (This is functionally equivalent to the `#>>`
operator.)
`json_extract_path_text('{"f2":{"f3":1},"f4":{"f5":99,"f6":"foo"}}', 'f4',
'f6')` → `foo`  
`json_object_keys` ( `json` ) → `setof text` `jsonb_object_keys` ( `jsonb` ) →
`setof text` Returns the set of keys in the top-level JSON object. `select *
from json_object_keys('{"f1":"abc","f2":{"f3":"a", "f4":"b"}}')` →

    
    
     json_object_keys
    ------------------
     f1
     f2
      
  
`json_populate_record` ( _`base`_ `anyelement`, _`from_json`_ `json` ) →
`anyelement` `jsonb_populate_record` ( _`base`_ `anyelement`, _`from_json`_
`jsonb` ) → `anyelement` Expands the top-level JSON object to a row having the
composite type of the _`base`_ argument. The JSON object is scanned for fields
whose names match column names of the output row type, and their values are
inserted into those columns of the output. (Fields that do not correspond to
any output column name are ignored.) In typical use, the value of _`base`_ is
just `NULL`, which means that any output columns that do not match any object
field will be filled with nulls. However, if _`base`_ isn't `NULL` then the
values it contains will be used for unmatched columns. To convert a JSON value
to the SQL type of an output column, the following rules are applied in
sequence:

  * A JSON null value is converted to an SQL null in all cases.
  * If the output column is of type `json` or `jsonb`, the JSON value is just reproduced exactly.
  * If the output column is a composite (row) type, and the JSON value is a JSON object, the fields of the object are converted to columns of the output row type by recursive application of these rules.
  * Likewise, if the output column is an array type and the JSON value is a JSON array, the elements of the JSON array are converted to elements of the output array by recursive application of these rules.
  * Otherwise, if the JSON value is a string, the contents of the string are fed to the input conversion function for the column's data type.
  * Otherwise, the ordinary text representation of the JSON value is fed to the input conversion function for the column's data type.

While the example below uses a constant JSON value, typical use would be to
reference a `json` or `jsonb` column laterally from another table in the
query's `FROM` clause. Writing `json_populate_record` in the `FROM` clause is
good practice, since all of the extracted columns are available for use
without duplicate function calls. `create type subrowtype as (d int, e text);`
`create type myrowtype as (a int, b text[], c subrowtype);` `select * from
json_populate_record(null::myrowtype, '{"a": 1, "b": ["2", "a b"], "c": {"d":
4, "e": "a b c"}, "x": "foo"}')` →

    
    
     a |   b       |      c
    ---+-----------+-------------
     1 | {2,"a b"} | (4,"a b c")
      
  
`json_populate_recordset` ( _`base`_ `anyelement`, _`from_json`_ `json` ) →
`setof anyelement` `jsonb_populate_recordset` ( _`base`_ `anyelement`,
_`from_json`_ `jsonb` ) → `setof anyelement` Expands the top-level JSON array
of objects to a set of rows having the composite type of the _`base`_
argument. Each element of the JSON array is processed as described above for
`json[b]_populate_record`. `create type twoints as (a int, b int);` `select *
from json_populate_recordset(null::twoints, '[{"a":1,"b":2}, {"a":3,"b":4}]')`
→

    
    
     a | b
    ---+---
     1 | 2
     3 | 4
      
  
`json_to_record` ( `json` ) → `record` `jsonb_to_record` ( `jsonb` ) →
`record` Expands the top-level JSON object to a row having the composite type
defined by an `AS` clause. (As with all functions returning `record`, the
calling query must explicitly define the structure of the record with an `AS`
clause.) The output record is filled from fields of the JSON object, in the
same way as described above for `json[b]_populate_record`. Since there is no
input record value, unmatched columns are always filled with nulls. `create
type myrowtype as (a int, b text);` `select * from
json_to_record('{"a":1,"b":[1,2,3],"c":[1,2,3],"e":"bar","r": {"a": 123, "b":
"a b c"}}') as x(a int, b text, c int[], d text, r myrowtype)` →

    
    
     a |    b    |    c    | d |       r
    ---+---------+---------+---+---------------
     1 | [1,2,3] | {1,2,3} |   | (123,"a b c")
      
  
`json_to_recordset` ( `json` ) → `setof record` `jsonb_to_recordset` ( `jsonb`
) → `setof record` Expands the top-level JSON array of objects to a set of
rows having the composite type defined by an `AS` clause. (As with all
functions returning `record`, the calling query must explicitly define the
structure of the record with an `AS` clause.) Each element of the JSON array
is processed as described above for `json[b]_populate_record`. `select * from
json_to_recordset('[{"a":1,"b":"foo"}, {"a":"2","c":"bar"}]') as x(a int, b
text)` →

    
    
     a |  b
    ---+-----
     1 | foo
     2 |
      
  
`jsonb_set` ( _`target`_ `jsonb`, _`path`_ `text[]`, _`new_value`_ `jsonb` [,
_`create_if_missing`_ `boolean` ] ) → `jsonb` Returns _`target`_ with the item
designated by _`path`_ replaced by _`new_value`_ , or with _`new_value`_ added
if _`create_if_missing`_ is true (which is the default) and the item
designated by _`path`_ does not exist. All earlier steps in the path must
exist, or the _`target`_ is returned unchanged. As with the path oriented
operators, negative integers that appear in the _`path`_ count from the end of
JSON arrays. If the last path step is an array index that is out of range, and
_`create_if_missing`_ is true, the new value is added at the beginning of the
array if the index is negative, or at the end of the array if it is positive.
`jsonb_set('[{"f1":1,"f2":null},2,null,3]', '{0,f1}', '[2,3,4]', false)` →
`[{"f1": [2, 3, 4], "f2": null}, 2, null, 3]`
`jsonb_set('[{"f1":1,"f2":null},2]', '{0,f3}', '[2,3,4]')` → `[{"f1": 1, "f2":
null, "f3": [2, 3, 4]}, 2]`  
`jsonb_set_lax` ( _`target`_ `jsonb`, _`path`_ `text[]`, _`new_value`_ `jsonb`
[, _`create_if_missing`_ `boolean` [, _`null_value_treatment`_ `text` ]] ) →
`jsonb` If _`new_value`_ is not `NULL`, behaves identically to `jsonb_set`.
Otherwise behaves according to the value of _`null_value_treatment`_ which
must be one of `'raise_exception'`, `'use_json_null'`, `'delete_key'`, or
`'return_target'`. The default is `'use_json_null'`.
`jsonb_set_lax('[{"f1":1,"f2":null},2,null,3]', '{0,f1}', null)` → `[{"f1":
null, "f2": null}, 2, null, 3]` `jsonb_set_lax('[{"f1":99,"f2":null},2]',
'{0,f3}', null, true, 'return_target')` → `[{"f1": 99, "f2": null}, 2]`  
`jsonb_insert` ( _`target`_ `jsonb`, _`path`_ `text[]`, _`new_value`_ `jsonb`
[, _`insert_after`_ `boolean` ] ) → `jsonb` Returns _`target`_ with
_`new_value`_ inserted. If the item designated by the _`path`_ is an array
element, _`new_value`_ will be inserted before that item if _`insert_after`_
is false (which is the default), or after it if _`insert_after`_ is true. If
the item designated by the _`path`_ is an object field, _`new_value`_ will be
inserted only if the object does not already contain that key. All earlier
steps in the path must exist, or the _`target`_ is returned unchanged. As with
the path oriented operators, negative integers that appear in the _`path`_
count from the end of JSON arrays. If the last path step is an array index
that is out of range, the new value is added at the beginning of the array if
the index is negative, or at the end of the array if it is positive.
`jsonb_insert('{"a": [0,1,2]}', '{a, 1}', '"new_value"')` → `{"a": [0,
"new_value", 1, 2]}` `jsonb_insert('{"a": [0,1,2]}', '{a, 1}', '"new_value"',
true)` → `{"a": [0, 1, "new_value", 2]}`  
`json_strip_nulls` ( `json` ) → `json` `jsonb_strip_nulls` ( `jsonb` ) →
`jsonb` Deletes all object fields that have null values from the given JSON
value, recursively. Null values that are not object fields are untouched.
`json_strip_nulls('[{"f1":1, "f2":null}, 2, null, 3]')` →
`[{"f1":1},2,null,3]`  
`jsonb_path_exists` ( _`target`_ `jsonb`, _`path`_ `jsonpath` [, _`vars`_
`jsonb` [, _`silent`_ `boolean` ]] ) → `boolean` Checks whether the JSON path
returns any item for the specified JSON value. If the _`vars`_ argument is
specified, it must be a JSON object, and its fields provide named values to be
substituted into the `jsonpath` expression. If the _`silent`_ argument is
specified and is `true`, the function suppresses the same errors as the `@?`
and `@@` operators do. `jsonb_path_exists('{"a":[1,2,3,4,5]}', '$.a[*] ? (@ >=
$min && @ <= $max)', '{"min":2, "max":4}')` → `t`  
`jsonb_path_match` ( _`target`_ `jsonb`, _`path`_ `jsonpath` [, _`vars`_
`jsonb` [, _`silent`_ `boolean` ]] ) → `boolean` Returns the result of a JSON
path predicate check for the specified JSON value. Only the first item of the
result is taken into account. If the result is not Boolean, then `NULL` is
returned. The optional _`vars`_ and _`silent`_ arguments act the same as for
`jsonb_path_exists`. `jsonb_path_match('{"a":[1,2,3,4,5]}', 'exists($.a[*] ?
(@ >= $min && @ <= $max))', '{"min":2, "max":4}')` → `t`  
`jsonb_path_query` ( _`target`_ `jsonb`, _`path`_ `jsonpath` [, _`vars`_
`jsonb` [, _`silent`_ `boolean` ]] ) → `setof jsonb` Returns all JSON items
returned by the JSON path for the specified JSON value. The optional _`vars`_
and _`silent`_ arguments act the same as for `jsonb_path_exists`. `select *
from jsonb_path_query('{"a":[1,2,3,4,5]}', '$.a[*] ? (@ >= $min && @ <=
$max)', '{"min":2, "max":4}')` →

    
    
     jsonb_path_query
    ------------------
     2
     3
     4
      
  
`jsonb_path_query_array` ( _`target`_ `jsonb`, _`path`_ `jsonpath` [, _`vars`_
`jsonb` [, _`silent`_ `boolean` ]] ) → `jsonb` Returns all JSON items returned
by the JSON path for the specified JSON value, as a JSON array. The optional
_`vars`_ and _`silent`_ arguments act the same as for `jsonb_path_exists`.
`jsonb_path_query_array('{"a":[1,2,3,4,5]}', '$.a[*] ? (@ >= $min && @ <=
$max)', '{"min":2, "max":4}')` → `[2, 3, 4]`  
`jsonb_path_query_first` ( _`target`_ `jsonb`, _`path`_ `jsonpath` [, _`vars`_
`jsonb` [, _`silent`_ `boolean` ]] ) → `jsonb` Returns the first JSON item
returned by the JSON path for the specified JSON value. Returns `NULL` if
there are no results. The optional _`vars`_ and _`silent`_ arguments act the
same as for `jsonb_path_exists`. `jsonb_path_query_first('{"a":[1,2,3,4,5]}',
'$.a[*] ? (@ >= $min && @ <= $max)', '{"min":2, "max":4}')` → `2`  
`jsonb_path_exists_tz` ( _`target`_ `jsonb`, _`path`_ `jsonpath` [, _`vars`_
`jsonb` [, _`silent`_ `boolean` ]] ) → `boolean` `jsonb_path_match_tz` (
_`target`_ `jsonb`, _`path`_ `jsonpath` [, _`vars`_ `jsonb` [, _`silent`_
`boolean` ]] ) → `boolean` `jsonb_path_query_tz` ( _`target`_ `jsonb`,
_`path`_ `jsonpath` [, _`vars`_ `jsonb` [, _`silent`_ `boolean` ]] ) → `setof
jsonb` `jsonb_path_query_array_tz` ( _`target`_ `jsonb`, _`path`_ `jsonpath`
[, _`vars`_ `jsonb` [, _`silent`_ `boolean` ]] ) → `jsonb`
`jsonb_path_query_first_tz` ( _`target`_ `jsonb`, _`path`_ `jsonpath` [,
_`vars`_ `jsonb` [, _`silent`_ `boolean` ]] ) → `jsonb` These functions act
like their counterparts described above without the `_tz` suffix, except that
these functions support comparisons of date/time values that require timezone-
aware conversions. The example below requires interpretation of the date-only
value `2015-08-02` as a timestamp with time zone, so the result depends on the
current [TimeZone](runtime-config-client.html#GUC-TIMEZONE) setting. Due to
this dependency, these functions are marked as stable, which means these
functions cannot be used in indexes. Their counterparts are immutable, and so
can be used in indexes; but they will throw errors if asked to make such
comparisons. `jsonb_path_exists_tz('["2015-08-01 12:00:00-05"]', '$[*] ?
(@.datetime() < "2015-08-02".datetime())')` → `t`  
`jsonb_pretty` ( `jsonb` ) → `text` Converts the given JSON value to pretty-
printed, indented text. `jsonb_pretty('[{"f1":1,"f2":null}, 2]')` →

    
    
    [
        {
            "f1": 1,
            "f2": null
        },
        2
    ]
      
  
`json_typeof` ( `json` ) → `text` `jsonb_typeof` ( `jsonb` ) → `text` Returns
the type of the top-level JSON value as a text string. Possible types are
`object`, `array`, `string`, `number`, `boolean`, and `null`. (The `null`
result should not be confused with an SQL NULL; see the examples.)
`json_typeof('-123.4')` → `number` `json_typeof('null'::json)` → `null`
`json_typeof(NULL::json) IS NULL` → `t`  
  
  

### 9.16.2. The SQL/JSON Path Language #

SQL/JSON path expressions specify the items to be retrieved from the JSON
data, similar to XPath expressions used for SQL access to XML. In PostgreSQL,
path expressions are implemented as the `jsonpath` data type and can use any
elements described in [Section 8.14.7](datatype-json.html#DATATYPE-JSONPATH
"8.14.7. jsonpath Type").

JSON query functions and operators pass the provided path expression to the
_path engine_ for evaluation. If the expression matches the queried JSON data,
the corresponding JSON item, or set of items, is returned. Path expressions
are written in the SQL/JSON path language and can include arithmetic
expressions and functions.

A path expression consists of a sequence of elements allowed by the `jsonpath`
data type. The path expression is normally evaluated from left to right, but
you can use parentheses to change the order of operations. If the evaluation
is successful, a sequence of JSON items is produced, and the evaluation result
is returned to the JSON query function that completes the specified
computation.

To refer to the JSON value being queried (the _context item_), use the `$`
variable in the path expression. It can be followed by one or more [accessor
operators](datatype-json.html#TYPE-JSONPATH-ACCESSORS "Table 8.25. jsonpath
Accessors"), which go down the JSON structure level by level to retrieve sub-
items of the context item. Each operator that follows deals with the result of
the previous evaluation step.

For example, suppose you have some JSON data from a GPS tracker that you would
like to parse, such as:

    
    
    {
      "track": {
        "segments": [
          {
            "location":   [ 47.763, 13.4034 ],
            "start time": "2018-10-14 10:05:14",
            "HR": 73
          },
          {
            "location":   [ 47.706, 13.2635 ],
            "start time": "2018-10-14 10:39:21",
            "HR": 135
          }
        ]
      }
    }
    

To retrieve the available track segments, you need to use the `._`key`_`
accessor operator to descend through surrounding JSON objects:

    
    
    $.track.segments
    

To retrieve the contents of an array, you typically use the `[*]` operator.
For example, the following path will return the location coordinates for all
the available track segments:

    
    
    $.track.segments[*].location
    

To return the coordinates of the first segment only, you can specify the
corresponding subscript in the `[]` accessor operator. Recall that JSON array
indexes are 0-relative:

    
    
    $.track.segments[0].location
    

The result of each path evaluation step can be processed by one or more
`jsonpath` operators and methods listed in [Section 9.16.2.2](functions-
json.html#FUNCTIONS-SQLJSON-PATH-OPERATORS "9.16.2.2. SQL/JSON Path Operators
and Methods"). Each method name must be preceded by a dot. For example, you
can get the size of an array:

    
    
    $.track.segments.size()
    

More examples of using `jsonpath` operators and methods within path
expressions appear below in [Section 9.16.2.2](functions-json.html#FUNCTIONS-
SQLJSON-PATH-OPERATORS "9.16.2.2. SQL/JSON Path Operators and Methods").

When defining a path, you can also use one or more _filter expressions_ that
work similarly to the `WHERE` clause in SQL. A filter expression begins with a
question mark and provides a condition in parentheses:

    
    
    ? (_condition_)
    

Filter expressions must be written just after the path evaluation step to
which they should apply. The result of that step is filtered to include only
those items that satisfy the provided condition. SQL/JSON defines three-valued
logic, so the condition can be `true`, `false`, or `unknown`. The `unknown`
value plays the same role as SQL `NULL` and can be tested for with the `is
unknown` predicate. Further path evaluation steps use only those items for
which the filter expression returned `true`.

The functions and operators that can be used in filter expressions are listed
in [Table 9.51](functions-json.html#FUNCTIONS-SQLJSON-FILTER-EX-TABLE
"Table 9.51. jsonpath Filter Expression Elements"). Within a filter
expression, the `@` variable denotes the value being filtered (i.e., one
result of the preceding path step). You can write accessor operators after `@`
to retrieve component items.

For example, suppose you would like to retrieve all heart rate values higher
than 130. You can achieve this using the following expression:

    
    
    $.track.segments[*].HR ? (@ > 130)
    

To get the start times of segments with such values, you have to filter out
irrelevant segments before returning the start times, so the filter expression
is applied to the previous step, and the path used in the condition is
different:

    
    
    $.track.segments[*] ? (@.HR > 130)."start time"
    

You can use several filter expressions in sequence, if required. For example,
the following expression selects start times of all segments that contain
locations with relevant coordinates and high heart rate values:

    
    
    $.track.segments[*] ? (@.location[1] < 13.4) ? (@.HR > 130)."start time"
    

Using filter expressions at different nesting levels is also allowed. The
following example first filters all segments by location, and then returns
high heart rate values for these segments, if available:

    
    
    $.track.segments[*] ? (@.location[1] < 13.4).HR ? (@ > 130)
    

You can also nest filter expressions within each other:

    
    
    $.track ? (exists(@.segments[*] ? (@.HR > 130))).segments.size()
    

This expression returns the size of the track if it contains any segments with
high heart rate values, or an empty sequence otherwise.

PostgreSQL's implementation of the SQL/JSON path language has the following
deviations from the SQL/JSON standard:

  * A path expression can be a Boolean predicate, although the SQL/JSON standard allows predicates only in filters. This is necessary for implementation of the `@@` operator. For example, the following `jsonpath` expression is valid in PostgreSQL:
        
        $.track.segments[*].HR < 70
        

  * There are minor differences in the interpretation of regular expression patterns used in `like_regex` filters, as described in [Section 9.16.2.3](functions-json.html#JSONPATH-REGULAR-EXPRESSIONS "9.16.2.3. SQL/JSON Regular Expressions").

#### 9.16.2.1. Strict and Lax Modes #

When you query JSON data, the path expression may not match the actual JSON
data structure. An attempt to access a non-existent member of an object or
element of an array results in a structural error. SQL/JSON path expressions
have two modes of handling structural errors:

  * lax (default) — the path engine implicitly adapts the queried data to the specified path. Any remaining structural errors are suppressed and converted to empty SQL/JSON sequences.

  * strict — if a structural error occurs, an error is raised.

The lax mode facilitates matching of a JSON document structure and path
expression if the JSON data does not conform to the expected schema. If an
operand does not match the requirements of a particular operation, it can be
automatically wrapped as an SQL/JSON array or unwrapped by converting its
elements into an SQL/JSON sequence before performing this operation. Besides,
comparison operators automatically unwrap their operands in the lax mode, so
you can compare SQL/JSON arrays out-of-the-box. An array of size 1 is
considered equal to its sole element. Automatic unwrapping is not performed
only when:

  * The path expression contains `type()` or `size()` methods that return the type and the number of elements in the array, respectively.

  * The queried JSON data contain nested arrays. In this case, only the outermost array is unwrapped, while all the inner arrays remain unchanged. Thus, implicit unwrapping can only go one level down within each path evaluation step.

For example, when querying the GPS data listed above, you can abstract from
the fact that it stores an array of segments when using the lax mode:

    
    
    lax $.track.segments.location
    

In the strict mode, the specified path must exactly match the structure of the
queried JSON document to return an SQL/JSON item, so using this path
expression will cause an error. To get the same result as in the lax mode, you
have to explicitly unwrap the `segments` array:

    
    
    strict $.track.segments[*].location
    

The `.**` accessor can lead to surprising results when using the lax mode. For
instance, the following query selects every `HR` value twice:

    
    
    lax $.**.HR
    

This happens because the `.**` accessor selects both the `segments` array and
each of its elements, while the `.HR` accessor automatically unwraps arrays
when using the lax mode. To avoid surprising results, we recommend using the
`.**` accessor only in the strict mode. The following query selects each `HR`
value just once:

    
    
    strict $.**.HR
    

#### 9.16.2.2. SQL/JSON Path Operators and Methods #

[Table 9.50](functions-json.html#FUNCTIONS-SQLJSON-OP-TABLE
"Table 9.50. jsonpath Operators and Methods") shows the operators and methods
available in `jsonpath`. Note that while the unary operators and methods can
be applied to multiple values resulting from a preceding path step, the binary
operators (addition etc.) can only be applied to single values.

**Table  9.50. `jsonpath` Operators and Methods**

Operator/Method Description Example(s)  
---  
_`number`_ `+` _`number`_ → `_`number`_` Addition `jsonb_path_query('[2]',
'$[0] + 3')` → `5`  
`+` _`number`_ → `_`number`_` Unary plus (no operation); unlike addition, this
can iterate over multiple values `jsonb_path_query_array('{"x": [2,3,4]}', '+
$.x')` → `[2, 3, 4]`  
_`number`_ `-` _`number`_ → `_`number`_` Subtraction `jsonb_path_query('[2]',
'7 - $[0]')` → `5`  
`-` _`number`_ → `_`number`_` Negation; unlike subtraction, this can iterate
over multiple values `jsonb_path_query_array('{"x": [2,3,4]}', '- $.x')` →
`[-2, -3, -4]`  
_`number`_ `*` _`number`_ → `_`number`_` Multiplication
`jsonb_path_query('[4]', '2 * $[0]')` → `8`  
_`number`_ `/` _`number`_ → `_`number`_` Division `jsonb_path_query('[8.5]',
'$[0] / 2')` → `4.2500000000000000`  
_`number`_ `%` _`number`_ → `_`number`_` Modulo (remainder)
`jsonb_path_query('[32]', '$[0] % 10')` → `2`  
_`value`_ `.` `type()` → `_`string`_` Type of the JSON item (see
`json_typeof`) `jsonb_path_query_array('[1, "2", {}]', '$[*].type()')` →
`["number", "string", "object"]`  
_`value`_ `.` `size()` → `_`number`_` Size of the JSON item (number of array
elements, or 1 if not an array) `jsonb_path_query('{"m": [11, 15]}',
'$.m.size()')` → `2`  
_`value`_ `.` `double()` → `_`number`_` Approximate floating-point number
converted from a JSON number or string `jsonb_path_query('{"len": "1.9"}',
'$.len.double() * 2')` → `3.8`  
_`number`_ `.` `ceiling()` → `_`number`_` Nearest integer greater than or
equal to the given number `jsonb_path_query('{"h": 1.3}', '$.h.ceiling()')` →
`2`  
_`number`_ `.` `floor()` → `_`number`_` Nearest integer less than or equal to
the given number `jsonb_path_query('{"h": 1.7}', '$.h.floor()')` → `1`  
_`number`_ `.` `abs()` → `_`number`_` Absolute value of the given number
`jsonb_path_query('{"z": -0.3}', '$.z.abs()')` → `0.3`  
_`string`_ `.` `datetime()` → `_`datetime_type`_` (see note) Date/time value
converted from a string `jsonb_path_query('["2015-8-1", "2015-08-12"]', '$[*]
? (@.datetime() < "2015-08-2".datetime())')` → `"2015-8-1"`  
_`string`_ `.` `datetime(_`template`_)` → `_`datetime_type`_` (see note)
Date/time value converted from a string using the specified `to_timestamp`
template `jsonb_path_query_array('["12:30", "18:40"]',
'$[*].datetime("HH24:MI")')` → `["12:30:00", "18:40:00"]`  
_`object`_ `.` `keyvalue()` → `_`array`_` The object's key-value pairs,
represented as an array of objects containing three fields: `"key"`,
`"value"`, and `"id"`; `"id"` is a unique identifier of the object the key-
value pair belongs to `jsonb_path_query_array('{"x": "20", "y": 32}',
'$.keyvalue()')` → `[{"id": 0, "key": "x", "value": "20"}, {"id": 0, "key":
"y", "value": 32}]`  
  
  

### Note

The result type of the `datetime()` and `datetime(_`template`_)` methods can
be `date`, `timetz`, `time`, `timestamptz`, or `timestamp`. Both methods
determine their result type dynamically.

The `datetime()` method sequentially tries to match its input string to the
ISO formats for `date`, `timetz`, `time`, `timestamptz`, and `timestamp`. It
stops on the first matching format and emits the corresponding data type.

The `datetime(_`template`_)` method determines the result type according to
the fields used in the provided template string.

The `datetime()` and `datetime(_`template`_)` methods use the same parsing
rules as the `to_timestamp` SQL function does (see [Section 9.8](functions-
formatting.html "9.8. Data Type Formatting Functions")), with three
exceptions. First, these methods don't allow unmatched template patterns.
Second, only the following separators are allowed in the template string:
minus sign, period, solidus (slash), comma, apostrophe, semicolon, colon and
space. Third, separators in the template string must exactly match the input
string.

If different date/time types need to be compared, an implicit cast is applied.
A `date` value can be cast to `timestamp` or `timestamptz`, `timestamp` can be
cast to `timestamptz`, and `time` to `timetz`. However, all but the first of
these conversions depend on the current [TimeZone](runtime-config-
client.html#GUC-TIMEZONE) setting, and thus can only be performed within
timezone-aware `jsonpath` functions.

[Table 9.51](functions-json.html#FUNCTIONS-SQLJSON-FILTER-EX-TABLE
"Table 9.51. jsonpath Filter Expression Elements") shows the available filter
expression elements.

**Table  9.51. `jsonpath` Filter Expression Elements**

Predicate/Value Description Example(s)  
---  
_`value`_ `==` _`value`_ → `boolean` Equality comparison (this, and the other
comparison operators, work on all JSON scalar values)
`jsonb_path_query_array('[1, "a", 1, 3]', '$[*] ? (@ == 1)')` → `[1, 1]`
`jsonb_path_query_array('[1, "a", 1, 3]', '$[*] ? (@ == "a")')` → `["a"]`  
_`value`_ `!=` _`value`_ → `boolean` _`value`_ `<>` _`value`_ → `boolean` Non-
equality comparison `jsonb_path_query_array('[1, 2, 1, 3]', '$[*] ? (@ !=
1)')` → `[2, 3]` `jsonb_path_query_array('["a", "b", "c"]', '$[*] ? (@ <>
"b")')` → `["a", "c"]`  
_`value`_ `<` _`value`_ → `boolean` Less-than comparison
`jsonb_path_query_array('[1, 2, 3]', '$[*] ? (@ < 2)')` → `[1]`  
_`value`_ `<=` _`value`_ → `boolean` Less-than-or-equal-to comparison
`jsonb_path_query_array('["a", "b", "c"]', '$[*] ? (@ <= "b")')` → `["a",
"b"]`  
_`value`_ `>` _`value`_ → `boolean` Greater-than comparison
`jsonb_path_query_array('[1, 2, 3]', '$[*] ? (@ > 2)')` → `[3]`  
_`value`_ `>=` _`value`_ → `boolean` Greater-than-or-equal-to comparison
`jsonb_path_query_array('[1, 2, 3]', '$[*] ? (@ >= 2)')` → `[2, 3]`  
`true` → `boolean` JSON constant `true` `jsonb_path_query('[{"name": "John",
"parent": false}, {"name": "Chris", "parent": true}]', '$[*] ? (@.parent ==
true)')` → `{"name": "Chris", "parent": true}`  
`false` → `boolean` JSON constant `false` `jsonb_path_query('[{"name": "John",
"parent": false}, {"name": "Chris", "parent": true}]', '$[*] ? (@.parent ==
false)')` → `{"name": "John", "parent": false}`  
`null` → `_`value`_` JSON constant `null` (note that, unlike in SQL,
comparison to `null` works normally) `jsonb_path_query('[{"name": "Mary",
"job": null}, {"name": "Michael", "job": "driver"}]', '$[*] ? (@.job == null)
.name')` → `"Mary"`  
_`boolean`_ `&&` _`boolean`_ → `boolean` Boolean AND `jsonb_path_query('[1, 3,
7]', '$[*] ? (@ > 1 && @ < 5)')` → `3`  
_`boolean`_ `||` _`boolean`_ → `boolean` Boolean OR `jsonb_path_query('[1, 3,
7]', '$[*] ? (@ < 1 || @ > 5)')` → `7`  
`!` _`boolean`_ → `boolean` Boolean NOT `jsonb_path_query('[1, 3, 7]', '$[*] ?
(!(@ < 5))')` → `7`  
_`boolean`_ `is unknown` → `boolean` Tests whether a Boolean condition is
`unknown`. `jsonb_path_query('[-1, 2, 7, "foo"]', '$[*] ? ((@ > 0) is
unknown)')` → `"foo"`  
_`string`_ `like_regex` _`string`_ [ `flag` _`string`_ ] → `boolean` Tests
whether the first operand matches the regular expression given by the second
operand, optionally with modifications described by a string of `flag`
characters (see [Section 9.16.2.3](functions-json.html#JSONPATH-REGULAR-
EXPRESSIONS "9.16.2.3. SQL/JSON Regular Expressions")).
`jsonb_path_query_array('["abc", "abd", "aBdC", "abdacb", "babc"]', '$[*] ? (@
like_regex "^ab.*c")')` → `["abc", "abdacb"]` `jsonb_path_query_array('["abc",
"abd", "aBdC", "abdacb", "babc"]', '$[*] ? (@ like_regex "^ab.*c" flag "i")')`
→ `["abc", "aBdC", "abdacb"]`  
_`string`_ `starts with` _`string`_ → `boolean` Tests whether the second
operand is an initial substring of the first operand.
`jsonb_path_query('["John Smith", "Mary Stone", "Bob Johnson"]', '$[*] ? (@
starts with "John")')` → `"John Smith"`  
`exists` `(` _`path_expression`_ `)` → `boolean` Tests whether a path
expression matches at least one SQL/JSON item. Returns `unknown` if the path
expression would result in an error; the second example uses this to avoid a
no-such-key error in strict mode. `jsonb_path_query('{"x": [1, 2], "y": [2,
4]}', 'strict $.* ? (exists (@ ? (@[*] > 2)))')` → `[2, 4]`
`jsonb_path_query_array('{"value": 41}', 'strict $ ? (exists (@.name))
.name')` → `[]`  
  
  

#### 9.16.2.3. SQL/JSON Regular Expressions #

SQL/JSON path expressions allow matching text to a regular expression with the
`like_regex` filter. For example, the following SQL/JSON path query would
case-insensitively match all strings in an array that start with an English
vowel:

    
    
    $[*] ? (@ like_regex "^[aeiou]" flag "i")
    

The optional `flag` string may include one or more of the characters `i` for
case-insensitive match, `m` to allow `^` and `$` to match at newlines, `s` to
allow `.` to match a newline, and `q` to quote the whole pattern (reducing the
behavior to a simple substring match).

The SQL/JSON standard borrows its definition for regular expressions from the
`LIKE_REGEX` operator, which in turn uses the XQuery standard. PostgreSQL does
not currently support the `LIKE_REGEX` operator. Therefore, the `like_regex`
filter is implemented using the POSIX regular expression engine described in
[Section 9.7.3](functions-matching.html#FUNCTIONS-POSIX-REGEXP "9.7.3. POSIX
Regular Expressions"). This leads to various minor discrepancies from standard
SQL/JSON behavior, which are cataloged in [Section 9.7.3.8](functions-
matching.html#POSIX-VS-XQUERY "9.7.3.8. Differences from SQL Standard and
XQuery"). Note, however, that the flag-letter incompatibilities described
there do not apply to SQL/JSON, as it translates the XQuery flag letters to
match what the POSIX engine expects.

Keep in mind that the pattern argument of `like_regex` is a JSON path string
literal, written according to the rules given in [Section 8.14.7](datatype-
json.html#DATATYPE-JSONPATH "8.14.7. jsonpath Type"). This means in particular
that any backslashes you want to use in the regular expression must be
doubled. For example, to match string values of the root document that contain
only digits:

    
    
    $.* ? (@ like_regex "^\\d+$")
    

* * *

[Prev](functions-xml.html "9.15. XML Functions")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](functions-sequence.html "9.17. Sequence Manipulation Functions")  
---|---|---  
9.15. XML Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  9.17. Sequence Manipulation Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-json.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

