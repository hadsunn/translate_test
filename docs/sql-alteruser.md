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

Supported Versions: [Current](/docs/current/sql-alteruser.html "PostgreSQL 17
- ALTER USER") ([17](/docs/17/sql-alteruser.html "PostgreSQL 17 - ALTER
USER")) / [16](/docs/16/sql-alteruser.html "PostgreSQL 16 - ALTER USER") /
[15](/docs/15/sql-alteruser.html "PostgreSQL 15 - ALTER USER") /
[14](/docs/14/sql-alteruser.html "PostgreSQL 14 - ALTER USER") /
[13](/docs/13/sql-alteruser.html "PostgreSQL 13 - ALTER USER")

Development Versions: [18](/docs/18/sql-alteruser.html "PostgreSQL 18 - ALTER
USER") / [devel](/docs/devel/sql-alteruser.html "PostgreSQL devel - ALTER
USER")

Unsupported versions: [12](/docs/12/sql-alteruser.html "PostgreSQL 12 - ALTER
USER") / [11](/docs/11/sql-alteruser.html "PostgreSQL 11 - ALTER USER") /
[10](/docs/10/sql-alteruser.html "PostgreSQL 10 - ALTER USER") /
[9.6](/docs/9.6/sql-alteruser.html "PostgreSQL 9.6 - ALTER USER") /
[9.5](/docs/9.5/sql-alteruser.html "PostgreSQL 9.5 - ALTER USER") /
[9.4](/docs/9.4/sql-alteruser.html "PostgreSQL 9.4 - ALTER USER") /
[9.3](/docs/9.3/sql-alteruser.html "PostgreSQL 9.3 - ALTER USER") /
[9.2](/docs/9.2/sql-alteruser.html "PostgreSQL 9.2 - ALTER USER") /
[9.1](/docs/9.1/sql-alteruser.html "PostgreSQL 9.1 - ALTER USER") /
[9.0](/docs/9.0/sql-alteruser.html "PostgreSQL 9.0 - ALTER USER") /
[8.4](/docs/8.4/sql-alteruser.html "PostgreSQL 8.4 - ALTER USER") /
[8.3](/docs/8.3/sql-alteruser.html "PostgreSQL 8.3 - ALTER USER") /
[8.2](/docs/8.2/sql-alteruser.html "PostgreSQL 8.2 - ALTER USER") /
[8.1](/docs/8.1/sql-alteruser.html "PostgreSQL 8.1 - ALTER USER") /
[8.0](/docs/8.0/sql-alteruser.html "PostgreSQL 8.0 - ALTER USER") /
[7.4](/docs/7.4/sql-alteruser.html "PostgreSQL 7.4 - ALTER USER") /
[7.3](/docs/7.3/sql-alteruser.html "PostgreSQL 7.3 - ALTER USER") /
[7.2](/docs/7.2/sql-alteruser.html "PostgreSQL 7.2 - ALTER USER") /
[7.1](/docs/7.1/sql-alteruser.html "PostgreSQL 7.1 - ALTER USER")

__

ALTER USER  
---  
[Prev](sql-altertype.html "ALTER TYPE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterusermapping.html "ALTER USER MAPPING")  
  
* * *

## ALTER USER

ALTER USER — change a database role

## Synopsis

    
    
    ALTER USER _role_specification_ [ WITH ] _option_ [ ... ]
    
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
    
    ALTER USER _name_ RENAME TO _new_name_
    
    ALTER USER { _role_specification_ | ALL } [ IN DATABASE _database_name_ ] SET _configuration_parameter_ { TO | = } { _value_ | DEFAULT }
    ALTER USER { _role_specification_ | ALL } [ IN DATABASE _database_name_ ] SET _configuration_parameter_ FROM CURRENT
    ALTER USER { _role_specification_ | ALL } [ IN DATABASE _database_name_ ] RESET _configuration_parameter_
    ALTER USER { _role_specification_ | ALL } [ IN DATABASE _database_name_ ] RESET ALL
    
    where _role_specification_ can be:
    
        _role_name_
      | CURRENT_ROLE
      | CURRENT_USER
      | SESSION_USER
    

## Description

`ALTER USER` is now an alias for [`ALTER ROLE`](sql-alterrole.html "ALTER
ROLE").

## Compatibility

The `ALTER USER` statement is a PostgreSQL extension. The SQL standard leaves
the definition of users to the implementation.

## See Also

[ALTER ROLE](sql-alterrole.html "ALTER ROLE")

* * *

[Prev](sql-altertype.html "ALTER TYPE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterusermapping.html "ALTER USER MAPPING")  
---|---|---  
ALTER TYPE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER USER MAPPING  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alteruser.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

