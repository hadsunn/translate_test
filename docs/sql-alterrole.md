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

Supported Versions: [Current](/docs/current/sql-alterrole.html "PostgreSQL 17
- ALTER ROLE") ([17](/docs/17/sql-alterrole.html "PostgreSQL 17 - ALTER
ROLE")) / [16](/docs/16/sql-alterrole.html "PostgreSQL 16 - ALTER ROLE") /
[15](/docs/15/sql-alterrole.html "PostgreSQL 15 - ALTER ROLE") /
[14](/docs/14/sql-alterrole.html "PostgreSQL 14 - ALTER ROLE") /
[13](/docs/13/sql-alterrole.html "PostgreSQL 13 - ALTER ROLE")

Development Versions: [18](/docs/18/sql-alterrole.html "PostgreSQL 18 - ALTER
ROLE") / [devel](/docs/devel/sql-alterrole.html "PostgreSQL devel - ALTER
ROLE")

Unsupported versions: [12](/docs/12/sql-alterrole.html "PostgreSQL 12 - ALTER
ROLE") / [11](/docs/11/sql-alterrole.html "PostgreSQL 11 - ALTER ROLE") /
[10](/docs/10/sql-alterrole.html "PostgreSQL 10 - ALTER ROLE") /
[9.6](/docs/9.6/sql-alterrole.html "PostgreSQL 9.6 - ALTER ROLE") /
[9.5](/docs/9.5/sql-alterrole.html "PostgreSQL 9.5 - ALTER ROLE") /
[9.4](/docs/9.4/sql-alterrole.html "PostgreSQL 9.4 - ALTER ROLE") /
[9.3](/docs/9.3/sql-alterrole.html "PostgreSQL 9.3 - ALTER ROLE") /
[9.2](/docs/9.2/sql-alterrole.html "PostgreSQL 9.2 - ALTER ROLE") /
[9.1](/docs/9.1/sql-alterrole.html "PostgreSQL 9.1 - ALTER ROLE") /
[9.0](/docs/9.0/sql-alterrole.html "PostgreSQL 9.0 - ALTER ROLE") /
[8.4](/docs/8.4/sql-alterrole.html "PostgreSQL 8.4 - ALTER ROLE") /
[8.3](/docs/8.3/sql-alterrole.html "PostgreSQL 8.3 - ALTER ROLE") /
[8.2](/docs/8.2/sql-alterrole.html "PostgreSQL 8.2 - ALTER ROLE") /
[8.1](/docs/8.1/sql-alterrole.html "PostgreSQL 8.1 - ALTER ROLE")

__

ALTER ROLE  
---  
[Prev](sql-alterpublication.html "ALTER PUBLICATION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterroutine.html "ALTER ROUTINE")  
  
* * *

## ALTER ROLE

ALTER ROLE — change a database role

## Synopsis

    
    
    ALTER ROLE _role_specification_ [ WITH ] _option_ [ ... ]
    
    where _option_ can be:
    
          SUPERUSER | NOSUPERUSER
        | CREATEDB | NOCREATEDB
        | CREATEROLE | NOCREATEROLE
        | INHERIT | NOINHERIT
        | LOGIN | NOLOGIN
        | REPLICATION | NOREPLICATION
        | BYPASSRLS | NOBYPASSRLS
        | CONNECTION LIMIT _connlimit_
        | [ ENCRYPTED ] PASSWORD '_password_ ' | PASSWORD NULL
        | VALID UNTIL '_timestamp_ '
    
    ALTER ROLE _name_ RENAME TO _new_name_
    
    ALTER ROLE { _role_specification_ | ALL } [ IN DATABASE _database_name_ ] SET _configuration_parameter_ { TO | = } { _value_ | DEFAULT }
    ALTER ROLE { _role_specification_ | ALL } [ IN DATABASE _database_name_ ] SET _configuration_parameter_ FROM CURRENT
    ALTER ROLE { _role_specification_ | ALL } [ IN DATABASE _database_name_ ] RESET _configuration_parameter_
    ALTER ROLE { _role_specification_ | ALL } [ IN DATABASE _database_name_ ] RESET ALL
    
    where _role_specification_ can be:
    
        _role_name_
      | CURRENT_ROLE
      | CURRENT_USER
      | SESSION_USER
    

## Description

`ALTER ROLE` changes the attributes of a PostgreSQL role.

The first variant of this command listed in the synopsis can change many of
the role attributes that can be specified in [`CREATE ROLE`](sql-
createrole.html "CREATE ROLE"). (All the possible attributes are covered,
except that there are no options for adding or removing memberships; use
[`GRANT`](sql-grant.html "GRANT") and [`REVOKE`](sql-revoke.html "REVOKE") for
that.) Attributes not mentioned in the command retain their previous settings.
Database superusers can change any of these settings for any role. Non-
superuser roles having `CREATEROLE` privilege can change most of these
properties, but only for non-superuser and non-replication roles for which
they have been granted `ADMIN OPTION`. Non-superusers cannot change the
`SUPERUSER` property and can change the `CREATEDB`, `REPLICATION`, and
`BYPASSRLS` properties only if they possess the corresponding property
themselves. Ordinary roles can only change their own password.

The second variant changes the name of the role. Database superusers can
rename any role. Roles having `CREATEROLE` privilege can rename non-superuser
roles for which they have been granted `ADMIN OPTION`. The current session
user cannot be renamed. (Connect as a different user if you need to do that.)
Because `MD5`-encrypted passwords use the role name as cryptographic salt,
renaming a role clears its password if the password is `MD5`-encrypted.

The remaining variants change a role's session default for a configuration
variable, either for all databases or, when the `IN DATABASE` clause is
specified, only for sessions in the named database. If `ALL` is specified
instead of a role name, this changes the setting for all roles. Using `ALL`
with `IN DATABASE` is effectively the same as using the command `ALTER
DATABASE ... SET ...`.

Whenever the role subsequently starts a new session, the specified value
becomes the session default, overriding whatever setting is present in
`postgresql.conf` or has been received from the `postgres` command line. This
only happens at login time; executing [`SET ROLE`](sql-set-role.html "SET
ROLE") or [`SET SESSION AUTHORIZATION`](sql-set-session-authorization.html
"SET SESSION AUTHORIZATION") does not cause new configuration values to be
set. Settings set for all databases are overridden by database-specific
settings attached to a role. Settings for specific databases or specific roles
override settings for all roles.

Superusers can change anyone's session defaults. Roles having `CREATEROLE`
privilege can change defaults for non-superuser roles for which they have been
granted `ADMIN OPTION`. Ordinary roles can only set defaults for themselves.
Certain configuration variables cannot be set this way, or can only be set if
a superuser issues the command. Only superusers can change a setting for all
roles in all databases.

## Parameters

_`name`_ #

    

The name of the role whose attributes are to be altered.

`CURRENT_ROLE`  
`CURRENT_USER` #

    

Alter the current user instead of an explicitly identified role.

`SESSION_USER` #

    

Alter the current session user instead of an explicitly identified role.

`SUPERUSER`  
`NOSUPERUSER`  
`CREATEDB`  
`NOCREATEDB`  
`CREATEROLE`  
`NOCREATEROLE`  
`INHERIT`  
`NOINHERIT`  
`LOGIN`  
`NOLOGIN`  
`REPLICATION`  
`NOREPLICATION`  
`BYPASSRLS`  
`NOBYPASSRLS`  
`CONNECTION LIMIT` _`connlimit`_  
[ `ENCRYPTED` ] `PASSWORD` '_`password`_ '  
`PASSWORD NULL`  
`VALID UNTIL` '_`timestamp`_ ' #

    

These clauses alter attributes originally set by [`CREATE ROLE`](sql-
createrole.html "CREATE ROLE"). For more information, see the `CREATE ROLE`
reference page.

_`new_name`_ #

    

The new name of the role.

_`database_name`_ #

    

The name of the database the configuration variable should be set in.

_`configuration_parameter`_  
 _`value`_ #

    

Set this role's session default for the specified configuration parameter to
the given value. If _`value`_ is `DEFAULT` or, equivalently, `RESET` is used,
the role-specific variable setting is removed, so the role will inherit the
system-wide default setting in new sessions. Use `RESET ALL` to clear all
role-specific settings. `SET FROM CURRENT` saves the session's current value
of the parameter as the role-specific value. If `IN DATABASE` is specified,
the configuration parameter is set or removed for the given role and database
only.

Role-specific variable settings take effect only at login; [`SET ROLE`](sql-
set-role.html "SET ROLE") and [`SET SESSION AUTHORIZATION`](sql-set-session-
authorization.html "SET SESSION AUTHORIZATION") do not process role-specific
variable settings.

See [SET](sql-set.html "SET") and [Chapter 20](runtime-config.html
"Chapter 20. Server Configuration") for more information about allowed
parameter names and values.

## Notes

Use [`CREATE ROLE`](sql-createrole.html "CREATE ROLE") to add new roles, and
[`DROP ROLE`](sql-droprole.html "DROP ROLE") to remove a role.

`ALTER ROLE` cannot change a role's memberships. Use [`GRANT`](sql-grant.html
"GRANT") and [`REVOKE`](sql-revoke.html "REVOKE") to do that.

Caution must be exercised when specifying an unencrypted password with this
command. The password will be transmitted to the server in cleartext, and it
might also be logged in the client's command history or the server log.
[psql](app-psql.html "psql") contains a command `\password` that can be used
to change a role's password without exposing the cleartext password.

It is also possible to tie a session default to a specific database rather
than to a role; see [ALTER DATABASE](sql-alterdatabase.html "ALTER DATABASE").
If there is a conflict, database-role-specific settings override role-specific
ones, which in turn override database-specific ones.

## Examples

Change a role's password:

    
    
    ALTER ROLE davide WITH PASSWORD 'hu8jmn3';
    

Remove a role's password:

    
    
    ALTER ROLE davide WITH PASSWORD NULL;
    

Change a password expiration date, specifying that the password should expire
at midday on 4th May 2015 using the time zone which is one hour ahead of UTC:

    
    
    ALTER ROLE chris VALID UNTIL 'May 4 12:00:00 2015 +1';
    

Make a password valid forever:

    
    
    ALTER ROLE fred VALID UNTIL 'infinity';
    

Give a role the ability to manage other roles and create new databases:

    
    
    ALTER ROLE miriam CREATEROLE CREATEDB;
    

Give a role a non-default setting of the [maintenance_work_mem](runtime-
config-resource.html#GUC-MAINTENANCE-WORK-MEM) parameter:

    
    
    ALTER ROLE worker_bee SET maintenance_work_mem = 100000;
    

Give a role a non-default, database-specific setting of the
[client_min_messages](runtime-config-client.html#GUC-CLIENT-MIN-MESSAGES)
parameter:

    
    
    ALTER ROLE fred IN DATABASE devel SET client_min_messages = DEBUG;
    

## Compatibility

The `ALTER ROLE` statement is a PostgreSQL extension.

## See Also

[CREATE ROLE](sql-createrole.html "CREATE ROLE"), [DROP ROLE](sql-
droprole.html "DROP ROLE"), [ALTER DATABASE](sql-alterdatabase.html "ALTER
DATABASE"), [SET](sql-set.html "SET")

* * *

[Prev](sql-alterpublication.html "ALTER PUBLICATION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterroutine.html "ALTER ROUTINE")  
---|---|---  
ALTER PUBLICATION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER ROUTINE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterrole.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

