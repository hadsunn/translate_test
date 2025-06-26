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

Supported Versions: [Current](/docs/current/sql-create-access-method.html
"PostgreSQL 17 - CREATE ACCESS METHOD") ([17](/docs/17/sql-create-access-
method.html "PostgreSQL 17 - CREATE ACCESS METHOD")) / [16](/docs/16/sql-
create-access-method.html "PostgreSQL 16 - CREATE ACCESS METHOD") /
[15](/docs/15/sql-create-access-method.html "PostgreSQL 15 - CREATE ACCESS
METHOD") / [14](/docs/14/sql-create-access-method.html "PostgreSQL 14 - CREATE
ACCESS METHOD") / [13](/docs/13/sql-create-access-method.html "PostgreSQL 13 -
CREATE ACCESS METHOD")

Development Versions: [18](/docs/18/sql-create-access-method.html "PostgreSQL
18 - CREATE ACCESS METHOD") / [devel](/docs/devel/sql-create-access-
method.html "PostgreSQL devel - CREATE ACCESS METHOD")

Unsupported versions: [12](/docs/12/sql-create-access-method.html "PostgreSQL
12 - CREATE ACCESS METHOD") / [11](/docs/11/sql-create-access-method.html
"PostgreSQL 11 - CREATE ACCESS METHOD") / [10](/docs/10/sql-create-access-
method.html "PostgreSQL 10 - CREATE ACCESS METHOD") / [9.6](/docs/9.6/sql-
create-access-method.html "PostgreSQL 9.6 - CREATE ACCESS METHOD")

__

CREATE ACCESS METHOD  
---  
[Prev](sql-copy.html "COPY")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createaggregate.html "CREATE AGGREGATE")  
  
* * *

## CREATE ACCESS METHOD

CREATE ACCESS METHOD — define a new access method

## Synopsis

    
    
    CREATE ACCESS METHOD _name_
        TYPE _access_method_type_
        HANDLER _handler_function_
    

## Description

`CREATE ACCESS METHOD` creates a new access method.

The access method name must be unique within the database.

Only superusers can define new access methods.

## Parameters

_`name`_

    

The name of the access method to be created.

_`access_method_type`_

    

This clause specifies the type of access method to define. Only `TABLE` and
`INDEX` are supported at present.

_`handler_function`_

    

_`handler_function`_ is the name (possibly schema-qualified) of a previously
registered function that represents the access method. The handler function
must be declared to take a single argument of type `internal`, and its return
type depends on the type of access method; for `TABLE` access methods, it must
be `table_am_handler` and for `INDEX` access methods, it must be
`index_am_handler`. The C-level API that the handler function must implement
varies depending on the type of access method. The table access method API is
described in [Chapter 63](tableam.html "Chapter 63. Table Access Method
Interface Definition") and the index access method API is described in
[Chapter 64](indexam.html "Chapter 64. Index Access Method Interface
Definition").

## Examples

Create an index access method `heptree` with handler function
`heptree_handler`:

    
    
    CREATE ACCESS METHOD heptree TYPE INDEX HANDLER heptree_handler;
    

## Compatibility

`CREATE ACCESS METHOD` is a PostgreSQL extension.

## See Also

[DROP ACCESS METHOD](sql-drop-access-method.html "DROP ACCESS METHOD"),
[CREATE OPERATOR CLASS](sql-createopclass.html "CREATE OPERATOR CLASS"),
[CREATE OPERATOR FAMILY](sql-createopfamily.html "CREATE OPERATOR FAMILY")

* * *

[Prev](sql-copy.html "COPY")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createaggregate.html "CREATE AGGREGATE")  
---|---|---  
COPY  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE AGGREGATE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-create-access-
method.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

