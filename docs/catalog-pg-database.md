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

Supported Versions: [Current](/docs/current/catalog-pg-database.html
"PostgreSQL 17 - 53.15. pg_database") ([17](/docs/17/catalog-pg-database.html
"PostgreSQL 17 - 53.15. pg_database")) / [16](/docs/16/catalog-pg-
database.html "PostgreSQL 16 - 53.15. pg_database") / [15](/docs/15/catalog-
pg-database.html "PostgreSQL 15 - 53.15. pg_database") /
[14](/docs/14/catalog-pg-database.html "PostgreSQL 14 - 53.15. pg_database") /
[13](/docs/13/catalog-pg-database.html "PostgreSQL 13 - 53.15. pg_database")

Development Versions: [18](/docs/18/catalog-pg-database.html "PostgreSQL 18 -
53.15. pg_database") / [devel](/docs/devel/catalog-pg-database.html
"PostgreSQL devel - 53.15. pg_database")

Unsupported versions: [12](/docs/12/catalog-pg-database.html "PostgreSQL 12 -
53.15. pg_database") / [11](/docs/11/catalog-pg-database.html "PostgreSQL 11 -
53.15. pg_database") / [10](/docs/10/catalog-pg-database.html "PostgreSQL 10 -
53.15. pg_database") / [9.6](/docs/9.6/catalog-pg-database.html "PostgreSQL
9.6 - 53.15. pg_database") / [9.5](/docs/9.5/catalog-pg-database.html
"PostgreSQL 9.5 - 53.15. pg_database") / [9.4](/docs/9.4/catalog-pg-
database.html "PostgreSQL 9.4 - 53.15. pg_database") /
[9.3](/docs/9.3/catalog-pg-database.html "PostgreSQL 9.3 -
53.15. pg_database") / [9.2](/docs/9.2/catalog-pg-database.html "PostgreSQL
9.2 - 53.15. pg_database") / [9.1](/docs/9.1/catalog-pg-database.html
"PostgreSQL 9.1 - 53.15. pg_database") / [9.0](/docs/9.0/catalog-pg-
database.html "PostgreSQL 9.0 - 53.15. pg_database") /
[8.4](/docs/8.4/catalog-pg-database.html "PostgreSQL 8.4 -
53.15. pg_database") / [8.3](/docs/8.3/catalog-pg-database.html "PostgreSQL
8.3 - 53.15. pg_database") / [8.2](/docs/8.2/catalog-pg-database.html
"PostgreSQL 8.2 - 53.15. pg_database") / [8.1](/docs/8.1/catalog-pg-
database.html "PostgreSQL 8.1 - 53.15. pg_database") /
[8.0](/docs/8.0/catalog-pg-database.html "PostgreSQL 8.0 -
53.15. pg_database") / [7.4](/docs/7.4/catalog-pg-database.html "PostgreSQL
7.4 - 53.15. pg_database") / [7.3](/docs/7.3/catalog-pg-database.html
"PostgreSQL 7.3 - 53.15. pg_database") / [7.2](/docs/7.2/catalog-pg-
database.html "PostgreSQL 7.2 - 53.15. pg_database") /
[7.1](/docs/7.1/catalog-pg-database.html "PostgreSQL 7.1 -
53.15. pg_database")

__

53.15. `pg_database`  
---  
[Prev](catalog-pg-conversion.html "53.14. pg_conversion")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-db-role-setting.html "53.16. pg_db_role_setting")  
  
* * *

## 53.15. `pg_database` #

The catalog `pg_database` stores information about the available databases.
Databases are created with the [`CREATE DATABASE`](sql-createdatabase.html
"CREATE DATABASE") command. Consult [Chapter 23](managing-databases.html
"Chapter 23. Managing Databases") for details about the meaning of some of the
parameters.

Unlike most system catalogs, `pg_database` is shared across all databases of a
cluster: there is only one copy of `pg_database` per cluster, not one per
database.

**Table  53.15. `pg_database` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`datname` `name` Database name  
`datdba` `oid` (references [`pg_authid`](catalog-pg-authid.html
"53.8. pg_authid").`oid`) Owner of the database, usually the user who created
it  
`encoding` `int4` Character encoding for this database
([`pg_encoding_to_char()`](functions-info.html#PG-ENCODING-TO-CHAR) can
translate this number to the encoding name)  
`datlocprovider` `char` Locale provider for this database: `c` = libc, `i` =
icu  
`datistemplate` `bool` If true, then this database can be cloned by any user
with `CREATEDB` privileges; if false, then only superusers or the owner of the
database can clone it.  
`datallowconn` `bool` If false then no one can connect to this database. This
is used to protect the `template0` database from being altered.  
`datconnlimit` `int4` Sets maximum number of concurrent connections that can
be made to this database. -1 means no limit, -2 indicates the database is
invalid.  
`datfrozenxid` `xid` All transaction IDs before this one have been replaced
with a permanent (“frozen”) transaction ID in this database. This is used to
track whether the database needs to be vacuumed in order to prevent
transaction ID wraparound or to allow `pg_xact` to be shrunk. It is the
minimum of the per-table [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`relfrozenxid` values.  
`datminmxid` `xid` All multixact IDs before this one have been replaced with a
transaction ID in this database. This is used to track whether the database
needs to be vacuumed in order to prevent multixact ID wraparound or to allow
`pg_multixact` to be shrunk. It is the minimum of the per-table
[`pg_class`](catalog-pg-class.html "53.11. pg_class").`relminmxid` values.  
`dattablespace` `oid` (references [`pg_tablespace`](catalog-pg-tablespace.html
"53.56. pg_tablespace").`oid`) The default tablespace for the database. Within
this database, all tables for which [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`reltablespace` is zero will be stored in this tablespace;
in particular, all the non-shared system catalogs will be there.  
`datcollate` `text` LC_COLLATE for this database  
`datctype` `text` LC_CTYPE for this database  
`daticulocale` `text` ICU locale ID for this database  
`daticurules` `text` ICU collation rules for this database  
`datcollversion` `text` Provider-specific version of the collation. This is
recorded when the database is created and then checked when it is used, to
detect changes in the collation definition that could lead to data corruption.  
`datacl` `aclitem[]` Access privileges; see [Section 5.7](ddl-priv.html
"5.7. Privileges") for details  
  
  

* * *

[Prev](catalog-pg-conversion.html "53.14. pg_conversion")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-db-role-setting.html "53.16. pg_db_role_setting")  
---|---|---  
53.14. `pg_conversion`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.16. `pg_db_role_setting`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-database.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

