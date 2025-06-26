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

Supported Versions: [Current](/docs/current/plpython-data.html "PostgreSQL 17
- 46.2. Data Values") ([17](/docs/17/plpython-data.html "PostgreSQL 17 -
46.2. Data Values")) / [16](/docs/16/plpython-data.html "PostgreSQL 16 -
46.2. Data Values") / [15](/docs/15/plpython-data.html "PostgreSQL 15 -
46.2. Data Values") / [14](/docs/14/plpython-data.html "PostgreSQL 14 -
46.2. Data Values") / [13](/docs/13/plpython-data.html "PostgreSQL 13 -
46.2. Data Values")

Development Versions: [18](/docs/18/plpython-data.html "PostgreSQL 18 -
46.2. Data Values") / [devel](/docs/devel/plpython-data.html "PostgreSQL devel
- 46.2. Data Values")

Unsupported versions: [12](/docs/12/plpython-data.html "PostgreSQL 12 -
46.2. Data Values") / [11](/docs/11/plpython-data.html "PostgreSQL 11 -
46.2. Data Values") / [10](/docs/10/plpython-data.html "PostgreSQL 10 -
46.2. Data Values") / [9.6](/docs/9.6/plpython-data.html "PostgreSQL 9.6 -
46.2. Data Values") / [9.5](/docs/9.5/plpython-data.html "PostgreSQL 9.5 -
46.2. Data Values") / [9.4](/docs/9.4/plpython-data.html "PostgreSQL 9.4 -
46.2. Data Values") / [9.3](/docs/9.3/plpython-data.html "PostgreSQL 9.3 -
46.2. Data Values") / [9.2](/docs/9.2/plpython-data.html "PostgreSQL 9.2 -
46.2. Data Values") / [9.1](/docs/9.1/plpython-data.html "PostgreSQL 9.1 -
46.2. Data Values") / [9.0](/docs/9.0/plpython-data.html "PostgreSQL 9.0 -
46.2. Data Values")

__

46.2. Data Values  
---  
[Prev](plpython-funcs.html "46.1. PL/Python Functions")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") | Chapter 46. PL/Python — Python Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpython-sharing.html "46.3. Sharing Data")  
  
* * *

## 46.2. Data Values #

[46.2.1. Data Type Mapping](plpython-data.html#PLPYTHON-DATA-TYPE-MAPPING)

[46.2.2. Null, None](plpython-data.html#PLPYTHON-DATA-NULL)

[46.2.3. Arrays, Lists](plpython-data.html#PLPYTHON-ARRAYS)

[46.2.4. Composite Types](plpython-data.html#PLPYTHON-DATA-COMPOSITE-TYPES)

[46.2.5. Set-Returning Functions](plpython-data.html#PLPYTHON-DATA-SET-
RETURNING-FUNCS)

Generally speaking, the aim of PL/Python is to provide a “natural” mapping
between the PostgreSQL and the Python worlds. This informs the data mapping
rules described below.

### 46.2.1. Data Type Mapping #

When a PL/Python function is called, its arguments are converted from their
PostgreSQL data type to a corresponding Python type:

  * PostgreSQL `boolean` is converted to Python `bool`.

  * PostgreSQL `smallint`, `int`, `bigint` and `oid` are converted to Python `int`.

  * PostgreSQL `real` and `double` are converted to Python `float`.

  * PostgreSQL `numeric` is converted to Python `Decimal`. This type is imported from the `cdecimal` package if that is available. Otherwise, `decimal.Decimal` from the standard library will be used. `cdecimal` is significantly faster than `decimal`. In Python 3.3 and up, however, `cdecimal` has been integrated into the standard library under the name `decimal`, so there is no longer any difference.

  * PostgreSQL `bytea` is converted to Python `bytes`.

  * All other data types, including the PostgreSQL character string types, are converted to a Python `str` (in Unicode like all Python strings).

  * For nonscalar data types, see below.

When a PL/Python function returns, its return value is converted to the
function's declared PostgreSQL return data type as follows:

  * When the PostgreSQL return type is `boolean`, the return value will be evaluated for truth according to the _Python_ rules. That is, 0 and empty string are false, but notably `'f'` is true.

  * When the PostgreSQL return type is `bytea`, the return value will be converted to Python `bytes` using the respective Python built-ins, with the result being converted to `bytea`.

  * For all other PostgreSQL return types, the return value is converted to a string using the Python built-in `str`, and the result is passed to the input function of the PostgreSQL data type. (If the Python value is a `float`, it is converted using the `repr` built-in instead of `str`, to avoid loss of precision.)

Strings are automatically converted to the PostgreSQL server encoding when
they are passed to PostgreSQL.

  * For nonscalar data types, see below.

Note that logical mismatches between the declared PostgreSQL return type and
the Python data type of the actual return object are not flagged; the value
will be converted in any case.

### 46.2.2. Null, None #

If an SQL null value is passed to a function, the argument value will appear
as `None` in Python. For example, the function definition of `pymax` shown in
[Section 46.1](plpython-funcs.html "46.1. PL/Python Functions") will return
the wrong answer for null inputs. We could add `STRICT` to the function
definition to make PostgreSQL do something more reasonable: if a null value is
passed, the function will not be called at all, but will just return a null
result automatically. Alternatively, we could check for null inputs in the
function body:

    
    
    CREATE FUNCTION pymax (a integer, b integer)
      RETURNS integer
    AS $$
      if (a is None) or (b is None):
        return None
      if a > b:
        return a
      return b
    $$ LANGUAGE plpython3u;
    

As shown above, to return an SQL null value from a PL/Python function, return
the value `None`. This can be done whether the function is strict or not.

### 46.2.3. Arrays, Lists #

SQL array values are passed into PL/Python as a Python list. To return an SQL
array value out of a PL/Python function, return a Python list:

    
    
    CREATE FUNCTION return_arr()
      RETURNS int[]
    AS $$
    return [1, 2, 3, 4, 5]
    $$ LANGUAGE plpython3u;
    
    SELECT return_arr();
     return_arr
    -------------
     {1,2,3,4,5}
    (1 row)
    

Multidimensional arrays are passed into PL/Python as nested Python lists. A
2-dimensional array is a list of lists, for example. When returning a multi-
dimensional SQL array out of a PL/Python function, the inner lists at each
level must all be of the same size. For example:

    
    
    CREATE FUNCTION test_type_conversion_array_int4(x int4[]) RETURNS int4[] AS $$
    plpy.info(x, type(x))
    return x
    $$ LANGUAGE plpython3u;
    
    SELECT * FROM test_type_conversion_array_int4(ARRAY[[1,2,3],[4,5,6]]);
    INFO:  ([[1, 2, 3], [4, 5, 6]], <type 'list'>)
     test_type_conversion_array_int4
    ---------------------------------
     {{1,2,3},{4,5,6}}
    (1 row)
    

Other Python sequences, like tuples, are also accepted for backwards-
compatibility with PostgreSQL versions 9.6 and below, when multi-dimensional
arrays were not supported. However, they are always treated as one-dimensional
arrays, because they are ambiguous with composite types. For the same reason,
when a composite type is used in a multi-dimensional array, it must be
represented by a tuple, rather than a list.

Note that in Python, strings are sequences, which can have undesirable effects
that might be familiar to Python programmers:

    
    
    CREATE FUNCTION return_str_arr()
      RETURNS varchar[]
    AS $$
    return "hello"
    $$ LANGUAGE plpython3u;
    
    SELECT return_str_arr();
     return_str_arr
    ----------------
     {h,e,l,l,o}
    (1 row)
    

### 46.2.4. Composite Types #

Composite-type arguments are passed to the function as Python mappings. The
element names of the mapping are the attribute names of the composite type. If
an attribute in the passed row has the null value, it has the value `None` in
the mapping. Here is an example:

    
    
    CREATE TABLE employee (
      name text,
      salary integer,
      age integer
    );
    
    CREATE FUNCTION overpaid (e employee)
      RETURNS boolean
    AS $$
      if e["salary"] > 200000:
        return True
      if (e["age"] < 30) and (e["salary"] > 100000):
        return True
      return False
    $$ LANGUAGE plpython3u;
    

There are multiple ways to return row or composite types from a Python
function. The following examples assume we have:

    
    
    CREATE TYPE named_value AS (
      name   text,
      value  integer
    );
    

A composite result can be returned as a:

Sequence type (a tuple or list, but not a set because it is not indexable)

    

Returned sequence objects must have the same number of items as the composite
result type has fields. The item with index 0 is assigned to the first field
of the composite type, 1 to the second and so on. For example:

    
    
    CREATE FUNCTION make_pair (name text, value integer)
      RETURNS named_value
    AS $$
      return ( name, value )
      # or alternatively, as list: return [ name, value ]
    $$ LANGUAGE plpython3u;
    

To return an SQL null for any column, insert `None` at the corresponding
position.

When an array of composite types is returned, it cannot be returned as a list,
because it is ambiguous whether the Python list represents a composite type,
or another array dimension.

Mapping (dictionary)

    

The value for each result type column is retrieved from the mapping with the
column name as key. Example:

    
    
    CREATE FUNCTION make_pair (name text, value integer)
      RETURNS named_value
    AS $$
      return { "name": name, "value": value }
    $$ LANGUAGE plpython3u;
    

Any extra dictionary key/value pairs are ignored. Missing keys are treated as
errors. To return an SQL null value for any column, insert `None` with the
corresponding column name as the key.

Object (any object providing method `__getattr__`)

    

This works the same as a mapping. Example:

    
    
    CREATE FUNCTION make_pair (name text, value integer)
      RETURNS named_value
    AS $$
      class named_value:
        def __init__ (self, n, v):
          self.name = n
          self.value = v
      return named_value(name, value)
    
      # or simply
      class nv: pass
      nv.name = name
      nv.value = value
      return nv
    $$ LANGUAGE plpython3u;
    

Functions with `OUT` parameters are also supported. For example:

    
    
    CREATE FUNCTION multiout_simple(OUT i integer, OUT j integer) AS $$
    return (1, 2)
    $$ LANGUAGE plpython3u;
    
    SELECT * FROM multiout_simple();
    

Output parameters of procedures are passed back the same way. For example:

    
    
    CREATE PROCEDURE python_triple(INOUT a integer, INOUT b integer) AS $$
    return (a * 3, b * 3)
    $$ LANGUAGE plpython3u;
    
    CALL python_triple(5, 10);
    

### 46.2.5. Set-Returning Functions #

A PL/Python function can also return sets of scalar or composite types. There
are several ways to achieve this because the returned object is internally
turned into an iterator. The following examples assume we have composite type:

    
    
    CREATE TYPE greeting AS (
      how text,
      who text
    );
    

A set result can be returned from a:

Sequence type (tuple, list, set)

    
    
    
    CREATE FUNCTION greet (how text)
      RETURNS SETOF greeting
    AS $$
      # return tuple containing lists as composite types
      # all other combinations work also
      return ( [ how, "World" ], [ how, "PostgreSQL" ], [ how, "PL/Python" ] )
    $$ LANGUAGE plpython3u;
    

Iterator (any object providing `__iter__` and `__next__` methods)

    
    
    
    CREATE FUNCTION greet (how text)
      RETURNS SETOF greeting
    AS $$
      class producer:
        def __init__ (self, how, who):
          self.how = how
          self.who = who
          self.ndx = -1
    
        def __iter__ (self):
          return self
    
        def __next__(self):
          self.ndx += 1
          if self.ndx == len(self.who):
            raise StopIteration
          return ( self.how, self.who[self.ndx] )
    
      return producer(how, [ "World", "PostgreSQL", "PL/Python" ])
    $$ LANGUAGE plpython3u;
    

Generator (`yield`)

    
    
    
    CREATE FUNCTION greet (how text)
      RETURNS SETOF greeting
    AS $$
      for who in [ "World", "PostgreSQL", "PL/Python" ]:
        yield ( how, who )
    $$ LANGUAGE plpython3u;
    

Set-returning functions with `OUT` parameters (using `RETURNS SETOF record`)
are also supported. For example:

    
    
    CREATE FUNCTION multiout_simple_setof(n integer, OUT integer, OUT integer) RETURNS SETOF record AS $$
    return [(1, 2)] * n
    $$ LANGUAGE plpython3u;
    
    SELECT * FROM multiout_simple_setof(3);
    

* * *

[Prev](plpython-funcs.html "46.1. PL/Python Functions")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") |  [Next](plpython-sharing.html "46.3. Sharing Data")  
---|---|---  
46.1. PL/Python Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  46.3. Sharing Data  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpython-data.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

