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

Supported Versions: [Current](/docs/current/sql-createoperator.html
"PostgreSQL 17 - CREATE OPERATOR") ([17](/docs/17/sql-createoperator.html
"PostgreSQL 17 - CREATE OPERATOR")) / [16](/docs/16/sql-createoperator.html
"PostgreSQL 16 - CREATE OPERATOR") / [15](/docs/15/sql-createoperator.html
"PostgreSQL 15 - CREATE OPERATOR") / [14](/docs/14/sql-createoperator.html
"PostgreSQL 14 - CREATE OPERATOR") / [13](/docs/13/sql-createoperator.html
"PostgreSQL 13 - CREATE OPERATOR")

Development Versions: [18](/docs/18/sql-createoperator.html "PostgreSQL 18 -
CREATE OPERATOR") / [devel](/docs/devel/sql-createoperator.html "PostgreSQL
devel - CREATE OPERATOR")

Unsupported versions: [12](/docs/12/sql-createoperator.html "PostgreSQL 12 -
CREATE OPERATOR") / [11](/docs/11/sql-createoperator.html "PostgreSQL 11 -
CREATE OPERATOR") / [10](/docs/10/sql-createoperator.html "PostgreSQL 10 -
CREATE OPERATOR") / [9.6](/docs/9.6/sql-createoperator.html "PostgreSQL 9.6 -
CREATE OPERATOR") / [9.5](/docs/9.5/sql-createoperator.html "PostgreSQL 9.5 -
CREATE OPERATOR") / [9.4](/docs/9.4/sql-createoperator.html "PostgreSQL 9.4 -
CREATE OPERATOR") / [9.3](/docs/9.3/sql-createoperator.html "PostgreSQL 9.3 -
CREATE OPERATOR") / [9.2](/docs/9.2/sql-createoperator.html "PostgreSQL 9.2 -
CREATE OPERATOR") / [9.1](/docs/9.1/sql-createoperator.html "PostgreSQL 9.1 -
CREATE OPERATOR") / [9.0](/docs/9.0/sql-createoperator.html "PostgreSQL 9.0 -
CREATE OPERATOR") / [8.4](/docs/8.4/sql-createoperator.html "PostgreSQL 8.4 -
CREATE OPERATOR") / [8.3](/docs/8.3/sql-createoperator.html "PostgreSQL 8.3 -
CREATE OPERATOR") / [8.2](/docs/8.2/sql-createoperator.html "PostgreSQL 8.2 -
CREATE OPERATOR") / [8.1](/docs/8.1/sql-createoperator.html "PostgreSQL 8.1 -
CREATE OPERATOR") / [8.0](/docs/8.0/sql-createoperator.html "PostgreSQL 8.0 -
CREATE OPERATOR") / [7.4](/docs/7.4/sql-createoperator.html "PostgreSQL 7.4 -
CREATE OPERATOR") / [7.3](/docs/7.3/sql-createoperator.html "PostgreSQL 7.3 -
CREATE OPERATOR") / [7.2](/docs/7.2/sql-createoperator.html "PostgreSQL 7.2 -
CREATE OPERATOR") / [7.1](/docs/7.1/sql-createoperator.html "PostgreSQL 7.1 -
CREATE OPERATOR")

__

CREATE OPERATOR  
---  
[Prev](sql-creatematerializedview.html "CREATE MATERIALIZED VIEW")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createopclass.html "CREATE OPERATOR CLASS")  
  
* * *

## CREATE OPERATOR

CREATE OPERATOR — define a new operator

## Synopsis

    
    
    CREATE OPERATOR _name_ (
        {FUNCTION|PROCEDURE} = _function_name_
        [, LEFTARG = _left_type_ ] [, RIGHTARG = _right_type_ ]
        [, COMMUTATOR = _com_op_ ] [, NEGATOR = _neg_op_ ]
        [, RESTRICT = _res_proc_ ] [, JOIN = _join_proc_ ]
        [, HASHES ] [, MERGES ]
    )
    

## Description

`CREATE OPERATOR` defines a new operator, _`name`_. The user who defines an
operator becomes its owner. If a schema name is given then the operator is
created in the specified schema. Otherwise it is created in the current
schema.

The operator name is a sequence of up to `NAMEDATALEN`-1 (63 by default)
characters from the following list:

  
+ - * / < > = ~ ! @ # % ^ & | ` ?  

There are a few restrictions on your choice of name:

  * `--` and `/*` cannot appear anywhere in an operator name, since they will be taken as the start of a comment.

  * A multicharacter operator name cannot end in `+` or `-`, unless the name also contains at least one of these characters:

  
~ ! @ # % ^ & | ` ?  

For example, `@-` is an allowed operator name, but `*-` is not. This
restriction allows PostgreSQL to parse SQL-compliant commands without
requiring spaces between tokens.

  * The symbol `=>` is reserved by the SQL grammar, so it cannot be used as an operator name.

The operator `!=` is mapped to `<>` on input, so these two names are always
equivalent.

For binary operators, both `LEFTARG` and `RIGHTARG` must be defined. For
prefix operators only `RIGHTARG` should be defined. The _`function_name`_
function must have been previously defined using `CREATE FUNCTION` and must be
defined to accept the correct number of arguments (either one or two) of the
indicated types.

In the syntax of `CREATE OPERATOR`, the keywords `FUNCTION` and `PROCEDURE`
are equivalent, but the referenced function must in any case be a function,
not a procedure. The use of the keyword `PROCEDURE` here is historical and
deprecated.

The other clauses specify optional operator optimization clauses. Their
meaning is detailed in [Section 38.15](xoper-optimization.html
"38.15. Operator Optimization Information").

To be able to create an operator, you must have `USAGE` privilege on the
argument types and the return type, as well as `EXECUTE` privilege on the
underlying function. If a commutator or negator operator is specified, you
must own these operators.

## Parameters

_`name`_

    

The name of the operator to be defined. See above for allowable characters.
The name can be schema-qualified, for example `CREATE OPERATOR myschema.+
(...)`. If not, then the operator is created in the current schema. Two
operators in the same schema can have the same name if they operate on
different data types. This is called _overloading_.

_`function_name`_

    

The function used to implement this operator.

_`left_type`_

    

The data type of the operator's left operand, if any. This option would be
omitted for a prefix operator.

_`right_type`_

    

The data type of the operator's right operand.

_`com_op`_

    

The commutator of this operator.

_`neg_op`_

    

The negator of this operator.

_`res_proc`_

    

The restriction selectivity estimator function for this operator.

_`join_proc`_

    

The join selectivity estimator function for this operator.

`HASHES`

    

Indicates this operator can support a hash join.

`MERGES`

    

Indicates this operator can support a merge join.

To give a schema-qualified operator name in _`com_op`_ or the other optional
arguments, use the `OPERATOR()` syntax, for example:

    
    
    COMMUTATOR = OPERATOR(myschema.===) ,
    

## Notes

Refer to [Section 38.14](xoper.html "38.14. User-Defined Operators") for
further information.

It is not possible to specify an operator's lexical precedence in `CREATE
OPERATOR`, because the parser's precedence behavior is hard-wired. See
[Section 4.1.6](sql-syntax-lexical.html#SQL-PRECEDENCE "4.1.6. Operator
Precedence") for precedence details.

The obsolete options `SORT1`, `SORT2`, `LTCMP`, and `GTCMP` were formerly used
to specify the names of sort operators associated with a merge-joinable
operator. This is no longer necessary, since information about associated
operators is found by looking at B-tree operator families instead. If one of
these options is given, it is ignored except for implicitly setting `MERGES`
true.

Use [`DROP OPERATOR`](sql-dropoperator.html "DROP OPERATOR") to delete user-
defined operators from a database. Use [`ALTER OPERATOR`](sql-
alteroperator.html "ALTER OPERATOR") to modify operators in a database.

## Examples

The following command defines a new operator, area-equality, for the data type
`box`:

    
    
    CREATE OPERATOR === (
        LEFTARG = box,
        RIGHTARG = box,
        FUNCTION = area_equal_function,
        COMMUTATOR = ===,
        NEGATOR = !==,
        RESTRICT = area_restriction_function,
        JOIN = area_join_function,
        HASHES, MERGES
    );
    

## Compatibility

`CREATE OPERATOR` is a PostgreSQL extension. There are no provisions for user-
defined operators in the SQL standard.

## See Also

[ALTER OPERATOR](sql-alteroperator.html "ALTER OPERATOR"), [CREATE OPERATOR
CLASS](sql-createopclass.html "CREATE OPERATOR CLASS"), [DROP OPERATOR](sql-
dropoperator.html "DROP OPERATOR")

* * *

[Prev](sql-creatematerializedview.html "CREATE MATERIALIZED VIEW")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createopclass.html "CREATE OPERATOR CLASS")  
---|---|---  
CREATE MATERIALIZED VIEW  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE OPERATOR CLASS  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createoperator.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

