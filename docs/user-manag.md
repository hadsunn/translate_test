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

Supported Versions: [Current](/docs/current/user-manag.html "PostgreSQL 17 -
Chapter 22. Database Roles") ([17](/docs/17/user-manag.html "PostgreSQL 17 -
Chapter 22. Database Roles")) / [16](/docs/16/user-manag.html "PostgreSQL 16 -
Chapter 22. Database Roles") / [15](/docs/15/user-manag.html "PostgreSQL 15 -
Chapter 22. Database Roles") / [14](/docs/14/user-manag.html "PostgreSQL 14 -
Chapter 22. Database Roles") / [13](/docs/13/user-manag.html "PostgreSQL 13 -
Chapter 22. Database Roles")

Development Versions: [18](/docs/18/user-manag.html "PostgreSQL 18 -
Chapter 22. Database Roles") / [devel](/docs/devel/user-manag.html "PostgreSQL
devel - Chapter 22. Database Roles")

Unsupported versions: [12](/docs/12/user-manag.html "PostgreSQL 12 -
Chapter 22. Database Roles") / [11](/docs/11/user-manag.html "PostgreSQL 11 -
Chapter 22. Database Roles") / [10](/docs/10/user-manag.html "PostgreSQL 10 -
Chapter 22. Database Roles") / [9.6](/docs/9.6/user-manag.html "PostgreSQL 9.6
- Chapter 22. Database Roles") / [9.5](/docs/9.5/user-manag.html "PostgreSQL
9.5 - Chapter 22. Database Roles") / [9.4](/docs/9.4/user-manag.html
"PostgreSQL 9.4 - Chapter 22. Database Roles") / [9.3](/docs/9.3/user-
manag.html "PostgreSQL 9.3 - Chapter 22. Database Roles") /
[9.2](/docs/9.2/user-manag.html "PostgreSQL 9.2 - Chapter 22. Database Roles")
/ [9.1](/docs/9.1/user-manag.html "PostgreSQL 9.1 - Chapter 22. Database
Roles") / [9.0](/docs/9.0/user-manag.html "PostgreSQL 9.0 -
Chapter 22. Database Roles") / [8.4](/docs/8.4/user-manag.html "PostgreSQL 8.4
- Chapter 22. Database Roles") / [8.3](/docs/8.3/user-manag.html "PostgreSQL
8.3 - Chapter 22. Database Roles") / [8.2](/docs/8.2/user-manag.html
"PostgreSQL 8.2 - Chapter 22. Database Roles") / [8.1](/docs/8.1/user-
manag.html "PostgreSQL 8.1 - Chapter 22. Database Roles") /
[8.0](/docs/8.0/user-manag.html "PostgreSQL 8.0 - Chapter 22. Database Roles")
/ [7.4](/docs/7.4/user-manag.html "PostgreSQL 7.4 - Chapter 22. Database
Roles") / [7.3](/docs/7.3/user-manag.html "PostgreSQL 7.3 -
Chapter 22. Database Roles") / [7.2](/docs/7.2/user-manag.html "PostgreSQL 7.2
- Chapter 22. Database Roles") / [7.1](/docs/7.1/user-manag.html "PostgreSQL
7.1 - Chapter 22. Database Roles")

__

Chapter 22. Database Roles  
---  
[Prev](client-authentication-problems.html "21.15. Authentication Problems")  | [Up](admin.html "Part III. Server Administration") | Part III. Server Administration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](database-roles.html "22.1. Database Roles")  
  
* * *

## Chapter 22. Database Roles

**Table of Contents**

[22.1. Database Roles](database-roles.html)

[22.2. Role Attributes](role-attributes.html)

[22.3. Role Membership](role-membership.html)

[22.4. Dropping Roles](role-removal.html)

[22.5. Predefined Roles](predefined-roles.html)

[22.6. Function Security](perm-functions.html)

PostgreSQL manages database access permissions using the concept of _roles_. A
role can be thought of as either a database user, or a group of database
users, depending on how the role is set up. Roles can own database objects
(for example, tables and functions) and can assign privileges on those objects
to other roles to control who has access to which objects. Furthermore, it is
possible to grant _membership_ in a role to another role, thus allowing the
member role to use privileges assigned to another role.

The concept of roles subsumes the concepts of “users” and “groups”. In
PostgreSQL versions before 8.1, users and groups were distinct kinds of
entities, but now there are only roles. Any role can act as a user, a group,
or both.

This chapter describes how to create and manage roles. More information about
the effects of role privileges on various database objects can be found in
[Section 5.7](ddl-priv.html "5.7. Privileges").

* * *

[Prev](client-authentication-problems.html "21.15. Authentication Problems")  | [Up](admin.html "Part III. Server Administration") |  [Next](database-roles.html "22.1. Database Roles")  
---|---|---  
21.15. Authentication Problems  | [Home](index.html "PostgreSQL 16.9 Documentation") |  22.1. Database Roles  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/user-manag.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

