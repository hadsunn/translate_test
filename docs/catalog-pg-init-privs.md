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

Supported Versions: [Current](/docs/current/catalog-pg-init-privs.html
"PostgreSQL 17 - 53.28. pg_init_privs") ([17](/docs/17/catalog-pg-init-
privs.html "PostgreSQL 17 - 53.28. pg_init_privs")) / [16](/docs/16/catalog-
pg-init-privs.html "PostgreSQL 16 - 53.28. pg_init_privs") /
[15](/docs/15/catalog-pg-init-privs.html "PostgreSQL 15 -
53.28. pg_init_privs") / [14](/docs/14/catalog-pg-init-privs.html "PostgreSQL
14 - 53.28. pg_init_privs") / [13](/docs/13/catalog-pg-init-privs.html
"PostgreSQL 13 - 53.28. pg_init_privs")

Development Versions: [18](/docs/18/catalog-pg-init-privs.html "PostgreSQL 18
- 53.28. pg_init_privs") / [devel](/docs/devel/catalog-pg-init-privs.html
"PostgreSQL devel - 53.28. pg_init_privs")

Unsupported versions: [12](/docs/12/catalog-pg-init-privs.html "PostgreSQL 12
- 53.28. pg_init_privs") / [11](/docs/11/catalog-pg-init-privs.html
"PostgreSQL 11 - 53.28. pg_init_privs") / [10](/docs/10/catalog-pg-init-
privs.html "PostgreSQL 10 - 53.28. pg_init_privs") / [9.6](/docs/9.6/catalog-
pg-init-privs.html "PostgreSQL 9.6 - 53.28. pg_init_privs")

__

53.28. `pg_init_privs`  
---  
[Prev](catalog-pg-inherits.html "53.27. pg_inherits")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-language.html "53.29. pg_language")  
  
* * *

## 53.28. `pg_init_privs` #

The catalog `pg_init_privs` records information about the initial privileges
of objects in the system. There is one entry for each object in the database
which has a non-default (non-NULL) initial set of privileges.

Objects can have initial privileges either by having those privileges set when
the system is initialized (by initdb) or when the object is created during a
[`CREATE EXTENSION`](sql-createextension.html "CREATE EXTENSION") and the
extension script sets initial privileges using the [`GRANT`](sql-grant.html
"GRANT") system. Note that the system will automatically handle recording of
the privileges during the extension script and that extension authors need
only use the `GRANT` and `REVOKE` statements in their script to have the
privileges recorded. The `privtype` column indicates if the initial privilege
was set by initdb or during a `CREATE EXTENSION` command.

Objects which have initial privileges set by initdb will have entries where
`privtype` is `'i'`, while objects which have initial privileges set by
`CREATE EXTENSION` will have entries where `privtype` is `'e'`.

**Table  53.28. `pg_init_privs` Columns**

Column Type Description  
---  
`objoid` `oid` (references any OID column) The OID of the specific object  
`classoid` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) The OID of the system catalog the object is in  
`objsubid` `int4` For a table column, this is the column number (the `objoid`
and `classoid` refer to the table itself). For all other object types, this
column is zero.  
`privtype` `char` A code defining the type of initial privilege of this
object; see text  
`initprivs` `aclitem[]` The initial access privileges; see [Section 5.7](ddl-
priv.html "5.7. Privileges") for details  
  
  

* * *

[Prev](catalog-pg-inherits.html "53.27. pg_inherits")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-language.html "53.29. pg_language")  
---|---|---  
53.27. `pg_inherits`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.29. `pg_language`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-init-privs.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

