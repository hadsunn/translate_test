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

Supported Versions: [Current](/docs/current/sql-alterschema.html "PostgreSQL
17 - ALTER SCHEMA") ([17](/docs/17/sql-alterschema.html "PostgreSQL 17 - ALTER
SCHEMA")) / [16](/docs/16/sql-alterschema.html "PostgreSQL 16 - ALTER SCHEMA")
/ [15](/docs/15/sql-alterschema.html "PostgreSQL 15 - ALTER SCHEMA") /
[14](/docs/14/sql-alterschema.html "PostgreSQL 14 - ALTER SCHEMA") /
[13](/docs/13/sql-alterschema.html "PostgreSQL 13 - ALTER SCHEMA")

Development Versions: [18](/docs/18/sql-alterschema.html "PostgreSQL 18 -
ALTER SCHEMA") / [devel](/docs/devel/sql-alterschema.html "PostgreSQL devel -
ALTER SCHEMA")

Unsupported versions: [12](/docs/12/sql-alterschema.html "PostgreSQL 12 -
ALTER SCHEMA") / [11](/docs/11/sql-alterschema.html "PostgreSQL 11 - ALTER
SCHEMA") / [10](/docs/10/sql-alterschema.html "PostgreSQL 10 - ALTER SCHEMA")
/ [9.6](/docs/9.6/sql-alterschema.html "PostgreSQL 9.6 - ALTER SCHEMA") /
[9.5](/docs/9.5/sql-alterschema.html "PostgreSQL 9.5 - ALTER SCHEMA") /
[9.4](/docs/9.4/sql-alterschema.html "PostgreSQL 9.4 - ALTER SCHEMA") /
[9.3](/docs/9.3/sql-alterschema.html "PostgreSQL 9.3 - ALTER SCHEMA") /
[9.2](/docs/9.2/sql-alterschema.html "PostgreSQL 9.2 - ALTER SCHEMA") /
[9.1](/docs/9.1/sql-alterschema.html "PostgreSQL 9.1 - ALTER SCHEMA") /
[9.0](/docs/9.0/sql-alterschema.html "PostgreSQL 9.0 - ALTER SCHEMA") /
[8.4](/docs/8.4/sql-alterschema.html "PostgreSQL 8.4 - ALTER SCHEMA") /
[8.3](/docs/8.3/sql-alterschema.html "PostgreSQL 8.3 - ALTER SCHEMA") /
[8.2](/docs/8.2/sql-alterschema.html "PostgreSQL 8.2 - ALTER SCHEMA") /
[8.1](/docs/8.1/sql-alterschema.html "PostgreSQL 8.1 - ALTER SCHEMA") /
[8.0](/docs/8.0/sql-alterschema.html "PostgreSQL 8.0 - ALTER SCHEMA") /
[7.4](/docs/7.4/sql-alterschema.html "PostgreSQL 7.4 - ALTER SCHEMA")

__

ALTER SCHEMA  
---  
[Prev](sql-alterrule.html "ALTER RULE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-altersequence.html "ALTER SEQUENCE")  
  
* * *

## ALTER SCHEMA

ALTER SCHEMA — change the definition of a schema

## Synopsis

    
    
    ALTER SCHEMA _name_ RENAME TO _new_name_
    ALTER SCHEMA _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    

## Description

`ALTER SCHEMA` changes the definition of a schema.

You must own the schema to use `ALTER SCHEMA`. To rename a schema you must
also have the `CREATE` privilege for the database. To alter the owner, you
must be able to `SET ROLE` to the new owning role, and that role must have the
`CREATE` privilege for the database. (Note that superusers have all these
privileges automatically.)

## Parameters

_`name`_

    

The name of an existing schema.

_`new_name`_

    

The new name of the schema. The new name cannot begin with `pg_`, as such
names are reserved for system schemas.

_`new_owner`_

    

The new owner of the schema.

## Compatibility

There is no `ALTER SCHEMA` statement in the SQL standard.

## See Also

[CREATE SCHEMA](sql-createschema.html "CREATE SCHEMA"), [DROP SCHEMA](sql-
dropschema.html "DROP SCHEMA")

* * *

[Prev](sql-alterrule.html "ALTER RULE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-altersequence.html "ALTER SEQUENCE")  
---|---|---  
ALTER RULE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER SEQUENCE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterschema.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

