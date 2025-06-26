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

Supported Versions: [Current](/docs/current/sql-dropaggregate.html "PostgreSQL
17 - DROP AGGREGATE") ([17](/docs/17/sql-dropaggregate.html "PostgreSQL 17 -
DROP AGGREGATE")) / [16](/docs/16/sql-dropaggregate.html "PostgreSQL 16 - DROP
AGGREGATE") / [15](/docs/15/sql-dropaggregate.html "PostgreSQL 15 - DROP
AGGREGATE") / [14](/docs/14/sql-dropaggregate.html "PostgreSQL 14 - DROP
AGGREGATE") / [13](/docs/13/sql-dropaggregate.html "PostgreSQL 13 - DROP
AGGREGATE")

Development Versions: [18](/docs/18/sql-dropaggregate.html "PostgreSQL 18 -
DROP AGGREGATE") / [devel](/docs/devel/sql-dropaggregate.html "PostgreSQL
devel - DROP AGGREGATE")

Unsupported versions: [12](/docs/12/sql-dropaggregate.html "PostgreSQL 12 -
DROP AGGREGATE") / [11](/docs/11/sql-dropaggregate.html "PostgreSQL 11 - DROP
AGGREGATE") / [10](/docs/10/sql-dropaggregate.html "PostgreSQL 10 - DROP
AGGREGATE") / [9.6](/docs/9.6/sql-dropaggregate.html "PostgreSQL 9.6 - DROP
AGGREGATE") / [9.5](/docs/9.5/sql-dropaggregate.html "PostgreSQL 9.5 - DROP
AGGREGATE") / [9.4](/docs/9.4/sql-dropaggregate.html "PostgreSQL 9.4 - DROP
AGGREGATE") / [9.3](/docs/9.3/sql-dropaggregate.html "PostgreSQL 9.3 - DROP
AGGREGATE") / [9.2](/docs/9.2/sql-dropaggregate.html "PostgreSQL 9.2 - DROP
AGGREGATE") / [9.1](/docs/9.1/sql-dropaggregate.html "PostgreSQL 9.1 - DROP
AGGREGATE") / [9.0](/docs/9.0/sql-dropaggregate.html "PostgreSQL 9.0 - DROP
AGGREGATE") / [8.4](/docs/8.4/sql-dropaggregate.html "PostgreSQL 8.4 - DROP
AGGREGATE") / [8.3](/docs/8.3/sql-dropaggregate.html "PostgreSQL 8.3 - DROP
AGGREGATE") / [8.2](/docs/8.2/sql-dropaggregate.html "PostgreSQL 8.2 - DROP
AGGREGATE") / [8.1](/docs/8.1/sql-dropaggregate.html "PostgreSQL 8.1 - DROP
AGGREGATE") / [8.0](/docs/8.0/sql-dropaggregate.html "PostgreSQL 8.0 - DROP
AGGREGATE") / [7.4](/docs/7.4/sql-dropaggregate.html "PostgreSQL 7.4 - DROP
AGGREGATE") / [7.3](/docs/7.3/sql-dropaggregate.html "PostgreSQL 7.3 - DROP
AGGREGATE") / [7.2](/docs/7.2/sql-dropaggregate.html "PostgreSQL 7.2 - DROP
AGGREGATE") / [7.1](/docs/7.1/sql-dropaggregate.html "PostgreSQL 7.1 - DROP
AGGREGATE")

__

DROP AGGREGATE  
---  
[Prev](sql-drop-access-method.html "DROP ACCESS METHOD")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropcast.html "DROP CAST")  
  
* * *

## DROP AGGREGATE

DROP AGGREGATE — remove an aggregate function

## Synopsis

    
    
    DROP AGGREGATE [ IF EXISTS ] _name_ ( _aggregate_signature_ ) [, ...] [ CASCADE | RESTRICT ]
    
    where _aggregate_signature_ is:
    
    * |
    [ _argmode_ ] [ _argname_ ] _argtype_ [ , ... ] |
    [ [ _argmode_ ] [ _argname_ ] _argtype_ [ , ... ] ] ORDER BY [ _argmode_ ] [ _argname_ ] _argtype_ [ , ... ]
    

## Description

`DROP AGGREGATE` removes an existing aggregate function. To execute this
command the current user must be the owner of the aggregate function.

## Parameters

`IF EXISTS`

    

Do not throw an error if the aggregate does not exist. A notice is issued in
this case.

_`name`_

    

The name (optionally schema-qualified) of an existing aggregate function.

_`argmode`_

    

The mode of an argument: `IN` or `VARIADIC`. If omitted, the default is `IN`.

_`argname`_

    

The name of an argument. Note that `DROP AGGREGATE` does not actually pay any
attention to argument names, since only the argument data types are needed to
determine the aggregate function's identity.

_`argtype`_

    

An input data type on which the aggregate function operates. To reference a
zero-argument aggregate function, write `*` in place of the list of argument
specifications. To reference an ordered-set aggregate function, write `ORDER
BY` between the direct and aggregated argument specifications.

`CASCADE`

    

Automatically drop objects that depend on the aggregate function (such as
views using it), and in turn all objects that depend on those objects (see
[Section 5.14](ddl-depend.html "5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the aggregate function if any objects depend on it. This is the
default.

## Notes

Alternative syntaxes for referencing ordered-set aggregates are described
under [ALTER AGGREGATE](sql-alteraggregate.html "ALTER AGGREGATE").

## Examples

To remove the aggregate function `myavg` for type `integer`:

    
    
    DROP AGGREGATE myavg(integer);
    

To remove the hypothetical-set aggregate function `myrank`, which takes an
arbitrary list of ordering columns and a matching list of direct arguments:

    
    
    DROP AGGREGATE myrank(VARIADIC "any" ORDER BY VARIADIC "any");
    

To remove multiple aggregate functions in one command:

    
    
    DROP AGGREGATE myavg(integer), myavg(bigint);
    

## Compatibility

There is no `DROP AGGREGATE` statement in the SQL standard.

## See Also

[ALTER AGGREGATE](sql-alteraggregate.html "ALTER AGGREGATE"), [CREATE
AGGREGATE](sql-createaggregate.html "CREATE AGGREGATE")

* * *

[Prev](sql-drop-access-method.html "DROP ACCESS METHOD")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropcast.html "DROP CAST")  
---|---|---  
DROP ACCESS METHOD  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP CAST  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropaggregate.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

