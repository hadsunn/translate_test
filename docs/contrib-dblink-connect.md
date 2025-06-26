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

Supported Versions: [Current](/docs/current/contrib-dblink-connect.html
"PostgreSQL 17 - dblink_connect") ([17](/docs/17/contrib-dblink-connect.html
"PostgreSQL 17 - dblink_connect")) / [16](/docs/16/contrib-dblink-connect.html
"PostgreSQL 16 - dblink_connect") / [15](/docs/15/contrib-dblink-connect.html
"PostgreSQL 15 - dblink_connect") / [14](/docs/14/contrib-dblink-connect.html
"PostgreSQL 14 - dblink_connect") / [13](/docs/13/contrib-dblink-connect.html
"PostgreSQL 13 - dblink_connect")

Development Versions: [18](/docs/18/contrib-dblink-connect.html "PostgreSQL 18
- dblink_connect") / [devel](/docs/devel/contrib-dblink-connect.html
"PostgreSQL devel - dblink_connect")

Unsupported versions: [12](/docs/12/contrib-dblink-connect.html "PostgreSQL 12
- dblink_connect") / [11](/docs/11/contrib-dblink-connect.html "PostgreSQL 11
- dblink_connect") / [10](/docs/10/contrib-dblink-connect.html "PostgreSQL 10
- dblink_connect") / [9.6](/docs/9.6/contrib-dblink-connect.html "PostgreSQL
9.6 - dblink_connect") / [9.5](/docs/9.5/contrib-dblink-connect.html
"PostgreSQL 9.5 - dblink_connect") / [9.4](/docs/9.4/contrib-dblink-
connect.html "PostgreSQL 9.4 - dblink_connect") / [9.3](/docs/9.3/contrib-
dblink-connect.html "PostgreSQL 9.3 - dblink_connect") /
[9.2](/docs/9.2/contrib-dblink-connect.html "PostgreSQL 9.2 - dblink_connect")
/ [9.1](/docs/9.1/contrib-dblink-connect.html "PostgreSQL 9.1 -
dblink_connect") / [9.0](/docs/9.0/contrib-dblink-connect.html "PostgreSQL 9.0
- dblink_connect") / [8.4](/docs/8.4/contrib-dblink-connect.html "PostgreSQL
8.4 - dblink_connect") / [8.3](/docs/8.3/contrib-dblink-connect.html
"PostgreSQL 8.3 - dblink_connect")

__

dblink_connect  
---  
[Prev](dblink.html "F.12. dblink — connect to other PostgreSQL databases")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") | F.12. dblink — connect to other PostgreSQL databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-connect-u.html "dblink_connect_u")  
  
* * *

## dblink_connect

dblink_connect — opens a persistent connection to a remote database

## Synopsis

    
    
    dblink_connect(text connstr) returns text
    dblink_connect(text connname, text connstr) returns text
    

## Description

`dblink_connect()` establishes a connection to a remote PostgreSQL database.
The server and database to be contacted are identified through a standard
libpq connection string. Optionally, a name can be assigned to the connection.
Multiple named connections can be open at once, but only one unnamed
connection is permitted at a time. The connection will persist until closed or
until the database session is ended.

The connection string may also be the name of an existing foreign server. It
is recommended to use the foreign-data wrapper `dblink_fdw` when defining the
foreign server. See the example below, as well as [CREATE SERVER](sql-
createserver.html "CREATE SERVER") and [CREATE USER MAPPING](sql-
createusermapping.html "CREATE USER MAPPING").

## Arguments

_`connname`_

    

The name to use for this connection; if omitted, an unnamed connection is
opened, replacing any existing unnamed connection.

_`connstr`_

    

libpq-style connection info string, for example `hostaddr=127.0.0.1 port=5432
dbname=mydb user=postgres password=mypasswd options=-csearch_path=`. For
details see [Section 34.1.1](libpq-connect.html#LIBPQ-CONNSTRING
"34.1.1. Connection Strings"). Alternatively, the name of a foreign server.

## Return Value

Returns status, which is always `OK` (since any error causes the function to
throw an error instead of returning).

## Notes

If untrusted users have access to a database that has not adopted a [secure
schema usage pattern](ddl-schemas.html#DDL-SCHEMAS-PATTERNS "5.9.6. Usage
Patterns"), begin each session by removing publicly-writable schemas from
`search_path`. One could, for example, add `options=-csearch_path=` to
_`connstr`_. This consideration is not specific to `dblink`; it applies to
every interface for executing arbitrary SQL commands.

Only superusers may use `dblink_connect` to create non-password-authenticated
and non-GSSAPI-authenticated connections. If non-superusers need this
capability, use `dblink_connect_u` instead.

It is unwise to choose connection names that contain equal signs, as this
opens a risk of confusion with connection info strings in other `dblink`
functions.

## Examples

    
    
    SELECT dblink_connect('dbname=postgres options=-csearch_path=');
     dblink_connect
    ----------------
     OK
    (1 row)
    
    SELECT dblink_connect('myconn', 'dbname=postgres options=-csearch_path=');
     dblink_connect
    ----------------
     OK
    (1 row)
    
    -- FOREIGN DATA WRAPPER functionality
    -- Note: local connection must require password authentication for this to work properly
    --       Otherwise, you will receive the following error from dblink_connect():
    --       ERROR:  password is required
    --       DETAIL:  Non-superuser cannot connect if the server does not request a password.
    --       HINT:  Target server's authentication method must be changed.
    
    CREATE SERVER fdtest FOREIGN DATA WRAPPER dblink_fdw OPTIONS (hostaddr '127.0.0.1', dbname 'contrib_regression');
    
    CREATE USER regress_dblink_user WITH PASSWORD 'secret';
    CREATE USER MAPPING FOR regress_dblink_user SERVER fdtest OPTIONS (user 'regress_dblink_user', password 'secret');
    GRANT USAGE ON FOREIGN SERVER fdtest TO regress_dblink_user;
    GRANT SELECT ON TABLE foo TO regress_dblink_user;
    
    \set ORIGINAL_USER :USER
    \c - regress_dblink_user
    SELECT dblink_connect('myconn', 'fdtest');
     dblink_connect
    ----------------
     OK
    (1 row)
    
    SELECT * FROM dblink('myconn', 'SELECT * FROM foo') AS t(a int, b text, c text[]);
     a  | b |       c
    ----+---+---------------
      0 | a | {a0,b0,c0}
      1 | b | {a1,b1,c1}
      2 | c | {a2,b2,c2}
      3 | d | {a3,b3,c3}
      4 | e | {a4,b4,c4}
      5 | f | {a5,b5,c5}
      6 | g | {a6,b6,c6}
      7 | h | {a7,b7,c7}
      8 | i | {a8,b8,c8}
      9 | j | {a9,b9,c9}
     10 | k | {a10,b10,c10}
    (11 rows)
    
    \c - :ORIGINAL_USER
    REVOKE USAGE ON FOREIGN SERVER fdtest FROM regress_dblink_user;
    REVOKE SELECT ON TABLE foo FROM regress_dblink_user;
    DROP USER MAPPING FOR regress_dblink_user SERVER fdtest;
    DROP USER regress_dblink_user;
    DROP SERVER fdtest;
    

* * *

[Prev](dblink.html "F.12. dblink — connect to other PostgreSQL databases")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") |  [Next](contrib-dblink-connect-u.html "dblink_connect_u")  
---|---|---  
F.12. dblink — connect to other PostgreSQL databases  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink_connect_u  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-dblink-connect.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

