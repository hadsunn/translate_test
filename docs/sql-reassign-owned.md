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

Supported Versions: [Current](/docs/current/sql-reassign-owned.html
"PostgreSQL 17 - REASSIGN OWNED") ([17](/docs/17/sql-reassign-owned.html
"PostgreSQL 17 - REASSIGN OWNED")) / [16](/docs/16/sql-reassign-owned.html
"PostgreSQL 16 - REASSIGN OWNED") / [15](/docs/15/sql-reassign-owned.html
"PostgreSQL 15 - REASSIGN OWNED") / [14](/docs/14/sql-reassign-owned.html
"PostgreSQL 14 - REASSIGN OWNED") / [13](/docs/13/sql-reassign-owned.html
"PostgreSQL 13 - REASSIGN OWNED")

Development Versions: [18](/docs/18/sql-reassign-owned.html "PostgreSQL 18 -
REASSIGN OWNED") / [devel](/docs/devel/sql-reassign-owned.html "PostgreSQL
devel - REASSIGN OWNED")

Unsupported versions: [12](/docs/12/sql-reassign-owned.html "PostgreSQL 12 -
REASSIGN OWNED") / [11](/docs/11/sql-reassign-owned.html "PostgreSQL 11 -
REASSIGN OWNED") / [10](/docs/10/sql-reassign-owned.html "PostgreSQL 10 -
REASSIGN OWNED") / [9.6](/docs/9.6/sql-reassign-owned.html "PostgreSQL 9.6 -
REASSIGN OWNED") / [9.5](/docs/9.5/sql-reassign-owned.html "PostgreSQL 9.5 -
REASSIGN OWNED") / [9.4](/docs/9.4/sql-reassign-owned.html "PostgreSQL 9.4 -
REASSIGN OWNED") / [9.3](/docs/9.3/sql-reassign-owned.html "PostgreSQL 9.3 -
REASSIGN OWNED") / [9.2](/docs/9.2/sql-reassign-owned.html "PostgreSQL 9.2 -
REASSIGN OWNED") / [9.1](/docs/9.1/sql-reassign-owned.html "PostgreSQL 9.1 -
REASSIGN OWNED") / [9.0](/docs/9.0/sql-reassign-owned.html "PostgreSQL 9.0 -
REASSIGN OWNED") / [8.4](/docs/8.4/sql-reassign-owned.html "PostgreSQL 8.4 -
REASSIGN OWNED") / [8.3](/docs/8.3/sql-reassign-owned.html "PostgreSQL 8.3 -
REASSIGN OWNED") / [8.2](/docs/8.2/sql-reassign-owned.html "PostgreSQL 8.2 -
REASSIGN OWNED")

__

REASSIGN OWNED  
---  
[Prev](sql-prepare-transaction.html "PREPARE TRANSACTION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-refreshmaterializedview.html "REFRESH MATERIALIZED VIEW")  
  
* * *

## REASSIGN OWNED

REASSIGN OWNED — change the ownership of database objects owned by a database
role

## Synopsis

    
    
    REASSIGN OWNED BY { _old_role_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER } [, ...]
                   TO { _new_role_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    

## Description

`REASSIGN OWNED` instructs the system to change the ownership of database
objects owned by any of the _`old_roles`_ to _`new_role`_.

## Parameters

_`old_role`_

    

The name of a role. The ownership of all the objects within the current
database, and of all shared objects (databases, tablespaces), owned by this
role will be reassigned to _`new_role`_.

_`new_role`_

    

The name of the role that will be made the new owner of the affected objects.

## Notes

`REASSIGN OWNED` is often used to prepare for the removal of one or more
roles. Because `REASSIGN OWNED` does not affect objects within other
databases, it is usually necessary to execute this command in each database
that contains objects owned by a role that is to be removed.

`REASSIGN OWNED` requires membership on both the source role(s) and the target
role.

The [`DROP OWNED`](sql-drop-owned.html "DROP OWNED") command is an alternative
that simply drops all the database objects owned by one or more roles.

The `REASSIGN OWNED` command does not affect any privileges granted to the
_`old_roles`_ on objects that are not owned by them. Likewise, it does not
affect default privileges created with `ALTER DEFAULT PRIVILEGES`. Use `DROP
OWNED` to revoke such privileges.

See [Section 22.4](role-removal.html "22.4. Dropping Roles") for more
discussion.

## Compatibility

The `REASSIGN OWNED` command is a PostgreSQL extension.

## See Also

[DROP OWNED](sql-drop-owned.html "DROP OWNED"), [DROP ROLE](sql-droprole.html
"DROP ROLE"), [ALTER DATABASE](sql-alterdatabase.html "ALTER DATABASE")

* * *

[Prev](sql-prepare-transaction.html "PREPARE TRANSACTION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-refreshmaterializedview.html "REFRESH MATERIALIZED VIEW")  
---|---|---  
PREPARE TRANSACTION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  REFRESH MATERIALIZED VIEW  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-reassign-owned.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

