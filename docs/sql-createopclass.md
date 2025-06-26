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

Supported Versions: [Current](/docs/current/sql-createopclass.html "PostgreSQL
17 - CREATE OPERATOR CLASS") ([17](/docs/17/sql-createopclass.html "PostgreSQL
17 - CREATE OPERATOR CLASS")) / [16](/docs/16/sql-createopclass.html
"PostgreSQL 16 - CREATE OPERATOR CLASS") / [15](/docs/15/sql-
createopclass.html "PostgreSQL 15 - CREATE OPERATOR CLASS") /
[14](/docs/14/sql-createopclass.html "PostgreSQL 14 - CREATE OPERATOR CLASS")
/ [13](/docs/13/sql-createopclass.html "PostgreSQL 13 - CREATE OPERATOR
CLASS")

Development Versions: [18](/docs/18/sql-createopclass.html "PostgreSQL 18 -
CREATE OPERATOR CLASS") / [devel](/docs/devel/sql-createopclass.html
"PostgreSQL devel - CREATE OPERATOR CLASS")

Unsupported versions: [12](/docs/12/sql-createopclass.html "PostgreSQL 12 -
CREATE OPERATOR CLASS") / [11](/docs/11/sql-createopclass.html "PostgreSQL 11
- CREATE OPERATOR CLASS") / [10](/docs/10/sql-createopclass.html "PostgreSQL
10 - CREATE OPERATOR CLASS") / [9.6](/docs/9.6/sql-createopclass.html
"PostgreSQL 9.6 - CREATE OPERATOR CLASS") / [9.5](/docs/9.5/sql-
createopclass.html "PostgreSQL 9.5 - CREATE OPERATOR CLASS") /
[9.4](/docs/9.4/sql-createopclass.html "PostgreSQL 9.4 - CREATE OPERATOR
CLASS") / [9.3](/docs/9.3/sql-createopclass.html "PostgreSQL 9.3 - CREATE
OPERATOR CLASS") / [9.2](/docs/9.2/sql-createopclass.html "PostgreSQL 9.2 -
CREATE OPERATOR CLASS") / [9.1](/docs/9.1/sql-createopclass.html "PostgreSQL
9.1 - CREATE OPERATOR CLASS") / [9.0](/docs/9.0/sql-createopclass.html
"PostgreSQL 9.0 - CREATE OPERATOR CLASS") / [8.4](/docs/8.4/sql-
createopclass.html "PostgreSQL 8.4 - CREATE OPERATOR CLASS") /
[8.3](/docs/8.3/sql-createopclass.html "PostgreSQL 8.3 - CREATE OPERATOR
CLASS") / [8.2](/docs/8.2/sql-createopclass.html "PostgreSQL 8.2 - CREATE
OPERATOR CLASS") / [8.1](/docs/8.1/sql-createopclass.html "PostgreSQL 8.1 -
CREATE OPERATOR CLASS") / [8.0](/docs/8.0/sql-createopclass.html "PostgreSQL
8.0 - CREATE OPERATOR CLASS") / [7.4](/docs/7.4/sql-createopclass.html
"PostgreSQL 7.4 - CREATE OPERATOR CLASS") / [7.3](/docs/7.3/sql-
createopclass.html "PostgreSQL 7.3 - CREATE OPERATOR CLASS")

__

CREATE OPERATOR CLASS  
---  
[Prev](sql-createoperator.html "CREATE OPERATOR")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createopfamily.html "CREATE OPERATOR FAMILY")  
  
* * *

## CREATE OPERATOR CLASS

CREATE OPERATOR CLASS — define a new operator class

## Synopsis

    
    
    CREATE OPERATOR CLASS _name_ [ DEFAULT ] FOR TYPE _data_type_
      USING _index_method_ [ FAMILY _family_name_ ] AS
      {  OPERATOR _strategy_number_ _operator_name_ [ ( _op_type_ , _op_type_ ) ] [ FOR SEARCH | FOR ORDER BY _sort_family_name_ ]
       | FUNCTION _support_number_ [ ( _op_type_ [ , _op_type_ ] ) ] _function_name_ ( _argument_type_ [, ...] )
       | STORAGE _storage_type_
      } [, ... ]
    

## Description

`CREATE OPERATOR CLASS` creates a new operator class. An operator class
defines how a particular data type can be used with an index. The operator
class specifies that certain operators will fill particular roles or
“strategies” for this data type and this index method. The operator class also
specifies the support functions to be used by the index method when the
operator class is selected for an index column. All the operators and
functions used by an operator class must be defined before the operator class
can be created.

If a schema name is given then the operator class is created in the specified
schema. Otherwise it is created in the current schema. Two operator classes in
the same schema can have the same name only if they are for different index
methods.

The user who defines an operator class becomes its owner. Presently, the
creating user must be a superuser. (This restriction is made because an
erroneous operator class definition could confuse or even crash the server.)

`CREATE OPERATOR CLASS` does not presently check whether the operator class
definition includes all the operators and functions required by the index
method, nor whether the operators and functions form a self-consistent set. It
is the user's responsibility to define a valid operator class.

