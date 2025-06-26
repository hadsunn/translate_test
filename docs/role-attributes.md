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

Supported Versions: [Current](/docs/current/role-attributes.html "PostgreSQL
17 - 22.2. Role Attributes") ([17](/docs/17/role-attributes.html "PostgreSQL
17 - 22.2. Role Attributes")) / [16](/docs/16/role-attributes.html "PostgreSQL
16 - 22.2. Role Attributes") / [15](/docs/15/role-attributes.html "PostgreSQL
15 - 22.2. Role Attributes") / [14](/docs/14/role-attributes.html "PostgreSQL
14 - 22.2. Role Attributes") / [13](/docs/13/role-attributes.html "PostgreSQL
13 - 22.2. Role Attributes")

Development Versions: [18](/docs/18/role-attributes.html "PostgreSQL 18 -
22.2. Role Attributes") / [devel](/docs/devel/role-attributes.html "PostgreSQL
devel - 22.2. Role Attributes")

Unsupported versions: [12](/docs/12/role-attributes.html "PostgreSQL 12 -
22.2. Role Attributes") / [11](/docs/11/role-attributes.html "PostgreSQL 11 -
22.2. Role Attributes") / [10](/docs/10/role-attributes.html "PostgreSQL 10 -
22.2. Role Attributes") / [9.6](/docs/9.6/role-attributes.html "PostgreSQL 9.6
- 22.2. Role Attributes") / [9.5](/docs/9.5/role-attributes.html "PostgreSQL
9.5 - 22.2. Role Attributes") / [9.4](/docs/9.4/role-attributes.html
"PostgreSQL 9.4 - 22.2. Role Attributes") / [9.3](/docs/9.3/role-
attributes.html "PostgreSQL 9.3 - 22.2. Role Attributes") /
[9.2](/docs/9.2/role-attributes.html "PostgreSQL 9.2 - 22.2. Role Attributes")
/ [9.1](/docs/9.1/role-attributes.html "PostgreSQL 9.1 - 22.2. Role
Attributes") / [9.0](/docs/9.0/role-attributes.html "PostgreSQL 9.0 -
22.2. Role Attributes") / [8.4](/docs/8.4/role-attributes.html "PostgreSQL 8.4
- 22.2. Role Attributes") / [8.3](/docs/8.3/role-attributes.html "PostgreSQL
8.3 - 22.2. Role Attributes") / [8.2](/docs/8.2/role-attributes.html
"PostgreSQL 8.2 - 22.2. Role Attributes") / [8.1](/docs/8.1/role-
attributes.html "PostgreSQL 8.1 - 22.2. Role Attributes")

__

22.2. Role Attributes  
---  
[Prev](database-roles.html "22.1. Database Roles")  | [Up](user-manag.html "Chapter 22. Database Roles") | Chapter 22. Database Roles | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](role-membership.html "22.3. Role Membership")  
  
* * *

## 22.2. Role Attributes #

A database role can have a number of attributes that define its privileges and
interact with the client authentication system.

login privilege

    

Only roles that have the `LOGIN` attribute can be used as the initial role
name for a database connection. A role with the `LOGIN` attribute can be
considered the same as a “database user”. To create a role with login
privilege, use either:

    
    
    CREATE ROLE _name_ LOGIN;
    CREATE USER _name_ ;
    

(`CREATE USER` is equivalent to `CREATE ROLE` except that `CREATE USER`
includes `LOGIN` by default, while `CREATE ROLE` does not.)

superuser status

    

A database superuser bypasses all permission checks, except the right to log
in. This is a dangerous privilege and should not be used carelessly; it is
best to do most of your work as a role that is not a superuser. To create a
new database superuser, use `CREATE ROLE _`name`_ SUPERUSER`. You must do this
as a role that is already a superuser.

database creation

    

A role must be explicitly given permission to create databases (except for
superusers, since those bypass all permission checks). To create such a role,
use `CREATE ROLE _`name`_ CREATEDB`.

role creation

    

A role must be explicitly given permission to create more roles (except for
superusers, since those bypass all permission checks). To create such a role,
use `CREATE ROLE _`name`_ CREATEROLE`. A role with `CREATEROLE` privilege can
alter and drop roles which have been granted to the `CREATEROLE` user with the
`ADMIN` option. Such a grant occurs automatically when a `CREATEROLE` user
that is not a superuser creates a new role, so that by default, a `CREATEROLE`
user can alter and drop the roles which they have created. Altering a role
includes most changes that can be made using `ALTER ROLE`, including, for
example, changing passwords. It also includes modifications to a role that can
be made using the `COMMENT` and `SECURITY LABEL` commands.

However, `CREATEROLE` does not convey the ability to create `SUPERUSER` roles,
nor does it convey any power over `SUPERUSER` roles that already exist.
Furthermore, `CREATEROLE` does not convey the power to create `REPLICATION`
users, nor the ability to grant or revoke the `REPLICATION` privilege, nor the
ability to modify the role properties of such users. However, it does allow
`ALTER ROLE ... SET` and `ALTER ROLE ... RENAME` to be used on `REPLICATION`
roles, as well as the use of `COMMENT ON ROLE`, `SECURITY LABEL ON ROLE`, and
`DROP ROLE`. Finally, `CREATEROLE` does not confer the ability to grant or
revoke the `BYPASSRLS` privilege.

initiating replication

    

A role must explicitly be given permission to initiate streaming replication
(except for superusers, since those bypass all permission checks). A role used
for streaming replication must have `LOGIN` permission as well. To create such
a role, use `CREATE ROLE _`name`_ REPLICATION LOGIN`.

password

    

A password is only significant if the client authentication method requires
the user to supply a password when connecting to the database. The `password`
and `md5` authentication methods make use of passwords. Database passwords are
separate from operating system passwords. Specify a password upon role
creation with `CREATE ROLE _`name`_ PASSWORD '_`string`_ '`.

inheritance of privileges

    

A role inherits the privileges of roles it is a member of, by default.
However, to create a role which does not inherit privileges by default, use
`CREATE ROLE _`name`_ NOINHERIT`. Alternatively, inheritance can be overridden
for individual grants by using `WITH INHERIT TRUE` or `WITH INHERIT FALSE`.

bypassing row-level security

    

A role must be explicitly given permission to bypass every row-level security
(RLS) policy (except for superusers, since those bypass all permission
checks). To create such a role, use `CREATE ROLE _`name`_ BYPASSRLS` as a
superuser.

connection limit

    

Connection limit can specify how many concurrent connections a role can make.
-1 (the default) means no limit. Specify connection limit upon role creation
with `CREATE ROLE _`name`_ CONNECTION LIMIT '_`integer`_ '`.

A role's attributes can be modified after creation with `ALTER ROLE`. See the
reference pages for the [CREATE ROLE](sql-createrole.html "CREATE ROLE") and
[ALTER ROLE](sql-alterrole.html "ALTER ROLE") commands for details.

A role can also have role-specific defaults for many of the run-time
configuration settings described in [Chapter 20](runtime-config.html
"Chapter 20. Server Configuration"). For example, if for some reason you want
to disable index scans (hint: not a good idea) anytime you connect, you can
use:

    
    
    ALTER ROLE myname SET enable_indexscan TO off;
    

This will save the setting (but not set it immediately). In subsequent
connections by this role it will appear as though `SET enable_indexscan TO
off` had been executed just before the session started. You can still alter
this setting during the session; it will only be the default. To remove a
role-specific default setting, use `ALTER ROLE _`rolename`_ RESET
_`varname`_`. Note that role-specific defaults attached to roles without
`LOGIN` privilege are fairly useless, since they will never be invoked.

When a non-superuser creates a role using the `CREATEROLE` privilege, the
created role is automatically granted back to the creating user, just as if
the bootstrap superuser had executed the command `GRANT created_user TO
creating_user WITH ADMIN TRUE, SET FALSE, INHERIT FALSE`. Since a `CREATEROLE`
user can only exercise special privileges with regard to an existing role if
they have `ADMIN OPTION` on it, this grant is just sufficient to allow a
`CREATEROLE` user to administer the roles they created. However, because it is
created with `INHERIT FALSE, SET FALSE`, the `CREATEROLE` user doesn't inherit
the privileges of the created role, nor can it access the privileges of that
role using `SET ROLE`. However, since any user who has `ADMIN OPTION` on a
role can grant membership in that role to any other user, the `CREATEROLE`
user can gain access to the created role by simply granting that role back to
themselves with the `INHERIT` and/or `SET` options. Thus, the fact that
privileges are not inherited by default nor is `SET ROLE` granted by default
is a safeguard against accidents, not a security feature. Also note that,
because this automatic grant is granted by the bootstrap user, it cannot be
removed or changed by the `CREATEROLE` user; however, any superuser could
revoke it, modify it, and/or issue additional such grants to other
`CREATEROLE` users. Whichever `CREATEROLE` users have `ADMIN OPTION` on a role
at any given time can administer it.

* * *

[Prev](database-roles.html "22.1. Database Roles")  | [Up](user-manag.html "Chapter 22. Database Roles") |  [Next](role-membership.html "22.3. Role Membership")  
---|---|---  
22.1. Database Roles  | [Home](index.html "PostgreSQL 16.9 Documentation") |  22.3. Role Membership  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/role-attributes.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

