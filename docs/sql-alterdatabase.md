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

Supported Versions: [Current](/docs/current/sql-alterdatabase.html "PostgreSQL
17 - ALTER DATABASE") ([17](/docs/17/sql-alterdatabase.html "PostgreSQL 17 -
ALTER DATABASE")) / [16](/docs/16/sql-alterdatabase.html "PostgreSQL 16 -
ALTER DATABASE") / [15](/docs/15/sql-alterdatabase.html "PostgreSQL 15 - ALTER
DATABASE") / [14](/docs/14/sql-alterdatabase.html "PostgreSQL 14 - ALTER
DATABASE") / [13](/docs/13/sql-alterdatabase.html "PostgreSQL 13 - ALTER
DATABASE")

Development Versions: [18](/docs/18/sql-alterdatabase.html "PostgreSQL 18 -
ALTER DATABASE") / [devel](/docs/devel/sql-alterdatabase.html "PostgreSQL
devel - ALTER DATABASE")

Unsupported versions: [12](/docs/12/sql-alterdatabase.html "PostgreSQL 12 -
ALTER DATABASE") / [11](/docs/11/sql-alterdatabase.html "PostgreSQL 11 - ALTER
DATABASE") / [10](/docs/10/sql-alterdatabase.html "PostgreSQL 10 - ALTER
DATABASE") / [9.6](/docs/9.6/sql-alterdatabase.html "PostgreSQL 9.6 - ALTER
DATABASE") / [9.5](/docs/9.5/sql-alterdatabase.html "PostgreSQL 9.5 - ALTER
DATABASE") / [9.4](/docs/9.4/sql-alterdatabase.html "PostgreSQL 9.4 - ALTER
DATABASE") / [9.3](/docs/9.3/sql-alterdatabase.html "PostgreSQL 9.3 - ALTER
DATABASE") / [9.2](/docs/9.2/sql-alterdatabase.html "PostgreSQL 9.2 - ALTER
DATABASE") / [9.1](/docs/9.1/sql-alterdatabase.html "PostgreSQL 9.1 - ALTER
DATABASE") / [9.0](/docs/9.0/sql-alterdatabase.html "PostgreSQL 9.0 - ALTER
DATABASE") / [8.4](/docs/8.4/sql-alterdatabase.html "PostgreSQL 8.4 - ALTER
DATABASE") / [8.3](/docs/8.3/sql-alterdatabase.html "PostgreSQL 8.3 - ALTER
DATABASE") / [8.2](/docs/8.2/sql-alterdatabase.html "PostgreSQL 8.2 - ALTER
DATABASE") / [8.1](/docs/8.1/sql-alterdatabase.html "PostgreSQL 8.1 - ALTER
DATABASE") / [8.0](/docs/8.0/sql-alterdatabase.html "PostgreSQL 8.0 - ALTER
DATABASE") / [7.4](/docs/7.4/sql-alterdatabase.html "PostgreSQL 7.4 - ALTER
DATABASE") / [7.3](/docs/7.3/sql-alterdatabase.html "PostgreSQL 7.3 - ALTER
DATABASE")

__

ALTER DATABASE  
---  
[Prev](sql-alterconversion.html "ALTER CONVERSION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterdefaultprivileges.html "ALTER DEFAULT PRIVILEGES")  
  
* * *

## ALTER DATABASE

ALTER DATABASE — change a database

## Synopsis

    
    
    ALTER DATABASE _name_ [ [ WITH ] _option_ [ ... ] ]
    
    where _option_ can be:
    
        ALLOW_CONNECTIONS _allowconn_
        CONNECTION LIMIT _connlimit_
        IS_TEMPLATE _istemplate_
    
    ALTER DATABASE _name_ RENAME TO _new_name_
    
    ALTER DATABASE _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    
    ALTER DATABASE _name_ SET TABLESPACE _new_tablespace_
    
    ALTER DATABASE _name_ REFRESH COLLATION VERSION
    
    ALTER DATABASE _name_ SET _configuration_parameter_ { TO | = } { _value_ | DEFAULT }
    ALTER DATABASE _name_ SET _configuration_parameter_ FROM CURRENT
    ALTER DATABASE _name_ RESET _configuration_parameter_
    ALTER DATABASE _name_ RESET ALL
    

## Description

`ALTER DATABASE` changes the attributes of a database.

The first form changes certain per-database settings. (See below for details.)
Only the database owner or a superuser can change these settings.

The second form changes the name of the database. Only the database owner or a
superuser can rename a database; non-superuser owners must also have the
`CREATEDB` privilege. The current database cannot be renamed. (Connect to a
different database if you need to do that.)

The third form changes the owner of the database. To alter the owner, you must
be able to `SET ROLE` to the new owning role, and you must have the `CREATEDB`
privilege. (Note that superusers have all these privileges automatically.)

The fourth form changes the default tablespace of the database. Only the
database owner or a superuser can do this; you must also have create privilege
for the new tablespace. This command physically moves any tables or indexes in
the database's old default tablespace to the new tablespace. The new default
tablespace must be empty for this database, and no one can be connected to the
database. Tables and indexes in non-default tablespaces are unaffected.

The remaining forms change the session default for a run-time configuration
variable for a PostgreSQL database. Whenever a new session is subsequently
started in that database, the specified value becomes the session default
value. The database-specific default overrides whatever setting is present in
`postgresql.conf` or has been received from the `postgres` command line. Only
the database owner or a superuser can change the session defaults for a
database. Certain variables cannot be set this way, or can only be set by a
superuser.

## Parameters

_`name`_

    

The name of the database whose attributes are to be altered.

_`allowconn`_

    

If false then no one can connect to this database.

_`connlimit`_

    

How many concurrent connections can be made to this database. -1 means no
limit.

_`istemplate`_

    

If true, then this database can be cloned by any user with `CREATEDB`
privileges; if false, then only superusers or the owner of the database can
clone it.

_`new_name`_

    

The new name of the database.

_`new_owner`_

    

The new owner of the database.

_`new_tablespace`_

    

The new default tablespace of the database.

This form of the command cannot be executed inside a transaction block.

`REFRESH COLLATION VERSION`

    

Update the database collation version. See [Notes](sql-
altercollation.html#SQL-ALTERCOLLATION-NOTES "Notes") for background.

_`configuration_parameter`_  
 _`value`_

    

Set this database's session default for the specified configuration parameter
to the given value. If _`value`_ is `DEFAULT` or, equivalently, `RESET` is
used, the database-specific setting is removed, so the system-wide default
setting will be inherited in new sessions. Use `RESET ALL` to clear all
database-specific settings. `SET FROM CURRENT` saves the session's current
value of the parameter as the database-specific value.

See [SET](sql-set.html "SET") and [Chapter 20](runtime-config.html
"Chapter 20. Server Configuration") for more information about allowed
parameter names and values.

## Notes

It is also possible to tie a session default to a specific role rather than to
a database; see [ALTER ROLE](sql-alterrole.html "ALTER ROLE"). Role-specific
settings override database-specific ones if there is a conflict.

## Examples

To disable index scans by default in the database `test`:

    
    
    ALTER DATABASE test SET enable_indexscan TO off;
    

## Compatibility

The `ALTER DATABASE` statement is a PostgreSQL extension.

## See Also

[CREATE DATABASE](sql-createdatabase.html "CREATE DATABASE"), [DROP
DATABASE](sql-dropdatabase.html "DROP DATABASE"), [SET](sql-set.html "SET"),
[CREATE TABLESPACE](sql-createtablespace.html "CREATE TABLESPACE")

* * *

[Prev](sql-alterconversion.html "ALTER CONVERSION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterdefaultprivileges.html "ALTER DEFAULT PRIVILEGES")  
---|---|---  
ALTER CONVERSION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER DEFAULT PRIVILEGES  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterdatabase.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

