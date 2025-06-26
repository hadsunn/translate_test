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

Supported Versions: [Current](/docs/current/ecpg-sql-connect.html "PostgreSQL
17 - CONNECT") ([17](/docs/17/ecpg-sql-connect.html "PostgreSQL 17 -
CONNECT")) / [16](/docs/16/ecpg-sql-connect.html "PostgreSQL 16 - CONNECT") /
[15](/docs/15/ecpg-sql-connect.html "PostgreSQL 15 - CONNECT") /
[14](/docs/14/ecpg-sql-connect.html "PostgreSQL 14 - CONNECT") /
[13](/docs/13/ecpg-sql-connect.html "PostgreSQL 13 - CONNECT")

Development Versions: [18](/docs/18/ecpg-sql-connect.html "PostgreSQL 18 -
CONNECT") / [devel](/docs/devel/ecpg-sql-connect.html "PostgreSQL devel -
CONNECT")

Unsupported versions: [12](/docs/12/ecpg-sql-connect.html "PostgreSQL 12 -
CONNECT") / [11](/docs/11/ecpg-sql-connect.html "PostgreSQL 11 - CONNECT") /
[10](/docs/10/ecpg-sql-connect.html "PostgreSQL 10 - CONNECT") /
[9.6](/docs/9.6/ecpg-sql-connect.html "PostgreSQL 9.6 - CONNECT") /
[9.5](/docs/9.5/ecpg-sql-connect.html "PostgreSQL 9.5 - CONNECT") /
[9.4](/docs/9.4/ecpg-sql-connect.html "PostgreSQL 9.4 - CONNECT") /
[9.3](/docs/9.3/ecpg-sql-connect.html "PostgreSQL 9.3 - CONNECT") /
[9.2](/docs/9.2/ecpg-sql-connect.html "PostgreSQL 9.2 - CONNECT") /
[9.1](/docs/9.1/ecpg-sql-connect.html "PostgreSQL 9.1 - CONNECT")

__

CONNECT  
---  
[Prev](ecpg-sql-allocate-descriptor.html "ALLOCATE DESCRIPTOR")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") | 36.14. Embedded SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-sql-deallocate-descriptor.html "DEALLOCATE DESCRIPTOR")  
  
* * *

## CONNECT

CONNECT — establish a database connection

## Synopsis

    
    
    CONNECT TO _connection_target_ [ AS _connection_name_ ] [ USER _connection_user_ ]
    CONNECT TO DEFAULT
    CONNECT _connection_user_
    DATABASE _connection_target_
    

## Description

The `CONNECT` command establishes a connection between the client and the
PostgreSQL server.

## Parameters

_`connection_target`_ #

    

_`connection_target`_ specifies the target server of the connection on one of
several forms.

[ _`database_name`_ ] [ `@`_`host`_ ] [ `:`_`port`_ ] #

    

Connect over TCP/IP

`unix:postgresql://`_`host`_ [ `:`_`port`_ ] `/` [ _`database_name`_ ] [
`?`_`connection_option`_ ] #

    

Connect over Unix-domain sockets

`tcp:postgresql://`_`host`_ [ `:`_`port`_ ] `/` [ _`database_name`_ ] [
`?`_`connection_option`_ ] #

    

Connect over TCP/IP

SQL string constant #

    

containing a value in one of the above forms

host variable #

    

host variable of type `char[]` or `VARCHAR[]` containing a value in one of the
above forms

_`connection_name`_ #

    

An optional identifier for the connection, so that it can be referred to in
other commands. This can be an SQL identifier or a host variable.

_`connection_user`_ #

    

The user name for the database connection.

This parameter can also specify user name and password, using one the forms
`_`user_name`_ /_`password`_`, `_`user_name`_ IDENTIFIED BY _`password`_`, or
`_`user_name`_ USING _`password`_`.

User name and password can be SQL identifiers, string constants, or host
variables.

`DEFAULT` #

    

Use all default connection parameters, as defined by libpq.

## Examples

Here a several variants for specifying connection parameters:

    
    
    EXEC SQL CONNECT TO "connectdb" AS main;
    EXEC SQL CONNECT TO "connectdb" AS second;
    EXEC SQL CONNECT TO "unix:postgresql://200.46.204.71/connectdb" AS main USER connectuser;
    EXEC SQL CONNECT TO "unix:postgresql://localhost/connectdb" AS main USER connectuser;
    EXEC SQL CONNECT TO 'connectdb' AS main;
    EXEC SQL CONNECT TO 'unix:postgresql://localhost/connectdb' AS main USER :user;
    EXEC SQL CONNECT TO :db AS :id;
    EXEC SQL CONNECT TO :db USER connectuser USING :pw;
    EXEC SQL CONNECT TO @localhost AS main USER connectdb;
    EXEC SQL CONNECT TO REGRESSDB1 as main;
    EXEC SQL CONNECT TO AS main USER connectdb;
    EXEC SQL CONNECT TO connectdb AS :id;
    EXEC SQL CONNECT TO connectdb AS main USER connectuser/connectdb;
    EXEC SQL CONNECT TO connectdb AS main;
    EXEC SQL CONNECT TO connectdb@localhost AS main;
    EXEC SQL CONNECT TO tcp:postgresql://localhost/ USER connectdb;
    EXEC SQL CONNECT TO tcp:postgresql://localhost/connectdb USER connectuser IDENTIFIED BY connectpw;
    EXEC SQL CONNECT TO tcp:postgresql://localhost:20/connectdb USER connectuser IDENTIFIED BY connectpw;
    EXEC SQL CONNECT TO unix:postgresql://localhost/ AS main USER connectdb;
    EXEC SQL CONNECT TO unix:postgresql://localhost/connectdb AS main USER connectuser;
    EXEC SQL CONNECT TO unix:postgresql://localhost/connectdb USER connectuser IDENTIFIED BY "connectpw";
    EXEC SQL CONNECT TO unix:postgresql://localhost/connectdb USER connectuser USING "connectpw";
    EXEC SQL CONNECT TO unix:postgresql://localhost/connectdb?connect_timeout=14 USER connectuser;
    

Here is an example program that illustrates the use of host variables to
specify connection parameters:

    
    
    int
    main(void)
    {
    EXEC SQL BEGIN DECLARE SECTION;
        char *dbname     = "testdb";    /* database name */
        char *user       = "testuser";  /* connection user name */
        char *connection = "tcp:postgresql://localhost:5432/testdb";
                                        /* connection string */
        char ver[256];                  /* buffer to store the version string */
    EXEC SQL END DECLARE SECTION;
    
        ECPGdebug(1, stderr);
    
        EXEC SQL CONNECT TO :dbname USER :user;
        EXEC SQL SELECT pg_catalog.set_config('search_path', '', false); EXEC SQL COMMIT;
        EXEC SQL SELECT version() INTO :ver;
        EXEC SQL DISCONNECT;
    
        printf("version: %s\n", ver);
    
        EXEC SQL CONNECT TO :connection USER :user;
        EXEC SQL SELECT pg_catalog.set_config('search_path', '', false); EXEC SQL COMMIT;
        EXEC SQL SELECT version() INTO :ver;
        EXEC SQL DISCONNECT;
    
        printf("version: %s\n", ver);
    
        return 0;
    }
    

## Compatibility

`CONNECT` is specified in the SQL standard, but the format of the connection
parameters is implementation-specific.

## See Also

[DISCONNECT](ecpg-sql-disconnect.html "DISCONNECT"), [SET CONNECTION](ecpg-
sql-set-connection.html "SET CONNECTION")

* * *

[Prev](ecpg-sql-allocate-descriptor.html "ALLOCATE DESCRIPTOR")  | [Up](ecpg-sql-commands.html "36.14. Embedded SQL Commands") |  [Next](ecpg-sql-deallocate-descriptor.html "DEALLOCATE DESCRIPTOR")  
---|---|---  
ALLOCATE DESCRIPTOR  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DEALLOCATE DESCRIPTOR  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-sql-connect.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

