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

Supported Versions: [Current](/docs/current/database-roles.html "PostgreSQL 17
- 22.1. Database Roles") ([17](/docs/17/database-roles.html "PostgreSQL 17 -
22.1. Database Roles")) / [16](/docs/16/database-roles.html "PostgreSQL 16 -
22.1. Database Roles") / [15](/docs/15/database-roles.html "PostgreSQL 15 -
22.1. Database Roles") / [14](/docs/14/database-roles.html "PostgreSQL 14 -
22.1. Database Roles") / [13](/docs/13/database-roles.html "PostgreSQL 13 -
22.1. Database Roles")

Development Versions: [18](/docs/18/database-roles.html "PostgreSQL 18 -
22.1. Database Roles") / [devel](/docs/devel/database-roles.html "PostgreSQL
devel - 22.1. Database Roles")

Unsupported versions: [12](/docs/12/database-roles.html "PostgreSQL 12 -
22.1. Database Roles") / [11](/docs/11/database-roles.html "PostgreSQL 11 -
22.1. Database Roles") / [10](/docs/10/database-roles.html "PostgreSQL 10 -
22.1. Database Roles") / [9.6](/docs/9.6/database-roles.html "PostgreSQL 9.6 -
22.1. Database Roles") / [9.5](/docs/9.5/database-roles.html "PostgreSQL 9.5 -
22.1. Database Roles") / [9.4](/docs/9.4/database-roles.html "PostgreSQL 9.4 -
22.1. Database Roles") / [9.3](/docs/9.3/database-roles.html "PostgreSQL 9.3 -
22.1. Database Roles") / [9.2](/docs/9.2/database-roles.html "PostgreSQL 9.2 -
22.1. Database Roles") / [9.1](/docs/9.1/database-roles.html "PostgreSQL 9.1 -
22.1. Database Roles") / [9.0](/docs/9.0/database-roles.html "PostgreSQL 9.0 -
22.1. Database Roles") / [8.4](/docs/8.4/database-roles.html "PostgreSQL 8.4 -
22.1. Database Roles") / [8.3](/docs/8.3/database-roles.html "PostgreSQL 8.3 -
22.1. Database Roles") / [8.2](/docs/8.2/database-roles.html "PostgreSQL 8.2 -
22.1. Database Roles")

__

22.1. Database Roles  
---  
[Prev](user-manag.html "Chapter 22. Database Roles")  | [Up](user-manag.html "Chapter 22. Database Roles") | Chapter 22. Database Roles | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](role-attributes.html "22.2. Role Attributes")  
  
* * *

## 22.1. Database Roles #

Database roles are conceptually completely separate from operating system
users. In practice it might be convenient to maintain a correspondence, but
this is not required. Database roles are global across a database cluster
installation (and not per individual database). To create a role use the
[`CREATE ROLE`](sql-createrole.html "CREATE ROLE") SQL command:

    
    
    CREATE ROLE _name_ ;
    

_`name`_ follows the rules for SQL identifiers: either unadorned without
special characters, or double-quoted. (In practice, you will usually want to
add additional options, such as `LOGIN`, to the command. More details appear
below.) To remove an existing role, use the analogous [`DROP ROLE`](sql-
droprole.html "DROP ROLE") command:

    
    
    DROP ROLE _name_ ;
    

For convenience, the programs [createuser](app-createuser.html "createuser")
and [dropuser](app-dropuser.html "dropuser") are provided as wrappers around
these SQL commands that can be called from the shell command line:

    
    
    createuser _name_
    dropuser _name_
    

To determine the set of existing roles, examine the `pg_roles` system catalog,
for example:

    
    
    SELECT rolname FROM pg_roles;
    

or to see just those capable of logging in:

    
    
    SELECT rolname FROM pg_roles WHERE rolcanlogin;
    

The [psql](app-psql.html "psql") program's `\du` meta-command is also useful
for listing the existing roles.

In order to bootstrap the database system, a freshly initialized system always
contains one predefined login-capable role. This role is always a “superuser”,
and it will have the same name as the operating system user that initialized
the database cluster with `initdb` unless a different name is specified. This
role is often named `postgres`. In order to create more roles you first have
to connect as this initial role.

Every connection to the database server is made using the name of some
particular role, and this role determines the initial access privileges for
commands issued in that connection. The role name to use for a particular
database connection is indicated by the client that is initiating the
connection request in an application-specific fashion. For example, the `psql`
program uses the `-U` command line option to indicate the role to connect as.
Many applications assume the name of the current operating system user by
default (including `createuser` and `psql`). Therefore it is often convenient
to maintain a naming correspondence between roles and operating system users.

The set of database roles a given client connection can connect as is
determined by the client authentication setup, as explained in [Chapter
21](client-authentication.html "Chapter 21. Client Authentication"). (Thus, a
client is not limited to connect as the role matching its operating system
user, just as a person's login name need not match his or her real name.)
Since the role identity determines the set of privileges available to a
connected client, it is important to carefully configure privileges when
setting up a multiuser environment.

* * *

[Prev](user-manag.html "Chapter 22. Database Roles")  | [Up](user-manag.html "Chapter 22. Database Roles") |  [Next](role-attributes.html "22.2. Role Attributes")  
---|---|---  
Chapter 22. Database Roles  | [Home](index.html "PostgreSQL 16.9 Documentation") |  22.2. Role Attributes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/database-roles.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

