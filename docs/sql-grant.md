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

Supported Versions: [Current](/docs/current/sql-grant.html "PostgreSQL 17 -
GRANT") ([17](/docs/17/sql-grant.html "PostgreSQL 17 - GRANT")) /
[16](/docs/16/sql-grant.html "PostgreSQL 16 - GRANT") / [15](/docs/15/sql-
grant.html "PostgreSQL 15 - GRANT") / [14](/docs/14/sql-grant.html "PostgreSQL
14 - GRANT") / [13](/docs/13/sql-grant.html "PostgreSQL 13 - GRANT")

Development Versions: [18](/docs/18/sql-grant.html "PostgreSQL 18 - GRANT") /
[devel](/docs/devel/sql-grant.html "PostgreSQL devel - GRANT")

Unsupported versions: [12](/docs/12/sql-grant.html "PostgreSQL 12 - GRANT") /
[11](/docs/11/sql-grant.html "PostgreSQL 11 - GRANT") / [10](/docs/10/sql-
grant.html "PostgreSQL 10 - GRANT") / [9.6](/docs/9.6/sql-grant.html
"PostgreSQL 9.6 - GRANT") / [9.5](/docs/9.5/sql-grant.html "PostgreSQL 9.5 -
GRANT") / [9.4](/docs/9.4/sql-grant.html "PostgreSQL 9.4 - GRANT") /
[9.3](/docs/9.3/sql-grant.html "PostgreSQL 9.3 - GRANT") /
[9.2](/docs/9.2/sql-grant.html "PostgreSQL 9.2 - GRANT") /
[9.1](/docs/9.1/sql-grant.html "PostgreSQL 9.1 - GRANT") /
[9.0](/docs/9.0/sql-grant.html "PostgreSQL 9.0 - GRANT") /
[8.4](/docs/8.4/sql-grant.html "PostgreSQL 8.4 - GRANT") /
[8.3](/docs/8.3/sql-grant.html "PostgreSQL 8.3 - GRANT") /
[8.2](/docs/8.2/sql-grant.html "PostgreSQL 8.2 - GRANT") /
[8.1](/docs/8.1/sql-grant.html "PostgreSQL 8.1 - GRANT") /
[8.0](/docs/8.0/sql-grant.html "PostgreSQL 8.0 - GRANT") /
[7.4](/docs/7.4/sql-grant.html "PostgreSQL 7.4 - GRANT") /
[7.3](/docs/7.3/sql-grant.html "PostgreSQL 7.3 - GRANT") /
[7.2](/docs/7.2/sql-grant.html "PostgreSQL 7.2 - GRANT") /
[7.1](/docs/7.1/sql-grant.html "PostgreSQL 7.1 - GRANT")

__

GRANT  
---  
[Prev](sql-fetch.html "FETCH")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-importforeignschema.html "IMPORT FOREIGN SCHEMA")  
  
* * *

## GRANT

GRANT — define access privileges

## Synopsis

    
    
    GRANT { { SELECT | INSERT | UPDATE | DELETE | TRUNCATE | REFERENCES | TRIGGER }
        [, ...] | ALL [ PRIVILEGES ] }
        ON { [ TABLE ] _table_name_ [, ...]
             | ALL TABLES IN SCHEMA _schema_name_ [, ...] }
        TO _role_specification_ [, ...] [ WITH GRANT OPTION ]
        [ GRANTED BY _role_specification_ ]
    
    GRANT { { SELECT | INSERT | UPDATE | REFERENCES } ( _column_name_ [, ...] )
        [, ...] | ALL [ PRIVILEGES ] ( _column_name_ [, ...] ) }
        ON [ TABLE ] _table_name_ [, ...]
        TO _role_specification_ [, ...] [ WITH GRANT OPTION ]
        [ GRANTED BY _role_specification_ ]
    
    GRANT { { USAGE | SELECT | UPDATE }
        [, ...] | ALL [ PRIVILEGES ] }
        ON { SEQUENCE _sequence_name_ [, ...]
             | ALL SEQUENCES IN SCHEMA _schema_name_ [, ...] }
        TO _role_specification_ [, ...] [ WITH GRANT OPTION ]
        [ GRANTED BY _role_specification_ ]
    
    GRANT { { CREATE | CONNECT | TEMPORARY | TEMP } [, ...] | ALL [ PRIVILEGES ] }
        ON DATABASE _database_name_ [, ...]
        TO _role_specification_ [, ...] [ WITH GRANT OPTION ]
        [ GRANTED BY _role_specification_ ]
    
    GRANT { USAGE | ALL [ PRIVILEGES ] }
        ON DOMAIN _domain_name_ [, ...]
        TO _role_specification_ [, ...] [ WITH GRANT OPTION ]
        [ GRANTED BY _role_specification_ ]
    
    GRANT { USAGE | ALL [ PRIVILEGES ] }
        ON FOREIGN DATA WRAPPER _fdw_name_ [, ...]
        TO _role_specification_ [, ...] [ WITH GRANT OPTION ]
        [ GRANTED BY _role_specification_ ]
    
    GRANT { USAGE | ALL [ PRIVILEGES ] }
        ON FOREIGN SERVER _server_name_ [, ...]
        TO _role_specification_ [, ...] [ WITH GRANT OPTION ]
        [ GRANTED BY _role_specification_ ]
    
    GRANT { EXECUTE | ALL [ PRIVILEGES ] }
        ON { { FUNCTION | PROCEDURE | ROUTINE } _routine_name_ [ ( [ [ _argmode_ ] [ _arg_name_ ] _arg_type_ [, ...] ] ) ] [, ...]
             | ALL { FUNCTIONS | PROCEDURES | ROUTINES } IN SCHEMA _schema_name_ [, ...] }
        TO _role_specification_ [, ...] [ WITH GRANT OPTION ]
        [ GRANTED BY _role_specification_ ]
    
    GRANT { USAGE | ALL [ PRIVILEGES ] }
        ON LANGUAGE _lang_name_ [, ...]
        TO _role_specification_ [, ...] [ WITH GRANT OPTION ]
        [ GRANTED BY _role_specification_ ]
    
    GRANT { { SELECT | UPDATE } [, ...] | ALL [ PRIVILEGES ] }
        ON LARGE OBJECT _loid_ [, ...]
        TO _role_specification_ [, ...] [ WITH GRANT OPTION ]
        [ GRANTED BY _role_specification_ ]
    
    GRANT { { SET | ALTER SYSTEM } [, ... ] | ALL [ PRIVILEGES ] }
        ON PARAMETER _configuration_parameter_ [, ...]
        TO _role_specification_ [, ...] [ WITH GRANT OPTION ]
        [ GRANTED BY _role_specification_ ]
    
    GRANT { { CREATE | USAGE } [, ...] | ALL [ PRIVILEGES ] }
        ON SCHEMA _schema_name_ [, ...]
        TO _role_specification_ [, ...] [ WITH GRANT OPTION ]
        [ GRANTED BY _role_specification_ ]
    
    GRANT { CREATE | ALL [ PRIVILEGES ] }
        ON TABLESPACE _tablespace_name_ [, ...]
        TO _role_specification_ [, ...] [ WITH GRANT OPTION ]
        [ GRANTED BY _role_specification_ ]
    
    GRANT { USAGE | ALL [ PRIVILEGES ] }
        ON TYPE _type_name_ [, ...]
        TO _role_specification_ [, ...] [ WITH GRANT OPTION ]
        [ GRANTED BY _role_specification_ ]
    
    GRANT _role_name_ [, ...] TO _role_specification_ [, ...]
        [ WITH { ADMIN | INHERIT | SET } { OPTION | TRUE | FALSE } ]
        [ GRANTED BY _role_specification_ ]
    
    where _role_specification_ can be:
    
        [ GROUP ] _role_name_
      | PUBLIC
      | CURRENT_ROLE
      | CURRENT_USER
      | SESSION_USER
    

## Description

The `GRANT` command has two basic variants: one that grants privileges on a
database object (table, column, view, foreign table, sequence, database,
foreign-data wrapper, foreign server, function, procedure, procedural
language, large object, configuration parameter, schema, tablespace, or type),
and one that grants membership in a role. These variants are similar in many
ways, but they are different enough to be described separately.

### GRANT on Database Objects

This variant of the `GRANT` command gives specific privileges on a database
object to one or more roles. These privileges are added to those already
granted, if any.

The key word `PUBLIC` indicates that the privileges are to be granted to all
roles, including those that might be created later. `PUBLIC` can be thought of
as an implicitly defined group that always includes all roles. Any particular
role will have the sum of privileges granted directly to it, privileges
granted to any role it is presently a member of, and privileges granted to
`PUBLIC`.

If `WITH GRANT OPTION` is specified, the recipient of the privilege can in
turn grant it to others. Without a grant option, the recipient cannot do that.
Grant options cannot be granted to `PUBLIC`.

If `GRANTED BY` is specified, the specified grantor must be the current user.
This clause is currently present in this form only for SQL compatibility.

There is no need to grant privileges to the owner of an object (usually the
user that created it), as the owner has all privileges by default. (The owner
could, however, choose to revoke some of their own privileges for safety.)

The right to drop an object, or to alter its definition in any way, is not
treated as a grantable privilege; it is inherent in the owner, and cannot be
granted or revoked. (However, a similar effect can be obtained by granting or
revoking membership in the role that owns the object; see below.) The owner
implicitly has all grant options for the object, too.

The possible privileges are:

`SELECT`  
`INSERT`  
`UPDATE`  
`DELETE`  
`TRUNCATE`  
`REFERENCES`  
`TRIGGER`  
`CREATE`  
`CONNECT`  
`TEMPORARY`  
`EXECUTE`  
`USAGE`  
`SET`  
`ALTER SYSTEM`

    

Specific types of privileges, as defined in [Section 5.7](ddl-priv.html
"5.7. Privileges").

`TEMP`

    

Alternative spelling for `TEMPORARY`.

`ALL PRIVILEGES`

    

Grant all of the privileges available for the object's type. The `PRIVILEGES`
key word is optional in PostgreSQL, though it is required by strict SQL.

The `FUNCTION` syntax works for plain functions, aggregate functions, and
window functions, but not for procedures; use `PROCEDURE` for those.
Alternatively, use `ROUTINE` to refer to a function, aggregate function,
window function, or procedure regardless of its precise type.

There is also an option to grant privileges on all objects of the same type
within one or more schemas. This functionality is currently supported only for
tables, sequences, functions, and procedures. `ALL TABLES` also affects views
and foreign tables, just like the specific-object `GRANT` command. `ALL
FUNCTIONS` also affects aggregate and window functions, but not procedures,
again just like the specific-object `GRANT` command. Use `ALL ROUTINES` to
include procedures.

### GRANT on Roles

This variant of the `GRANT` command grants membership in a role to one or more
other roles, and the modification of membership options `SET`, `INHERIT`, and
`ADMIN`; see [Section 22.3](role-membership.html "22.3. Role Membership") for
details. Membership in a role is significant because it potentially allows
access to the privileges granted to a role to each of its members, and
potentially also the ability to make changes to the role itself. However, the
actual permissions conferred depend on the options associated with the grant.
To modify that options of an existing membership, simply specify the
membership with updated option values.

Each of the options described below can be set to either `TRUE` or `FALSE`.
The keyword `OPTION` is accepted as a synonym for `TRUE`, so that `WITH ADMIN
OPTION` is a synonym for `WITH ADMIN TRUE`. When altering an existing
membership the omission of an option results in the current value being
retained.

The `ADMIN` option allows the member to in turn grant membership in the role
to others, and revoke membership in the role as well. Without the admin
option, ordinary users cannot do that. A role is not considered to hold `WITH
ADMIN OPTION` on itself. Database superusers can grant or revoke membership in
any role to anyone. This option defaults to `FALSE`.

The `INHERIT` option controls the inheritance status of the new membership;
see [Section 22.3](role-membership.html "22.3. Role Membership") for details
on inheritance. If it is set to `TRUE`, it causes the new member to inherit
from the granted role. If set to `FALSE`, the new member does not inherit. If
unspecified when creating a new role membership, this defaults to the
inheritance attribute of the new member.

The `SET` option, if it is set to `TRUE`, allows the member to change to the
granted role using the [`SET ROLE`](sql-set-role.html "SET ROLE") command. If
a role is an indirect member of another role, it can use `SET ROLE` to change
to that role only if there is a chain of grants each of which has `SET TRUE`.
This option defaults to `TRUE`.

To create an object owned by another role or give ownership of an existing
object to another role, you must have the ability to `SET ROLE` to that role;
otherwise, commands such as `ALTER ... OWNER TO` or `CREATE DATABASE ...
OWNER` will fail. However, a user who inherits the privileges of a role but
does not have the ability to `SET ROLE` to that role may be able to obtain
full access to the role by manipulating existing objects owned by that role
(e.g. they could redefine an existing function to act as a Trojan horse).
Therefore, if a role's privileges are to be inherited but should not be
accessible via `SET ROLE`, it should not own any SQL objects.

If `GRANTED BY` is specified, the grant is recorded as having been done by the
specified role. A user can only attribute a grant to another role if they
possess the privileges of that role. The role recorded as the grantor must
have `ADMIN OPTION` on the target role, unless it is the bootstrap superuser.
When a grant is recorded as having a grantor other than the bootstrap
superuser, it depends on the grantor continuing to possess `ADMIN OPTION` on
the role; so, if `ADMIN OPTION` is revoked, dependent grants must be revoked
as well.

Unlike the case with privileges, membership in a role cannot be granted to
`PUBLIC`. Note also that this form of the command does not allow the noise
word `GROUP` in _`role_specification`_.

## Notes

The [`REVOKE`](sql-revoke.html "REVOKE") command is used to revoke access
privileges.

Since PostgreSQL 8.1, the concepts of users and groups have been unified into
a single kind of entity called a role. It is therefore no longer necessary to
use the keyword `GROUP` to identify whether a grantee is a user or a group.
`GROUP` is still allowed in the command, but it is a noise word.

A user may perform `SELECT`, `INSERT`, etc. on a column if they hold that
privilege for either the specific column or its whole table. Granting the
privilege at the table level and then revoking it for one column will not do
what one might wish: the table-level grant is unaffected by a column-level
operation.

When a non-owner of an object attempts to `GRANT` privileges on the object,
the command will fail outright if the user has no privileges whatsoever on the
object. As long as some privilege is available, the command will proceed, but
it will grant only those privileges for which the user has grant options. The
`GRANT ALL PRIVILEGES` forms will issue a warning message if no grant options
are held, while the other forms will issue a warning if grant options for any
of the privileges specifically named in the command are not held. (In
principle these statements apply to the object owner as well, but since the
owner is always treated as holding all grant options, the cases can never
occur.)

It should be noted that database superusers can access all objects regardless
of object privilege settings. This is comparable to the rights of `root` in a
Unix system. As with `root`, it's unwise to operate as a superuser except when
absolutely necessary.

If a superuser chooses to issue a `GRANT` or `REVOKE` command, the command is
performed as though it were issued by the owner of the affected object. In
particular, privileges granted via such a command will appear to have been
granted by the object owner. (For role membership, the membership appears to
have been granted by the bootstrap superuser.)

`GRANT` and `REVOKE` can also be done by a role that is not the owner of the
affected object, but is a member of the role that owns the object, or is a
member of a role that holds privileges `WITH GRANT OPTION` on the object. In
this case the privileges will be recorded as having been granted by the role
that actually owns the object or holds the privileges `WITH GRANT OPTION`. For
example, if table `t1` is owned by role `g1`, of which role `u1` is a member,
then `u1` can grant privileges on `t1` to `u2`, but those privileges will
appear to have been granted directly by `g1`. Any other member of role `g1`
could revoke them later.

If the role executing `GRANT` holds the required privileges indirectly via
more than one role membership path, it is unspecified which containing role
will be recorded as having done the grant. In such cases it is best practice
to use `SET ROLE` to become the specific role you want to do the `GRANT` as.

Granting permission on a table does not automatically extend permissions to
any sequences used by the table, including sequences tied to `SERIAL` columns.
Permissions on sequences must be set separately.

See [Section 5.7](ddl-priv.html "5.7. Privileges") for more information about
specific privilege types, as well as how to inspect objects' privileges.

## Examples

Grant insert privilege to all users on table `films`:

    
    
    GRANT INSERT ON films TO PUBLIC;
    

Grant all available privileges to user `manuel` on view `kinds`:

    
    
    GRANT ALL PRIVILEGES ON kinds TO manuel;
    

Note that while the above will indeed grant all privileges if executed by a
superuser or the owner of `kinds`, when executed by someone else it will only
grant those permissions for which the someone else has grant options.

Grant membership in role `admins` to user `joe`:

    
    
    GRANT admins TO joe;
    

## Compatibility

According to the SQL standard, the `PRIVILEGES` key word in `ALL PRIVILEGES`
is required. The SQL standard does not support setting the privileges on more
than one object per command.

PostgreSQL allows an object owner to revoke their own ordinary privileges: for
example, a table owner can make the table read-only to themselves by revoking
their own `INSERT`, `UPDATE`, `DELETE`, and `TRUNCATE` privileges. This is not
possible according to the SQL standard. The reason is that PostgreSQL treats
the owner's privileges as having been granted by the owner to themselves;
therefore they can revoke them too. In the SQL standard, the owner's
privileges are granted by an assumed entity “_SYSTEM”. Not being “_SYSTEM”,
the owner cannot revoke these rights.

According to the SQL standard, grant options can be granted to `PUBLIC`;
PostgreSQL only supports granting grant options to roles.

The SQL standard allows the `GRANTED BY` option to specify only `CURRENT_USER`
or `CURRENT_ROLE`. The other variants are PostgreSQL extensions.

The SQL standard provides for a `USAGE` privilege on other kinds of objects:
character sets, collations, translations.

In the SQL standard, sequences only have a `USAGE` privilege, which controls
the use of the `NEXT VALUE FOR` expression, which is equivalent to the
function `nextval` in PostgreSQL. The sequence privileges `SELECT` and
`UPDATE` are PostgreSQL extensions. The application of the sequence `USAGE`
privilege to the `currval` function is also a PostgreSQL extension (as is the
function itself).

Privileges on databases, tablespaces, schemas, languages, and configuration
parameters are PostgreSQL extensions.

## See Also

[REVOKE](sql-revoke.html "REVOKE"), [ALTER DEFAULT PRIVILEGES](sql-
alterdefaultprivileges.html "ALTER DEFAULT PRIVILEGES")

* * *

[Prev](sql-fetch.html "FETCH")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-importforeignschema.html "IMPORT FOREIGN SCHEMA")  
---|---|---  
FETCH  | [Home](index.html "PostgreSQL 16.9 Documentation") |  IMPORT FOREIGN SCHEMA  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-grant.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

