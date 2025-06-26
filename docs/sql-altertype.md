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

Supported Versions: [Current](/docs/current/sql-altertype.html "PostgreSQL 17
- ALTER TYPE") ([17](/docs/17/sql-altertype.html "PostgreSQL 17 - ALTER
TYPE")) / [16](/docs/16/sql-altertype.html "PostgreSQL 16 - ALTER TYPE") /
[15](/docs/15/sql-altertype.html "PostgreSQL 15 - ALTER TYPE") /
[14](/docs/14/sql-altertype.html "PostgreSQL 14 - ALTER TYPE") /
[13](/docs/13/sql-altertype.html "PostgreSQL 13 - ALTER TYPE")

Development Versions: [18](/docs/18/sql-altertype.html "PostgreSQL 18 - ALTER
TYPE") / [devel](/docs/devel/sql-altertype.html "PostgreSQL devel - ALTER
TYPE")

Unsupported versions: [12](/docs/12/sql-altertype.html "PostgreSQL 12 - ALTER
TYPE") / [11](/docs/11/sql-altertype.html "PostgreSQL 11 - ALTER TYPE") /
[10](/docs/10/sql-altertype.html "PostgreSQL 10 - ALTER TYPE") /
[9.6](/docs/9.6/sql-altertype.html "PostgreSQL 9.6 - ALTER TYPE") /
[9.5](/docs/9.5/sql-altertype.html "PostgreSQL 9.5 - ALTER TYPE") /
[9.4](/docs/9.4/sql-altertype.html "PostgreSQL 9.4 - ALTER TYPE") /
[9.3](/docs/9.3/sql-altertype.html "PostgreSQL 9.3 - ALTER TYPE") /
[9.2](/docs/9.2/sql-altertype.html "PostgreSQL 9.2 - ALTER TYPE") /
[9.1](/docs/9.1/sql-altertype.html "PostgreSQL 9.1 - ALTER TYPE") /
[9.0](/docs/9.0/sql-altertype.html "PostgreSQL 9.0 - ALTER TYPE") /
[8.4](/docs/8.4/sql-altertype.html "PostgreSQL 8.4 - ALTER TYPE") /
[8.3](/docs/8.3/sql-altertype.html "PostgreSQL 8.3 - ALTER TYPE") /
[8.2](/docs/8.2/sql-altertype.html "PostgreSQL 8.2 - ALTER TYPE") /
[8.1](/docs/8.1/sql-altertype.html "PostgreSQL 8.1 - ALTER TYPE") /
[8.0](/docs/8.0/sql-altertype.html "PostgreSQL 8.0 - ALTER TYPE")

__

ALTER TYPE  
---  
[Prev](sql-altertrigger.html "ALTER TRIGGER")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alteruser.html "ALTER USER")  
  
* * *

## ALTER TYPE

ALTER TYPE — change the definition of a type

## Synopsis

    
    
    ALTER TYPE _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER TYPE _name_ RENAME TO _new_name_
    ALTER TYPE _name_ SET SCHEMA _new_schema_
    ALTER TYPE _name_ RENAME ATTRIBUTE _attribute_name_ TO _new_attribute_name_ [ CASCADE | RESTRICT ]
    ALTER TYPE _name_ _action_ [, ... ]
    ALTER TYPE _name_ ADD VALUE [ IF NOT EXISTS ] _new_enum_value_ [ { BEFORE | AFTER } _neighbor_enum_value_ ]
    ALTER TYPE _name_ RENAME VALUE _existing_enum_value_ TO _new_enum_value_
    ALTER TYPE _name_ SET ( _property_ = _value_ [, ... ] )
    
    where _action_ is one of:
    
        ADD ATTRIBUTE _attribute_name_ _data_type_ [ COLLATE _collation_ ] [ CASCADE | RESTRICT ]
        DROP ATTRIBUTE [ IF EXISTS ] _attribute_name_ [ CASCADE | RESTRICT ]
        ALTER ATTRIBUTE _attribute_name_ [ SET DATA ] TYPE _data_type_ [ COLLATE _collation_ ] [ CASCADE | RESTRICT ]
    

## Description

`ALTER TYPE` changes the definition of an existing type. There are several
subforms:

`OWNER`

    

This form changes the owner of the type.

`RENAME`

    

This form changes the name of the type.

`SET SCHEMA`

    

This form moves the type into another schema.

`RENAME ATTRIBUTE`

    

This form is only usable with composite types. It changes the name of an
individual attribute of the type.

`ADD ATTRIBUTE`

    

This form adds a new attribute to a composite type, using the same syntax as
[`CREATE TYPE`](sql-createtype.html "CREATE TYPE").

`DROP ATTRIBUTE [ IF EXISTS ]`

    

This form drops an attribute from a composite type. If `IF EXISTS` is
specified and the attribute does not exist, no error is thrown. In this case a
notice is issued instead.

`ALTER ATTRIBUTE ... SET DATA TYPE`

    

This form changes the type of an attribute of a composite type.

`ADD VALUE [ IF NOT EXISTS ] [ BEFORE | AFTER ]`
    

This form adds a new value to an enum type. The new value's place in the
enum's ordering can be specified as being `BEFORE` or `AFTER` one of the
existing values. Otherwise, the new item is added at the end of the list of
values.

If `IF NOT EXISTS` is specified, it is not an error if the type already
contains the new value: a notice is issued but no other action is taken.
Otherwise, an error will occur if the new value is already present.

`RENAME VALUE`

    

This form renames a value of an enum type. The value's place in the enum's
ordering is not affected. An error will occur if the specified value is not
present or the new name is already present.

`SET ( _`property`_ = _`value`_ [, ... ] )`

    

This form is only applicable to base types. It allows adjustment of a subset
of the base-type properties that can be set in `CREATE TYPE`. Specifically,
these properties can be changed:

  * `RECEIVE` can be set to the name of a binary input function, or `NONE` to remove the type's binary input function. Using this option requires superuser privilege.

  * `SEND` can be set to the name of a binary output function, or `NONE` to remove the type's binary output function. Using this option requires superuser privilege.

  * `TYPMOD_IN` can be set to the name of a type modifier input function, or `NONE` to remove the type's type modifier input function. Using this option requires superuser privilege.

  * `TYPMOD_OUT` can be set to the name of a type modifier output function, or `NONE` to remove the type's type modifier output function. Using this option requires superuser privilege.

  * `ANALYZE` can be set to the name of a type-specific statistics collection function, or `NONE` to remove the type's statistics collection function. Using this option requires superuser privilege.

  * `SUBSCRIPT` can be set to the name of a type-specific subscripting handler function, or `NONE` to remove the type's subscripting handler function. Using this option requires superuser privilege.

  * `STORAGE` can be set to `plain`, `extended`, `external`, or `main` (see [Section 73.2](storage-toast.html "73.2. TOAST") for more information about what these mean). However, changing from `plain` to another setting requires superuser privilege (because it requires that the type's C functions all be TOAST-ready), and changing to `plain` from another setting is not allowed at all (since the type may already have TOASTed values present in the database). Note that changing this option doesn't by itself change any stored data, it just sets the default TOAST strategy to be used for table columns created in the future. See [ALTER TABLE](sql-altertable.html "ALTER TABLE") to change the TOAST strategy for existing table columns.

See [CREATE TYPE](sql-createtype.html "CREATE TYPE") for more details about
these type properties. Note that where appropriate, a change in these
properties for a base type will be propagated automatically to domains based
on that type.

The `ADD ATTRIBUTE`, `DROP ATTRIBUTE`, and `ALTER ATTRIBUTE` actions can be
combined into a list of multiple alterations to apply in parallel. For
example, it is possible to add several attributes and/or alter the type of
several attributes in a single command.

You must own the type to use `ALTER TYPE`. To change the schema of a type, you
must also have `CREATE` privilege on the new schema. To alter the owner, you
must be able to `SET ROLE` to the new owning role, and that role must have
`CREATE` privilege on the type's schema. (These restrictions enforce that
altering the owner doesn't do anything you couldn't do by dropping and
recreating the type. However, a superuser can alter ownership of any type
anyway.) To add an attribute or alter an attribute type, you must also have
`USAGE` privilege on the attribute's data type.

## Parameters

_`name`_

    

The name (possibly schema-qualified) of an existing type to alter.

_`new_name`_

    

The new name for the type.

_`new_owner`_

    

The user name of the new owner of the type.

_`new_schema`_

    

The new schema for the type.

_`attribute_name`_

    

The name of the attribute to add, alter, or drop.

_`new_attribute_name`_

    

The new name of the attribute to be renamed.

_`data_type`_

    

The data type of the attribute to add, or the new type of the attribute to
alter.

_`new_enum_value`_

    

The new value to be added to an enum type's list of values, or the new name to
be given to an existing value. Like all enum literals, it needs to be quoted.

_`neighbor_enum_value`_

    

The existing enum value that the new value should be added immediately before
or after in the enum type's sort ordering. Like all enum literals, it needs to
be quoted.

_`existing_enum_value`_

    

The existing enum value that should be renamed. Like all enum literals, it
needs to be quoted.

_`property`_

    

The name of a base-type property to be modified; see above for possible
values.

`CASCADE`

    

Automatically propagate the operation to typed tables of the type being
altered, and their descendants.

`RESTRICT`

    

Refuse the operation if the type being altered is the type of a typed table.
This is the default.

## Notes

If `ALTER TYPE ... ADD VALUE` (the form that adds a new value to an enum type)
is executed inside a transaction block, the new value cannot be used until
after the transaction has been committed.

Comparisons involving an added enum value will sometimes be slower than
comparisons involving only original members of the enum type. This will
usually only occur if `BEFORE` or `AFTER` is used to set the new value's sort
position somewhere other than at the end of the list. However, sometimes it
will happen even though the new value is added at the end (this occurs if the
OID counter “wrapped around” since the original creation of the enum type).
The slowdown is usually insignificant; but if it matters, optimal performance
can be regained by dropping and recreating the enum type, or by dumping and
restoring the database.

## Examples

To rename a data type:

    
    
    ALTER TYPE electronic_mail RENAME TO email;
    

To change the owner of the type `email` to `joe`:

    
    
    ALTER TYPE email OWNER TO joe;
    

To change the schema of the type `email` to `customers`:

    
    
    ALTER TYPE email SET SCHEMA customers;
    

To add a new attribute to a composite type:

    
    
    ALTER TYPE compfoo ADD ATTRIBUTE f3 int;
    

To add a new value to an enum type in a particular sort position:

    
    
    ALTER TYPE colors ADD VALUE 'orange' AFTER 'red';
    

To rename an enum value:

    
    
    ALTER TYPE colors RENAME VALUE 'purple' TO 'mauve';
    

To create binary I/O functions for an existing base type:

    
    
    CREATE FUNCTION mytypesend(mytype) RETURNS bytea ...;
    CREATE FUNCTION mytyperecv(internal, oid, integer) RETURNS mytype ...;
    ALTER TYPE mytype SET (
        SEND = mytypesend,
        RECEIVE = mytyperecv
    );
    

## Compatibility

The variants to add and drop attributes are part of the SQL standard; the
other variants are PostgreSQL extensions.

## See Also

[CREATE TYPE](sql-createtype.html "CREATE TYPE"), [DROP TYPE](sql-
droptype.html "DROP TYPE")

* * *

[Prev](sql-altertrigger.html "ALTER TRIGGER")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alteruser.html "ALTER USER")  
---|---|---  
ALTER TRIGGER  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER USER  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-altertype.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

