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

Supported Versions: [Current](/docs/current/predefined-roles.html "PostgreSQL
17 - 22.5. Predefined Roles") ([17](/docs/17/predefined-roles.html "PostgreSQL
17 - 22.5. Predefined Roles")) / [16](/docs/16/predefined-roles.html
"PostgreSQL 16 - 22.5. Predefined Roles") / [15](/docs/15/predefined-
roles.html "PostgreSQL 15 - 22.5. Predefined Roles") /
[14](/docs/14/predefined-roles.html "PostgreSQL 14 - 22.5. Predefined Roles")

Development Versions: [18](/docs/18/predefined-roles.html "PostgreSQL 18 -
22.5. Predefined Roles") / [devel](/docs/devel/predefined-roles.html
"PostgreSQL devel - 22.5. Predefined Roles")

__

22.5. Predefined Roles  
---  
[Prev](role-removal.html "22.4. Dropping Roles")  | [Up](user-manag.html "Chapter 22. Database Roles") | Chapter 22. Database Roles | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](perm-functions.html "22.6. Function Security")  
  
* * *

## 22.5. Predefined Roles #

PostgreSQL provides a set of predefined roles that provide access to certain,
commonly needed, privileged capabilities and information. Administrators
(including roles that have the `CREATEROLE` privilege) can `GRANT` these roles
to users and/or other roles in their environment, providing those users with
access to the specified capabilities and information.

The predefined roles are described in [Table 22.1](predefined-
roles.html#PREDEFINED-ROLES-TABLE "Table 22.1. Predefined Roles"). Note that
the specific permissions for each of the roles may change in the future as
additional capabilities are added. Administrators should monitor the release
notes for changes.

**Table  22.1. Predefined Roles**

Role | Allowed Access  
---|---  
pg_read_all_data | Read all data (tables, views, sequences), as if having `SELECT` rights on those objects, and USAGE rights on all schemas, even without having it explicitly. This role does not have the role attribute `BYPASSRLS` set. If RLS is being used, an administrator may wish to set `BYPASSRLS` on roles which this role is GRANTed to.  
pg_write_all_data | Write all data (tables, views, sequences), as if having `INSERT`, `UPDATE`, and `DELETE` rights on those objects, and USAGE rights on all schemas, even without having it explicitly. This role does not have the role attribute `BYPASSRLS` set. If RLS is being used, an administrator may wish to set `BYPASSRLS` on roles which this role is GRANTed to.  
pg_read_all_settings | Read all configuration variables, even those normally visible only to superusers.  
pg_read_all_stats | Read all pg_stat_* views and use various statistics related extensions, even those normally visible only to superusers.  
pg_stat_scan_tables | Execute monitoring functions that may take `ACCESS SHARE` locks on tables, potentially for a long time.  
pg_monitor | Read/execute various monitoring views and functions. This role is a member of `pg_read_all_settings`, `pg_read_all_stats` and `pg_stat_scan_tables`.  
pg_database_owner | None. Membership consists, implicitly, of the current database owner.  
pg_signal_backend | Signal another backend to cancel a query or terminate its session.  
pg_read_server_files | Allow reading files from any location the database can access on the server with COPY and other file-access functions.  
pg_write_server_files | Allow writing to files in any location the database can access on the server with COPY and other file-access functions.  
pg_execute_server_program | Allow executing programs on the database server as the user the database runs as with COPY and other functions which allow executing a server-side program.  
pg_checkpoint | Allow executing the [`CHECKPOINT`](sql-checkpoint.html "CHECKPOINT") command.  
pg_use_reserved_connections | Allow use of connection slots reserved via [reserved_connections](runtime-config-connection.html#GUC-RESERVED-CONNECTIONS).  
pg_create_subscription | Allow users with `CREATE` permission on the database to issue [`CREATE SUBSCRIPTION`](sql-createsubscription.html "CREATE SUBSCRIPTION").  
  
  

The `pg_monitor`, `pg_read_all_settings`, `pg_read_all_stats` and
`pg_stat_scan_tables` roles are intended to allow administrators to easily
configure a role for the purpose of monitoring the database server. They grant
a set of common privileges allowing the role to read various useful
configuration settings, statistics and other system information normally
restricted to superusers.

The `pg_database_owner` role has one implicit, situation-dependent member,
namely the owner of the current database. Like any role, it can own objects or
receive grants of access privileges. Consequently, once `pg_database_owner`
has rights within a template database, each owner of a database instantiated
from that template will exercise those rights. `pg_database_owner` cannot be a
member of any role, and it cannot have non-implicit members. Initially, this
role owns the `public` schema, so each database owner governs local use of the
schema.

The `pg_signal_backend` role is intended to allow administrators to enable
trusted, but non-superuser, roles to send signals to other backends. Currently
this role enables sending of signals for canceling a query on another backend
or terminating its session. A user granted this role cannot however send
signals to a backend owned by a superuser. See [Section 9.27.2](functions-
admin.html#FUNCTIONS-ADMIN-SIGNAL "9.27.2. Server Signaling Functions").

The `pg_read_server_files`, `pg_write_server_files` and
`pg_execute_server_program` roles are intended to allow administrators to have
trusted, but non-superuser, roles which are able to access files and run
programs on the database server as the user the database runs as. As these
roles are able to access any file on the server file system, they bypass all
database-level permission checks when accessing files directly and they could
be used to gain superuser-level access, therefore great care should be taken
when granting these roles to users.

Care should be taken when granting these roles to ensure they are only used
where needed and with the understanding that these roles grant access to
privileged information.

Administrators can grant access to these roles to users using the
[`GRANT`](sql-grant.html "GRANT") command, for example:

    
    
    GRANT pg_signal_backend TO admin_user;
    

* * *

[Prev](role-removal.html "22.4. Dropping Roles")  | [Up](user-manag.html "Chapter 22. Database Roles") |  [Next](perm-functions.html "22.6. Function Security")  
---|---|---  
22.4. Dropping Roles  | [Home](index.html "PostgreSQL 16.9 Documentation") |  22.6. Function Security  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/predefined-roles.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

