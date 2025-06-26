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

Supported Versions: [Current](/docs/current/sql-alterusermapping.html
"PostgreSQL 17 - ALTER USER MAPPING") ([17](/docs/17/sql-alterusermapping.html
"PostgreSQL 17 - ALTER USER MAPPING")) / [16](/docs/16/sql-
alterusermapping.html "PostgreSQL 16 - ALTER USER MAPPING") /
[15](/docs/15/sql-alterusermapping.html "PostgreSQL 15 - ALTER USER MAPPING")
/ [14](/docs/14/sql-alterusermapping.html "PostgreSQL 14 - ALTER USER
MAPPING") / [13](/docs/13/sql-alterusermapping.html "PostgreSQL 13 - ALTER
USER MAPPING")

Development Versions: [18](/docs/18/sql-alterusermapping.html "PostgreSQL 18 -
ALTER USER MAPPING") / [devel](/docs/devel/sql-alterusermapping.html
"PostgreSQL devel - ALTER USER MAPPING")

Unsupported versions: [12](/docs/12/sql-alterusermapping.html "PostgreSQL 12 -
ALTER USER MAPPING") / [11](/docs/11/sql-alterusermapping.html "PostgreSQL 11
- ALTER USER MAPPING") / [10](/docs/10/sql-alterusermapping.html "PostgreSQL
10 - ALTER USER MAPPING") / [9.6](/docs/9.6/sql-alterusermapping.html
"PostgreSQL 9.6 - ALTER USER MAPPING") / [9.5](/docs/9.5/sql-
alterusermapping.html "PostgreSQL 9.5 - ALTER USER MAPPING") /
[9.4](/docs/9.4/sql-alterusermapping.html "PostgreSQL 9.4 - ALTER USER
MAPPING") / [9.3](/docs/9.3/sql-alterusermapping.html "PostgreSQL 9.3 - ALTER
USER MAPPING") / [9.2](/docs/9.2/sql-alterusermapping.html "PostgreSQL 9.2 -
ALTER USER MAPPING") / [9.1](/docs/9.1/sql-alterusermapping.html "PostgreSQL
9.1 - ALTER USER MAPPING") / [9.0](/docs/9.0/sql-alterusermapping.html
"PostgreSQL 9.0 - ALTER USER MAPPING") / [8.4](/docs/8.4/sql-
alterusermapping.html "PostgreSQL 8.4 - ALTER USER MAPPING")

__

ALTER USER MAPPING  
---  
[Prev](sql-alteruser.html "ALTER USER")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterview.html "ALTER VIEW")  
  
* * *

## ALTER USER MAPPING

ALTER USER MAPPING — change the definition of a user mapping

## Synopsis

    
    
    ALTER USER MAPPING FOR { _user_name_ | USER | CURRENT_ROLE | CURRENT_USER | SESSION_USER | PUBLIC }
        SERVER _server_name_
        OPTIONS ( [ ADD | SET | DROP ] _option_ ['_value_ '] [, ... ] )
    

## Description

`ALTER USER MAPPING` changes the definition of a user mapping.

The owner of a foreign server can alter user mappings for that server for any
user. Also, a user can alter a user mapping for their own user name if `USAGE`
privilege on the server has been granted to the user.

## Parameters

_`user_name`_

    

User name of the mapping. `CURRENT_ROLE`, `CURRENT_USER`, and `USER` match the
name of the current user. `PUBLIC` is used to match all present and future
user names in the system.

_`server_name`_

    

Server name of the user mapping.

`OPTIONS ( [ ADD | SET | DROP ] _`option`_ ['_`value`_ '] [, ... ] )`
    

Change options for the user mapping. The new options override any previously
specified options. `ADD`, `SET`, and `DROP` specify the action to be
performed. `ADD` is assumed if no operation is explicitly specified. Option
names must be unique; options are also validated by the server's foreign-data
wrapper.

## Examples

Change the password for user mapping `bob`, server `foo`:

    
    
    ALTER USER MAPPING FOR bob SERVER foo OPTIONS (SET password 'public');
    

## Compatibility

`ALTER USER MAPPING` conforms to ISO/IEC 9075-9 (SQL/MED). There is a subtle
syntax issue: The standard omits the `FOR` key word. Since both `CREATE USER
MAPPING` and `DROP USER MAPPING` use `FOR` in analogous positions, and IBM DB2
(being the other major SQL/MED implementation) also requires it for `ALTER
USER MAPPING`, PostgreSQL diverges from the standard here in the interest of
consistency and interoperability.

## See Also

[CREATE USER MAPPING](sql-createusermapping.html "CREATE USER MAPPING"), [DROP
USER MAPPING](sql-dropusermapping.html "DROP USER MAPPING")

* * *

[Prev](sql-alteruser.html "ALTER USER")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterview.html "ALTER VIEW")  
---|---|---  
ALTER USER  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER VIEW  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterusermapping.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

