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

Supported Versions: [Current](/docs/current/sql-createserver.html "PostgreSQL
17 - CREATE SERVER") ([17](/docs/17/sql-createserver.html "PostgreSQL 17 -
CREATE SERVER")) / [16](/docs/16/sql-createserver.html "PostgreSQL 16 - CREATE
SERVER") / [15](/docs/15/sql-createserver.html "PostgreSQL 15 - CREATE
SERVER") / [14](/docs/14/sql-createserver.html "PostgreSQL 14 - CREATE
SERVER") / [13](/docs/13/sql-createserver.html "PostgreSQL 13 - CREATE
SERVER")

Development Versions: [18](/docs/18/sql-createserver.html "PostgreSQL 18 -
CREATE SERVER") / [devel](/docs/devel/sql-createserver.html "PostgreSQL devel
- CREATE SERVER")

Unsupported versions: [12](/docs/12/sql-createserver.html "PostgreSQL 12 -
CREATE SERVER") / [11](/docs/11/sql-createserver.html "PostgreSQL 11 - CREATE
SERVER") / [10](/docs/10/sql-createserver.html "PostgreSQL 10 - CREATE
SERVER") / [9.6](/docs/9.6/sql-createserver.html "PostgreSQL 9.6 - CREATE
SERVER") / [9.5](/docs/9.5/sql-createserver.html "PostgreSQL 9.5 - CREATE
SERVER") / [9.4](/docs/9.4/sql-createserver.html "PostgreSQL 9.4 - CREATE
SERVER") / [9.3](/docs/9.3/sql-createserver.html "PostgreSQL 9.3 - CREATE
SERVER") / [9.2](/docs/9.2/sql-createserver.html "PostgreSQL 9.2 - CREATE
SERVER") / [9.1](/docs/9.1/sql-createserver.html "PostgreSQL 9.1 - CREATE
SERVER") / [9.0](/docs/9.0/sql-createserver.html "PostgreSQL 9.0 - CREATE
SERVER") / [8.4](/docs/8.4/sql-createserver.html "PostgreSQL 8.4 - CREATE
SERVER")

__

CREATE SERVER  
---  
[Prev](sql-createsequence.html "CREATE SEQUENCE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createstatistics.html "CREATE STATISTICS")  
  
* * *

## CREATE SERVER

CREATE SERVER — define a new foreign server

## Synopsis

    
    
    CREATE SERVER [ IF NOT EXISTS ] _server_name_ [ TYPE '_server_type_ ' ] [ VERSION '_server_version_ ' ]
        FOREIGN DATA WRAPPER _fdw_name_
        [ OPTIONS ( _option_ '_value_ ' [, ... ] ) ]
    

## Description

`CREATE SERVER` defines a new foreign server. The user who defines the server
becomes its owner.

A foreign server typically encapsulates connection information that a foreign-
data wrapper uses to access an external data resource. Additional user-
specific connection information may be specified by means of user mappings.

The server name must be unique within the database.

Creating a server requires `USAGE` privilege on the foreign-data wrapper being
used.

## Parameters

`IF NOT EXISTS`

    

Do not throw an error if a server with the same name already exists. A notice
is issued in this case. Note that there is no guarantee that the existing
server is anything like the one that would have been created.

_`server_name`_

    

The name of the foreign server to be created.

_`server_type`_

    

Optional server type, potentially useful to foreign-data wrappers.

_`server_version`_

    

Optional server version, potentially useful to foreign-data wrappers.

_`fdw_name`_

    

The name of the foreign-data wrapper that manages the server.

`OPTIONS ( _`option`_ '_`value`_ ' [, ... ] )`

    

This clause specifies the options for the server. The options typically define
the connection details of the server, but the actual names and values are
dependent on the server's foreign-data wrapper.

## Notes

When using the [dblink](dblink.html "F.12. dblink — connect to other
PostgreSQL databases") module, a foreign server's name can be used as an
argument of the [dblink_connect](contrib-dblink-connect.html "dblink_connect")
function to indicate the connection parameters. It is necessary to have the
`USAGE` privilege on the foreign server to be able to use it in this way.

If the foreign server supports sort pushdown, it is necessary for it to have
the same sort ordering as the local server.

## Examples

Create a server `myserver` that uses the foreign-data wrapper `postgres_fdw`:

    
    
    CREATE SERVER myserver FOREIGN DATA WRAPPER postgres_fdw OPTIONS (host 'foo', dbname 'foodb', port '5432');
    

See [postgres_fdw](postgres-fdw.html "F.38. postgres_fdw — access data stored
in external PostgreSQL servers") for more details.

## Compatibility

`CREATE SERVER` conforms to ISO/IEC 9075-9 (SQL/MED).

## See Also

[ALTER SERVER](sql-alterserver.html "ALTER SERVER"), [DROP SERVER](sql-
dropserver.html "DROP SERVER"), [CREATE FOREIGN DATA WRAPPER](sql-
createforeigndatawrapper.html "CREATE FOREIGN DATA WRAPPER"), [CREATE FOREIGN
TABLE](sql-createforeigntable.html "CREATE FOREIGN TABLE"), [CREATE USER
MAPPING](sql-createusermapping.html "CREATE USER MAPPING")

* * *

[Prev](sql-createsequence.html "CREATE SEQUENCE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createstatistics.html "CREATE STATISTICS")  
---|---|---  
CREATE SEQUENCE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE STATISTICS  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createserver.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

