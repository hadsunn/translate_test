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

Supported Versions: [Current](/docs/current/datatype-oid.html "PostgreSQL 17 -
8.19. Object Identifier Types") ([17](/docs/17/datatype-oid.html "PostgreSQL
17 - 8.19. Object Identifier Types")) / [16](/docs/16/datatype-oid.html
"PostgreSQL 16 - 8.19. Object Identifier Types") / [15](/docs/15/datatype-
oid.html "PostgreSQL 15 - 8.19. Object Identifier Types") /
[14](/docs/14/datatype-oid.html "PostgreSQL 14 - 8.19. Object Identifier
Types") / [13](/docs/13/datatype-oid.html "PostgreSQL 13 - 8.19. Object
Identifier Types")

Development Versions: [18](/docs/18/datatype-oid.html "PostgreSQL 18 -
8.19. Object Identifier Types") / [devel](/docs/devel/datatype-oid.html
"PostgreSQL devel - 8.19. Object Identifier Types")

Unsupported versions: [12](/docs/12/datatype-oid.html "PostgreSQL 12 -
8.19. Object Identifier Types") / [11](/docs/11/datatype-oid.html "PostgreSQL
11 - 8.19. Object Identifier Types") / [10](/docs/10/datatype-oid.html
"PostgreSQL 10 - 8.19. Object Identifier Types") / [9.6](/docs/9.6/datatype-
oid.html "PostgreSQL 9.6 - 8.19. Object Identifier Types") /
[9.5](/docs/9.5/datatype-oid.html "PostgreSQL 9.5 - 8.19. Object Identifier
Types") / [9.4](/docs/9.4/datatype-oid.html "PostgreSQL 9.4 - 8.19. Object
Identifier Types") / [9.3](/docs/9.3/datatype-oid.html "PostgreSQL 9.3 -
8.19. Object Identifier Types") / [9.2](/docs/9.2/datatype-oid.html
"PostgreSQL 9.2 - 8.19. Object Identifier Types") / [9.1](/docs/9.1/datatype-
oid.html "PostgreSQL 9.1 - 8.19. Object Identifier Types") /
[9.0](/docs/9.0/datatype-oid.html "PostgreSQL 9.0 - 8.19. Object Identifier
Types") / [8.4](/docs/8.4/datatype-oid.html "PostgreSQL 8.4 - 8.19. Object
Identifier Types") / [8.3](/docs/8.3/datatype-oid.html "PostgreSQL 8.3 -
8.19. Object Identifier Types") / [8.2](/docs/8.2/datatype-oid.html
"PostgreSQL 8.2 - 8.19. Object Identifier Types") / [8.1](/docs/8.1/datatype-
oid.html "PostgreSQL 8.1 - 8.19. Object Identifier Types") /
[8.0](/docs/8.0/datatype-oid.html "PostgreSQL 8.0 - 8.19. Object Identifier
Types") / [7.4](/docs/7.4/datatype-oid.html "PostgreSQL 7.4 - 8.19. Object
Identifier Types") / [7.3](/docs/7.3/datatype-oid.html "PostgreSQL 7.3 -
8.19. Object Identifier Types")

__

8.19. Object Identifier Types  
---  
[Prev](domains.html "8.18. Domain Types")  | [Up](datatype.html "Chapter 8. Data Types") | Chapter 8. Data Types | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datatype-pg-lsn.html "8.20. pg_lsn Type")  
  
* * *

## 8.19. Object Identifier Types #

Object identifiers (OIDs) are used internally by PostgreSQL as primary keys
for various system tables. Type `oid` represents an object identifier. There
are also several alias types for `oid`, each named `reg _`something`_`. [Table
8.26](datatype-oid.html#DATATYPE-OID-TABLE "Table 8.26. Object Identifier
Types") shows an overview.

The `oid` type is currently implemented as an unsigned four-byte integer.
Therefore, it is not large enough to provide database-wide uniqueness in large
databases, or even in large individual tables.

The `oid` type itself has few operations beyond comparison. It can be cast to
integer, however, and then manipulated using the standard integer operators.
(Beware of possible signed-versus-unsigned confusion if you do this.)

The OID alias types have no operations of their own except for specialized
input and output routines. These routines are able to accept and display
symbolic names for system objects, rather than the raw numeric value that type
`oid` would use. The alias types allow simplified lookup of OID values for
objects. For example, to examine the `pg_attribute` rows related to a table
`mytable`, one could write:

    
    
    SELECT * FROM pg_attribute WHERE attrelid = 'mytable'::regclass;
    

rather than:

    
    
    SELECT * FROM pg_attribute
      WHERE attrelid = (SELECT oid FROM pg_class WHERE relname = 'mytable');
    

While that doesn't look all that bad by itself, it's still oversimplified. A
far more complicated sub-select would be needed to select the right OID if
there are multiple tables named `mytable` in different schemas. The `regclass`
input converter handles the table lookup according to the schema path setting,
and so it does the “right thing” automatically. Similarly, casting a table's
OID to `regclass` is handy for symbolic display of a numeric OID.

**Table  8.26. Object Identifier Types**

Name | References | Description | Value Example  
---|---|---|---  
`oid` | any | numeric object identifier | `564182`  
`regclass` | `pg_class` | relation name | `pg_type`  
`regcollation` | `pg_collation` | collation name | `"POSIX"`  
`regconfig` | `pg_ts_config` | text search configuration | `english`  
`regdictionary` | `pg_ts_dict` | text search dictionary | `simple`  
`regnamespace` | `pg_namespace` | namespace name | `pg_catalog`  
`regoper` | `pg_operator` | operator name | `+`  
`regoperator` | `pg_operator` | operator with argument types | `*(integer,​integer)` or `-(NONE,​integer)`  
`regproc` | `pg_proc` | function name | `sum`  
`regprocedure` | `pg_proc` | function with argument types | `sum(int4)`  
`regrole` | `pg_authid` | role name | `smithee`  
`regtype` | `pg_type` | data type name | `integer`  
  
  

All of the OID alias types for objects that are grouped by namespace accept
schema-qualified names, and will display schema-qualified names on output if
the object would not be found in the current search path without being
qualified. For example, `myschema.mytable` is acceptable input for `regclass`
(if there is such a table). That value might be output as `myschema.mytable`,
or just `mytable`, depending on the current search path. The `regproc` and
`regoper` alias types will only accept input names that are unique (not
overloaded), so they are of limited use; for most uses `regprocedure` or
`regoperator` are more appropriate. For `regoperator`, unary operators are
identified by writing `NONE` for the unused operand.

The input functions for these types allow whitespace between tokens, and will
fold upper-case letters to lower case, except within double quotes; this is
done to make the syntax rules similar to the way object names are written in
SQL. Conversely, the output functions will use double quotes if needed to make
the output be a valid SQL identifier. For example, the OID of a function named
`Foo` (with upper case `F`) taking two integer arguments could be entered as
`' "Foo" ( int, integer ) '::regprocedure`. The output would look like
`"Foo"(integer,integer)`. Both the function name and the argument type names
could be schema-qualified, too.

Many built-in PostgreSQL functions accept the OID of a table, or another kind
of database object, and for convenience are declared as taking `regclass` (or
the appropriate OID alias type). This means you do not have to look up the
object's OID by hand, but can just enter its name as a string literal. For
example, the `nextval(regclass)` function takes a sequence relation's OID, so
you could call it like this:

    
    
    nextval('foo')              _operates on sequencefoo_
    nextval('FOO')              _same as above_
    nextval('"Foo"')            _operates on sequenceFoo_
    nextval('myschema.foo')     _operates onmyschema.foo_
    nextval('"myschema".foo')   _same as above_
    nextval('foo')              _searches search path forfoo_
    

### Note

When you write the argument of such a function as an unadorned literal string,
it becomes a constant of type `regclass` (or the appropriate type). Since this
is really just an OID, it will track the originally identified object despite
later renaming, schema reassignment, etc. This “early binding” behavior is
usually desirable for object references in column defaults and views. But
sometimes you might want “late binding” where the object reference is resolved
at run time. To get late-binding behavior, force the constant to be stored as
a `text` constant instead of `regclass`:

    
    
    nextval('foo'::text)      _foo is looked up at runtime_
    

The `to_regclass()` function and its siblings can also be used to perform run-
time lookups. See [Table 9.72](functions-info.html#FUNCTIONS-INFO-CATALOG-
TABLE "Table 9.72. System Catalog Information Functions").

Another practical example of use of `regclass` is to look up the OID of a
table listed in the `information_schema` views, which don't supply such OIDs
directly. One might for example wish to call the `pg_relation_size()`
function, which requires the table OID. Taking the above rules into account,
the correct way to do that is

    
    
    SELECT table_schema, table_name,
           pg_relation_size((quote_ident(table_schema) || '.' ||
                             quote_ident(table_name))::regclass)
    FROM information_schema.tables
    WHERE ...
    

The `quote_ident()` function will take care of double-quoting the identifiers
where needed. The seemingly easier

    
    
    SELECT pg_relation_size(table_name)
    FROM information_schema.tables
    WHERE ...
    

is _not recommended_ , because it will fail for tables that are outside your
search path or have names that require quoting.

An additional property of most of the OID alias types is the creation of
dependencies. If a constant of one of these types appears in a stored
expression (such as a column default expression or view), it creates a
dependency on the referenced object. For example, if a column has a default
expression `nextval('my_seq'::regclass)`, PostgreSQL understands that the
default expression depends on the sequence `my_seq`, so the system will not
let the sequence be dropped without first removing the default expression. The
alternative of `nextval('my_seq'::text)` does not create a dependency.
(`regrole` is an exception to this property. Constants of this type are not
allowed in stored expressions.)

Another identifier type used by the system is `xid`, or transaction
(abbreviated xact) identifier. This is the data type of the system columns
`xmin` and `xmax`. Transaction identifiers are 32-bit quantities. In some
contexts, a 64-bit variant `xid8` is used. Unlike `xid` values, `xid8` values
increase strictly monotonically and cannot be reused in the lifetime of a
database cluster. See [Section 74.1](transaction-id.html "74.1. Transactions
and Identifiers") for more details.

A third identifier type used by the system is `cid`, or command identifier.
This is the data type of the system columns `cmin` and `cmax`. Command
identifiers are also 32-bit quantities.

A final identifier type used by the system is `tid`, or tuple identifier (row
identifier). This is the data type of the system column `ctid`. A tuple ID is
a pair (block number, tuple index within block) that identifies the physical
location of the row within its table.

(The system columns are further explained in [Section 5.5](ddl-system-
columns.html "5.5. System Columns").)

* * *

[Prev](domains.html "8.18. Domain Types")  | [Up](datatype.html "Chapter 8. Data Types") |  [Next](datatype-pg-lsn.html "8.20. pg_lsn Type")  
---|---|---  
8.18. Domain Types  | [Home](index.html "PostgreSQL 16.9 Documentation") |  8.20. `pg_lsn` Type  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datatype-oid.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

