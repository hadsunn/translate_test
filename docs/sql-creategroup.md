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

Supported Versions: [Current](/docs/current/sql-creategroup.html "PostgreSQL
17 - CREATE GROUP") ([17](/docs/17/sql-creategroup.html "PostgreSQL 17 -
CREATE GROUP")) / [16](/docs/16/sql-creategroup.html "PostgreSQL 16 - CREATE
GROUP") / [15](/docs/15/sql-creategroup.html "PostgreSQL 15 - CREATE GROUP") /
[14](/docs/14/sql-creategroup.html "PostgreSQL 14 - CREATE GROUP") /
[13](/docs/13/sql-creategroup.html "PostgreSQL 13 - CREATE GROUP")

Development Versions: [18](/docs/18/sql-creategroup.html "PostgreSQL 18 -
CREATE GROUP") / [devel](/docs/devel/sql-creategroup.html "PostgreSQL devel -
CREATE GROUP")

Unsupported versions: [12](/docs/12/sql-creategroup.html "PostgreSQL 12 -
CREATE GROUP") / [11](/docs/11/sql-creategroup.html "PostgreSQL 11 - CREATE
GROUP") / [10](/docs/10/sql-creategroup.html "PostgreSQL 10 - CREATE GROUP") /
[9.6](/docs/9.6/sql-creategroup.html "PostgreSQL 9.6 - CREATE GROUP") /
[9.5](/docs/9.5/sql-creategroup.html "PostgreSQL 9.5 - CREATE GROUP") /
[9.4](/docs/9.4/sql-creategroup.html "PostgreSQL 9.4 - CREATE GROUP") /
[9.3](/docs/9.3/sql-creategroup.html "PostgreSQL 9.3 - CREATE GROUP") /
[9.2](/docs/9.2/sql-creategroup.html "PostgreSQL 9.2 - CREATE GROUP") /
[9.1](/docs/9.1/sql-creategroup.html "PostgreSQL 9.1 - CREATE GROUP") /
[9.0](/docs/9.0/sql-creategroup.html "PostgreSQL 9.0 - CREATE GROUP") /
[8.4](/docs/8.4/sql-creategroup.html "PostgreSQL 8.4 - CREATE GROUP") /
[8.3](/docs/8.3/sql-creategroup.html "PostgreSQL 8.3 - CREATE GROUP") /
[8.2](/docs/8.2/sql-creategroup.html "PostgreSQL 8.2 - CREATE GROUP") /
[8.1](/docs/8.1/sql-creategroup.html "PostgreSQL 8.1 - CREATE GROUP") /
[8.0](/docs/8.0/sql-creategroup.html "PostgreSQL 8.0 - CREATE GROUP") /
[7.4](/docs/7.4/sql-creategroup.html "PostgreSQL 7.4 - CREATE GROUP") /
[7.3](/docs/7.3/sql-creategroup.html "PostgreSQL 7.3 - CREATE GROUP") /
[7.2](/docs/7.2/sql-creategroup.html "PostgreSQL 7.2 - CREATE GROUP") /
[7.1](/docs/7.1/sql-creategroup.html "PostgreSQL 7.1 - CREATE GROUP")

__

CREATE GROUP  
---  
[Prev](sql-createfunction.html "CREATE FUNCTION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createindex.html "CREATE INDEX")  
  
* * *

## CREATE GROUP

CREATE GROUP — define a new database role

## Synopsis

    
    
    CREATE GROUP _name_ [ [ WITH ] _option_ [ ... ] ]
    
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

`CREATE GROUP` is now an alias for [CREATE ROLE](sql-createrole.html "CREATE
ROLE").

## Compatibility

There is no `CREATE GROUP` statement in the SQL standard.

## See Also

[CREATE ROLE](sql-createrole.html "CREATE ROLE")

* * *

[Prev](sql-createfunction.html "CREATE FUNCTION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createindex.html "CREATE INDEX")  
---|---|---  
CREATE FUNCTION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE INDEX  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-creategroup.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

