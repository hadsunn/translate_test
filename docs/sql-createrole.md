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

Supported Versions: [Current](/docs/current/sql-createrole.html "PostgreSQL 17
- CREATE ROLE") ([17](/docs/17/sql-createrole.html "PostgreSQL 17 - CREATE
ROLE")) / [16](/docs/16/sql-createrole.html "PostgreSQL 16 - CREATE ROLE") /
[15](/docs/15/sql-createrole.html "PostgreSQL 15 - CREATE ROLE") /
[14](/docs/14/sql-createrole.html "PostgreSQL 14 - CREATE ROLE") /
[13](/docs/13/sql-createrole.html "PostgreSQL 13 - CREATE ROLE")

Development Versions: [18](/docs/18/sql-createrole.html "PostgreSQL 18 -
CREATE ROLE") / [devel](/docs/devel/sql-createrole.html "PostgreSQL devel -
CREATE ROLE")

Unsupported versions: [12](/docs/12/sql-createrole.html "PostgreSQL 12 -
CREATE ROLE") / [11](/docs/11/sql-createrole.html "PostgreSQL 11 - CREATE
ROLE") / [10](/docs/10/sql-createrole.html "PostgreSQL 10 - CREATE ROLE") /
[9.6](/docs/9.6/sql-createrole.html "PostgreSQL 9.6 - CREATE ROLE") /
[9.5](/docs/9.5/sql-createrole.html "PostgreSQL 9.5 - CREATE ROLE") /
[9.4](/docs/9.4/sql-createrole.html "PostgreSQL 9.4 - CREATE ROLE") /
[9.3](/docs/9.3/sql-createrole.html "PostgreSQL 9.3 - CREATE ROLE") /
[9.2](/docs/9.2/sql-createrole.html "PostgreSQL 9.2 - CREATE ROLE") /
[9.1](/docs/9.1/sql-createrole.html "PostgreSQL 9.1 - CREATE ROLE") /
[9.0](/docs/9.0/sql-createrole.html "PostgreSQL 9.0 - CREATE ROLE") /
[8.4](/docs/8.4/sql-createrole.html "PostgreSQL 8.4 - CREATE ROLE") /
[8.3](/docs/8.3/sql-createrole.html "PostgreSQL 8.3 - CREATE ROLE") /
[8.2](/docs/8.2/sql-createrole.html "PostgreSQL 8.2 - CREATE ROLE") /
[8.1](/docs/8.1/sql-createrole.html "PostgreSQL 8.1 - CREATE ROLE")

__

CREATE ROLE  
---  
[Prev](sql-createpublication.html "CREATE PUBLICATION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createrule.html "CREATE RULE")  
  
* * *

## CREATE ROLE

CREATE ROLE — define a new database role

## Synopsis

    
    
    CREATE ROLE _name_ [ [ WITH ] _option_ [ ... ] ]
    
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
        | IN ROLE _role_name_ [, ...]
        | IN GROUP _role_name_ [, ...]
        | ROLE _role_name_ [, ...]
        | ADMIN _role_name_ [, ...]
        | USER _role_name_ [, ...]
        | SYSID _uid_
    

## Description

`CREATE ROLE` adds a new role to a PostgreSQL database cluster. A role is an
entity that can own database objects and have database privileges; a role can
be considered a “user”, a “group”, or both depending on how it is used. Refer
to [Chapter 22](user-manag.html "Chapter 22. Database Roles") and [Chapter
21](client-authentication.html "Chapter 21. Client Authentication") for
information about managing users and authentication. You must have
`CREATEROLE` privilege or be a database superuser to use this command.

Note that roles are defined at the database cluster level, and so are valid in
all databases in the cluster.

During role creation it is possible to immediately assign the newly created
role to be a member of an existing role, and also assign existing roles to be
members of the newly created role. The rules for which initial role membership
options are enabled are described below in the `IN ROLE`, `ROLE`, and `ADMIN`
clauses. The [GRANT](sql-grant.html "GRANT") command has fine-grained option
control during membership creation, and the ability to modify these options
after the new role is created.

## Parameters

_`name`_

    

The name of the new role.

`SUPERUSER`  
`NOSUPERUSER`

    

These clauses determine whether the new role is a “superuser”, who can
override all access restrictions within the database. Superuser status is
dangerous and should be used only when really needed. You must yourself be a
superuser to create a new superuser. If not specified, `NOSUPERUSER` is the
default.

`CREATEDB`  
`NOCREATEDB`

    

These clauses define a role's ability to create databases. If `CREATEDB` is
specified, the role being defined will be allowed to create new databases.
Specifying `NOCREATEDB` will deny a role the ability to create databases. If
not specified, `NOCREATEDB` is the default. Only superuser roles or roles with
`CREATEDB` can specify `CREATEDB`.

`CREATEROLE`  
`NOCREATEROLE`

    

These clauses determine whether a role will be permitted to create, alter,
drop, comment on, and change the security label for other roles. See [role
creation](role-attributes.html#ROLE-CREATION) for more details about what
capabilities are conferred by this privilege. If not specified, `NOCREATEROLE`
is the default.

`INHERIT`  
`NOINHERIT`

    

This affects the membership inheritance status when this role is added as a
member of another role, both in this and future commands. Specifically, it
controls the inheritance status of memberships added with this command using
the `IN ROLE` clause, and in later commands using the `ROLE` clause. It is
also used as the default inheritance status when adding this role as a member
using the `GRANT` command. If not specified, `INHERIT` is the default.

In PostgreSQL versions before 16, inheritance was a role-level attribute that
controlled all runtime membership checks for that role.

`LOGIN`  
`NOLOGIN`

    

These clauses determine whether a role is allowed to log in; that is, whether
the role can be given as the initial session authorization name during client
connection. A role having the `LOGIN` attribute can be thought of as a user.
Roles without this attribute are useful for managing database privileges, but
are not users in the usual sense of the word. If not specified, `NOLOGIN` is
the default, except when `CREATE ROLE` is invoked through its alternative
spelling [`CREATE USER`](sql-createuser.html "CREATE USER").

`REPLICATION`  
`NOREPLICATION`

    

These clauses determine whether a role is a replication role. A role must have
this attribute (or be a superuser) in order to be able to connect to the
server in replication mode (physical or logical replication) and in order to
be able to create or drop replication slots. A role having the `REPLICATION`
attribute is a very highly privileged role, and should only be used on roles
actually used for replication. If not specified, `NOREPLICATION` is the
default. Only superuser roles or roles with `REPLICATION` can specify
`REPLICATION`.

`BYPASSRLS`  
`NOBYPASSRLS`

    

These clauses determine whether a role bypasses every row-level security (RLS)
policy. `NOBYPASSRLS` is the default. Only superuser roles or roles with
`BYPASSRLS` can specify `BYPASSRLS`.

Note that pg_dump will set `row_security` to `OFF` by default, to ensure all
contents of a table are dumped out. If the user running pg_dump does not have
appropriate permissions, an error will be returned. However, superusers and
the owner of the table being dumped always bypass RLS.

`CONNECTION LIMIT` _`connlimit`_

    

If role can log in, this specifies how many concurrent connections the role
can make. -1 (the default) means no limit. Note that only normal connections
are counted towards this limit. Neither prepared transactions nor background
worker connections are counted towards this limit.

[ `ENCRYPTED` ] `PASSWORD` '_`password`_ '  
`PASSWORD NULL`

    

Sets the role's password. (A password is only of use for roles having the
`LOGIN` attribute, but you can nonetheless define one for roles without it.)
If you do not plan to use password authentication you can omit this option. If
no password is specified, the password will be set to null and password
authentication will always fail for that user. A null password can optionally
be written explicitly as `PASSWORD NULL`.

### Note

Specifying an empty string will also set the password to null, but that was
not the case before PostgreSQL version 10. In earlier versions, an empty
string could be used, or not, depending on the authentication method and the
exact version, and libpq would refuse to use it in any case. To avoid the
ambiguity, specifying an empty string should be avoided.

The password is always stored encrypted in the system catalogs. The
`ENCRYPTED` keyword has no effect, but is accepted for backwards
compatibility. The method of encryption is determined by the configuration
parameter [password_encryption](runtime-config-connection.html#GUC-PASSWORD-
ENCRYPTION). If the presented password string is already in MD5-encrypted or
SCRAM-encrypted format, then it is stored as-is regardless of
`password_encryption` (since the system cannot decrypt the specified encrypted
password string, to encrypt it in a different format). This allows reloading
of encrypted passwords during dump/restore.

`VALID UNTIL` '_`timestamp`_ '

    

The `VALID UNTIL` clause sets a date and time after which the role's password
is no longer valid. If this clause is omitted the password will be valid for
all time.

`IN ROLE` _`role_name`_

    

The `IN ROLE` clause causes the new role to be automatically added as a member
of the specified existing roles. The new membership will have the `SET` option
enabled and the `ADMIN` option disabled. The `INHERIT` option will be enabled
unless the `NOINHERIT` option is specified.

`IN GROUP` _`role_name`_

    

`IN GROUP` is an obsolete spelling of `IN ROLE`.

`ROLE` _`role_name`_

    

The `ROLE` clause causes one or more specified existing roles to be
automatically added as members, with the `SET` option enabled. This in effect
makes the new role a “group”. Roles named in this clause with the role-level
`INHERIT` attribute will have the `INHERIT` option enabled in the new
membership. New memberships will have the `ADMIN` option disabled.

`ADMIN` _`role_name`_

    

The `ADMIN` clause has the same effect as `ROLE`, but the named roles are
added as members of the new role with `ADMIN` enabled, giving them the right
to grant membership in the new role to others.

`USER` _`role_name`_

    

The `USER` clause is an obsolete spelling of the `ROLE` clause.

`SYSID` _`uid`_

    

The `SYSID` clause is ignored, but is accepted for backwards compatibility.

## Notes

Use [`ALTER ROLE`](sql-alterrole.html "ALTER ROLE") to change the attributes
of a role, and [`DROP ROLE`](sql-droprole.html "DROP ROLE") to remove a role.
All the attributes specified by `CREATE ROLE` can be modified by later `ALTER
ROLE` commands.

The preferred way to add and remove members of roles that are being used as
groups is to use [`GRANT`](sql-grant.html "GRANT") and [`REVOKE`](sql-
revoke.html "REVOKE").

The `VALID UNTIL` clause defines an expiration time for a password only, not
for the role per se. In particular, the expiration time is not enforced when
logging in using a non-password-based authentication method.

The role attributes defined here are non-inheritable, i.e., being a member of
a role with, e.g., `CREATEDB` will not allow the member to create new
databases even if the membership grant has the `INHERIT` option. Of course, if
the membership grant has the `SET` option the member role would be able to
[`SET ROLE`](sql-set-role.html "SET ROLE") to the createdb role and then
create a new database.

The membership grants created by the `IN ROLE`, `ROLE`, and `ADMIN` clauses
have the role executing this command as the grantor.

The `INHERIT` attribute is the default for reasons of backwards compatibility:
in prior releases of PostgreSQL, users always had access to all privileges of
groups they were members of. However, `NOINHERIT` provides a closer match to
the semantics specified in the SQL standard.

PostgreSQL includes a program [createuser](app-createuser.html "createuser")
that has the same functionality as `CREATE ROLE` (in fact, it calls this
command) but can be run from the command shell.

The `CONNECTION LIMIT` option is only enforced approximately; if two new
sessions start at about the same time when just one connection “slot” remains
for the role, it is possible that both will fail. Also, the limit is never
enforced for superusers.

Caution must be exercised when specifying an unencrypted password with this
command. The password will be transmitted to the server in cleartext, and it
might also be logged in the client's command history or the server log. The
command [createuser](app-createuser.html "createuser"), however, transmits the
password encrypted. Also, [psql](app-psql.html "psql") contains a command
`\password` that can be used to safely change the password later.

## Examples

Create a role that can log in, but don't give it a password:

    
    
    CREATE ROLE jonathan LOGIN;
    

Create a role with a password:

    
    
    CREATE USER davide WITH PASSWORD 'jw8s0F4';
    

(`CREATE USER` is the same as `CREATE ROLE` except that it implies `LOGIN`.)

Create a role with a password that is valid until the end of 2004. After one
second has ticked in 2005, the password is no longer valid.

    
    
    CREATE ROLE miriam WITH LOGIN PASSWORD 'jw8s0F4' VALID UNTIL '2005-01-01';
    

Create a role that can create databases and manage roles:

    
    
    CREATE ROLE admin WITH CREATEDB CREATEROLE;
    

## Compatibility

The `CREATE ROLE` statement is in the SQL standard, but the standard only
requires the syntax

    
    
    CREATE ROLE _name_ [ WITH ADMIN _role_name_ ]
    

Multiple initial administrators, and all the other options of `CREATE ROLE`,
are PostgreSQL extensions.

The SQL standard defines the concepts of users and roles, but it regards them
as distinct concepts and leaves all commands defining users to be specified by
each database implementation. In PostgreSQL we have chosen to unify users and
roles into a single kind of entity. Roles therefore have many more optional
attributes than they do in the standard.

The behavior specified by the SQL standard is most closely approximated
creating SQL-standard users as PostgreSQL roles with the `NOINHERIT` option,
and SQL-standard roles as PostgreSQL roles with the `INHERIT` option.

## See Also

[SET ROLE](sql-set-role.html "SET ROLE"), [ALTER ROLE](sql-alterrole.html
"ALTER ROLE"), [DROP ROLE](sql-droprole.html "DROP ROLE"), [GRANT](sql-
grant.html "GRANT"), [REVOKE](sql-revoke.html "REVOKE"), [createuser](app-
createuser.html "createuser"), [createrole_self_grant](runtime-config-
client.html#GUC-CREATEROLE-SELF-GRANT)

* * *

[Prev](sql-createpublication.html "CREATE PUBLICATION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createrule.html "CREATE RULE")  
---|---|---  
CREATE PUBLICATION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE RULE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createrole.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

