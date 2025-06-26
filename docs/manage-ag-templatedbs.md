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

Supported Versions: [Current](/docs/current/manage-ag-templatedbs.html
"PostgreSQL 17 - 23.3. Template Databases") ([17](/docs/17/manage-ag-
templatedbs.html "PostgreSQL 17 - 23.3. Template Databases")) /
[16](/docs/16/manage-ag-templatedbs.html "PostgreSQL 16 - 23.3. Template
Databases") / [15](/docs/15/manage-ag-templatedbs.html "PostgreSQL 15 -
23.3. Template Databases") / [14](/docs/14/manage-ag-templatedbs.html
"PostgreSQL 14 - 23.3. Template Databases") / [13](/docs/13/manage-ag-
templatedbs.html "PostgreSQL 13 - 23.3. Template Databases")

Development Versions: [18](/docs/18/manage-ag-templatedbs.html "PostgreSQL 18
- 23.3. Template Databases") / [devel](/docs/devel/manage-ag-templatedbs.html
"PostgreSQL devel - 23.3. Template Databases")

Unsupported versions: [12](/docs/12/manage-ag-templatedbs.html "PostgreSQL 12
- 23.3. Template Databases") / [11](/docs/11/manage-ag-templatedbs.html
"PostgreSQL 11 - 23.3. Template Databases") / [10](/docs/10/manage-ag-
templatedbs.html "PostgreSQL 10 - 23.3. Template Databases") /
[9.6](/docs/9.6/manage-ag-templatedbs.html "PostgreSQL 9.6 - 23.3. Template
Databases") / [9.5](/docs/9.5/manage-ag-templatedbs.html "PostgreSQL 9.5 -
23.3. Template Databases") / [9.4](/docs/9.4/manage-ag-templatedbs.html
"PostgreSQL 9.4 - 23.3. Template Databases") / [9.3](/docs/9.3/manage-ag-
templatedbs.html "PostgreSQL 9.3 - 23.3. Template Databases") /
[9.2](/docs/9.2/manage-ag-templatedbs.html "PostgreSQL 9.2 - 23.3. Template
Databases") / [9.1](/docs/9.1/manage-ag-templatedbs.html "PostgreSQL 9.1 -
23.3. Template Databases") / [9.0](/docs/9.0/manage-ag-templatedbs.html
"PostgreSQL 9.0 - 23.3. Template Databases") / [8.4](/docs/8.4/manage-ag-
templatedbs.html "PostgreSQL 8.4 - 23.3. Template Databases") /
[8.3](/docs/8.3/manage-ag-templatedbs.html "PostgreSQL 8.3 - 23.3. Template
Databases") / [8.2](/docs/8.2/manage-ag-templatedbs.html "PostgreSQL 8.2 -
23.3. Template Databases") / [8.1](/docs/8.1/manage-ag-templatedbs.html
"PostgreSQL 8.1 - 23.3. Template Databases") / [8.0](/docs/8.0/manage-ag-
templatedbs.html "PostgreSQL 8.0 - 23.3. Template Databases") /
[7.4](/docs/7.4/manage-ag-templatedbs.html "PostgreSQL 7.4 - 23.3. Template
Databases") / [7.3](/docs/7.3/manage-ag-templatedbs.html "PostgreSQL 7.3 -
23.3. Template Databases")

__

23.3. Template Databases  
---  
[Prev](manage-ag-createdb.html "23.2. Creating a Database")  | [Up](managing-databases.html "Chapter 23. Managing Databases") | Chapter 23. Managing Databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](manage-ag-config.html "23.4. Database Configuration")  
  
* * *

## 23.3. Template Databases #

`CREATE DATABASE` actually works by copying an existing database. By default,
it copies the standard system database named `template1`. Thus that database
is the “template” from which new databases are made. If you add objects to
`template1`, these objects will be copied into subsequently created user
databases. This behavior allows site-local modifications to the standard set
of objects in databases. For example, if you install the procedural language
PL/Perl in `template1`, it will automatically be available in user databases
without any extra action being taken when those databases are created.

However, `CREATE DATABASE` does not copy database-level `GRANT` permissions
attached to the source database. The new database has default database-level
permissions.

There is a second standard system database named `template0`. This database
contains the same data as the initial contents of `template1`, that is, only
the standard objects predefined by your version of PostgreSQL. `template0`
should never be changed after the database cluster has been initialized. By
instructing `CREATE DATABASE` to copy `template0` instead of `template1`, you
can create a “pristine” user database (one where no user-defined objects exist
and where the system objects have not been altered) that contains none of the
site-local additions in `template1`. This is particularly handy when restoring
a `pg_dump` dump: the dump script should be restored in a pristine database to
ensure that one recreates the correct contents of the dumped database, without
conflicting with objects that might have been added to `template1` later on.

Another common reason for copying `template0` instead of `template1` is that
new encoding and locale settings can be specified when copying `template0`,
whereas a copy of `template1` must use the same settings it does. This is
because `template1` might contain encoding-specific or locale-specific data,
while `template0` is known not to.

To create a database by copying `template0`, use:

    
    
    CREATE DATABASE _dbname_ TEMPLATE template0;
    

from the SQL environment, or:

    
    
    createdb -T template0 _dbname_
    

from the shell.

It is possible to create additional template databases, and indeed one can
copy any database in a cluster by specifying its name as the template for
`CREATE DATABASE`. It is important to understand, however, that this is not
(yet) intended as a general-purpose “`COPY DATABASE`” facility. The principal
limitation is that no other sessions can be connected to the source database
while it is being copied. `CREATE DATABASE` will fail if any other connection
exists when it starts; during the copy operation, new connections to the
source database are prevented.

Two useful flags exist in `pg_database` for each database: the columns
`datistemplate` and `datallowconn`. `datistemplate` can be set to indicate
that a database is intended as a template for `CREATE DATABASE`. If this flag
is set, the database can be cloned by any user with `CREATEDB` privileges; if
it is not set, only superusers and the owner of the database can clone it. If
`datallowconn` is false, then no new connections to that database will be
allowed (but existing sessions are not terminated simply by setting the flag
false). The `template0` database is normally marked `datallowconn = false` to
prevent its modification. Both `template0` and `template1` should always be
marked with `datistemplate = true`.

### Note

`template1` and `template0` do not have any special status beyond the fact
that the name `template1` is the default source database name for `CREATE
DATABASE`. For example, one could drop `template1` and recreate it from
`template0` without any ill effects. This course of action might be advisable
if one has carelessly added a bunch of junk in `template1`. (To delete
`template1`, it must have `pg_database.datistemplate = false`.)

The `postgres` database is also created when a database cluster is
initialized. This database is meant as a default database for users and
applications to connect to. It is simply a copy of `template1` and can be
dropped and recreated if necessary.

* * *

[Prev](manage-ag-createdb.html "23.2. Creating a Database")  | [Up](managing-databases.html "Chapter 23. Managing Databases") |  [Next](manage-ag-config.html "23.4. Database Configuration")  
---|---|---  
23.2. Creating a Database  | [Home](index.html "PostgreSQL 16.9 Documentation") |  23.4. Database Configuration  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/manage-ag-templatedbs.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

