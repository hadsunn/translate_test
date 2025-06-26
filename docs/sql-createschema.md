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

Supported Versions: [Current](/docs/current/sql-createschema.html "PostgreSQL
17 - CREATE SCHEMA") ([17](/docs/17/sql-createschema.html "PostgreSQL 17 -
CREATE SCHEMA")) / [16](/docs/16/sql-createschema.html "PostgreSQL 16 - CREATE
SCHEMA") / [15](/docs/15/sql-createschema.html "PostgreSQL 15 - CREATE
SCHEMA") / [14](/docs/14/sql-createschema.html "PostgreSQL 14 - CREATE
SCHEMA") / [13](/docs/13/sql-createschema.html "PostgreSQL 13 - CREATE
SCHEMA")

Development Versions: [18](/docs/18/sql-createschema.html "PostgreSQL 18 -
CREATE SCHEMA") / [devel](/docs/devel/sql-createschema.html "PostgreSQL devel
- CREATE SCHEMA")

Unsupported versions: [12](/docs/12/sql-createschema.html "PostgreSQL 12 -
CREATE SCHEMA") / [11](/docs/11/sql-createschema.html "PostgreSQL 11 - CREATE
SCHEMA") / [10](/docs/10/sql-createschema.html "PostgreSQL 10 - CREATE
SCHEMA") / [9.6](/docs/9.6/sql-createschema.html "PostgreSQL 9.6 - CREATE
SCHEMA") / [9.5](/docs/9.5/sql-createschema.html "PostgreSQL 9.5 - CREATE
SCHEMA") / [9.4](/docs/9.4/sql-createschema.html "PostgreSQL 9.4 - CREATE
SCHEMA") / [9.3](/docs/9.3/sql-createschema.html "PostgreSQL 9.3 - CREATE
SCHEMA") / [9.2](/docs/9.2/sql-createschema.html "PostgreSQL 9.2 - CREATE
SCHEMA") / [9.1](/docs/9.1/sql-createschema.html "PostgreSQL 9.1 - CREATE
SCHEMA") / [9.0](/docs/9.0/sql-createschema.html "PostgreSQL 9.0 - CREATE
SCHEMA") / [8.4](/docs/8.4/sql-createschema.html "PostgreSQL 8.4 - CREATE
SCHEMA") / [8.3](/docs/8.3/sql-createschema.html "PostgreSQL 8.3 - CREATE
SCHEMA") / [8.2](/docs/8.2/sql-createschema.html "PostgreSQL 8.2 - CREATE
SCHEMA") / [8.1](/docs/8.1/sql-createschema.html "PostgreSQL 8.1 - CREATE
SCHEMA") / [8.0](/docs/8.0/sql-createschema.html "PostgreSQL 8.0 - CREATE
SCHEMA") / [7.4](/docs/7.4/sql-createschema.html "PostgreSQL 7.4 - CREATE
SCHEMA") / [7.3](/docs/7.3/sql-createschema.html "PostgreSQL 7.3 - CREATE
SCHEMA")

__

CREATE SCHEMA  
---  
[Prev](sql-createrule.html "CREATE RULE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createsequence.html "CREATE SEQUENCE")  
  
* * *

## CREATE SCHEMA

CREATE SCHEMA — define a new schema

## Synopsis

    
    
    CREATE SCHEMA _schema_name_ [ AUTHORIZATION _role_specification_ ] [ _schema_element_ [ ... ] ]
    CREATE SCHEMA AUTHORIZATION _role_specification_ [ _schema_element_ [ ... ] ]
    CREATE SCHEMA IF NOT EXISTS _schema_name_ [ AUTHORIZATION _role_specification_ ]
    CREATE SCHEMA IF NOT EXISTS AUTHORIZATION _role_specification_
    
    where _role_specification_ can be:
    
        _user_name_
      | CURRENT_ROLE
      | CURRENT_USER
      | SESSION_USER
    

## Description

`CREATE SCHEMA` enters a new schema into the current database. The schema name
must be distinct from the name of any existing schema in the current database.

A schema is essentially a namespace: it contains named objects (tables, data
types, functions, and operators) whose names can duplicate those of other
objects existing in other schemas. Named objects are accessed either by
“qualifying” their names with the schema name as a prefix, or by setting a
search path that includes the desired schema(s). A `CREATE` command specifying
an unqualified object name creates the object in the current schema (the one
at the front of the search path, which can be determined with the function
`current_schema`).

Optionally, `CREATE SCHEMA` can include subcommands to create objects within
the new schema. The subcommands are treated essentially the same as separate
commands issued after creating the schema, except that if the `AUTHORIZATION`
clause is used, all the created objects will be owned by that user.

## Parameters

_`schema_name`_

    

The name of a schema to be created. If this is omitted, the _`user_name`_ is
used as the schema name. The name cannot begin with `pg_`, as such names are
reserved for system schemas.

_`user_name`_

    

The role name of the user who will own the new schema. If omitted, defaults to
the user executing the command. To create a schema owned by another role, you
must be able to `SET ROLE` to that role.

_`schema_element`_

    

An SQL statement defining an object to be created within the schema.
Currently, only `CREATE TABLE`, `CREATE VIEW`, `CREATE INDEX`, `CREATE
SEQUENCE`, `CREATE TRIGGER` and `GRANT` are accepted as clauses within `CREATE
SCHEMA`. Other kinds of objects may be created in separate commands after the
schema is created.

`IF NOT EXISTS`

    

Do nothing (except issuing a notice) if a schema with the same name already
exists. _`schema_element`_ subcommands cannot be included when this option is
used.

## Notes

To create a schema, the invoking user must have the `CREATE` privilege for the
current database. (Of course, superusers bypass this check.)

## Examples

Create a schema:

    
    
    CREATE SCHEMA myschema;
    

Create a schema for user `joe`; the schema will also be named `joe`:

    
    
    CREATE SCHEMA AUTHORIZATION joe;
    

Create a schema named `test` that will be owned by user `joe`, unless there
already is a schema named `test`. (It does not matter whether `joe` owns the
pre-existing schema.)

    
    
    CREATE SCHEMA IF NOT EXISTS test AUTHORIZATION joe;
    

Create a schema and create a table and view within it:

    
    
    CREATE SCHEMA hollywood
        CREATE TABLE films (title text, release date, awards text[])
        CREATE VIEW winners AS
            SELECT title, release FROM films WHERE awards IS NOT NULL;
    

Notice that the individual subcommands do not end with semicolons.

The following is an equivalent way of accomplishing the same result:

    
    
    CREATE SCHEMA hollywood;
    CREATE TABLE hollywood.films (title text, release date, awards text[]);
    CREATE VIEW hollywood.winners AS
        SELECT title, release FROM hollywood.films WHERE awards IS NOT NULL;
    

## Compatibility

The SQL standard allows a `DEFAULT CHARACTER SET` clause in `CREATE SCHEMA`,
as well as more subcommand types than are presently accepted by PostgreSQL.

The SQL standard specifies that the subcommands in `CREATE SCHEMA` can appear
in any order. The present PostgreSQL implementation does not handle all cases
of forward references in subcommands; it might sometimes be necessary to
reorder the subcommands in order to avoid forward references.

According to the SQL standard, the owner of a schema always owns all objects
within it. PostgreSQL allows schemas to contain objects owned by users other
than the schema owner. This can happen only if the schema owner grants the
`CREATE` privilege on their schema to someone else, or a superuser chooses to
create objects in it.

The `IF NOT EXISTS` option is a PostgreSQL extension.

## See Also

[ALTER SCHEMA](sql-alterschema.html "ALTER SCHEMA"), [DROP SCHEMA](sql-
dropschema.html "DROP SCHEMA")

* * *

[Prev](sql-createrule.html "CREATE RULE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createsequence.html "CREATE SEQUENCE")  
---|---|---  
CREATE RULE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE SEQUENCE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createschema.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

