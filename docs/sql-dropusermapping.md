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

Supported Versions: [Current](/docs/current/sql-dropusermapping.html
"PostgreSQL 17 - DROP USER MAPPING") ([17](/docs/17/sql-dropusermapping.html
"PostgreSQL 17 - DROP USER MAPPING")) / [16](/docs/16/sql-dropusermapping.html
"PostgreSQL 16 - DROP USER MAPPING") / [15](/docs/15/sql-dropusermapping.html
"PostgreSQL 15 - DROP USER MAPPING") / [14](/docs/14/sql-dropusermapping.html
"PostgreSQL 14 - DROP USER MAPPING") / [13](/docs/13/sql-dropusermapping.html
"PostgreSQL 13 - DROP USER MAPPING")

Development Versions: [18](/docs/18/sql-dropusermapping.html "PostgreSQL 18 -
DROP USER MAPPING") / [devel](/docs/devel/sql-dropusermapping.html "PostgreSQL
devel - DROP USER MAPPING")

Unsupported versions: [12](/docs/12/sql-dropusermapping.html "PostgreSQL 12 -
DROP USER MAPPING") / [11](/docs/11/sql-dropusermapping.html "PostgreSQL 11 -
DROP USER MAPPING") / [10](/docs/10/sql-dropusermapping.html "PostgreSQL 10 -
DROP USER MAPPING") / [9.6](/docs/9.6/sql-dropusermapping.html "PostgreSQL 9.6
- DROP USER MAPPING") / [9.5](/docs/9.5/sql-dropusermapping.html "PostgreSQL
9.5 - DROP USER MAPPING") / [9.4](/docs/9.4/sql-dropusermapping.html
"PostgreSQL 9.4 - DROP USER MAPPING") / [9.3](/docs/9.3/sql-
dropusermapping.html "PostgreSQL 9.3 - DROP USER MAPPING") /
[9.2](/docs/9.2/sql-dropusermapping.html "PostgreSQL 9.2 - DROP USER MAPPING")
/ [9.1](/docs/9.1/sql-dropusermapping.html "PostgreSQL 9.1 - DROP USER
MAPPING") / [9.0](/docs/9.0/sql-dropusermapping.html "PostgreSQL 9.0 - DROP
USER MAPPING") / [8.4](/docs/8.4/sql-dropusermapping.html "PostgreSQL 8.4 -
DROP USER MAPPING")

__

DROP USER MAPPING  
---  
[Prev](sql-dropuser.html "DROP USER")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropview.html "DROP VIEW")  
  
* * *

## DROP USER MAPPING

DROP USER MAPPING — remove a user mapping for a foreign server

## Synopsis

    
    
    DROP USER MAPPING [ IF EXISTS ] FOR { _user_name_ | USER | CURRENT_ROLE | CURRENT_USER | PUBLIC } SERVER _server_name_
    

## Description

`DROP USER MAPPING` removes an existing user mapping from foreign server.

The owner of a foreign server can drop user mappings for that server for any
user. Also, a user can drop a user mapping for their own user name if `USAGE`
privilege on the server has been granted to the user.

## Parameters

`IF EXISTS`

    

Do not throw an error if the user mapping does not exist. A notice is issued
in this case.

_`user_name`_

    

User name of the mapping. `CURRENT_ROLE`, `CURRENT_USER`, and `USER` match the
name of the current user. `PUBLIC` is used to match all present and future
user names in the system.

_`server_name`_

    

Server name of the user mapping.

## Examples

Drop a user mapping `bob`, server `foo` if it exists:

    
    
    DROP USER MAPPING IF EXISTS FOR bob SERVER foo;
    

## Compatibility

`DROP USER MAPPING` conforms to ISO/IEC 9075-9 (SQL/MED). The `IF EXISTS`
clause is a PostgreSQL extension.

## See Also

[CREATE USER MAPPING](sql-createusermapping.html "CREATE USER MAPPING"),
[ALTER USER MAPPING](sql-alterusermapping.html "ALTER USER MAPPING")

* * *

[Prev](sql-dropuser.html "DROP USER")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropview.html "DROP VIEW")  
---|---|---  
DROP USER  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP VIEW  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropusermapping.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

