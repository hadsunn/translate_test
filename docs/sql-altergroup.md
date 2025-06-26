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

Supported Versions: [Current](/docs/current/sql-altergroup.html "PostgreSQL 17
- ALTER GROUP") ([17](/docs/17/sql-altergroup.html "PostgreSQL 17 - ALTER
GROUP")) / [16](/docs/16/sql-altergroup.html "PostgreSQL 16 - ALTER GROUP") /
[15](/docs/15/sql-altergroup.html "PostgreSQL 15 - ALTER GROUP") /
[14](/docs/14/sql-altergroup.html "PostgreSQL 14 - ALTER GROUP") /
[13](/docs/13/sql-altergroup.html "PostgreSQL 13 - ALTER GROUP")

Development Versions: [18](/docs/18/sql-altergroup.html "PostgreSQL 18 - ALTER
GROUP") / [devel](/docs/devel/sql-altergroup.html "PostgreSQL devel - ALTER
GROUP")

Unsupported versions: [12](/docs/12/sql-altergroup.html "PostgreSQL 12 - ALTER
GROUP") / [11](/docs/11/sql-altergroup.html "PostgreSQL 11 - ALTER GROUP") /
[10](/docs/10/sql-altergroup.html "PostgreSQL 10 - ALTER GROUP") /
[9.6](/docs/9.6/sql-altergroup.html "PostgreSQL 9.6 - ALTER GROUP") /
[9.5](/docs/9.5/sql-altergroup.html "PostgreSQL 9.5 - ALTER GROUP") /
[9.4](/docs/9.4/sql-altergroup.html "PostgreSQL 9.4 - ALTER GROUP") /
[9.3](/docs/9.3/sql-altergroup.html "PostgreSQL 9.3 - ALTER GROUP") /
[9.2](/docs/9.2/sql-altergroup.html "PostgreSQL 9.2 - ALTER GROUP") /
[9.1](/docs/9.1/sql-altergroup.html "PostgreSQL 9.1 - ALTER GROUP") /
[9.0](/docs/9.0/sql-altergroup.html "PostgreSQL 9.0 - ALTER GROUP") /
[8.4](/docs/8.4/sql-altergroup.html "PostgreSQL 8.4 - ALTER GROUP") /
[8.3](/docs/8.3/sql-altergroup.html "PostgreSQL 8.3 - ALTER GROUP") /
[8.2](/docs/8.2/sql-altergroup.html "PostgreSQL 8.2 - ALTER GROUP") /
[8.1](/docs/8.1/sql-altergroup.html "PostgreSQL 8.1 - ALTER GROUP") /
[8.0](/docs/8.0/sql-altergroup.html "PostgreSQL 8.0 - ALTER GROUP") /
[7.4](/docs/7.4/sql-altergroup.html "PostgreSQL 7.4 - ALTER GROUP") /
[7.3](/docs/7.3/sql-altergroup.html "PostgreSQL 7.3 - ALTER GROUP") /
[7.2](/docs/7.2/sql-altergroup.html "PostgreSQL 7.2 - ALTER GROUP") /
[7.1](/docs/7.1/sql-altergroup.html "PostgreSQL 7.1 - ALTER GROUP")

__

ALTER GROUP  
---  
[Prev](sql-alterfunction.html "ALTER FUNCTION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterindex.html "ALTER INDEX")  
  
* * *

## ALTER GROUP

ALTER GROUP — change role name or membership

## Synopsis

    
    
    ALTER GROUP _role_specification_ ADD USER _user_name_ [, ... ]
    ALTER GROUP _role_specification_ DROP USER _user_name_ [, ... ]
    
    where _role_specification_ can be:
    
        _role_name_
      | CURRENT_ROLE
      | CURRENT_USER
      | SESSION_USER
    
    ALTER GROUP _group_name_ RENAME TO _new_name_
    

## Description

`ALTER GROUP` changes the attributes of a user group. This is an obsolete
command, though still accepted for backwards compatibility, because groups
(and users too) have been superseded by the more general concept of roles.

The first two variants add users to a group or remove them from a group. (Any
role can play the part of either a “user” or a “group” for this purpose.)
These variants are effectively equivalent to granting or revoking membership
in the role named as the “group”; so the preferred way to do this is to use
[`GRANT`](sql-grant.html "GRANT") or [`REVOKE`](sql-revoke.html "REVOKE").
Note that `GRANT` and `REVOKE` have additional options which are not available
with this command, such as the ability to grant and revoke `ADMIN OPTION`, and
the ability to specify the grantor.

The third variant changes the name of the group. This is exactly equivalent to
renaming the role with [`ALTER ROLE`](sql-alterrole.html "ALTER ROLE").

## Parameters

_`group_name`_

    

The name of the group (role) to modify.

_`user_name`_

    

Users (roles) that are to be added to or removed from the group. The users
must already exist; `ALTER GROUP` does not create or drop users.

_`new_name`_

    

The new name of the group.

## Examples

Add users to a group:

    
    
    ALTER GROUP staff ADD USER karl, john;
    

Remove a user from a group:

    
    
    ALTER GROUP workers DROP USER beth;
    

## Compatibility

There is no `ALTER GROUP` statement in the SQL standard.

## See Also

[GRANT](sql-grant.html "GRANT"), [REVOKE](sql-revoke.html "REVOKE"), [ALTER
ROLE](sql-alterrole.html "ALTER ROLE")

* * *

[Prev](sql-alterfunction.html "ALTER FUNCTION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterindex.html "ALTER INDEX")  
---|---|---  
ALTER FUNCTION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER INDEX  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-altergroup.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

