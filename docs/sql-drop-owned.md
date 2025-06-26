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

Supported Versions: [Current](/docs/current/sql-drop-owned.html "PostgreSQL 17
- DROP OWNED") ([17](/docs/17/sql-drop-owned.html "PostgreSQL 17 - DROP
OWNED")) / [16](/docs/16/sql-drop-owned.html "PostgreSQL 16 - DROP OWNED") /
[15](/docs/15/sql-drop-owned.html "PostgreSQL 15 - DROP OWNED") /
[14](/docs/14/sql-drop-owned.html "PostgreSQL 14 - DROP OWNED") /
[13](/docs/13/sql-drop-owned.html "PostgreSQL 13 - DROP OWNED")

Development Versions: [18](/docs/18/sql-drop-owned.html "PostgreSQL 18 - DROP
OWNED") / [devel](/docs/devel/sql-drop-owned.html "PostgreSQL devel - DROP
OWNED")

Unsupported versions: [12](/docs/12/sql-drop-owned.html "PostgreSQL 12 - DROP
OWNED") / [11](/docs/11/sql-drop-owned.html "PostgreSQL 11 - DROP OWNED") /
[10](/docs/10/sql-drop-owned.html "PostgreSQL 10 - DROP OWNED") /
[9.6](/docs/9.6/sql-drop-owned.html "PostgreSQL 9.6 - DROP OWNED") /
[9.5](/docs/9.5/sql-drop-owned.html "PostgreSQL 9.5 - DROP OWNED") /
[9.4](/docs/9.4/sql-drop-owned.html "PostgreSQL 9.4 - DROP OWNED") /
[9.3](/docs/9.3/sql-drop-owned.html "PostgreSQL 9.3 - DROP OWNED") /
[9.2](/docs/9.2/sql-drop-owned.html "PostgreSQL 9.2 - DROP OWNED") /
[9.1](/docs/9.1/sql-drop-owned.html "PostgreSQL 9.1 - DROP OWNED") /
[9.0](/docs/9.0/sql-drop-owned.html "PostgreSQL 9.0 - DROP OWNED") /
[8.4](/docs/8.4/sql-drop-owned.html "PostgreSQL 8.4 - DROP OWNED") /
[8.3](/docs/8.3/sql-drop-owned.html "PostgreSQL 8.3 - DROP OWNED") /
[8.2](/docs/8.2/sql-drop-owned.html "PostgreSQL 8.2 - DROP OWNED")

__

DROP OWNED  
---  
[Prev](sql-dropopfamily.html "DROP OPERATOR FAMILY")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-droppolicy.html "DROP POLICY")  
  
* * *

## DROP OWNED

DROP OWNED — remove database objects owned by a database role

## Synopsis

    
    
    DROP OWNED BY { _name_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER } [, ...] [ CASCADE | RESTRICT ]
    

## Description

`DROP OWNED` drops all the objects within the current database that are owned
by one of the specified roles. Any privileges granted to the given roles on
objects in the current database or on shared objects (databases, tablespaces,
configuration parameters) will also be revoked.

## Parameters

_`name`_

    

The name of a role whose objects will be dropped, and whose privileges will be
revoked.

`CASCADE`

    

Automatically drop objects that depend on the affected objects, and in turn
all objects that depend on those objects (see [Section 5.14](ddl-depend.html
"5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the objects owned by a role if any other database objects
depend on one of the affected objects. This is the default.

## Notes

`DROP OWNED` is often used to prepare for the removal of one or more roles.
Because `DROP OWNED` only affects the objects in the current database, it is
usually necessary to execute this command in each database that contains
objects owned by a role that is to be removed.

Using the `CASCADE` option might make the command recurse to objects owned by
other users.

The [`REASSIGN OWNED`](sql-reassign-owned.html "REASSIGN OWNED") command is an
alternative that reassigns the ownership of all the database objects owned by
one or more roles. However, `REASSIGN OWNED` does not deal with privileges for
other objects.

Databases and tablespaces owned by the role(s) will not be removed.

See [Section 22.4](role-removal.html "22.4. Dropping Roles") for more
discussion.

## Compatibility

The `DROP OWNED` command is a PostgreSQL extension.

## See Also

[REASSIGN OWNED](sql-reassign-owned.html "REASSIGN OWNED"), [DROP ROLE](sql-
droprole.html "DROP ROLE")

* * *

[Prev](sql-dropopfamily.html "DROP OPERATOR FAMILY")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-droppolicy.html "DROP POLICY")  
---|---|---  
DROP OPERATOR FAMILY  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP POLICY  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-drop-owned.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

