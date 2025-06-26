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

Supported Versions: [Current](/docs/current/sql-dropfunction.html "PostgreSQL
17 - DROP FUNCTION") ([17](/docs/17/sql-dropfunction.html "PostgreSQL 17 -
DROP FUNCTION")) / [16](/docs/16/sql-dropfunction.html "PostgreSQL 16 - DROP
FUNCTION") / [15](/docs/15/sql-dropfunction.html "PostgreSQL 15 - DROP
FUNCTION") / [14](/docs/14/sql-dropfunction.html "PostgreSQL 14 - DROP
FUNCTION") / [13](/docs/13/sql-dropfunction.html "PostgreSQL 13 - DROP
FUNCTION")

Development Versions: [18](/docs/18/sql-dropfunction.html "PostgreSQL 18 -
DROP FUNCTION") / [devel](/docs/devel/sql-dropfunction.html "PostgreSQL devel
- DROP FUNCTION")

Unsupported versions: [12](/docs/12/sql-dropfunction.html "PostgreSQL 12 -
DROP FUNCTION") / [11](/docs/11/sql-dropfunction.html "PostgreSQL 11 - DROP
FUNCTION") / [10](/docs/10/sql-dropfunction.html "PostgreSQL 10 - DROP
FUNCTION") / [9.6](/docs/9.6/sql-dropfunction.html "PostgreSQL 9.6 - DROP
FUNCTION") / [9.5](/docs/9.5/sql-dropfunction.html "PostgreSQL 9.5 - DROP
FUNCTION") / [9.4](/docs/9.4/sql-dropfunction.html "PostgreSQL 9.4 - DROP
FUNCTION") / [9.3](/docs/9.3/sql-dropfunction.html "PostgreSQL 9.3 - DROP
FUNCTION") / [9.2](/docs/9.2/sql-dropfunction.html "PostgreSQL 9.2 - DROP
FUNCTION") / [9.1](/docs/9.1/sql-dropfunction.html "PostgreSQL 9.1 - DROP
FUNCTION") / [9.0](/docs/9.0/sql-dropfunction.html "PostgreSQL 9.0 - DROP
FUNCTION") / [8.4](/docs/8.4/sql-dropfunction.html "PostgreSQL 8.4 - DROP
FUNCTION") / [8.3](/docs/8.3/sql-dropfunction.html "PostgreSQL 8.3 - DROP
FUNCTION") / [8.2](/docs/8.2/sql-dropfunction.html "PostgreSQL 8.2 - DROP
FUNCTION") / [8.1](/docs/8.1/sql-dropfunction.html "PostgreSQL 8.1 - DROP
FUNCTION") / [8.0](/docs/8.0/sql-dropfunction.html "PostgreSQL 8.0 - DROP
FUNCTION") / [7.4](/docs/7.4/sql-dropfunction.html "PostgreSQL 7.4 - DROP
FUNCTION") / [7.3](/docs/7.3/sql-dropfunction.html "PostgreSQL 7.3 - DROP
FUNCTION") / [7.2](/docs/7.2/sql-dropfunction.html "PostgreSQL 7.2 - DROP
FUNCTION") / [7.1](/docs/7.1/sql-dropfunction.html "PostgreSQL 7.1 - DROP
FUNCTION")

__

DROP FUNCTION  
---  
[Prev](sql-dropforeigntable.html "DROP FOREIGN TABLE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropgroup.html "DROP GROUP")  
  
* * *

## DROP FUNCTION

DROP FUNCTION — remove a function

## Synopsis

    
    
    DROP FUNCTION [ IF EXISTS ] _name_ [ ( [ [ _argmode_ ] [ _argname_ ] _argtype_ [, ...] ] ) ] [, ...]
        [ CASCADE | RESTRICT ]
    

## Description

`DROP FUNCTION` removes the definition of an existing function. To execute
this command the user must be the owner of the function. The argument types to
the function must be specified, since several different functions can exist
with the same name and different argument lists.

## Parameters

`IF EXISTS`

    

Do not throw an error if the function does not exist. A notice is issued in
this case.

_`name`_

    

The name (optionally schema-qualified) of an existing function. If no argument
list is specified, the name must be unique in its schema.

_`argmode`_

    

The mode of an argument: `IN`, `OUT`, `INOUT`, or `VARIADIC`. If omitted, the
default is `IN`. Note that `DROP FUNCTION` does not actually pay any attention
to `OUT` arguments, since only the input arguments are needed to determine the
function's identity. So it is sufficient to list the `IN`, `INOUT`, and
`VARIADIC` arguments.

_`argname`_

    

The name of an argument. Note that `DROP FUNCTION` does not actually pay any
attention to argument names, since only the argument data types are needed to
determine the function's identity.

_`argtype`_

    

The data type(s) of the function's arguments (optionally schema-qualified), if
any.

`CASCADE`

    

Automatically drop objects that depend on the function (such as operators or
triggers), and in turn all objects that depend on those objects (see [Section
5.14](ddl-depend.html "5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the function if any objects depend on it. This is the default.

## Examples

This command removes the square root function:

    
    
    DROP FUNCTION sqrt(integer);
    

Drop multiple functions in one command:

    
    
    DROP FUNCTION sqrt(integer), sqrt(bigint);
    

If the function name is unique in its schema, it can be referred to without an
argument list:

    
    
    DROP FUNCTION update_employee_salaries;
    

Note that this is different from

    
    
    DROP FUNCTION update_employee_salaries();
    

which refers to a function with zero arguments, whereas the first variant can
refer to a function with any number of arguments, including zero, as long as
the name is unique.

## Compatibility

This command conforms to the SQL standard, with these PostgreSQL extensions:

  * The standard only allows one function to be dropped per command.

  * The `IF EXISTS` option

  * The ability to specify argument modes and names

## See Also

[CREATE FUNCTION](sql-createfunction.html "CREATE FUNCTION"), [ALTER
FUNCTION](sql-alterfunction.html "ALTER FUNCTION"), [DROP PROCEDURE](sql-
dropprocedure.html "DROP PROCEDURE"), [DROP ROUTINE](sql-droproutine.html
"DROP ROUTINE")

* * *

[Prev](sql-dropforeigntable.html "DROP FOREIGN TABLE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropgroup.html "DROP GROUP")  
---|---|---  
DROP FOREIGN TABLE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP GROUP  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropfunction.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

