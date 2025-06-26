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

Supported Versions: [Current](/docs/current/role-membership.html "PostgreSQL
17 - 22.3. Role Membership") ([17](/docs/17/role-membership.html "PostgreSQL
17 - 22.3. Role Membership")) / [16](/docs/16/role-membership.html "PostgreSQL
16 - 22.3. Role Membership") / [15](/docs/15/role-membership.html "PostgreSQL
15 - 22.3. Role Membership") / [14](/docs/14/role-membership.html "PostgreSQL
14 - 22.3. Role Membership") / [13](/docs/13/role-membership.html "PostgreSQL
13 - 22.3. Role Membership")

Development Versions: [18](/docs/18/role-membership.html "PostgreSQL 18 -
22.3. Role Membership") / [devel](/docs/devel/role-membership.html "PostgreSQL
devel - 22.3. Role Membership")

Unsupported versions: [12](/docs/12/role-membership.html "PostgreSQL 12 -
22.3. Role Membership") / [11](/docs/11/role-membership.html "PostgreSQL 11 -
22.3. Role Membership") / [10](/docs/10/role-membership.html "PostgreSQL 10 -
22.3. Role Membership") / [9.6](/docs/9.6/role-membership.html "PostgreSQL 9.6
- 22.3. Role Membership") / [9.5](/docs/9.5/role-membership.html "PostgreSQL
9.5 - 22.3. Role Membership") / [9.4](/docs/9.4/role-membership.html
"PostgreSQL 9.4 - 22.3. Role Membership") / [9.3](/docs/9.3/role-
membership.html "PostgreSQL 9.3 - 22.3. Role Membership") /
[9.2](/docs/9.2/role-membership.html "PostgreSQL 9.2 - 22.3. Role Membership")
/ [9.1](/docs/9.1/role-membership.html "PostgreSQL 9.1 - 22.3. Role
Membership") / [9.0](/docs/9.0/role-membership.html "PostgreSQL 9.0 -
22.3. Role Membership") / [8.4](/docs/8.4/role-membership.html "PostgreSQL 8.4
- 22.3. Role Membership") / [8.3](/docs/8.3/role-membership.html "PostgreSQL
8.3 - 22.3. Role Membership") / [8.2](/docs/8.2/role-membership.html
"PostgreSQL 8.2 - 22.3. Role Membership") / [8.1](/docs/8.1/role-
membership.html "PostgreSQL 8.1 - 22.3. Role Membership")

__

22.3. Role Membership  
---  
[Prev](role-attributes.html "22.2. Role Attributes")  | [Up](user-manag.html "Chapter 22. Database Roles") | Chapter 22. Database Roles | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](role-removal.html "22.4. Dropping Roles")  
  
* * *

## 22.3. Role Membership #

It is frequently convenient to group users together to ease management of
privileges: that way, privileges can be granted to, or revoked from, a group
as a whole. In PostgreSQL this is done by creating a role that represents the
group, and then granting _membership_ in the group role to individual user
roles.

To set up a group role, first create the role:

    
    
    CREATE ROLE _name_ ;
    

Typically a role being used as a group would not have the `LOGIN` attribute,
though you can set it if you wish.

Once the group role exists, you can add and remove members using the
[`GRANT`](sql-grant.html "GRANT") and [`REVOKE`](sql-revoke.html "REVOKE")
commands:

    
    
    GRANT _group_role_ TO _role1_ , ... ;
    REVOKE _group_role_ FROM _role1_ , ... ;
    

You can grant membership to other group roles, too (since there isn't really
any distinction between group roles and non-group roles). The database will
not let you set up circular membership loops. Also, it is not permitted to
grant membership in a role to `PUBLIC`.

The members of a group role can use the privileges of the role in two ways.
First, member roles that have been granted membership with the `SET` option
can do [`SET ROLE`](sql-set-role.html "SET ROLE") to temporarily “become” the
group role. In this state, the database session has access to the privileges
of the group role rather than the original login role, and any database
objects created are considered owned by the group role not the login role.
Second, member roles that have been granted membership with the `INHERIT`
option automatically have use of the privileges of those directly or
indirectly a member of, though the chain stops at memberships lacking the
inherit option. As an example, suppose we have done:

    
    
    CREATE ROLE joe LOGIN;
    CREATE ROLE admin;
    CREATE ROLE wheel;
    CREATE ROLE island;
    GRANT admin TO joe WITH INHERIT TRUE;
    GRANT wheel TO admin WITH INHERIT FALSE;
    GRANT island TO joe WITH INHERIT TRUE, SET FALSE;
    

Immediately after connecting as role `joe`, a database session will have use
of privileges granted directly to `joe` plus any privileges granted to `admin`
and `island`, because `joe` “inherits” those privileges. However, privileges
granted to `wheel` are not available, because even though `joe` is indirectly
a member of `wheel`, the membership is via `admin` which was granted using
`WITH INHERIT FALSE`. After:

    
    
    SET ROLE admin;
    

the session would have use of only those privileges granted to `admin`, and
not those granted to `joe` or `island`. After:

    
    
    SET ROLE wheel;
    

the session would have use of only those privileges granted to `wheel`, and
not those granted to either `joe` or `admin`. The original privilege state can
be restored with any of:

    
    
    SET ROLE joe;
    SET ROLE NONE;
    RESET ROLE;
    

### Note

The `SET ROLE` command always allows selecting any role that the original
login role is directly or indirectly a member of, provided that there is a
chain of membership grants each of which has `SET TRUE` (which is the
default). Thus, in the above example, it is not necessary to become `admin`
before becoming `wheel`. On the other hand, it is not possible to become
`island` at all; `joe` can only access those privileges via inheritance.

### Note

In the SQL standard, there is a clear distinction between users and roles, and
users do not automatically inherit privileges while roles do. This behavior
can be obtained in PostgreSQL by giving roles being used as SQL roles the
`INHERIT` attribute, while giving roles being used as SQL users the
`NOINHERIT` attribute. However, PostgreSQL defaults to giving all roles the
`INHERIT` attribute, for backward compatibility with pre-8.1 releases in which
users always had use of permissions granted to groups they were members of.

The role attributes `LOGIN`, `SUPERUSER`, `CREATEDB`, and `CREATEROLE` can be
thought of as special privileges, but they are never inherited as ordinary
privileges on database objects are. You must actually `SET ROLE` to a specific
role having one of these attributes in order to make use of the attribute.
Continuing the above example, we might choose to grant `CREATEDB` and
`CREATEROLE` to the `admin` role. Then a session connecting as role `joe`
would not have these privileges immediately, only after doing `SET ROLE
admin`.

To destroy a group role, use [`DROP ROLE`](sql-droprole.html "DROP ROLE"):

    
    
    DROP ROLE _name_ ;
    

Any memberships in the group role are automatically revoked (but the member
roles are not otherwise affected).

* * *

[Prev](role-attributes.html "22.2. Role Attributes")  | [Up](user-manag.html "Chapter 22. Database Roles") |  [Next](role-removal.html "22.4. Dropping Roles")  
---|---|---  
22.2. Role Attributes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  22.4. Dropping Roles  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/role-membership.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

