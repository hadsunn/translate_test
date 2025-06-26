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

Supported Versions: [Current](/docs/current/sql-set-role.html "PostgreSQL 17 -
SET ROLE") ([17](/docs/17/sql-set-role.html "PostgreSQL 17 - SET ROLE")) /
[16](/docs/16/sql-set-role.html "PostgreSQL 16 - SET ROLE") /
[15](/docs/15/sql-set-role.html "PostgreSQL 15 - SET ROLE") /
[14](/docs/14/sql-set-role.html "PostgreSQL 14 - SET ROLE") /
[13](/docs/13/sql-set-role.html "PostgreSQL 13 - SET ROLE")

Development Versions: [18](/docs/18/sql-set-role.html "PostgreSQL 18 - SET
ROLE") / [devel](/docs/devel/sql-set-role.html "PostgreSQL devel - SET ROLE")

Unsupported versions: [12](/docs/12/sql-set-role.html "PostgreSQL 12 - SET
ROLE") / [11](/docs/11/sql-set-role.html "PostgreSQL 11 - SET ROLE") /
[10](/docs/10/sql-set-role.html "PostgreSQL 10 - SET ROLE") /
[9.6](/docs/9.6/sql-set-role.html "PostgreSQL 9.6 - SET ROLE") /
[9.5](/docs/9.5/sql-set-role.html "PostgreSQL 9.5 - SET ROLE") /
[9.4](/docs/9.4/sql-set-role.html "PostgreSQL 9.4 - SET ROLE") /
[9.3](/docs/9.3/sql-set-role.html "PostgreSQL 9.3 - SET ROLE") /
[9.2](/docs/9.2/sql-set-role.html "PostgreSQL 9.2 - SET ROLE") /
[9.1](/docs/9.1/sql-set-role.html "PostgreSQL 9.1 - SET ROLE") /
[9.0](/docs/9.0/sql-set-role.html "PostgreSQL 9.0 - SET ROLE") /
[8.4](/docs/8.4/sql-set-role.html "PostgreSQL 8.4 - SET ROLE") /
[8.3](/docs/8.3/sql-set-role.html "PostgreSQL 8.3 - SET ROLE") /
[8.2](/docs/8.2/sql-set-role.html "PostgreSQL 8.2 - SET ROLE") /
[8.1](/docs/8.1/sql-set-role.html "PostgreSQL 8.1 - SET ROLE")

__

SET ROLE  
---  
[Prev](sql-set-constraints.html "SET CONSTRAINTS")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-set-session-authorization.html "SET SESSION AUTHORIZATION")  
  
* * *

## SET ROLE

SET ROLE — set the current user identifier of the current session

## Synopsis

    
    
    SET [ SESSION | LOCAL ] ROLE _role_name_
    SET [ SESSION | LOCAL ] ROLE NONE
    RESET ROLE
    

## Description

This command sets the current user identifier of the current SQL session to be
_`role_name`_. The role name can be written as either an identifier or a
string literal. After `SET ROLE`, permissions checking for SQL commands is
carried out as though the named role were the one that had logged in
originally.

The current session user must have the `SET` option for the specified
_`role_name`_ , either directly or indirectly via a chain of memberships with
the `SET` option. (If the session user is a superuser, any role can be
selected.)

The `SESSION` and `LOCAL` modifiers act the same as for the regular
[`SET`](sql-set.html "SET") command.

`SET ROLE NONE` sets the current user identifier to the current session user
identifier, as returned by `session_user`. `RESET ROLE` sets the current user
identifier to the connection-time setting specified by the [command-line
options](libpq-connect.html#LIBPQ-CONNECT-OPTIONS), [`ALTER ROLE`](sql-
alterrole.html "ALTER ROLE"), or [`ALTER DATABASE`](sql-alterdatabase.html
"ALTER DATABASE"), if any such settings exist. Otherwise, `RESET ROLE` sets
the current user identifier to the current session user identifier. These
forms can be executed by any user.

## Notes

Using this command, it is possible to either add privileges or restrict one's
privileges. If the session user role has been granted memberships `WITH
INHERIT TRUE`, it automatically has all the privileges of every such role. In
this case, `SET ROLE` effectively drops all the privileges except for those
which the target role directly possesses or inherits. On the other hand, if
the session user role has been granted memberships `WITH INHERIT FALSE`, the
privileges of the granted roles can't be accessed by default. However, if the
role was granted `WITH SET TRUE`, the session user can use `SET ROLE` to drop
the privileges assigned directly to the session user and instead acquire the
privileges available to the named role. If the role was granted `WITH INHERIT
FALSE, SET FALSE` then the privileges of that role cannot be exercised either
with or without `SET ROLE`.

Note that when a superuser chooses to `SET ROLE` to a non-superuser role, they
lose their superuser privileges.

`SET ROLE` has effects comparable to [`SET SESSION AUTHORIZATION`](sql-set-
session-authorization.html "SET SESSION AUTHORIZATION"), but the privilege
checks involved are quite different. Also, `SET SESSION AUTHORIZATION`
determines which roles are allowable for later `SET ROLE` commands, whereas
changing roles with `SET ROLE` does not change the set of roles allowed to a
later `SET ROLE`.

`SET ROLE` does not process session variables as specified by the role's
[`ALTER ROLE`](sql-alterrole.html "ALTER ROLE") settings; this only happens
during login.

`SET ROLE` cannot be used within a `SECURITY DEFINER` function.

## Examples

    
    
    SELECT SESSION_USER, CURRENT_USER;
    
     session_user | current_user
    --------------+--------------
     peter        | peter
    
    SET ROLE 'paul';
    
    SELECT SESSION_USER, CURRENT_USER;
    
     session_user | current_user
    --------------+--------------
     peter        | paul
    

## Compatibility

PostgreSQL allows identifier syntax (`"_`rolename`_ "`), while the SQL
standard requires the role name to be written as a string literal. SQL does
not allow this command during a transaction; PostgreSQL does not make this
restriction because there is no reason to. The `SESSION` and `LOCAL` modifiers
are a PostgreSQL extension, as is the `RESET` syntax.

## See Also

[SET SESSION AUTHORIZATION](sql-set-session-authorization.html "SET SESSION
AUTHORIZATION")

* * *

[Prev](sql-set-constraints.html "SET CONSTRAINTS")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-set-session-authorization.html "SET SESSION AUTHORIZATION")  
---|---|---  
SET CONSTRAINTS  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SET SESSION AUTHORIZATION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-set-role.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

