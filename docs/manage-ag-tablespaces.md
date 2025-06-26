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

Supported Versions: [Current](/docs/current/manage-ag-tablespaces.html
"PostgreSQL 17 - 23.6. Tablespaces") ([17](/docs/17/manage-ag-tablespaces.html
"PostgreSQL 17 - 23.6. Tablespaces")) / [16](/docs/16/manage-ag-
tablespaces.html "PostgreSQL 16 - 23.6. Tablespaces") / [15](/docs/15/manage-
ag-tablespaces.html "PostgreSQL 15 - 23.6. Tablespaces") /
[14](/docs/14/manage-ag-tablespaces.html "PostgreSQL 14 - 23.6. Tablespaces")
/ [13](/docs/13/manage-ag-tablespaces.html "PostgreSQL 13 -
23.6. Tablespaces")

Development Versions: [18](/docs/18/manage-ag-tablespaces.html "PostgreSQL 18
- 23.6. Tablespaces") / [devel](/docs/devel/manage-ag-tablespaces.html
"PostgreSQL devel - 23.6. Tablespaces")

Unsupported versions: [12](/docs/12/manage-ag-tablespaces.html "PostgreSQL 12
- 23.6. Tablespaces") / [11](/docs/11/manage-ag-tablespaces.html "PostgreSQL
11 - 23.6. Tablespaces") / [10](/docs/10/manage-ag-tablespaces.html
"PostgreSQL 10 - 23.6. Tablespaces") / [9.6](/docs/9.6/manage-ag-
tablespaces.html "PostgreSQL 9.6 - 23.6. Tablespaces") /
[9.5](/docs/9.5/manage-ag-tablespaces.html "PostgreSQL 9.5 -
23.6. Tablespaces") / [9.4](/docs/9.4/manage-ag-tablespaces.html "PostgreSQL
9.4 - 23.6. Tablespaces") / [9.3](/docs/9.3/manage-ag-tablespaces.html
"PostgreSQL 9.3 - 23.6. Tablespaces") / [9.2](/docs/9.2/manage-ag-
tablespaces.html "PostgreSQL 9.2 - 23.6. Tablespaces") /
[9.1](/docs/9.1/manage-ag-tablespaces.html "PostgreSQL 9.1 -
23.6. Tablespaces") / [9.0](/docs/9.0/manage-ag-tablespaces.html "PostgreSQL
9.0 - 23.6. Tablespaces") / [8.4](/docs/8.4/manage-ag-tablespaces.html
"PostgreSQL 8.4 - 23.6. Tablespaces") / [8.3](/docs/8.3/manage-ag-
tablespaces.html "PostgreSQL 8.3 - 23.6. Tablespaces") /
[8.2](/docs/8.2/manage-ag-tablespaces.html "PostgreSQL 8.2 -
23.6. Tablespaces") / [8.1](/docs/8.1/manage-ag-tablespaces.html "PostgreSQL
8.1 - 23.6. Tablespaces") / [8.0](/docs/8.0/manage-ag-tablespaces.html
"PostgreSQL 8.0 - 23.6. Tablespaces")

__

23.6. Tablespaces  
---  
[Prev](manage-ag-dropdb.html "23.5. Destroying a Database")  | [Up](managing-databases.html "Chapter 23. Managing Databases") | Chapter 23. Managing Databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](charset.html "Chapter 24. Localization")  
  
* * *

## 23.6. Tablespaces #

Tablespaces in PostgreSQL allow database administrators to define locations in
the file system where the files representing database objects can be stored.
Once created, a tablespace can be referred to by name when creating database
objects.

By using tablespaces, an administrator can control the disk layout of a
PostgreSQL installation. This is useful in at least two ways. First, if the
partition or volume on which the cluster was initialized runs out of space and
cannot be extended, a tablespace can be created on a different partition and
used until the system can be reconfigured.

Second, tablespaces allow an administrator to use knowledge of the usage
pattern of database objects to optimize performance. For example, an index
which is very heavily used can be placed on a very fast, highly available
disk, such as an expensive solid state device. At the same time a table
storing archived data which is rarely used or not performance critical could
be stored on a less expensive, slower disk system.

### Warning

Even though located outside the main PostgreSQL data directory, tablespaces
are an integral part of the database cluster and _cannot_ be treated as an
autonomous collection of data files. They are dependent on metadata contained
in the main data directory, and therefore cannot be attached to a different
database cluster or backed up individually. Similarly, if you lose a
tablespace (file deletion, disk failure, etc.), the database cluster might
become unreadable or unable to start. Placing a tablespace on a temporary file
system like a RAM disk risks the reliability of the entire cluster.

