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

Supported Versions: [Current](/docs/current/role-removal.html "PostgreSQL 17 -
22.4. Dropping Roles") ([17](/docs/17/role-removal.html "PostgreSQL 17 -
22.4. Dropping Roles")) / [16](/docs/16/role-removal.html "PostgreSQL 16 -
22.4. Dropping Roles") / [15](/docs/15/role-removal.html "PostgreSQL 15 -
22.4. Dropping Roles") / [14](/docs/14/role-removal.html "PostgreSQL 14 -
22.4. Dropping Roles") / [13](/docs/13/role-removal.html "PostgreSQL 13 -
22.4. Dropping Roles")

Development Versions: [18](/docs/18/role-removal.html "PostgreSQL 18 -
22.4. Dropping Roles") / [devel](/docs/devel/role-removal.html "PostgreSQL
devel - 22.4. Dropping Roles")

Unsupported versions: [12](/docs/12/role-removal.html "PostgreSQL 12 -
22.4. Dropping Roles") / [11](/docs/11/role-removal.html "PostgreSQL 11 -
22.4. Dropping Roles") / [10](/docs/10/role-removal.html "PostgreSQL 10 -
22.4. Dropping Roles") / [9.6](/docs/9.6/role-removal.html "PostgreSQL 9.6 -
22.4. Dropping Roles") / [9.5](/docs/9.5/role-removal.html "PostgreSQL 9.5 -
22.4. Dropping Roles") / [9.4](/docs/9.4/role-removal.html "PostgreSQL 9.4 -
22.4. Dropping Roles") / [9.3](/docs/9.3/role-removal.html "PostgreSQL 9.3 -
22.4. Dropping Roles") / [9.2](/docs/9.2/role-removal.html "PostgreSQL 9.2 -
22.4. Dropping Roles") / [9.1](/docs/9.1/role-removal.html "PostgreSQL 9.1 -
22.4. Dropping Roles")

__

22.4. Dropping Roles  
---  
[Prev](role-membership.html "22.3. Role Membership")  | [Up](user-manag.html "Chapter 22. Database Roles") | Chapter 22. Database Roles | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](predefined-roles.html "22.5. Predefined Roles")  
  
* * *

## 22.4. Dropping Roles #

Because roles can own database objects and can hold privileges to access other
objects, dropping a role is often not just a matter of a quick [`DROP
ROLE`](sql-droprole.html "DROP ROLE"). Any objects owned by the role must
first be dropped or reassigned to other owners; and any permissions granted to
the role must be revoked.

Ownership of objects can be transferred one at a time using `ALTER` commands,
for example:

    
    
    ALTER TABLE bobs_table OWNER TO alice;
    

Alternatively, the [`REASSIGN OWNED`](sql-reassign-owned.html "REASSIGN
OWNED") command can be used to reassign ownership of all objects owned by the
role-to-be-dropped to a single other role. Because `REASSIGN OWNED` cannot
access objects in other databases, it is necessary to run it in each database
that contains objects owned by the role. (Note that the first such `REASSIGN
OWNED` will change the ownership of any shared-across-databases objects, that
is databases or tablespaces, that are owned by the role-to-be-dropped.)

Once any valuable objects have been transferred to new owners, any remaining
objects owned by the role-to-be-dropped can be dropped with the [`DROP
OWNED`](sql-drop-owned.html "DROP OWNED") command. Again, this command cannot
access objects in other databases, so it is necessary to run it in each
database that contains objects owned by the role. Also, `DROP OWNED` will not
drop entire databases or tablespaces, so it is necessary to do that manually
if the role owns any databases or tablespaces that have not been transferred
to new owners.

`DROP OWNED` also takes care of removing any privileges granted to the target
role for objects that do not belong to it. Because `REASSIGN OWNED` does not
touch such objects, it's typically necessary to run both `REASSIGN OWNED` and
`DROP OWNED` (in that order!) to fully remove the dependencies of a role to be
dropped.

In short then, the most general recipe for removing a role that has been used
to own objects is:

    
    
    REASSIGN OWNED BY doomed_role TO successor_role;
    DROP OWNED BY doomed_role;
    -- repeat the above commands in each database of the cluster
    DROP ROLE doomed_role;
    

When not all owned objects are to be transferred to the same successor owner,
it's best to handle the exceptions manually and then perform the above steps
to mop up.

If `DROP ROLE` is attempted while dependent objects still remain, it will
issue messages identifying which objects need to be reassigned or dropped.

* * *

[Prev](role-membership.html "22.3. Role Membership")  | [Up](user-manag.html "Chapter 22. Database Roles") |  [Next](predefined-roles.html "22.5. Predefined Roles")  
---|---|---  
22.3. Role Membership  | [Home](index.html "PostgreSQL 16.9 Documentation") |  22.5. Predefined Roles  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/role-removal.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

