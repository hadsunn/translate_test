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

Supported Versions: [Current](/docs/current/sql-createusermapping.html
"PostgreSQL 17 - CREATE USER MAPPING") ([17](/docs/17/sql-
createusermapping.html "PostgreSQL 17 - CREATE USER MAPPING")) /
[16](/docs/16/sql-createusermapping.html "PostgreSQL 16 - CREATE USER
MAPPING") / [15](/docs/15/sql-createusermapping.html "PostgreSQL 15 - CREATE
USER MAPPING") / [14](/docs/14/sql-createusermapping.html "PostgreSQL 14 -
CREATE USER MAPPING") / [13](/docs/13/sql-createusermapping.html "PostgreSQL
13 - CREATE USER MAPPING")

Development Versions: [18](/docs/18/sql-createusermapping.html "PostgreSQL 18
- CREATE USER MAPPING") / [devel](/docs/devel/sql-createusermapping.html
"PostgreSQL devel - CREATE USER MAPPING")

Unsupported versions: [12](/docs/12/sql-createusermapping.html "PostgreSQL 12
- CREATE USER MAPPING") / [11](/docs/11/sql-createusermapping.html "PostgreSQL
11 - CREATE USER MAPPING") / [10](/docs/10/sql-createusermapping.html
"PostgreSQL 10 - CREATE USER MAPPING") / [9.6](/docs/9.6/sql-
createusermapping.html "PostgreSQL 9.6 - CREATE USER MAPPING") /
[9.5](/docs/9.5/sql-createusermapping.html "PostgreSQL 9.5 - CREATE USER
MAPPING") / [9.4](/docs/9.4/sql-createusermapping.html "PostgreSQL 9.4 -
CREATE USER MAPPING") / [9.3](/docs/9.3/sql-createusermapping.html "PostgreSQL
9.3 - CREATE USER MAPPING") / [9.2](/docs/9.2/sql-createusermapping.html
"PostgreSQL 9.2 - CREATE USER MAPPING") / [9.1](/docs/9.1/sql-
createusermapping.html "PostgreSQL 9.1 - CREATE USER MAPPING") /
[9.0](/docs/9.0/sql-createusermapping.html "PostgreSQL 9.0 - CREATE USER
MAPPING") / [8.4](/docs/8.4/sql-createusermapping.html "PostgreSQL 8.4 -
CREATE USER MAPPING")

__

CREATE USER MAPPING  
---  
[Prev](sql-createuser.html "CREATE USER")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createview.html "CREATE VIEW")  
  
* * *

## CREATE USER MAPPING

CREATE USER MAPPING — define a new mapping of a user to a foreign server

## Synopsis

    
    
    CREATE USER MAPPING [ IF NOT EXISTS ] FOR { _user_name_ | USER | CURRENT_ROLE | CURRENT_USER | PUBLIC }
        SERVER _server_name_
        [ OPTIONS ( _option_ '_value_ ' [ , ... ] ) ]
    

## Description

`CREATE USER MAPPING` defines a mapping of a user to a foreign server. A user
mapping typically encapsulates connection information that a foreign-data
wrapper uses together with the information encapsulated by a foreign server to
access an external data resource.

The owner of a foreign server can create user mappings for that server for any
user. Also, a user can create a user mapping for their own user name if
`USAGE` privilege on the server has been granted to the user.

## Parameters

`IF NOT EXISTS`

    

Do not throw an error if a mapping of the given user to the given foreign
server already exists. A notice is issued in this case. Note that there is no
guarantee that the existing user mapping is anything like the one that would
have been created.

_`user_name`_

    

The name of an existing user that is mapped to foreign server. `CURRENT_ROLE`,
`CURRENT_USER`, and `USER` match the name of the current user. When `PUBLIC`
is specified, a so-called public mapping is created that is used when no user-
specific mapping is applicable.

_`server_name`_

    

The name of an existing server for which the user mapping is to be created.

`OPTIONS ( _`option`_ '_`value`_ ' [, ... ] )`

    

This clause specifies the options of the user mapping. The options typically
define the actual user name and password of the mapping. Option names must be
unique. The allowed option names and values are specific to the server's
foreign-data wrapper.

## Examples

Create a user mapping for user `bob`, server `foo`:

    
    
    CREATE USER MAPPING FOR bob SERVER foo OPTIONS (user 'bob', password 'secret');
    

## Compatibility

`CREATE USER MAPPING` conforms to ISO/IEC 9075-9 (SQL/MED).

## See Also

[ALTER USER MAPPING](sql-alterusermapping.html "ALTER USER MAPPING"), [DROP
USER MAPPING](sql-dropusermapping.html "DROP USER MAPPING"), [CREATE FOREIGN
DATA WRAPPER](sql-createforeigndatawrapper.html "CREATE FOREIGN DATA
WRAPPER"), [CREATE SERVER](sql-createserver.html "CREATE SERVER")

* * *

[Prev](sql-createuser.html "CREATE USER")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createview.html "CREATE VIEW")  
---|---|---  
CREATE USER  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE VIEW  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createusermapping.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

