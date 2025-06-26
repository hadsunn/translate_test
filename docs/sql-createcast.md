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

Supported Versions: [Current](/docs/current/sql-createcast.html "PostgreSQL 17
- CREATE CAST") ([17](/docs/17/sql-createcast.html "PostgreSQL 17 - CREATE
CAST")) / [16](/docs/16/sql-createcast.html "PostgreSQL 16 - CREATE CAST") /
[15](/docs/15/sql-createcast.html "PostgreSQL 15 - CREATE CAST") /
[14](/docs/14/sql-createcast.html "PostgreSQL 14 - CREATE CAST") /
[13](/docs/13/sql-createcast.html "PostgreSQL 13 - CREATE CAST")

Development Versions: [18](/docs/18/sql-createcast.html "PostgreSQL 18 -
CREATE CAST") / [devel](/docs/devel/sql-createcast.html "PostgreSQL devel -
CREATE CAST")

Unsupported versions: [12](/docs/12/sql-createcast.html "PostgreSQL 12 -
CREATE CAST") / [11](/docs/11/sql-createcast.html "PostgreSQL 11 - CREATE
CAST") / [10](/docs/10/sql-createcast.html "PostgreSQL 10 - CREATE CAST") /
[9.6](/docs/9.6/sql-createcast.html "PostgreSQL 9.6 - CREATE CAST") /
[9.5](/docs/9.5/sql-createcast.html "PostgreSQL 9.5 - CREATE CAST") /
[9.4](/docs/9.4/sql-createcast.html "PostgreSQL 9.4 - CREATE CAST") /
[9.3](/docs/9.3/sql-createcast.html "PostgreSQL 9.3 - CREATE CAST") /
[9.2](/docs/9.2/sql-createcast.html "PostgreSQL 9.2 - CREATE CAST") /
[9.1](/docs/9.1/sql-createcast.html "PostgreSQL 9.1 - CREATE CAST") /
[9.0](/docs/9.0/sql-createcast.html "PostgreSQL 9.0 - CREATE CAST") /
[8.4](/docs/8.4/sql-createcast.html "PostgreSQL 8.4 - CREATE CAST") /
[8.3](/docs/8.3/sql-createcast.html "PostgreSQL 8.3 - CREATE CAST") /
[8.2](/docs/8.2/sql-createcast.html "PostgreSQL 8.2 - CREATE CAST") /
[8.1](/docs/8.1/sql-createcast.html "PostgreSQL 8.1 - CREATE CAST") /
[8.0](/docs/8.0/sql-createcast.html "PostgreSQL 8.0 - CREATE CAST") /
[7.4](/docs/7.4/sql-createcast.html "PostgreSQL 7.4 - CREATE CAST") /
[7.3](/docs/7.3/sql-createcast.html "PostgreSQL 7.3 - CREATE CAST")

__

CREATE CAST  
---  
[Prev](sql-createaggregate.html "CREATE AGGREGATE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createcollation.html "CREATE COLLATION")  
  
* * *

## CREATE CAST

CREATE CAST — define a new cast

## Synopsis

    
    
    CREATE CAST (_source_type_ AS _target_type_)
        WITH FUNCTION _function_name_ [ (_argument_type_ [, ...]) ]
        [ AS ASSIGNMENT | AS IMPLICIT ]
    
    CREATE CAST (_source_type_ AS _target_type_)
        WITHOUT FUNCTION
        [ AS ASSIGNMENT | AS IMPLICIT ]
    
    CREATE CAST (_source_type_ AS _target_type_)
        WITH INOUT
        [ AS ASSIGNMENT | AS IMPLICIT ]
    

## Description

`CREATE CAST` defines a new cast. A cast specifies how to perform a conversion
between two data types. For example,

    
    
    SELECT CAST(42 AS float8);
    

converts the integer constant 42 to type `float8` by invoking a previously
specified function, in this case `float8(int4)`. (If no suitable cast has been
defined, the conversion fails.)

Two types can be _binary coercible_ , which means that the conversion can be
performed “for free” without invoking any function. This requires that
corresponding values use the same internal representation. For instance, the
types `text` and `varchar` are binary coercible both ways. Binary coercibility
is not necessarily a symmetric relationship. For example, the cast from `xml`
to `text` can be performed for free in the present implementation, but the
reverse direction requires a function that performs at least a syntax check.
(Two types that are binary coercible both ways are also referred to as binary
compatible.)

You can define a cast as an _I/O conversion cast_ by using the `WITH INOUT`
syntax. An I/O conversion cast is performed by invoking the output function of
the source data type, and passing the resulting string to the input function
of the target data type. In many common cases, this feature avoids the need to
write a separate cast function for conversion. An I/O conversion cast acts the
same as a regular function-based cast; only the implementation is different.

By default, a cast can be invoked only by an explicit cast request, that is an
explicit `CAST(_`x`_ AS _`typename`_)` or _`x`_`::`_`typename`_ construct.

If the cast is marked `AS ASSIGNMENT` then it can be invoked implicitly when
assigning a value to a column of the target data type. For example, supposing
that `foo.f1` is a column of type `text`, then:

    
    
    INSERT INTO foo (f1) VALUES (42);
    

will be allowed if the cast from type `integer` to type `text` is marked `AS
ASSIGNMENT`, otherwise not. (We generally use the term _assignment cast_ to
describe this kind of cast.)

If the cast is marked `AS IMPLICIT` then it can be invoked implicitly in any
context, whether assignment or internally in an expression. (We generally use
the term _implicit cast_ to describe this kind of cast.) For example, consider
this query:

    
    
    SELECT 2 + 4.0;
    

The parser initially marks the constants as being of type `integer` and
`numeric` respectively. There is no `integer` `+` `numeric` operator in the
system catalogs, but there is a `numeric` `+` `numeric` operator. The query
will therefore succeed if a cast from `integer` to `numeric` is available and
is marked `AS IMPLICIT` — which in fact it is. The parser will apply the
implicit cast and resolve the query as if it had been written

    
    
    SELECT CAST ( 2 AS numeric ) + 4.0;
    

Now, the catalogs also provide a cast from `numeric` to `integer`. If that
cast were marked `AS IMPLICIT` — which it is not — then the parser would be
faced with choosing between the above interpretation and the alternative of
casting the `numeric` constant to `integer` and applying the `integer` `+`
`integer` operator. Lacking any knowledge of which choice to prefer, it would
give up and declare the query ambiguous. The fact that only one of the two
casts is implicit is the way in which we teach the parser to prefer resolution
of a mixed `numeric`-and-`integer` expression as `numeric`; there is no built-
in knowledge about that.

It is wise to be conservative about marking casts as implicit. An
overabundance of implicit casting paths can cause PostgreSQL to choose
surprising interpretations of commands, or to be unable to resolve commands at
all because there are multiple possible interpretations. A good rule of thumb
is to make a cast implicitly invokable only for information-preserving
transformations between types in the same general type category. For example,
the cast from `int2` to `int4` can reasonably be implicit, but the cast from
`float8` to `int4` should probably be assignment-only. Cross-type-category
casts, such as `text` to `int4`, are best made explicit-only.

### Note

Sometimes it is necessary for usability or standards-compliance reasons to
provide multiple implicit casts among a set of types, resulting in ambiguity
that cannot be avoided as above. The parser has a fallback heuristic based on
_type categories_ and _preferred types_ that can help to provide desired
behavior in such cases. See [CREATE TYPE](sql-createtype.html "CREATE TYPE")
for more information.

To be able to create a cast, you must own the source or the target data type
and have `USAGE` privilege on the other type. To create a binary-coercible
cast, you must be superuser. (This restriction is made because an erroneous
binary-coercible cast conversion can easily crash the server.)

## Parameters

_`source_type`_

    

The name of the source data type of the cast.

_`target_type`_

    

The name of the target data type of the cast.

`_`function_name`_[(_`argument_type`_ [, ...])]`

    

The function used to perform the cast. The function name can be schema-
qualified. If it is not, the function will be looked up in the schema search
path. The function's result data type must match the target type of the cast.
Its arguments are discussed below. If no argument list is specified, the
function name must be unique in its schema.

`WITHOUT FUNCTION`

    

Indicates that the source type is binary-coercible to the target type, so no
function is required to perform the cast.

`WITH INOUT`

    

Indicates that the cast is an I/O conversion cast, performed by invoking the
output function of the source data type, and passing the resulting string to
the input function of the target data type.

`AS ASSIGNMENT`

    

Indicates that the cast can be invoked implicitly in assignment contexts.

`AS IMPLICIT`

    

Indicates that the cast can be invoked implicitly in any context.

Cast implementation functions can have one to three arguments. The first
argument type must be identical to or binary-coercible from the cast's source
type. The second argument, if present, must be type `integer`; it receives the
type modifier associated with the destination type, or `-1` if there is none.
The third argument, if present, must be type `boolean`; it receives `true` if
the cast is an explicit cast, `false` otherwise. (Bizarrely, the SQL standard
demands different behaviors for explicit and implicit casts in some cases.
This argument is supplied for functions that must implement such casts. It is
not recommended that you design your own data types so that this matters.)

The return type of a cast function must be identical to or binary-coercible to
the cast's target type.

Ordinarily a cast must have different source and target data types. However,
it is allowed to declare a cast with identical source and target types if it
has a cast implementation function with more than one argument. This is used
to represent type-specific length coercion functions in the system catalogs.
The named function is used to coerce a value of the type to the type modifier
value given by its second argument.

When a cast has different source and target types and a function that takes
more than one argument, it supports converting from one type to another and
applying a length coercion in a single step. When no such entry is available,
coercion to a type that uses a type modifier involves two cast steps, one to
convert between data types and a second to apply the modifier.

A cast to or from a domain type currently has no effect. Casting to or from a
domain uses the casts associated with its underlying type.

## Notes

Use [`DROP CAST`](sql-dropcast.html "DROP CAST") to remove user-defined casts.

Remember that if you want to be able to convert types both ways you need to
declare casts both ways explicitly.

It is normally not necessary to create casts between user-defined types and
the standard string types (`text`, `varchar`, and `char(_`n`_)`, as well as
user-defined types that are defined to be in the string category). PostgreSQL
provides automatic I/O conversion casts for that. The automatic casts to
string types are treated as assignment casts, while the automatic casts from
string types are explicit-only. You can override this behavior by declaring
your own cast to replace an automatic cast, but usually the only reason to do
so is if you want the conversion to be more easily invokable than the standard
assignment-only or explicit-only setting. Another possible reason is that you
want the conversion to behave differently from the type's I/O function; but
that is sufficiently surprising that you should think twice about whether it's
a good idea. (A small number of the built-in types do indeed have different
behaviors for conversions, mostly because of requirements of the SQL
standard.)

While not required, it is recommended that you continue to follow this old
convention of naming cast implementation functions after the target data type.
Many users are used to being able to cast data types using a function-style
notation, that is _`typename`_(_`x`_). This notation is in fact nothing more
nor less than a call of the cast implementation function; it is not specially
treated as a cast. If your conversion functions are not named to support this
convention then you will have surprised users. Since PostgreSQL allows
overloading of the same function name with different argument types, there is
no difficulty in having multiple conversion functions from different types
that all use the target type's name.

### Note

Actually the preceding paragraph is an oversimplification: there are two cases
in which a function-call construct will be treated as a cast request without
having matched it to an actual function. If a function call _`name`_(_`x`_)
does not exactly match any existing function, but _`name`_ is the name of a
data type and `pg_cast` provides a binary-coercible cast to this type from the
type of _`x`_ , then the call will be construed as a binary-coercible cast.
This exception is made so that binary-coercible casts can be invoked using
functional syntax, even though they lack any function. Likewise, if there is
no `pg_cast` entry but the cast would be to or from a string type, the call
will be construed as an I/O conversion cast. This exception allows I/O
conversion casts to be invoked using functional syntax.

### Note

There is also an exception to the exception: I/O conversion casts from
composite types to string types cannot be invoked using functional syntax, but
must be written in explicit cast syntax (either `CAST` or `::` notation). This
exception was added because after the introduction of automatically-provided
I/O conversion casts, it was found too easy to accidentally invoke such a cast
when a function or column reference was intended.

## Examples

To create an assignment cast from type `bigint` to type `int4` using the
function `int4(bigint)`:

    
    
    CREATE CAST (bigint AS int4) WITH FUNCTION int4(bigint) AS ASSIGNMENT;
    

(This cast is already predefined in the system.)

## Compatibility

The `CREATE CAST` command conforms to the SQL standard, except that SQL does
not make provisions for binary-coercible types or extra arguments to
implementation functions. `AS IMPLICIT` is a PostgreSQL extension, too.

## See Also

[CREATE FUNCTION](sql-createfunction.html "CREATE FUNCTION"), [CREATE
TYPE](sql-createtype.html "CREATE TYPE"), [DROP CAST](sql-dropcast.html "DROP
CAST")

* * *

[Prev](sql-createaggregate.html "CREATE AGGREGATE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createcollation.html "CREATE COLLATION")  
---|---|---  
CREATE AGGREGATE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE COLLATION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createcast.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

