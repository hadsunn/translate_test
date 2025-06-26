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

Supported Versions: [Current](/docs/current/sql-droprole.html "PostgreSQL 17 -
DROP ROLE") ([17](/docs/17/sql-droprole.html "PostgreSQL 17 - DROP ROLE")) /
[16](/docs/16/sql-droprole.html "PostgreSQL 16 - DROP ROLE") /
[15](/docs/15/sql-droprole.html "PostgreSQL 15 - DROP ROLE") /
[14](/docs/14/sql-droprole.html "PostgreSQL 14 - DROP ROLE") /
[13](/docs/13/sql-droprole.html "PostgreSQL 13 - DROP ROLE")

Development Versions: [18](/docs/18/sql-droprole.html "PostgreSQL 18 - DROP
ROLE") / [devel](/docs/devel/sql-droprole.html "PostgreSQL devel - DROP ROLE")

Unsupported versions: [12](/docs/12/sql-droprole.html "PostgreSQL 12 - DROP
ROLE") / [11](/docs/11/sql-droprole.html "PostgreSQL 11 - DROP ROLE") /
[10](/docs/10/sql-droprole.html "PostgreSQL 10 - DROP ROLE") /
[9.6](/docs/9.6/sql-droprole.html "PostgreSQL 9.6 - DROP ROLE") /
[9.5](/docs/9.5/sql-droprole.html "PostgreSQL 9.5 - DROP ROLE") /
[9.4](/docs/9.4/sql-droprole.html "PostgreSQL 9.4 - DROP ROLE") /
[9.3](/docs/9.3/sql-droprole.html "PostgreSQL 9.3 - DROP ROLE") /
[9.2](/docs/9.2/sql-droprole.html "PostgreSQL 9.2 - DROP ROLE") /
[9.1](/docs/9.1/sql-droprole.html "PostgreSQL 9.1 - DROP ROLE") /
[9.0](/docs/9.0/sql-droprole.html "PostgreSQL 9.0 - DROP ROLE") /
[8.4](/docs/8.4/sql-droprole.html "PostgreSQL 8.4 - DROP ROLE") /
[8.3](/docs/8.3/sql-droprole.html "PostgreSQL 8.3 - DROP ROLE") /
[8.2](/docs/8.2/sql-droprole.html "PostgreSQL 8.2 - DROP ROLE") /
[8.1](/docs/8.1/sql-droprole.html "PostgreSQL 8.1 - DROP ROLE")

__

DROP ROLE  
---  
[Prev](sql-droppublication.html "DROP PUBLICATION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-droproutine.html "DROP ROUTINE")  
  
* * *

## DROP ROLE

DROP ROLE — remove a database role

## Synopsis

    
    
    DROP ROLE [ IF EXISTS ] _name_ [, ...]
    

## Description

`DROP ROLE` removes the specified role(s). To drop a superuser role, you must
be a superuser yourself; to drop non-superuser roles, you must have
`CREATEROLE` privilege and have been granted `ADMIN OPTION` on the role.

A role cannot be removed if it is still referenced in any database of the
cluster; an error will be raised if so. Before dropping the role, you must
drop all the objects it owns (or reassign their ownership) and revoke any
privileges the role has been granted on other objects. The [`REASSIGN
OWNED`](sql-reassign-owned.html "REASSIGN OWNED") and [`DROP OWNED`](sql-drop-
owned.html "DROP OWNED") commands can be useful for this purpose; see [Section
22.4](role-removal.html "22.4. Dropping Roles") for more discussion.

However, it is not necessary to remove role memberships involving the role;
`DROP ROLE` automatically revokes any memberships of the target role in other
roles, and of other roles in the target role. The other roles are not dropped
nor otherwise affected.

## Parameters

`IF EXISTS`

    

Do not throw an error if the role does not exist. A notice is issued in this
case.

_`name`_

    

The name of the role to remove.

## Notes

PostgreSQL includes a program [dropuser](app-dropuser.html "dropuser") that
has the same functionality as this command (in fact, it calls this command)
but can be run from the command shell.

## Examples

To drop a role:

    
    
    DROP ROLE jonathan;
    

## Compatibility

The SQL standard defines `DROP ROLE`, but it allows only one role to be
dropped at a time, and it specifies different privilege requirements than
PostgreSQL uses.

## See Also

[CREATE ROLE](sql-createrole.html "CREATE ROLE"), [ALTER ROLE](sql-
alterrole.html "ALTER ROLE"), [SET ROLE](sql-set-role.html "SET ROLE")

* * *

[Prev](sql-droppublication.html "DROP PUBLICATION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-droproutine.html "DROP ROUTINE")  
---|---|---  
DROP PUBLICATION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP ROUTINE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-droprole.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

