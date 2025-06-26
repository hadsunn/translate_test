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

Supported Versions: [Current](/docs/current/sql-createopfamily.html
"PostgreSQL 17 - CREATE OPERATOR FAMILY") ([17](/docs/17/sql-
createopfamily.html "PostgreSQL 17 - CREATE OPERATOR FAMILY")) /
[16](/docs/16/sql-createopfamily.html "PostgreSQL 16 - CREATE OPERATOR
FAMILY") / [15](/docs/15/sql-createopfamily.html "PostgreSQL 15 - CREATE
OPERATOR FAMILY") / [14](/docs/14/sql-createopfamily.html "PostgreSQL 14 -
CREATE OPERATOR FAMILY") / [13](/docs/13/sql-createopfamily.html "PostgreSQL
13 - CREATE OPERATOR FAMILY")

Development Versions: [18](/docs/18/sql-createopfamily.html "PostgreSQL 18 -
CREATE OPERATOR FAMILY") / [devel](/docs/devel/sql-createopfamily.html
"PostgreSQL devel - CREATE OPERATOR FAMILY")

Unsupported versions: [12](/docs/12/sql-createopfamily.html "PostgreSQL 12 -
CREATE OPERATOR FAMILY") / [11](/docs/11/sql-createopfamily.html "PostgreSQL
11 - CREATE OPERATOR FAMILY") / [10](/docs/10/sql-createopfamily.html
"PostgreSQL 10 - CREATE OPERATOR FAMILY") / [9.6](/docs/9.6/sql-
createopfamily.html "PostgreSQL 9.6 - CREATE OPERATOR FAMILY") /
[9.5](/docs/9.5/sql-createopfamily.html "PostgreSQL 9.5 - CREATE OPERATOR
FAMILY") / [9.4](/docs/9.4/sql-createopfamily.html "PostgreSQL 9.4 - CREATE
OPERATOR FAMILY") / [9.3](/docs/9.3/sql-createopfamily.html "PostgreSQL 9.3 -
CREATE OPERATOR FAMILY") / [9.2](/docs/9.2/sql-createopfamily.html "PostgreSQL
9.2 - CREATE OPERATOR FAMILY") / [9.1](/docs/9.1/sql-createopfamily.html
"PostgreSQL 9.1 - CREATE OPERATOR FAMILY") / [9.0](/docs/9.0/sql-
createopfamily.html "PostgreSQL 9.0 - CREATE OPERATOR FAMILY") /
[8.4](/docs/8.4/sql-createopfamily.html "PostgreSQL 8.4 - CREATE OPERATOR
FAMILY") / [8.3](/docs/8.3/sql-createopfamily.html "PostgreSQL 8.3 - CREATE
OPERATOR FAMILY")

__

CREATE OPERATOR FAMILY  
---  
[Prev](sql-createopclass.html "CREATE OPERATOR CLASS")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createpolicy.html "CREATE POLICY")  
  
* * *

## CREATE OPERATOR FAMILY

CREATE OPERATOR FAMILY — define a new operator family

## Synopsis

    
    
    CREATE OPERATOR FAMILY _name_ USING _index_method_
    

## Description

`CREATE OPERATOR FAMILY` creates a new operator family. An operator family
defines a collection of related operator classes, and perhaps some additional
operators and support functions that are compatible with these operator
classes but not essential for the functioning of any individual index.
(Operators and functions that are essential to indexes should be grouped
within the relevant operator class, rather than being “loose” in the operator
family. Typically, single-data-type operators are bound to operator classes,
while cross-data-type operators can be loose in an operator family containing
operator classes for both data types.)

The new operator family is initially empty. It should be populated by issuing
subsequent `CREATE OPERATOR CLASS` commands to add contained operator classes,
and optionally `ALTER OPERATOR FAMILY` commands to add “loose” operators and
their corresponding support functions.

If a schema name is given then the operator family is created in the specified
schema. Otherwise it is created in the current schema. Two operator families
in the same schema can have the same name only if they are for different index
methods.

The user who defines an operator family becomes its owner. Presently, the
creating user must be a superuser. (This restriction is made because an
erroneous operator family definition could confuse or even crash the server.)

Refer to [Section 38.16](xindex.html "38.16. Interfacing Extensions to
Indexes") for further information.

## Parameters

_`name`_

    

The name of the operator family to be created. The name can be schema-
qualified.

_`index_method`_

    

The name of the index method this operator family is for.

## Compatibility

`CREATE OPERATOR FAMILY` is a PostgreSQL extension. There is no `CREATE
OPERATOR FAMILY` statement in the SQL standard.

## See Also

[ALTER OPERATOR FAMILY](sql-alteropfamily.html "ALTER OPERATOR FAMILY"), [DROP
OPERATOR FAMILY](sql-dropopfamily.html "DROP OPERATOR FAMILY"), [CREATE
OPERATOR CLASS](sql-createopclass.html "CREATE OPERATOR CLASS"), [ALTER
OPERATOR CLASS](sql-alteropclass.html "ALTER OPERATOR CLASS"), [DROP OPERATOR
CLASS](sql-dropopclass.html "DROP OPERATOR CLASS")

* * *

[Prev](sql-createopclass.html "CREATE OPERATOR CLASS")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createpolicy.html "CREATE POLICY")  
---|---|---  
CREATE OPERATOR CLASS  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE POLICY  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createopfamily.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

