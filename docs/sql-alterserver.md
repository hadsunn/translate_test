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

Supported Versions: [Current](/docs/current/sql-alterserver.html "PostgreSQL
17 - ALTER SERVER") ([17](/docs/17/sql-alterserver.html "PostgreSQL 17 - ALTER
SERVER")) / [16](/docs/16/sql-alterserver.html "PostgreSQL 16 - ALTER SERVER")
/ [15](/docs/15/sql-alterserver.html "PostgreSQL 15 - ALTER SERVER") /
[14](/docs/14/sql-alterserver.html "PostgreSQL 14 - ALTER SERVER") /
[13](/docs/13/sql-alterserver.html "PostgreSQL 13 - ALTER SERVER")

Development Versions: [18](/docs/18/sql-alterserver.html "PostgreSQL 18 -
ALTER SERVER") / [devel](/docs/devel/sql-alterserver.html "PostgreSQL devel -
ALTER SERVER")

Unsupported versions: [12](/docs/12/sql-alterserver.html "PostgreSQL 12 -
ALTER SERVER") / [11](/docs/11/sql-alterserver.html "PostgreSQL 11 - ALTER
SERVER") / [10](/docs/10/sql-alterserver.html "PostgreSQL 10 - ALTER SERVER")
/ [9.6](/docs/9.6/sql-alterserver.html "PostgreSQL 9.6 - ALTER SERVER") /
[9.5](/docs/9.5/sql-alterserver.html "PostgreSQL 9.5 - ALTER SERVER") /
[9.4](/docs/9.4/sql-alterserver.html "PostgreSQL 9.4 - ALTER SERVER") /
[9.3](/docs/9.3/sql-alterserver.html "PostgreSQL 9.3 - ALTER SERVER") /
[9.2](/docs/9.2/sql-alterserver.html "PostgreSQL 9.2 - ALTER SERVER") /
[9.1](/docs/9.1/sql-alterserver.html "PostgreSQL 9.1 - ALTER SERVER") /
[9.0](/docs/9.0/sql-alterserver.html "PostgreSQL 9.0 - ALTER SERVER") /
[8.4](/docs/8.4/sql-alterserver.html "PostgreSQL 8.4 - ALTER SERVER")

__

ALTER SERVER  
---  
[Prev](sql-altersequence.html "ALTER SEQUENCE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterstatistics.html "ALTER STATISTICS")  
  
* * *

## ALTER SERVER

ALTER SERVER — change the definition of a foreign server

## Synopsis

    
    
    ALTER SERVER _name_ [ VERSION '_new_version_ ' ]
        [ OPTIONS ( [ ADD | SET | DROP ] _option_ ['_value_ '] [, ... ] ) ]
    ALTER SERVER _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER SERVER _name_ RENAME TO _new_name_
    

## Description

`ALTER SERVER` changes the definition of a foreign server. The first form
changes the server version string or the generic options of the server (at
least one clause is required). The second form changes the owner of the
server.

To alter the server you must be the owner of the server. Additionally to alter
the owner, you must be able to `SET ROLE` to the new owning role, and you must
have `USAGE` privilege on the server's foreign-data wrapper. (Note that
superusers satisfy all these criteria automatically.)

## Parameters

_`name`_

    

The name of an existing server.

_`new_version`_

    

New server version.

`OPTIONS ( [ ADD | SET | DROP ] _`option`_ ['_`value`_ '] [, ... ] )`
    

Change options for the server. `ADD`, `SET`, and `DROP` specify the action to
be performed. `ADD` is assumed if no operation is explicitly specified. Option
names must be unique; names and values are also validated using the server's
foreign-data wrapper library.

_`new_owner`_

    

The user name of the new owner of the foreign server.

_`new_name`_

    

The new name for the foreign server.

## Examples

Alter server `foo`, add connection options:

    
    
    ALTER SERVER foo OPTIONS (host 'foo', dbname 'foodb');
    

Alter server `foo`, change version, change `host` option:

    
    
    ALTER SERVER foo VERSION '8.4' OPTIONS (SET host 'baz');
    

## Compatibility

`ALTER SERVER` conforms to ISO/IEC 9075-9 (SQL/MED). The `OWNER TO` and
`RENAME` forms are PostgreSQL extensions.

## See Also

[CREATE SERVER](sql-createserver.html "CREATE SERVER"), [DROP SERVER](sql-
dropserver.html "DROP SERVER")

* * *

[Prev](sql-altersequence.html "ALTER SEQUENCE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterstatistics.html "ALTER STATISTICS")  
---|---|---  
ALTER SEQUENCE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER STATISTICS  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterserver.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

