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

Supported Versions: [Current](/docs/current/manage-ag-overview.html
"PostgreSQL 17 - 23.1. Overview") ([17](/docs/17/manage-ag-overview.html
"PostgreSQL 17 - 23.1. Overview")) / [16](/docs/16/manage-ag-overview.html
"PostgreSQL 16 - 23.1. Overview") / [15](/docs/15/manage-ag-overview.html
"PostgreSQL 15 - 23.1. Overview") / [14](/docs/14/manage-ag-overview.html
"PostgreSQL 14 - 23.1. Overview") / [13](/docs/13/manage-ag-overview.html
"PostgreSQL 13 - 23.1. Overview")

Development Versions: [18](/docs/18/manage-ag-overview.html "PostgreSQL 18 -
23.1. Overview") / [devel](/docs/devel/manage-ag-overview.html "PostgreSQL
devel - 23.1. Overview")

Unsupported versions: [12](/docs/12/manage-ag-overview.html "PostgreSQL 12 -
23.1. Overview") / [11](/docs/11/manage-ag-overview.html "PostgreSQL 11 -
23.1. Overview") / [10](/docs/10/manage-ag-overview.html "PostgreSQL 10 -
23.1. Overview") / [9.6](/docs/9.6/manage-ag-overview.html "PostgreSQL 9.6 -
23.1. Overview") / [9.5](/docs/9.5/manage-ag-overview.html "PostgreSQL 9.5 -
23.1. Overview") / [9.4](/docs/9.4/manage-ag-overview.html "PostgreSQL 9.4 -
23.1. Overview") / [9.3](/docs/9.3/manage-ag-overview.html "PostgreSQL 9.3 -
23.1. Overview") / [9.2](/docs/9.2/manage-ag-overview.html "PostgreSQL 9.2 -
23.1. Overview") / [9.1](/docs/9.1/manage-ag-overview.html "PostgreSQL 9.1 -
23.1. Overview") / [9.0](/docs/9.0/manage-ag-overview.html "PostgreSQL 9.0 -
23.1. Overview") / [8.4](/docs/8.4/manage-ag-overview.html "PostgreSQL 8.4 -
23.1. Overview") / [8.3](/docs/8.3/manage-ag-overview.html "PostgreSQL 8.3 -
23.1. Overview") / [8.2](/docs/8.2/manage-ag-overview.html "PostgreSQL 8.2 -
23.1. Overview")

__

23.1. Overview  
---  
[Prev](managing-databases.html "Chapter 23. Managing Databases")  | [Up](managing-databases.html "Chapter 23. Managing Databases") | Chapter 23. Managing Databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](manage-ag-createdb.html "23.2. Creating a Database")  
  
* * *

## 23.1. Overview #

A small number of objects, like role, database, and tablespace names, are
defined at the cluster level and stored in the `pg_global` tablespace. Inside
the cluster are multiple databases, which are isolated from each other but can
access cluster-level objects. Inside each database are multiple schemas, which
contain objects like tables and functions. So the full hierarchy is: cluster,
database, schema, table (or some other kind of object, such as a function).

When connecting to the database server, a client must specify the database
name in its connection request. It is not possible to access more than one
database per connection. However, clients can open multiple connections to the
same database, or different databases. Database-level security has two
components: access control (see [Section 21.1](auth-pg-hba-conf.html
"21.1. The pg_hba.conf File")), managed at the connection level, and
authorization control (see [Section 5.7](ddl-priv.html "5.7. Privileges")),
managed via the grant system. Foreign data wrappers (see
[postgres_fdw](postgres-fdw.html "F.38. postgres_fdw — access data stored in
external PostgreSQL servers")) allow for objects within one database to act as
proxies for objects in other database or clusters. The older dblink module
(see [dblink](dblink.html "F.12. dblink — connect to other PostgreSQL
databases")) provides a similar capability. By default, all users can connect
to all databases using all connection methods.

If one PostgreSQL server cluster is planned to contain unrelated projects or
users that should be, for the most part, unaware of each other, it is
recommended to put them into separate databases and adjust authorizations and
access controls accordingly. If the projects or users are interrelated, and
thus should be able to use each other's resources, they should be put in the
same database but probably into separate schemas; this provides a modular
structure with namespace isolation and authorization control. More information
about managing schemas is in [Section 5.9](ddl-schemas.html "5.9. Schemas").

While multiple databases can be created within a single cluster, it is advised
to consider carefully whether the benefits outweigh the risks and limitations.
In particular, the impact that having a shared WAL (see [Chapter 30](wal.html
"Chapter 30. Reliability and the Write-Ahead Log")) has on backup and recovery
options. While individual databases in the cluster are isolated when
considered from the user's perspective, they are closely bound from the
database administrator's point-of-view.

Databases are created with the `CREATE DATABASE` command (see [Section
23.2](manage-ag-createdb.html "23.2. Creating a Database")) and destroyed with
the `DROP DATABASE` command (see [Section 23.5](manage-ag-dropdb.html
"23.5. Destroying a Database")). To determine the set of existing databases,
examine the `pg_database` system catalog, for example

    
    
    SELECT datname FROM pg_database;
    

The [psql](app-psql.html "psql") program's `\l` meta-command and `-l` command-
line option are also useful for listing the existing databases.

### Note

The SQL standard calls databases “catalogs”, but there is no difference in
practice.

* * *

[Prev](managing-databases.html "Chapter 23. Managing Databases")  | [Up](managing-databases.html "Chapter 23. Managing Databases") |  [Next](manage-ag-createdb.html "23.2. Creating a Database")  
---|---|---  
Chapter 23. Managing Databases  | [Home](index.html "PostgreSQL 16.9 Documentation") |  23.2. Creating a Database  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/manage-ag-overview.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