To define a tablespace, use the [CREATE TABLESPACE](sql-createtablespace.html
"CREATE TABLESPACE") command, for example::

    
    
    CREATE TABLESPACE fastspace LOCATION '/ssd1/postgresql/data';
    

The location must be an existing, empty directory that is owned by the
PostgreSQL operating system user. All objects subsequently created within the
tablespace will be stored in files underneath this directory. The location
must not be on removable or transient storage, as the cluster might fail to
function if the tablespace is missing or lost.

### Note

There is usually not much point in making more than one tablespace per logical
file system, since you cannot control the location of individual files within
a logical file system. However, PostgreSQL does not enforce any such
limitation, and indeed it is not directly aware of the file system boundaries
on your system. It just stores files in the directories you tell it to use.

Creation of the tablespace itself must be done as a database superuser, but
after that you can allow ordinary database users to use it. To do that, grant
them the `CREATE` privilege on it.

Tables, indexes, and entire databases can be assigned to particular
tablespaces. To do so, a user with the `CREATE` privilege on a given
tablespace must pass the tablespace name as a parameter to the relevant
command. For example, the following creates a table in the tablespace
`space1`:

    
    
    CREATE TABLE foo(i int) TABLESPACE space1;
    

Alternatively, use the [default_tablespace](runtime-config-client.html#GUC-
DEFAULT-TABLESPACE) parameter:

    
    
    SET default_tablespace = space1;
    CREATE TABLE foo(i int);
    

When `default_tablespace` is set to anything but an empty string, it supplies
an implicit `TABLESPACE` clause for `CREATE TABLE` and `CREATE INDEX` commands
that do not have an explicit one.

There is also a [temp_tablespaces](runtime-config-client.html#GUC-TEMP-
TABLESPACES) parameter, which determines the placement of temporary tables and
indexes, as well as temporary files that are used for purposes such as sorting
large data sets. This can be a list of tablespace names, rather than only one,
so that the load associated with temporary objects can be spread over multiple
tablespaces. A random member of the list is picked each time a temporary
object is to be created.

The tablespace associated with a database is used to store the system catalogs
of that database. Furthermore, it is the default tablespace used for tables,
indexes, and temporary files created within the database, if no `TABLESPACE`
clause is given and no other selection is specified by `default_tablespace` or
`temp_tablespaces` (as appropriate). If a database is created without
specifying a tablespace for it, it uses the same tablespace as the template
database it is copied from.

Two tablespaces are automatically created when the database cluster is
initialized. The `pg_global` tablespace is used for shared system catalogs.
The `pg_default` tablespace is the default tablespace of the `template1` and
`template0` databases (and, therefore, will be the default tablespace for
other databases as well, unless overridden by a `TABLESPACE` clause in `CREATE
DATABASE`).

Once created, a tablespace can be used from any database, provided the
requesting user has sufficient privilege. This means that a tablespace cannot
be dropped until all objects in all databases using the tablespace have been
removed.

To remove an empty tablespace, use the [DROP TABLESPACE](sql-
droptablespace.html "DROP TABLESPACE") command.

To determine the set of existing tablespaces, examine the
[`pg_tablespace`](catalog-pg-tablespace.html "53.56. pg_tablespace") system
catalog, for example

    
    
    SELECT spcname FROM pg_tablespace;
    

The [psql](app-psql.html "psql") program's `\db` meta-command is also useful
for listing the existing tablespaces.

The directory `$PGDATA/pg_tblspc` contains symbolic links that point to each
of the non-built-in tablespaces defined in the cluster. Although not
recommended, it is possible to adjust the tablespace layout by hand by
redefining these links. Under no circumstances perform this operation while
the server is running. Note that in PostgreSQL 9.1 and earlier you will also
need to update the `pg_tablespace` catalog with the new locations. (If you do
not, `pg_dump` will continue to output the old tablespace locations.)

* * *

[Prev](manage-ag-dropdb.html "23.5. Destroying a Database")  | [Up](managing-databases.html "Chapter 23. Managing Databases") |  [Next](charset.html "Chapter 24. Localization")  
---|---|---  
23.5. Destroying a Database  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 24. Localization  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/manage-ag-tablespaces.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

