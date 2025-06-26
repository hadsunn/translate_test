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

Supported Versions: [Current](/docs/current/sql-revoke.html "PostgreSQL 17 -
REVOKE") ([17](/docs/17/sql-revoke.html "PostgreSQL 17 - REVOKE")) /
[16](/docs/16/sql-revoke.html "PostgreSQL 16 - REVOKE") / [15](/docs/15/sql-
revoke.html "PostgreSQL 15 - REVOKE") / [14](/docs/14/sql-revoke.html
"PostgreSQL 14 - REVOKE") / [13](/docs/13/sql-revoke.html "PostgreSQL 13 -
REVOKE")

Development Versions: [18](/docs/18/sql-revoke.html "PostgreSQL 18 - REVOKE")
/ [devel](/docs/devel/sql-revoke.html "PostgreSQL devel - REVOKE")

Unsupported versions: [12](/docs/12/sql-revoke.html "PostgreSQL 12 - REVOKE")
/ [11](/docs/11/sql-revoke.html "PostgreSQL 11 - REVOKE") / [10](/docs/10/sql-
revoke.html "PostgreSQL 10 - REVOKE") / [9.6](/docs/9.6/sql-revoke.html
"PostgreSQL 9.6 - REVOKE") / [9.5](/docs/9.5/sql-revoke.html "PostgreSQL 9.5 -
REVOKE") / [9.4](/docs/9.4/sql-revoke.html "PostgreSQL 9.4 - REVOKE") /
[9.3](/docs/9.3/sql-revoke.html "PostgreSQL 9.3 - REVOKE") /
[9.2](/docs/9.2/sql-revoke.html "PostgreSQL 9.2 - REVOKE") /
[9.1](/docs/9.1/sql-revoke.html "PostgreSQL 9.1 - REVOKE") /
[9.0](/docs/9.0/sql-revoke.html "PostgreSQL 9.0 - REVOKE") /
[8.4](/docs/8.4/sql-revoke.html "PostgreSQL 8.4 - REVOKE") /
[8.3](/docs/8.3/sql-revoke.html "PostgreSQL 8.3 - REVOKE") /
[8.2](/docs/8.2/sql-revoke.html "PostgreSQL 8.2 - REVOKE") /
[8.1](/docs/8.1/sql-revoke.html "PostgreSQL 8.1 - REVOKE") /
[8.0](/docs/8.0/sql-revoke.html "PostgreSQL 8.0 - REVOKE") /
[7.4](/docs/7.4/sql-revoke.html "PostgreSQL 7.4 - REVOKE") /
[7.3](/docs/7.3/sql-revoke.html "PostgreSQL 7.3 - REVOKE") /
[7.2](/docs/7.2/sql-revoke.html "PostgreSQL 7.2 - REVOKE") /
[7.1](/docs/7.1/sql-revoke.html "PostgreSQL 7.1 - REVOKE")

__

REVOKE  
---  
[Prev](sql-reset.html "RESET")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-rollback.html "ROLLBACK")  
  
* * *

## REVOKE

REVOKE — remove access privileges

## Synopsis

    
    
    REVOKE [ GRANT OPTION FOR ]
        { { SELECT | INSERT | UPDATE | DELETE | TRUNCATE | REFERENCES | TRIGGER }
        [, ...] | ALL [ PRIVILEGES ] }
        ON { [ TABLE ] _table_name_ [, ...]
             | ALL TABLES IN SCHEMA _schema_name_ [, ...] }
        FROM _role_specification_ [, ...]
        [ GRANTED BY _role_specification_ ]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { { SELECT | INSERT | UPDATE | REFERENCES } ( _column_name_ [, ...] )
        [, ...] | ALL [ PRIVILEGES ] ( _column_name_ [, ...] ) }
        ON [ TABLE ] _table_name_ [, ...]
        FROM _role_specification_ [, ...]
        [ GRANTED BY _role_specification_ ]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { { USAGE | SELECT | UPDATE }
        [, ...] | ALL [ PRIVILEGES ] }
        ON { SEQUENCE _sequence_name_ [, ...]
             | ALL SEQUENCES IN SCHEMA _schema_name_ [, ...] }
        FROM _role_specification_ [, ...]
        [ GRANTED BY _role_specification_ ]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { { CREATE | CONNECT | TEMPORARY | TEMP } [, ...] | ALL [ PRIVILEGES ] }
        ON DATABASE _database_name_ [, ...]
        FROM _role_specification_ [, ...]
        [ GRANTED BY _role_specification_ ]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { USAGE | ALL [ PRIVILEGES ] }
        ON DOMAIN _domain_name_ [, ...]
        FROM _role_specification_ [, ...]
        [ GRANTED BY _role_specification_ ]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { USAGE | ALL [ PRIVILEGES ] }
        ON FOREIGN DATA WRAPPER _fdw_name_ [, ...]
        FROM _role_specification_ [, ...]
        [ GRANTED BY _role_specification_ ]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { USAGE | ALL [ PRIVILEGES ] }
        ON FOREIGN SERVER _server_name_ [, ...]
        FROM _role_specification_ [, ...]
        [ GRANTED BY _role_specification_ ]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { EXECUTE | ALL [ PRIVILEGES ] }
        ON { { FUNCTION | PROCEDURE | ROUTINE } _function_name_ [ ( [ [ _argmode_ ] [ _arg_name_ ] _arg_type_ [, ...] ] ) ] [, ...]
             | ALL { FUNCTIONS | PROCEDURES | ROUTINES } IN SCHEMA _schema_name_ [, ...] }
        FROM _role_specification_ [, ...]
        [ GRANTED BY _role_specification_ ]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { USAGE | ALL [ PRIVILEGES ] }
        ON LANGUAGE _lang_name_ [, ...]
        FROM _role_specification_ [, ...]
        [ GRANTED BY _role_specification_ ]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { { SELECT | UPDATE } [, ...] | ALL [ PRIVILEGES ] }
        ON LARGE OBJECT _loid_ [, ...]
        FROM _role_specification_ [, ...]
        [ GRANTED BY _role_specification_ ]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { { SET | ALTER SYSTEM } [, ...] | ALL [ PRIVILEGES ] }
        ON PARAMETER _configuration_parameter_ [, ...]
        FROM _role_specification_ [, ...]
        [ GRANTED BY _role_specification_ ]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { { CREATE | USAGE } [, ...] | ALL [ PRIVILEGES ] }
        ON SCHEMA _schema_name_ [, ...]
        FROM _role_specification_ [, ...]
        [ GRANTED BY _role_specification_ ]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { CREATE | ALL [ PRIVILEGES ] }
        ON TABLESPACE _tablespace_name_ [, ...]
        FROM _role_specification_ [, ...]
        [ GRANTED BY _role_specification_ ]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ GRANT OPTION FOR ]
        { USAGE | ALL [ PRIVILEGES ] }
        ON TYPE _type_name_ [, ...]
        FROM _role_specification_ [, ...]
        [ GRANTED BY _role_specification_ ]
        [ CASCADE | RESTRICT ]
    
    REVOKE [ { ADMIN | INHERIT | SET } OPTION FOR ]
        _role_name_ [, ...] FROM _role_specification_ [, ...]
        [ GRANTED BY _role_specification_ ]
        [ CASCADE | RESTRICT ]
    
    where _role_specification_ can be:
    
        [ GROUP ] _role_name_
      | PUBLIC
      | CURRENT_ROLE
      | CURRENT_USER
      | SESSION_USER
    

## Description

The `REVOKE` command revokes previously granted privileges from one or more
roles. The key word `PUBLIC` refers to the implicitly defined group of all
roles.

See the description of the [`GRANT`](sql-grant.html "GRANT") command for the
meaning of the privilege types.

Note that any particular role will have the sum of privileges granted directly
to it, privileges granted to any role it is presently a member of, and
privileges granted to `PUBLIC`. Thus, for example, revoking `SELECT` privilege
from `PUBLIC` does not necessarily mean that all roles have lost `SELECT`
privilege on the object: those who have it granted directly or via another
role will still have it. Similarly, revoking `SELECT` from a user might not
prevent that user from using `SELECT` if `PUBLIC` or another membership role
still has `SELECT` rights.

If `GRANT OPTION FOR` is specified, only the grant option for the privilege is
revoked, not the privilege itself. Otherwise, both the privilege and the grant
option are revoked.

If a user holds a privilege with grant option and has granted it to other
users then the privileges held by those other users are called dependent
privileges. If the privilege or the grant option held by the first user is
being revoked and dependent privileges exist, those dependent privileges are
also revoked if `CASCADE` is specified; if it is not, the revoke action will
fail. This recursive revocation only affects privileges that were granted
through a chain of users that is traceable to the user that is the subject of
this `REVOKE` command. Thus, the affected users might effectively keep the
privilege if it was also granted through other users.

When revoking privileges on a table, the corresponding column privileges (if
any) are automatically revoked on each column of the table, as well. On the
other hand, if a role has been granted privileges on a table, then revoking
the same privileges from individual columns will have no effect.

When revoking membership in a role, `GRANT OPTION` is instead called `ADMIN
OPTION`, but the behavior is similar. Note that, in releases prior to
PostgreSQL 16, dependent privileges were not tracked for grants of role
membership, and thus `CASCADE` had no effect for role membership. This is no
longer the case. Note also that this form of the command does not allow the
noise word `GROUP` in _`role_specification`_.

Just as `ADMIN OPTION` can be removed from an existing role grant, it is also
possible to revoke `INHERIT OPTION` or `SET OPTION`. This is equivalent to
setting the value of the corresponding option to `FALSE`.

## Notes

A user can only revoke privileges that were granted directly by that user. If,
for example, user A has granted a privilege with grant option to user B, and
user B has in turn granted it to user C, then user A cannot revoke the
privilege directly from C. Instead, user A could revoke the grant option from
user B and use the `CASCADE` option so that the privilege is in turn revoked
from user C. For another example, if both A and B have granted the same
privilege to C, A can revoke their own grant but not B's grant, so C will
still effectively have the privilege.

When a non-owner of an object attempts to `REVOKE` privileges on the object,
the command will fail outright if the user has no privileges whatsoever on the
object. As long as some privilege is available, the command will proceed, but
it will revoke only those privileges for which the user has grant options. The
`REVOKE ALL PRIVILEGES` forms will issue a warning message if no grant options
are held, while the other forms will issue a warning if grant options for any
of the privileges specifically named in the command are not held. (In
principle these statements apply to the object owner as well, but since the
owner is always treated as holding all grant options, the cases can never
occur.)

If a superuser chooses to issue a `GRANT` or `REVOKE` command, the command is
performed as though it were issued by the owner of the affected object. (Since
roles do not have owners, in the case of a `GRANT` of role membership, the
command is performed as though it were issued by the bootstrap superuser.)
Since all privileges ultimately come from the object owner (possibly
indirectly via chains of grant options), it is possible for a superuser to
revoke all privileges, but this might require use of `CASCADE` as stated
above.

`REVOKE` can also be done by a role that is not the owner of the affected
object, but is a member of the role that owns the object, or is a member of a
role that holds privileges `WITH GRANT OPTION` on the object. In this case the
command is performed as though it were issued by the containing role that
actually owns the object or holds the privileges `WITH GRANT OPTION`. For
example, if table `t1` is owned by role `g1`, of which role `u1` is a member,
then `u1` can revoke privileges on `t1` that are recorded as being granted by
`g1`. This would include grants made by `u1` as well as by other members of
role `g1`.

If the role executing `REVOKE` holds privileges indirectly via more than one
role membership path, it is unspecified which containing role will be used to
perform the command. In such cases it is best practice to use `SET ROLE` to
become the specific role you want to do the `REVOKE` as. Failure to do so
might lead to revoking privileges other than the ones you intended, or not
revoking anything at all.

See [Section 5.7](ddl-priv.html "5.7. Privileges") for more information about
specific privilege types, as well as how to inspect objects' privileges.

## Examples

Revoke insert privilege for the public on table `films`:

    
    
    REVOKE INSERT ON films FROM PUBLIC;
    

Revoke all privileges from user `manuel` on view `kinds`:

    
    
    REVOKE ALL PRIVILEGES ON kinds FROM manuel;
    

Note that this actually means “revoke all privileges that I granted”.

Revoke membership in role `admins` from user `joe`:

    
    
    REVOKE admins FROM joe;
    

## Compatibility

The compatibility notes of the [`GRANT`](sql-grant.html "GRANT") command apply
analogously to `REVOKE`. The keyword `RESTRICT` or `CASCADE` is required
according to the standard, but PostgreSQL assumes `RESTRICT` by default.

## See Also

[GRANT](sql-grant.html "GRANT"), [ALTER DEFAULT PRIVILEGES](sql-
alterdefaultprivileges.html "ALTER DEFAULT PRIVILEGES")

* * *

[Prev](sql-reset.html "RESET")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-rollback.html "ROLLBACK")  
---|---|---  
RESET  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ROLLBACK  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-revoke.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

