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

Supported Versions: [Current](/docs/current/sql-createtransform.html
"PostgreSQL 17 - CREATE TRANSFORM") ([17](/docs/17/sql-createtransform.html
"PostgreSQL 17 - CREATE TRANSFORM")) / [16](/docs/16/sql-createtransform.html
"PostgreSQL 16 - CREATE TRANSFORM") / [15](/docs/15/sql-createtransform.html
"PostgreSQL 15 - CREATE TRANSFORM") / [14](/docs/14/sql-createtransform.html
"PostgreSQL 14 - CREATE TRANSFORM") / [13](/docs/13/sql-createtransform.html
"PostgreSQL 13 - CREATE TRANSFORM")

Development Versions: [18](/docs/18/sql-createtransform.html "PostgreSQL 18 -
CREATE TRANSFORM") / [devel](/docs/devel/sql-createtransform.html "PostgreSQL
devel - CREATE TRANSFORM")

Unsupported versions: [12](/docs/12/sql-createtransform.html "PostgreSQL 12 -
CREATE TRANSFORM") / [11](/docs/11/sql-createtransform.html "PostgreSQL 11 -
CREATE TRANSFORM") / [10](/docs/10/sql-createtransform.html "PostgreSQL 10 -
CREATE TRANSFORM") / [9.6](/docs/9.6/sql-createtransform.html "PostgreSQL 9.6
- CREATE TRANSFORM") / [9.5](/docs/9.5/sql-createtransform.html "PostgreSQL
9.5 - CREATE TRANSFORM")

__

CREATE TRANSFORM  
---  
[Prev](sql-createtstemplate.html "CREATE TEXT SEARCH TEMPLATE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createtrigger.html "CREATE TRIGGER")  
  
* * *

## CREATE TRANSFORM

CREATE TRANSFORM — define a new transform

## Synopsis

    
    
    CREATE [ OR REPLACE ] TRANSFORM FOR _type_name_ LANGUAGE _lang_name_ (
        FROM SQL WITH FUNCTION _from_sql_function_name_ [ (_argument_type_ [, ...]) ],
        TO SQL WITH FUNCTION _to_sql_function_name_ [ (_argument_type_ [, ...]) ]
    );
    

## Description

`CREATE TRANSFORM` defines a new transform. `CREATE OR REPLACE TRANSFORM` will
either create a new transform, or replace an existing definition.

A transform specifies how to adapt a data type to a procedural language. For
example, when writing a function in PL/Python using the `hstore` type,
PL/Python has no prior knowledge how to present `hstore` values in the Python
environment. Language implementations usually default to using the text
representation, but that is inconvenient when, for example, an associative
array or a list would be more appropriate.

A transform specifies two functions:

  * A “from SQL” function that converts the type from the SQL environment to the language. This function will be invoked on the arguments of a function written in the language.

  * A “to SQL” function that converts the type from the language to the SQL environment. This function will be invoked on the return value of a function written in the language.

It is not necessary to provide both of these functions. If one is not
specified, the language-specific default behavior will be used if necessary.
(To prevent a transformation in a certain direction from happening at all, you
could also write a transform function that always errors out.)

To be able to create a transform, you must own and have `USAGE` privilege on
the type, have `USAGE` privilege on the language, and own and have `EXECUTE`
privilege on the from-SQL and to-SQL functions, if specified.

## Parameters

_`type_name`_

    

The name of the data type of the transform.

_`lang_name`_

    

The name of the language of the transform.

`_`from_sql_function_name`_[(_`argument_type`_ [, ...])]`

    

The name of the function for converting the type from the SQL environment to
the language. It must take one argument of type `internal` and return type
`internal`. The actual argument will be of the type for the transform, and the
function should be coded as if it were. (But it is not allowed to declare an
SQL-level function returning `internal` without at least one argument of type
`internal`.) The actual return value will be something specific to the
language implementation. If no argument list is specified, the function name
must be unique in its schema.

`_`to_sql_function_name`_[(_`argument_type`_ [, ...])]`

    

The name of the function for converting the type from the language to the SQL
environment. It must take one argument of type `internal` and return the type
that is the type for the transform. The actual argument value will be
something specific to the language implementation. If no argument list is
specified, the function name must be unique in its schema.

## Notes

Use [`DROP TRANSFORM`](sql-droptransform.html "DROP TRANSFORM") to remove
transforms.

## Examples

To create a transform for type `hstore` and language `plpython3u`, first set
up the type and the language:

    
    
    CREATE TYPE hstore ...;
    
    CREATE EXTENSION plpython3u;
    

Then create the necessary functions:

    
    
    CREATE FUNCTION hstore_to_plpython(val internal) RETURNS internal
    LANGUAGE C STRICT IMMUTABLE
    AS ...;
    
    CREATE FUNCTION plpython_to_hstore(val internal) RETURNS hstore
    LANGUAGE C STRICT IMMUTABLE
    AS ...;
    

And finally create the transform to connect them all together:

    
    
    CREATE TRANSFORM FOR hstore LANGUAGE plpython3u (
        FROM SQL WITH FUNCTION hstore_to_plpython(internal),
        TO SQL WITH FUNCTION plpython_to_hstore(internal)
    );
    

In practice, these commands would be wrapped up in an extension.

The `contrib` section contains a number of extensions that provide transforms,
which can serve as real-world examples.

## Compatibility

This form of `CREATE TRANSFORM` is a PostgreSQL extension. There is a `CREATE
TRANSFORM` command in the SQL standard, but it is for adapting data types to
client languages. That usage is not supported by PostgreSQL.

## See Also

[CREATE FUNCTION](sql-createfunction.html "CREATE FUNCTION"), [CREATE
LANGUAGE](sql-createlanguage.html "CREATE LANGUAGE"), [CREATE TYPE](sql-
createtype.html "CREATE TYPE"), [DROP TRANSFORM](sql-droptransform.html "DROP
TRANSFORM")

* * *

[Prev](sql-createtstemplate.html "CREATE TEXT SEARCH TEMPLATE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createtrigger.html "CREATE TRIGGER")  
---|---|---  
CREATE TEXT SEARCH TEMPLATE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE TRIGGER  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createtransform.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

