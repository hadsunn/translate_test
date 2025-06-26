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

Supported Versions: [Current](/docs/current/sql-alteropfamily.html "PostgreSQL
17 - ALTER OPERATOR FAMILY") ([17](/docs/17/sql-alteropfamily.html "PostgreSQL
17 - ALTER OPERATOR FAMILY")) / [16](/docs/16/sql-alteropfamily.html
"PostgreSQL 16 - ALTER OPERATOR FAMILY") / [15](/docs/15/sql-
alteropfamily.html "PostgreSQL 15 - ALTER OPERATOR FAMILY") /
[14](/docs/14/sql-alteropfamily.html "PostgreSQL 14 - ALTER OPERATOR FAMILY")
/ [13](/docs/13/sql-alteropfamily.html "PostgreSQL 13 - ALTER OPERATOR
FAMILY")

Development Versions: [18](/docs/18/sql-alteropfamily.html "PostgreSQL 18 -
ALTER OPERATOR FAMILY") / [devel](/docs/devel/sql-alteropfamily.html
"PostgreSQL devel - ALTER OPERATOR FAMILY")

Unsupported versions: [12](/docs/12/sql-alteropfamily.html "PostgreSQL 12 -
ALTER OPERATOR FAMILY") / [11](/docs/11/sql-alteropfamily.html "PostgreSQL 11
- ALTER OPERATOR FAMILY") / [10](/docs/10/sql-alteropfamily.html "PostgreSQL
10 - ALTER OPERATOR FAMILY") / [9.6](/docs/9.6/sql-alteropfamily.html
"PostgreSQL 9.6 - ALTER OPERATOR FAMILY") / [9.5](/docs/9.5/sql-
alteropfamily.html "PostgreSQL 9.5 - ALTER OPERATOR FAMILY") /
[9.4](/docs/9.4/sql-alteropfamily.html "PostgreSQL 9.4 - ALTER OPERATOR
FAMILY") / [9.3](/docs/9.3/sql-alteropfamily.html "PostgreSQL 9.3 - ALTER
OPERATOR FAMILY") / [9.2](/docs/9.2/sql-alteropfamily.html "PostgreSQL 9.2 -
ALTER OPERATOR FAMILY") / [9.1](/docs/9.1/sql-alteropfamily.html "PostgreSQL
9.1 - ALTER OPERATOR FAMILY") / [9.0](/docs/9.0/sql-alteropfamily.html
"PostgreSQL 9.0 - ALTER OPERATOR FAMILY") / [8.4](/docs/8.4/sql-
alteropfamily.html "PostgreSQL 8.4 - ALTER OPERATOR FAMILY") /
[8.3](/docs/8.3/sql-alteropfamily.html "PostgreSQL 8.3 - ALTER OPERATOR
FAMILY")

__

ALTER OPERATOR FAMILY  
---  
[Prev](sql-alteropclass.html "ALTER OPERATOR CLASS")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterpolicy.html "ALTER POLICY")  
  
* * *

## ALTER OPERATOR FAMILY

ALTER OPERATOR FAMILY — change the definition of an operator family

## Synopsis

    
    
    ALTER OPERATOR FAMILY _name_ USING _index_method_ ADD
      {  OPERATOR _strategy_number_ _operator_name_ ( _op_type_ , _op_type_ )
                  [ FOR SEARCH | FOR ORDER BY _sort_family_name_ ]
       | FUNCTION _support_number_ [ ( _op_type_ [ , _op_type_ ] ) ]
                  _function_name_ [ ( _argument_type_ [, ...] ) ]
      } [, ... ]
    
    ALTER OPERATOR FAMILY _name_ USING _index_method_ DROP
      {  OPERATOR _strategy_number_ ( _op_type_ [ , _op_type_ ] )
       | FUNCTION _support_number_ ( _op_type_ [ , _op_type_ ] )
      } [, ... ]
    
    ALTER OPERATOR FAMILY _name_ USING _index_method_
        RENAME TO _new_name_
    
    ALTER OPERATOR FAMILY _name_ USING _index_method_
        OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    
    ALTER OPERATOR FAMILY _name_ USING _index_method_
        SET SCHEMA _new_schema_
    

## Description

`ALTER OPERATOR FAMILY` changes the definition of an operator family. You can
add operators and support functions to the family, remove them from the
family, or change the family's name or owner.

When operators and support functions are added to a family with `ALTER
OPERATOR FAMILY`, they are not part of any specific operator class within the
family, but are just “loose” within the family. This indicates that these
operators and functions are compatible with the family's semantics, but are
not required for correct functioning of any specific index. (Operators and
functions that are so required should be declared as part of an operator
class, instead; see [CREATE OPERATOR CLASS](sql-createopclass.html "CREATE
OPERATOR CLASS").) PostgreSQL will allow loose members of a family to be
dropped from the family at any time, but members of an operator class cannot
be dropped without dropping the whole class and any indexes that depend on it.
Typically, single-data-type operators and functions are part of operator
classes because they are needed to support an index on that specific data
type, while cross-data-type operators and functions are made loose members of
the family.

You must be a superuser to use `ALTER OPERATOR FAMILY`. (This restriction is
made because an erroneous operator family definition could confuse or even
crash the server.)

`ALTER OPERATOR FAMILY` does not presently check whether the operator family
definition includes all the operators and functions required by the index
method, nor whether the operators and functions form a self-consistent set. It
is the user's responsibility to define a valid operator family.

Refer to [Section 38.16](xindex.html "38.16. Interfacing Extensions to
Indexes") for further information.

## Parameters

_`name`_

    

The name (optionally schema-qualified) of an existing operator family.

_`index_method`_

    

The name of the index method this operator family is for.

_`strategy_number`_

    

The index method's strategy number for an operator associated with the
operator family.

_`operator_name`_

    

The name (optionally schema-qualified) of an operator associated with the
operator family.

_`op_type`_

    

In an `OPERATOR` clause, the operand data type(s) of the operator, or `NONE`
to signify a prefix operator. Unlike the comparable syntax in `CREATE OPERATOR
CLASS`, the operand data types must always be specified.

In an `ADD FUNCTION` clause, the operand data type(s) the function is intended
to support, if different from the input data type(s) of the function. For
B-tree comparison functions and hash functions it is not necessary to specify
_`op_type`_ since the function's input data type(s) are always the correct
ones to use. For B-tree sort support functions, B-Tree equal image functions,
and all functions in GiST, SP-GiST and GIN operator classes, it is necessary
to specify the operand data type(s) the function is to be used with.

In a `DROP FUNCTION` clause, the operand data type(s) the function is intended
to support must be specified.

_`sort_family_name`_

    

The name (optionally schema-qualified) of an existing `btree` operator family
that describes the sort ordering associated with an ordering operator.

If neither `FOR SEARCH` nor `FOR ORDER BY` is specified, `FOR SEARCH` is the
default.

_`support_number`_

    

The index method's support function number for a function associated with the
operator family.

_`function_name`_

    

The name (optionally schema-qualified) of a function that is an index method
support function for the operator family. If no argument list is specified,
the name must be unique in its schema.

_`argument_type`_

    

The parameter data type(s) of the function.

_`new_name`_

    

The new name of the operator family.

_`new_owner`_

    

The new owner of the operator family.

_`new_schema`_

    

The new schema for the operator family.

The `OPERATOR` and `FUNCTION` clauses can appear in any order.

## Notes

Notice that the `DROP` syntax only specifies the “slot” in the operator
family, by strategy or support number and input data type(s). The name of the
operator or function occupying the slot is not mentioned. Also, for `DROP
FUNCTION` the type(s) to specify are the input data type(s) the function is
intended to support; for GiST, SP-GiST and GIN indexes this might have nothing
to do with the actual input argument types of the function.

Because the index machinery does not check access permissions on functions
before using them, including a function or operator in an operator family is
tantamount to granting public execute permission on it. This is usually not an
issue for the sorts of functions that are useful in an operator family.

The operators should not be defined by SQL functions. An SQL function is
likely to be inlined into the calling query, which will prevent the optimizer
from recognizing that the query matches an index.

Before PostgreSQL 8.4, the `OPERATOR` clause could include a `RECHECK` option.
This is no longer supported because whether an index operator is “lossy” is
now determined on-the-fly at run time. This allows efficient handling of cases
where an operator might or might not be lossy.

## Examples

The following example command adds cross-data-type operators and support
functions to an operator family that already contains B-tree operator classes
for data types `int4` and `int2`.

    
    
    ALTER OPERATOR FAMILY integer_ops USING btree ADD
    
      -- int4 vs int2
      OPERATOR 1 < (int4, int2) ,
      OPERATOR 2 <= (int4, int2) ,
      OPERATOR 3 = (int4, int2) ,
      OPERATOR 4 >= (int4, int2) ,
      OPERATOR 5 > (int4, int2) ,
      FUNCTION 1 btint42cmp(int4, int2) ,
    
      -- int2 vs int4
      OPERATOR 1 < (int2, int4) ,
      OPERATOR 2 <= (int2, int4) ,
      OPERATOR 3 = (int2, int4) ,
      OPERATOR 4 >= (int2, int4) ,
      OPERATOR 5 > (int2, int4) ,
      FUNCTION 1 btint24cmp(int2, int4) ;
    

To remove these entries again:

    
    
    ALTER OPERATOR FAMILY integer_ops USING btree DROP
    
      -- int4 vs int2
      OPERATOR 1 (int4, int2) ,
      OPERATOR 2 (int4, int2) ,
      OPERATOR 3 (int4, int2) ,
      OPERATOR 4 (int4, int2) ,
      OPERATOR 5 (int4, int2) ,
      FUNCTION 1 (int4, int2) ,
    
      -- int2 vs int4
      OPERATOR 1 (int2, int4) ,
      OPERATOR 2 (int2, int4) ,
      OPERATOR 3 (int2, int4) ,
      OPERATOR 4 (int2, int4) ,
      OPERATOR 5 (int2, int4) ,
      FUNCTION 1 (int2, int4) ;
    

## Compatibility

There is no `ALTER OPERATOR FAMILY` statement in the SQL standard.

## See Also

[CREATE OPERATOR FAMILY](sql-createopfamily.html "CREATE OPERATOR FAMILY"),
[DROP OPERATOR FAMILY](sql-dropopfamily.html "DROP OPERATOR FAMILY"), [CREATE
OPERATOR CLASS](sql-createopclass.html "CREATE OPERATOR CLASS"), [ALTER
OPERATOR CLASS](sql-alteropclass.html "ALTER OPERATOR CLASS"), [DROP OPERATOR
CLASS](sql-dropopclass.html "DROP OPERATOR CLASS")

* * *

[Prev](sql-alteropclass.html "ALTER OPERATOR CLASS")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterpolicy.html "ALTER POLICY")  
---|---|---  
ALTER OPERATOR CLASS  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER POLICY  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alteropfamily.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