Related operator classes can be grouped into _operator families_. To add a new
operator class to an existing family, specify the `FAMILY` option in `CREATE
OPERATOR CLASS`. Without this option, the new class is placed into a family
named the same as the new class (creating that family if it doesn't already
exist).

Refer to [Section 38.16](xindex.html "38.16. Interfacing Extensions to
Indexes") for further information.

## Parameters

_`name`_

    

The name of the operator class to be created. The name can be schema-
qualified.

`DEFAULT`

    

If present, the operator class will become the default operator class for its
data type. At most one operator class can be the default for a specific data
type and index method.

_`data_type`_

    

The column data type that this operator class is for.

_`index_method`_

    

The name of the index method this operator class is for.

_`family_name`_

    

The name of the existing operator family to add this operator class to. If not
specified, a family named the same as the operator class is used (creating it,
if it doesn't already exist).

_`strategy_number`_

    

The index method's strategy number for an operator associated with the
operator class.

_`operator_name`_

    

The name (optionally schema-qualified) of an operator associated with the
operator class.

_`op_type`_

    

In an `OPERATOR` clause, the operand data type(s) of the operator, or `NONE`
to signify a prefix operator. The operand data types can be omitted in the
normal case where they are the same as the operator class's data type.

In a `FUNCTION` clause, the operand data type(s) the function is intended to
support, if different from the input data type(s) of the function (for B-tree
comparison functions and hash functions) or the class's data type (for B-tree
sort support functions, B-tree equal image functions, and all functions in
GiST, SP-GiST, GIN and BRIN operator classes). These defaults are correct, and
so _`op_type`_ need not be specified in `FUNCTION` clauses, except for the
case of a B-tree sort support function that is meant to support cross-data-
type comparisons.

_`sort_family_name`_

    

The name (optionally schema-qualified) of an existing `btree` operator family
that describes the sort ordering associated with an ordering operator.

If neither `FOR SEARCH` nor `FOR ORDER BY` is specified, `FOR SEARCH` is the
default.

_`support_number`_

    

The index method's support function number for a function associated with the
operator class.

_`function_name`_

    

The name (optionally schema-qualified) of a function that is an index method
support function for the operator class.

_`argument_type`_

    

The parameter data type(s) of the function.

_`storage_type`_

    

The data type actually stored in the index. Normally this is the same as the
column data type, but some index methods (currently GiST, GIN, SP-GiST and
BRIN) allow it to be different. The `STORAGE` clause must be omitted unless
the index method allows a different type to be used. If the column
_`data_type`_ is specified as `anyarray`, the _`storage_type`_ can be declared
as `anyelement` to indicate that the index entries are members of the element
type belonging to the actual array type that each particular index is created
for.

The `OPERATOR`, `FUNCTION`, and `STORAGE` clauses can appear in any order.

## Notes

Because the index machinery does not check access permissions on functions
before using them, including a function or operator in an operator class is
tantamount to granting public execute permission on it. This is usually not an
issue for the sorts of functions that are useful in an operator class.

The operators should not be defined by SQL functions. An SQL function is
likely to be inlined into the calling query, which will prevent the optimizer
from recognizing that the query matches an index.

Before PostgreSQL 8.4, the `OPERATOR` clause could include a `RECHECK` option.
This is no longer supported because whether an index operator is “lossy” is
now determined on-the-fly at run time. This allows efficient handling of cases
where an operator might or might not be lossy.

## Examples

The following example command defines a GiST index operator class for the data
type `_int4` (array of `int4`). See the [intarray](intarray.html
"F.20. intarray — manipulate arrays of integers") module for the complete
example.

    
    
    CREATE OPERATOR CLASS gist__int_ops
        DEFAULT FOR TYPE _int4 USING gist AS
            OPERATOR        3       &&,
            OPERATOR        6       = (anyarray, anyarray),
            OPERATOR        7       @>,
            OPERATOR        8       <@,
            OPERATOR        20      @@ (_int4, query_int),
            FUNCTION        1       g_int_consistent (internal, _int4, smallint, oid, internal),
            FUNCTION        2       g_int_union (internal, internal),
            FUNCTION        3       g_int_compress (internal),
            FUNCTION        4       g_int_decompress (internal),
            FUNCTION        5       g_int_penalty (internal, internal, internal),
            FUNCTION        6       g_int_picksplit (internal, internal),
            FUNCTION        7       g_int_same (_int4, _int4, internal);
    

## Compatibility

`CREATE OPERATOR CLASS` is a PostgreSQL extension. There is no `CREATE
OPERATOR CLASS` statement in the SQL standard.

## See Also

[ALTER OPERATOR CLASS](sql-alteropclass.html "ALTER OPERATOR CLASS"), [DROP
OPERATOR CLASS](sql-dropopclass.html "DROP OPERATOR CLASS"), [CREATE OPERATOR
FAMILY](sql-createopfamily.html "CREATE OPERATOR FAMILY"), [ALTER OPERATOR
FAMILY](sql-alteropfamily.html "ALTER OPERATOR FAMILY")

* * *

[Prev](sql-createoperator.html "CREATE OPERATOR")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createopfamily.html "CREATE OPERATOR FAMILY")  
---|---|---  
CREATE OPERATOR  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE OPERATOR FAMILY  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createopclass.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

