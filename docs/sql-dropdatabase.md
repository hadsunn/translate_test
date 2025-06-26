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

Supported Versions: [Current](/docs/current/sql-dropdatabase.html "PostgreSQL
17 - DROP DATABASE") ([17](/docs/17/sql-dropdatabase.html "PostgreSQL 17 -
DROP DATABASE")) / [16](/docs/16/sql-dropdatabase.html "PostgreSQL 16 - DROP
DATABASE") / [15](/docs/15/sql-dropdatabase.html "PostgreSQL 15 - DROP
DATABASE") / [14](/docs/14/sql-dropdatabase.html "PostgreSQL 14 - DROP
DATABASE") / [13](/docs/13/sql-dropdatabase.html "PostgreSQL 13 - DROP
DATABASE")

Development Versions: [18](/docs/18/sql-dropdatabase.html "PostgreSQL 18 -
DROP DATABASE") / [devel](/docs/devel/sql-dropdatabase.html "PostgreSQL devel
- DROP DATABASE")

Unsupported versions: [12](/docs/12/sql-dropdatabase.html "PostgreSQL 12 -
DROP DATABASE") / [11](/docs/11/sql-dropdatabase.html "PostgreSQL 11 - DROP
DATABASE") / [10](/docs/10/sql-dropdatabase.html "PostgreSQL 10 - DROP
DATABASE") / [9.6](/docs/9.6/sql-dropdatabase.html "PostgreSQL 9.6 - DROP
DATABASE") / [9.5](/docs/9.5/sql-dropdatabase.html "PostgreSQL 9.5 - DROP
DATABASE") / [9.4](/docs/9.4/sql-dropdatabase.html "PostgreSQL 9.4 - DROP
DATABASE") / [9.3](/docs/9.3/sql-dropdatabase.html "PostgreSQL 9.3 - DROP
DATABASE") / [9.2](/docs/9.2/sql-dropdatabase.html "PostgreSQL 9.2 - DROP
DATABASE") / [9.1](/docs/9.1/sql-dropdatabase.html "PostgreSQL 9.1 - DROP
DATABASE") / [9.0](/docs/9.0/sql-dropdatabase.html "PostgreSQL 9.0 - DROP
DATABASE") / [8.4](/docs/8.4/sql-dropdatabase.html "PostgreSQL 8.4 - DROP
DATABASE") / [8.3](/docs/8.3/sql-dropdatabase.html "PostgreSQL 8.3 - DROP
DATABASE") / [8.2](/docs/8.2/sql-dropdatabase.html "PostgreSQL 8.2 - DROP
DATABASE") / [8.1](/docs/8.1/sql-dropdatabase.html "PostgreSQL 8.1 - DROP
DATABASE") / [8.0](/docs/8.0/sql-dropdatabase.html "PostgreSQL 8.0 - DROP
DATABASE") / [7.4](/docs/7.4/sql-dropdatabase.html "PostgreSQL 7.4 - DROP
DATABASE") / [7.3](/docs/7.3/sql-dropdatabase.html "PostgreSQL 7.3 - DROP
DATABASE") / [7.2](/docs/7.2/sql-dropdatabase.html "PostgreSQL 7.2 - DROP
DATABASE") / [7.1](/docs/7.1/sql-dropdatabase.html "PostgreSQL 7.1 - DROP
DATABASE")

__

DROP DATABASE  
---  
[Prev](sql-dropconversion.html "DROP CONVERSION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropdomain.html "DROP DOMAIN")  
  
* * *

## DROP DATABASE

DROP DATABASE — remove a database

## Synopsis

    
    
    DROP DATABASE [ IF EXISTS ] _name_ [ [ WITH ] ( _option_ [, ...] ) ]
    
    where _option_ can be:
    
        FORCE
    

## Description

`DROP DATABASE` drops a database. It removes the catalog entries for the
database and deletes the directory containing the data. It can only be
executed by the database owner. It cannot be executed while you are connected
to the target database. (Connect to `postgres` or any other database to issue
this command.) Also, if anyone else is connected to the target database, this
command will fail unless you use the `FORCE` option described below.

`DROP DATABASE` cannot be undone. Use it with care!

## Parameters

`IF EXISTS`

    

Do not throw an error if the database does not exist. A notice is issued in
this case.

_`name`_

    

The name of the database to remove.

`FORCE`

    

Attempt to terminate all existing connections to the target database. It
doesn't terminate if prepared transactions, active logical replication slots
or subscriptions are present in the target database.

This terminates background worker connections and connections that the current
user has permission to terminate with `pg_terminate_backend`, described in
[Section 9.27.2](functions-admin.html#FUNCTIONS-ADMIN-SIGNAL "9.27.2. Server
Signaling Functions"). If connections would remain, this command will fail.

## Notes

`DROP DATABASE` cannot be executed inside a transaction block.

This command cannot be executed while connected to the target database. Thus,
it might be more convenient to use the program [dropdb](app-dropdb.html
"dropdb") instead, which is a wrapper around this command.

## Compatibility

There is no `DROP DATABASE` statement in the SQL standard.

## See Also

[CREATE DATABASE](sql-createdatabase.html "CREATE DATABASE")

* * *

[Prev](sql-dropconversion.html "DROP CONVERSION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropdomain.html "DROP DOMAIN")  
---|---|---  
DROP CONVERSION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP DOMAIN  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropdatabase.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

