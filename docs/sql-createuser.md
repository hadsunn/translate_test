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

Supported Versions: [Current](/docs/current/sql-createuser.html "PostgreSQL 17
- CREATE USER") ([17](/docs/17/sql-createuser.html "PostgreSQL 17 - CREATE
USER")) / [16](/docs/16/sql-createuser.html "PostgreSQL 16 - CREATE USER") /
[15](/docs/15/sql-createuser.html "PostgreSQL 15 - CREATE USER") /
[14](/docs/14/sql-createuser.html "PostgreSQL 14 - CREATE USER") /
[13](/docs/13/sql-createuser.html "PostgreSQL 13 - CREATE USER")

Development Versions: [18](/docs/18/sql-createuser.html "PostgreSQL 18 -
CREATE USER") / [devel](/docs/devel/sql-createuser.html "PostgreSQL devel -
CREATE USER")

Unsupported versions: [12](/docs/12/sql-createuser.html "PostgreSQL 12 -
CREATE USER") / [11](/docs/11/sql-createuser.html "PostgreSQL 11 - CREATE
USER") / [10](/docs/10/sql-createuser.html "PostgreSQL 10 - CREATE USER") /
[9.6](/docs/9.6/sql-createuser.html "PostgreSQL 9.6 - CREATE USER") /
[9.5](/docs/9.5/sql-createuser.html "PostgreSQL 9.5 - CREATE USER") /
[9.4](/docs/9.4/sql-createuser.html "PostgreSQL 9.4 - CREATE USER") /
[9.3](/docs/9.3/sql-createuser.html "PostgreSQL 9.3 - CREATE USER") /
[9.2](/docs/9.2/sql-createuser.html "PostgreSQL 9.2 - CREATE USER") /
[9.1](/docs/9.1/sql-createuser.html "PostgreSQL 9.1 - CREATE USER") /
[9.0](/docs/9.0/sql-createuser.html "PostgreSQL 9.0 - CREATE USER") /
[8.4](/docs/8.4/sql-createuser.html "PostgreSQL 8.4 - CREATE USER") /
[8.3](/docs/8.3/sql-createuser.html "PostgreSQL 8.3 - CREATE USER") /
[8.2](/docs/8.2/sql-createuser.html "PostgreSQL 8.2 - CREATE USER") /
[8.1](/docs/8.1/sql-createuser.html "PostgreSQL 8.1 - CREATE USER") /
[8.0](/docs/8.0/sql-createuser.html "PostgreSQL 8.0 - CREATE USER") /
[7.4](/docs/7.4/sql-createuser.html "PostgreSQL 7.4 - CREATE USER") /
[7.3](/docs/7.3/sql-createuser.html "PostgreSQL 7.3 - CREATE USER") /
[7.2](/docs/7.2/sql-createuser.html "PostgreSQL 7.2 - CREATE USER") /
[7.1](/docs/7.1/sql-createuser.html "PostgreSQL 7.1 - CREATE USER")

__

CREATE USER  
---  
[Prev](sql-createtype.html "CREATE TYPE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createusermapping.html "CREATE USER MAPPING")  
  
* * *

## CREATE USER

CREATE USER — define a new database role

## Synopsis

    
    
    CREATE USER _name_ [ [ WITH ] _option_ [ ... ] ]
    
    where _option_ can be:
    
          SUPERUSER | NOSUPERUSER
        | CREATEDB | NOCREATEDB
        | CREATEROLE | NOCREATEROLE
        | INHERIT | NOINHERIT
        | LOGIN | NOLOGIN
        | REPLICATION | NOREPLICATION
        | BYPASSRLS | NOBYPASSRLS
        | CONNECTION LIMIT _connlimit_
        | [ ENCRYPTED ] PASSWORD '_password_ ' | PASSWORD NULL
        | VALID UNTIL '_timestamp_ '
        | IN ROLE _role_name_ [, ...]
        | IN GROUP _role_name_ [, ...]
        | ROLE _role_name_ [, ...]
        | ADMIN _role_name_ [, ...]
        | USER _role_name_ [, ...]
        | SYSID _uid_
    

## Description

`CREATE USER` is now an alias for [`CREATE ROLE`](sql-createrole.html "CREATE
ROLE"). The only difference is that when the command is spelled `CREATE USER`,
`LOGIN` is assumed by default, whereas `NOLOGIN` is assumed when the command
is spelled `CREATE ROLE`.

## Compatibility

The `CREATE USER` statement is a PostgreSQL extension. The SQL standard leaves
the definition of users to the implementation.

## See Also

[CREATE ROLE](sql-createrole.html "CREATE ROLE")

* * *

[Prev](sql-createtype.html "CREATE TYPE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createusermapping.html "CREATE USER MAPPING")  
---|---|---  
CREATE TYPE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE USER MAPPING  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createuser.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

