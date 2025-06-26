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

Supported Versions: [Current](/docs/current/app-createuser.html "PostgreSQL 17
- createuser") ([17](/docs/17/app-createuser.html "PostgreSQL 17 -
createuser")) / [16](/docs/16/app-createuser.html "PostgreSQL 16 -
createuser") / [15](/docs/15/app-createuser.html "PostgreSQL 15 - createuser")
/ [14](/docs/14/app-createuser.html "PostgreSQL 14 - createuser") /
[13](/docs/13/app-createuser.html "PostgreSQL 13 - createuser")

Development Versions: [18](/docs/18/app-createuser.html "PostgreSQL 18 -
createuser") / [devel](/docs/devel/app-createuser.html "PostgreSQL devel -
createuser")

Unsupported versions: [12](/docs/12/app-createuser.html "PostgreSQL 12 -
createuser") / [11](/docs/11/app-createuser.html "PostgreSQL 11 - createuser")
/ [10](/docs/10/app-createuser.html "PostgreSQL 10 - createuser") /
[9.6](/docs/9.6/app-createuser.html "PostgreSQL 9.6 - createuser") /
[9.5](/docs/9.5/app-createuser.html "PostgreSQL 9.5 - createuser") /
[9.4](/docs/9.4/app-createuser.html "PostgreSQL 9.4 - createuser") /
[9.3](/docs/9.3/app-createuser.html "PostgreSQL 9.3 - createuser") /
[9.2](/docs/9.2/app-createuser.html "PostgreSQL 9.2 - createuser") /
[9.1](/docs/9.1/app-createuser.html "PostgreSQL 9.1 - createuser") /
[9.0](/docs/9.0/app-createuser.html "PostgreSQL 9.0 - createuser") /
[8.4](/docs/8.4/app-createuser.html "PostgreSQL 8.4 - createuser") /
[8.3](/docs/8.3/app-createuser.html "PostgreSQL 8.3 - createuser") /
[8.2](/docs/8.2/app-createuser.html "PostgreSQL 8.2 - createuser") /
[8.1](/docs/8.1/app-createuser.html "PostgreSQL 8.1 - createuser") /
[8.0](/docs/8.0/app-createuser.html "PostgreSQL 8.0 - createuser") /
[7.4](/docs/7.4/app-createuser.html "PostgreSQL 7.4 - createuser") /
[7.3](/docs/7.3/app-createuser.html "PostgreSQL 7.3 - createuser") /
[7.2](/docs/7.2/app-createuser.html "PostgreSQL 7.2 - createuser") /
[7.1](/docs/7.1/app-createuser.html "PostgreSQL 7.1 - createuser")

__

createuser  
---  
[Prev](app-createdb.html "createdb")  | [Up](reference-client.html "PostgreSQL Client Applications") | PostgreSQL Client Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](app-dropdb.html "dropdb")  
  
* * *

## createuser

createuser — define a new PostgreSQL user account

## Synopsis

`createuser` [_`connection-option`_...] [_`option`_...] [_`username`_]

## Description

createuser creates a new PostgreSQL user (or more precisely, a role). Only
superusers and users with `CREATEROLE` privilege can create new users, so
createuser must be invoked by someone who can connect as a superuser or a user
with `CREATEROLE` privilege.

If you wish to create a role with the `SUPERUSER`, `REPLICATION`, or
`BYPASSRLS` privilege, you must connect as a superuser, not merely with
`CREATEROLE` privilege. Being a superuser implies the ability to bypass all
access permission checks within the database, so superuser access should not
be granted lightly. `CREATEROLE` also conveys [very extensive
privileges](role-attributes.html#ROLE-CREATION).

createuser is a wrapper around the SQL command [`CREATE ROLE`](sql-
createrole.html "CREATE ROLE"). There is no effective difference between
creating users via this utility and via other methods for accessing the
server.

## Options

createuser accepts the following command-line arguments:

_`username`_

    

Specifies the name of the PostgreSQL user to be created. This name must be
different from all existing roles in this PostgreSQL installation.

`-a _`role`_`  
`--with-admin=_`role`_`

    

Specifies an existing role that will be automatically added as a member of the
new role with admin option, giving it the right to grant membership in the new
role to others. Multiple existing roles can be specified by writing multiple
`-a` switches.

`-c _`number`_`  
`--connection-limit=_`number`_`

    

Set a maximum number of connections for the new user. The default is to set no
limit.

`-d`  
`--createdb`

    

The new user will be allowed to create databases.

`-D`  
`--no-createdb`

    

The new user will not be allowed to create databases. This is the default.

`-e`  
`--echo`

    

Echo the commands that createuser generates and sends to the server.

`-E`  
`--encrypted`

    

This option is obsolete but still accepted for backward compatibility.

`-g _`role`_`  
`--member-of=_`role`_`  
`--role=_`role`_` (deprecated)

    

Specifies the new role should be automatically added as a member of the
specified existing role. Multiple existing roles can be specified by writing
multiple `-g` switches.

`-i`  
`--inherit`

    

The new role will automatically inherit privileges of roles it is a member of.
This is the default.

`-I`  
`--no-inherit`

    

The new role will not automatically inherit privileges of roles it is a member
of.

`--interactive`

    

Prompt for the user name if none is specified on the command line, and also
prompt for whichever of the options `-d`/`-D`, `-r`/`-R`, `-s`/`-S` is not
specified on the command line. (This was the default behavior up to PostgreSQL
9.1.)

`-l`  
`--login`

    

The new user will be allowed to log in (that is, the user name can be used as
the initial session user identifier). This is the default.

`-L`  
`--no-login`

    

The new user will not be allowed to log in. (A role without login privilege is
still useful as a means of managing database permissions.)

`-m _`role`_`  
`--with-member=_`role`_`

    

Specifies an existing role that will be automatically added as a member of the
new role. Multiple existing roles can be specified by writing multiple `-m`
switches.

`-P`  
`--pwprompt`

    

If given, createuser will issue a prompt for the password of the new user.
This is not necessary if you do not plan on using password authentication.

`-r`  
`--createrole`

    

The new user will be allowed to create, alter, drop, comment on, change the
security label for other roles; that is, this user will have `CREATEROLE`
privilege. See [role creation](role-attributes.html#ROLE-CREATION) for more
details about what capabilities are conferred by this privilege.

`-R`  
`--no-createrole`

    

The new user will not be allowed to create new roles. This is the default.

`-s`  
`--superuser`

    

The new user will be a superuser.

`-S`  
`--no-superuser`

    

The new user will not be a superuser. This is the default.

`-v _`timestamp`_`  
`--valid-until=_`timestamp`_`

    

Set a date and time after which the role's password is no longer valid. The
default is to set no password expiry date.

`-V`  
`--version`

    

Print the createuser version and exit.

`--bypassrls`

    

The new user will bypass every row-level security (RLS) policy.

`--no-bypassrls`

    

The new user will not bypass row-level security (RLS) policies. This is the
default.

`--replication`

    

The new user will have the `REPLICATION` privilege, which is described more
fully in the documentation for [CREATE ROLE](sql-createrole.html "CREATE
ROLE").

`--no-replication`

    

The new user will not have the `REPLICATION` privilege, which is described
more fully in the documentation for [CREATE ROLE](sql-createrole.html "CREATE
ROLE"). This is the default.

`-?`  
`--help`

    

Show help about createuser command line arguments, and exit.

createuser also accepts the following command-line arguments for connection
parameters:

`-h _`host`_`  
`--host=_`host`_`

    

Specifies the host name of the machine on which the server is running. If the
value begins with a slash, it is used as the directory for the Unix domain
socket.

`-p _`port`_`  
`--port=_`port`_`

    

Specifies the TCP port or local Unix domain socket file extension on which the
server is listening for connections.

`-U _`username`_`  
`--username=_`username`_`

    

User name to connect as (not the user name to create).

`-w`  
`--no-password`

    

Never issue a password prompt. If the server requires password authentication
and a password is not available by other means such as a `.pgpass` file, the
connection attempt will fail. This option can be useful in batch jobs and
scripts where no user is present to enter a password.

`-W`  
`--password`

    

Force createuser to prompt for a password (for connecting to the server, not
for the password of the new user).

This option is never essential, since createuser will automatically prompt for
a password if the server demands password authentication. However, createuser
will waste a connection attempt finding out that the server wants a password.
In some cases it is worth typing `-W` to avoid the extra connection attempt.

## Environment

`PGHOST`  
`PGPORT`  
`PGUSER`

    

Default connection parameters

`PG_COLOR`

    

Specifies whether to use color in diagnostic messages. Possible values are
`always`, `auto` and `never`.

This utility, like most other PostgreSQL utilities, also uses the environment
variables supported by libpq (see [Section 34.15](libpq-envars.html
"34.15. Environment Variables")).

## Diagnostics

In case of difficulty, see [CREATE ROLE](sql-createrole.html "CREATE ROLE")
and [psql](app-psql.html "psql") for discussions of potential problems and
error messages. The database server must be running at the targeted host.
Also, any default connection settings and environment variables used by the
libpq front-end library will apply.

## Examples

To create a user `joe` on the default database server:

    
    
    $ **createuser joe**
    

To create a user `joe` on the default database server with prompting for some
additional attributes:

    
    
    $ **createuser --interactive joe**
    Shall the new role be a superuser? (y/n) **n**
    Shall the new role be allowed to create databases? (y/n) **n**
    Shall the new role be allowed to create more new roles? (y/n) **n**
    

To create the same user `joe` using the server on host `eden`, port 5000, with
attributes explicitly specified, taking a look at the underlying command:

    
    
    $ **createuser -h eden -p 5000 -S -D -R -e joe**
    CREATE ROLE joe NOSUPERUSER NOCREATEDB NOCREATEROLE INHERIT LOGIN;
    

To create the user `joe` as a superuser, and assign a password immediately:

    
    
    $ **createuser -P -s -e joe**
    Enter password for new role: **xyzzy**
    Enter it again: **xyzzy**
    CREATE ROLE joe PASSWORD 'md5b5f5ba1a423792b526f799ae4eb3d59e' SUPERUSER CREATEDB CREATEROLE INHERIT LOGIN;
    

In the above example, the new password isn't actually echoed when typed, but
we show what was typed for clarity. As you see, the password is encrypted
before it is sent to the client.

## See Also

[dropuser](app-dropuser.html "dropuser"), [CREATE ROLE](sql-createrole.html
"CREATE ROLE"), [createrole_self_grant](runtime-config-client.html#GUC-
CREATEROLE-SELF-GRANT)

* * *

[Prev](app-createdb.html "createdb")  | [Up](reference-client.html "PostgreSQL Client Applications") |  [Next](app-dropdb.html "dropdb")  
---|---|---  
createdb  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dropdb  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/app-createuser.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

