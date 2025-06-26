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

Supported Versions: [Current](/docs/current/sql-alterdefaultprivileges.html
"PostgreSQL 17 - ALTER DEFAULT PRIVILEGES") ([17](/docs/17/sql-
alterdefaultprivileges.html "PostgreSQL 17 - ALTER DEFAULT PRIVILEGES")) /
[16](/docs/16/sql-alterdefaultprivileges.html "PostgreSQL 16 - ALTER DEFAULT
PRIVILEGES") / [15](/docs/15/sql-alterdefaultprivileges.html "PostgreSQL 15 -
ALTER DEFAULT PRIVILEGES") / [14](/docs/14/sql-alterdefaultprivileges.html
"PostgreSQL 14 - ALTER DEFAULT PRIVILEGES") / [13](/docs/13/sql-
alterdefaultprivileges.html "PostgreSQL 13 - ALTER DEFAULT PRIVILEGES")

Development Versions: [18](/docs/18/sql-alterdefaultprivileges.html
"PostgreSQL 18 - ALTER DEFAULT PRIVILEGES") / [devel](/docs/devel/sql-
alterdefaultprivileges.html "PostgreSQL devel - ALTER DEFAULT PRIVILEGES")

Unsupported versions: [12](/docs/12/sql-alterdefaultprivileges.html
"PostgreSQL 12 - ALTER DEFAULT PRIVILEGES") / [11](/docs/11/sql-
alterdefaultprivileges.html "PostgreSQL 11 - ALTER DEFAULT PRIVILEGES") /
[10](/docs/10/sql-alterdefaultprivileges.html "PostgreSQL 10 - ALTER DEFAULT
PRIVILEGES") / [9.6](/docs/9.6/sql-alterdefaultprivileges.html "PostgreSQL 9.6
- ALTER DEFAULT PRIVILEGES") / [9.5](/docs/9.5/sql-alterdefaultprivileges.html
"PostgreSQL 9.5 - ALTER DEFAULT PRIVILEGES") / [9.4](/docs/9.4/sql-
alterdefaultprivileges.html "PostgreSQL 9.4 - ALTER DEFAULT PRIVILEGES") /
[9.3](/docs/9.3/sql-alterdefaultprivileges.html "PostgreSQL 9.3 - ALTER
DEFAULT PRIVILEGES") / [9.2](/docs/9.2/sql-alterdefaultprivileges.html
"PostgreSQL 9.2 - ALTER DEFAULT PRIVILEGES") / [9.1](/docs/9.1/sql-
alterdefaultprivileges.html "PostgreSQL 9.1 - ALTER DEFAULT PRIVILEGES") /
[9.0](/docs/9.0/sql-alterdefaultprivileges.html "PostgreSQL 9.0 - ALTER
DEFAULT PRIVILEGES")

__

ALTER DEFAULT PRIVILEGES  
---  
[Prev](sql-alterdatabase.html "ALTER DATABASE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterdomain.html "ALTER DOMAIN")  
  
* * *

## ALTER DEFAULT PRIVILEGES

ALTER DEFAULT PRIVILEGES — define default access privileges

## Synopsis

    
    
    ALTER DEFAULT PRIVILEGES
        [ FOR { ROLE | USER } _target_role_ [, ...] ]
        [ IN SCHEMA _schema_name_ [, ...] ]
        _abbreviated_grant_or_revoke_
    
    where _abbreviated_grant_or_revoke_ is one of:
    
    GRANT { { SELECT | INSERT | UPDATE | DELETE | TRUNCATE | REFERENCES | TRIGGER }
        [, ...] | ALL [ PRIVILEGES ] }
        ON TABLES
        TO { [ GROUP ] _role_name_ | PUBLIC } [, ...] [ WITH GRANT OPTION ]
    
    GRANT { { USAGE | SELECT | UPDATE }
        [, ...] | ALL [ PRIVILEGES ] }
        ON SEQUENCES
        TO { [ GROUP ] _role_name_ | PUBLIC } [, ...] [ WITH GRANT OPTION ]
    
    GRANT { EXECUTE | ALL [ PRIVILEGES ] }
        ON { FUNCTIONS | ROUTINES }
        TO { [ GROUP ] _role_name_ | PUBLIC } [, ...] [ WITH GRANT OPTION ]
    
    GRANT { USAGE | ALL [ PRIVILEGES ] }
        ON TYPES
        TO { [ GROUP ] _role_name_ | PUBLIC } [, ...] [ WITH GRANT OPTION ]
    
    GRANT { { USAGE | CREATE }
        [, ...] | ALL [ PRIVILEGES ] }
        ON SCHEMAS
        TO { [ GROUP ] _role_name_ | PUBLIC } [, ...] [ WITH GRANT OPTION ]
    
    REVOKE [ GRANT OPTION FOR ]
        { { SELECT | INSERT | UPDATE | DELETE | TRUNCATE | REFERENCES | TRIGGER }
        [, ...] | ALL [ PRIVILEGES ] }
        ON TABLES
        FROM { [ GROUP ] _role_name_ | PUBLIC } [, ...]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { { USAGE | SELECT | UPDATE }
        [, ...] | ALL [ PRIVILEGES ] }
        ON SEQUENCES
        FROM { [ GROUP ] _role_name_ | PUBLIC } [, ...]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { EXECUTE | ALL [ PRIVILEGES ] }
        ON { FUNCTIONS | ROUTINES }
        FROM { [ GROUP ] _role_name_ | PUBLIC } [, ...]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { USAGE | ALL [ PRIVILEGES ] }
        ON TYPES
        FROM { [ GROUP ] _role_name_ | PUBLIC } [, ...]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { { USAGE | CREATE }
        [, ...] | ALL [ PRIVILEGES ] }
        ON SCHEMAS
        FROM { [ GROUP ] _role_name_ | PUBLIC } [, ...]
        [ CASCADE | RESTRICT ]
    

## Description

`ALTER DEFAULT PRIVILEGES` allows you to set the privileges that will be
applied to objects created in the future. (It does not affect privileges
assigned to already-existing objects.) Privileges can be set globally (i.e.,
for all objects created in the current database), or just for objects created
in specified schemas.

While you can change your own default privileges and the defaults of roles
that you are a member of, at object creation time, new object permissions are
only affected by the default privileges of the current role, and are not
inherited from any roles in which the current role is a member.

As explained in [Section 5.7](ddl-priv.html "5.7. Privileges"), the default
privileges for any object type normally grant all grantable permissions to the
object owner, and may grant some privileges to `PUBLIC` as well. However, this
behavior can be changed by altering the global default privileges with `ALTER
DEFAULT PRIVILEGES`.

Currently, only the privileges for schemas, tables (including views and
foreign tables), sequences, functions, and types (including domains) can be
altered. For this command, functions include aggregates and procedures. The
words `FUNCTIONS` and `ROUTINES` are equivalent in this command. (`ROUTINES`
is preferred going forward as the standard term for functions and procedures
taken together. In earlier PostgreSQL releases, only the word `FUNCTIONS` was
allowed. It is not possible to set default privileges for functions and
procedures separately.)

Default privileges that are specified per-schema are added to whatever the
global default privileges are for the particular object type. This means you
cannot revoke privileges per-schema if they are granted globally (either by
default, or according to a previous `ALTER DEFAULT PRIVILEGES` command that
did not specify a schema). Per-schema `REVOKE` is only useful to reverse the
effects of a previous per-schema `GRANT`.

### Parameters

_`target_role`_

    

Change default privileges for objects created by the _`target_role`_ , or the
current role if unspecified.

_`schema_name`_

    

The name of an existing schema. If specified, the default privileges are
altered for objects later created in that schema. If `IN SCHEMA` is omitted,
the global default privileges are altered. `IN SCHEMA` is not allowed when
setting privileges for schemas, since schemas can't be nested.

_`role_name`_

    

The name of an existing role to grant or revoke privileges for. This
parameter, and all the other parameters in _`abbreviated_grant_or_revoke`_ ,
act as described under [GRANT](sql-grant.html "GRANT") or [REVOKE](sql-
revoke.html "REVOKE"), except that one is setting permissions for a whole
class of objects rather than specific named objects.

## Notes

Use [psql](app-psql.html "psql")'s `\ddp` command to obtain information about
existing assignments of default privileges. The meaning of the privilege
display is the same as explained for `\dp` in [Section 5.7](ddl-priv.html
"5.7. Privileges").

If you wish to drop a role for which the default privileges have been altered,
it is necessary to reverse the changes in its default privileges or use `DROP
OWNED BY` to get rid of the default privileges entry for the role.

## Examples

Grant SELECT privilege to everyone for all tables (and views) you subsequently
create in schema `myschema`, and allow role `webuser` to INSERT into them too:

    
    
    ALTER DEFAULT PRIVILEGES IN SCHEMA myschema GRANT SELECT ON TABLES TO PUBLIC;
    ALTER DEFAULT PRIVILEGES IN SCHEMA myschema GRANT INSERT ON TABLES TO webuser;
    

Undo the above, so that subsequently-created tables won't have any more
permissions than normal:

    
    
    ALTER DEFAULT PRIVILEGES IN SCHEMA myschema REVOKE SELECT ON TABLES FROM PUBLIC;
    ALTER DEFAULT PRIVILEGES IN SCHEMA myschema REVOKE INSERT ON TABLES FROM webuser;
    

Remove the public EXECUTE permission that is normally granted on functions,
for all functions subsequently created by role `admin`:

    
    
    ALTER DEFAULT PRIVILEGES FOR ROLE admin REVOKE EXECUTE ON FUNCTIONS FROM PUBLIC;
    

Note however that you _cannot_ accomplish that effect with a command limited
to a single schema. This command has no effect, unless it is undoing a
matching `GRANT`:

    
    
    ALTER DEFAULT PRIVILEGES IN SCHEMA public REVOKE EXECUTE ON FUNCTIONS FROM PUBLIC;
    

That's because per-schema default privileges can only add privileges to the
global setting, not remove privileges granted by it.

## Compatibility

There is no `ALTER DEFAULT PRIVILEGES` statement in the SQL standard.

## See Also

[GRANT](sql-grant.html "GRANT"), [REVOKE](sql-revoke.html "REVOKE")

* * *

[Prev](sql-alterdatabase.html "ALTER DATABASE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterdomain.html "ALTER DOMAIN")  
---|---|---  
ALTER DATABASE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER DOMAIN  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-
alterdefaultprivileges.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

