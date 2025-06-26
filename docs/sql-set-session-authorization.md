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

Supported Versions: [Current](/docs/current/sql-set-session-authorization.html
"PostgreSQL 17 - SET SESSION AUTHORIZATION") ([17](/docs/17/sql-set-session-
authorization.html "PostgreSQL 17 - SET SESSION AUTHORIZATION")) /
[16](/docs/16/sql-set-session-authorization.html "PostgreSQL 16 - SET SESSION
AUTHORIZATION") / [15](/docs/15/sql-set-session-authorization.html "PostgreSQL
15 - SET SESSION AUTHORIZATION") / [14](/docs/14/sql-set-session-
authorization.html "PostgreSQL 14 - SET SESSION AUTHORIZATION") /
[13](/docs/13/sql-set-session-authorization.html "PostgreSQL 13 - SET SESSION
AUTHORIZATION")

Development Versions: [18](/docs/18/sql-set-session-authorization.html
"PostgreSQL 18 - SET SESSION AUTHORIZATION") / [devel](/docs/devel/sql-set-
session-authorization.html "PostgreSQL devel - SET SESSION AUTHORIZATION")

Unsupported versions: [12](/docs/12/sql-set-session-authorization.html
"PostgreSQL 12 - SET SESSION AUTHORIZATION") / [11](/docs/11/sql-set-session-
authorization.html "PostgreSQL 11 - SET SESSION AUTHORIZATION") /
[10](/docs/10/sql-set-session-authorization.html "PostgreSQL 10 - SET SESSION
AUTHORIZATION") / [9.6](/docs/9.6/sql-set-session-authorization.html
"PostgreSQL 9.6 - SET SESSION AUTHORIZATION") / [9.5](/docs/9.5/sql-set-
session-authorization.html "PostgreSQL 9.5 - SET SESSION AUTHORIZATION") /
[9.4](/docs/9.4/sql-set-session-authorization.html "PostgreSQL 9.4 - SET
SESSION AUTHORIZATION") / [9.3](/docs/9.3/sql-set-session-authorization.html
"PostgreSQL 9.3 - SET SESSION AUTHORIZATION") / [9.2](/docs/9.2/sql-set-
session-authorization.html "PostgreSQL 9.2 - SET SESSION AUTHORIZATION") /
[9.1](/docs/9.1/sql-set-session-authorization.html "PostgreSQL 9.1 - SET
SESSION AUTHORIZATION") / [9.0](/docs/9.0/sql-set-session-authorization.html
"PostgreSQL 9.0 - SET SESSION AUTHORIZATION") / [8.4](/docs/8.4/sql-set-
session-authorization.html "PostgreSQL 8.4 - SET SESSION AUTHORIZATION") /
[8.3](/docs/8.3/sql-set-session-authorization.html "PostgreSQL 8.3 - SET
SESSION AUTHORIZATION") / [8.2](/docs/8.2/sql-set-session-authorization.html
"PostgreSQL 8.2 - SET SESSION AUTHORIZATION") / [8.1](/docs/8.1/sql-set-
session-authorization.html "PostgreSQL 8.1 - SET SESSION AUTHORIZATION") /
[8.0](/docs/8.0/sql-set-session-authorization.html "PostgreSQL 8.0 - SET
SESSION AUTHORIZATION") / [7.4](/docs/7.4/sql-set-session-authorization.html
"PostgreSQL 7.4 - SET SESSION AUTHORIZATION") / [7.3](/docs/7.3/sql-set-
session-authorization.html "PostgreSQL 7.3 - SET SESSION AUTHORIZATION") /
[7.2](/docs/7.2/sql-set-session-authorization.html "PostgreSQL 7.2 - SET
SESSION AUTHORIZATION")

__

SET SESSION AUTHORIZATION  
---  
[Prev](sql-set-role.html "SET ROLE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-set-transaction.html "SET TRANSACTION")  
  
* * *

## SET SESSION AUTHORIZATION

SET SESSION AUTHORIZATION — set the session user identifier and the current
user identifier of the current session

## Synopsis

    
    
    SET [ SESSION | LOCAL ] SESSION AUTHORIZATION _user_name_
    SET [ SESSION | LOCAL ] SESSION AUTHORIZATION DEFAULT
    RESET SESSION AUTHORIZATION
    

## Description

This command sets the session user identifier and the current user identifier
of the current SQL session to be _`user_name`_. The user name can be written
as either an identifier or a string literal. Using this command, it is
possible, for example, to temporarily become an unprivileged user and later
switch back to being a superuser.

The session user identifier is initially set to be the (possibly
authenticated) user name provided by the client. The current user identifier
is normally equal to the session user identifier, but might change temporarily
in the context of `SECURITY DEFINER` functions and similar mechanisms; it can
also be changed by [`SET ROLE`](sql-set-role.html "SET ROLE"). The current
user identifier is relevant for permission checking.

The session user identifier can be changed only if the initial session user
(the _authenticated user_) had the superuser privilege. Otherwise, the command
is accepted only if it specifies the authenticated user name.

The `SESSION` and `LOCAL` modifiers act the same as for the regular
[`SET`](sql-set.html "SET") command.

The `DEFAULT` and `RESET` forms reset the session and current user identifiers
to be the originally authenticated user name. These forms can be executed by
any user.

## Notes

`SET SESSION AUTHORIZATION` cannot be used within a `SECURITY DEFINER`
function.

## Examples

    
    
    SELECT SESSION_USER, CURRENT_USER;
    
     session_user | current_user
    --------------+--------------
     peter        | peter
    
    SET SESSION AUTHORIZATION 'paul';
    
    SELECT SESSION_USER, CURRENT_USER;
    
     session_user | current_user
    --------------+--------------
     paul         | paul
    

## Compatibility

The SQL standard allows some other expressions to appear in place of the
literal _`user_name`_ , but these options are not important in practice.
PostgreSQL allows identifier syntax (`"_`username`_ "`), which SQL does not.
SQL does not allow this command during a transaction; PostgreSQL does not make
this restriction because there is no reason to. The `SESSION` and `LOCAL`
modifiers are a PostgreSQL extension, as is the `RESET` syntax.

The privileges necessary to execute this command are left implementation-
defined by the standard.

## See Also

[SET ROLE](sql-set-role.html "SET ROLE")

* * *

[Prev](sql-set-role.html "SET ROLE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-set-transaction.html "SET TRANSACTION")  
---|---|---  
SET ROLE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SET TRANSACTION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-set-session-
authorization.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

