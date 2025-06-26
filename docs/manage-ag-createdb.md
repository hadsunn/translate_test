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

Supported Versions: [Current](/docs/current/manage-ag-createdb.html
"PostgreSQL 17 - 23.2. Creating a Database") ([17](/docs/17/manage-ag-
createdb.html "PostgreSQL 17 - 23.2. Creating a Database")) /
[16](/docs/16/manage-ag-createdb.html "PostgreSQL 16 - 23.2. Creating a
Database") / [15](/docs/15/manage-ag-createdb.html "PostgreSQL 15 -
23.2. Creating a Database") / [14](/docs/14/manage-ag-createdb.html
"PostgreSQL 14 - 23.2. Creating a Database") / [13](/docs/13/manage-ag-
createdb.html "PostgreSQL 13 - 23.2. Creating a Database")

Development Versions: [18](/docs/18/manage-ag-createdb.html "PostgreSQL 18 -
23.2. Creating a Database") / [devel](/docs/devel/manage-ag-createdb.html
"PostgreSQL devel - 23.2. Creating a Database")

Unsupported versions: [12](/docs/12/manage-ag-createdb.html "PostgreSQL 12 -
23.2. Creating a Database") / [11](/docs/11/manage-ag-createdb.html
"PostgreSQL 11 - 23.2. Creating a Database") / [10](/docs/10/manage-ag-
createdb.html "PostgreSQL 10 - 23.2. Creating a Database") /
[9.6](/docs/9.6/manage-ag-createdb.html "PostgreSQL 9.6 - 23.2. Creating a
Database") / [9.5](/docs/9.5/manage-ag-createdb.html "PostgreSQL 9.5 -
23.2. Creating a Database") / [9.4](/docs/9.4/manage-ag-createdb.html
"PostgreSQL 9.4 - 23.2. Creating a Database") / [9.3](/docs/9.3/manage-ag-
createdb.html "PostgreSQL 9.3 - 23.2. Creating a Database") /
[9.2](/docs/9.2/manage-ag-createdb.html "PostgreSQL 9.2 - 23.2. Creating a
Database") / [9.1](/docs/9.1/manage-ag-createdb.html "PostgreSQL 9.1 -
23.2. Creating a Database") / [9.0](/docs/9.0/manage-ag-createdb.html
"PostgreSQL 9.0 - 23.2. Creating a Database") / [8.4](/docs/8.4/manage-ag-
createdb.html "PostgreSQL 8.4 - 23.2. Creating a Database") /
[8.3](/docs/8.3/manage-ag-createdb.html "PostgreSQL 8.3 - 23.2. Creating a
Database") / [8.2](/docs/8.2/manage-ag-createdb.html "PostgreSQL 8.2 -
23.2. Creating a Database") / [8.1](/docs/8.1/manage-ag-createdb.html
"PostgreSQL 8.1 - 23.2. Creating a Database") / [8.0](/docs/8.0/manage-ag-
createdb.html "PostgreSQL 8.0 - 23.2. Creating a Database") /
[7.4](/docs/7.4/manage-ag-createdb.html "PostgreSQL 7.4 - 23.2. Creating a
Database") / [7.3](/docs/7.3/manage-ag-createdb.html "PostgreSQL 7.3 -
23.2. Creating a Database")

__

23.2. Creating a Database  
---  
[Prev](manage-ag-overview.html "23.1. Overview")  | [Up](managing-databases.html "Chapter 23. Managing Databases") | Chapter 23. Managing Databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](manage-ag-templatedbs.html "23.3. Template Databases")  
  
* * *

## 23.2. Creating a Database #

In order to create a database, the PostgreSQL server must be up and running
(see [Section 19.3](server-start.html "19.3. Starting the Database Server")).

Databases are created with the SQL command [CREATE DATABASE](sql-
createdatabase.html "CREATE DATABASE"):

    
    
    CREATE DATABASE _name_ ;
    

where _`name`_ follows the usual rules for SQL identifiers. The current role
automatically becomes the owner of the new database. It is the privilege of
the owner of a database to remove it later (which also removes all the objects
in it, even if they have a different owner).

The creation of databases is a restricted operation. See [Section 22.2](role-
attributes.html "22.2. Role Attributes") for how to grant permission.

Since you need to be connected to the database server in order to execute the
`CREATE DATABASE` command, the question remains how the _first_ database at
any given site can be created. The first database is always created by the
`initdb` command when the data storage area is initialized. (See [Section
19.2](creating-cluster.html "19.2. Creating a Database Cluster").) This
database is called `postgres`. So to create the first “ordinary” database you
can connect to `postgres`.

Two additional databases, `template1` and `template0`, are also created during
database cluster initialization. Whenever a new database is created within the
cluster, `template1` is essentially cloned. This means that any changes you
make in `template1` are propagated to all subsequently created databases.
Because of this, avoid creating objects in `template1` unless you want them
propagated to every newly created database. `template0` is meant as a pristine
copy of the original contents of `template1`. It can be cloned instead of
`template1` when it is important to make a database without any such site-
local additions. More details appear in [Section 23.3](manage-ag-
templatedbs.html "23.3. Template Databases").

As a convenience, there is a program you can execute from the shell to create
new databases, `createdb`.

    
    
    createdb _dbname_
    

`createdb` does no magic. It connects to the `postgres` database and issues
the `CREATE DATABASE` command, exactly as described above. The [createdb](app-
createdb.html "createdb") reference page contains the invocation details. Note
that `createdb` without any arguments will create a database with the current
user name.

### Note

[Chapter 21](client-authentication.html "Chapter 21. Client Authentication")
contains information about how to restrict who can connect to a given
database.

Sometimes you want to create a database for someone else, and have them become
the owner of the new database, so they can configure and manage it themselves.
To achieve that, use one of the following commands:

    
    
    CREATE DATABASE _dbname_ OWNER _rolename_ ;
    

from the SQL environment, or:

    
    
    createdb -O _rolename_ _dbname_
    

from the shell. Only the superuser is allowed to create a database for someone
else (that is, for a role you are not a member of).

* * *

[Prev](manage-ag-overview.html "23.1. Overview")  | [Up](managing-databases.html "Chapter 23. Managing Databases") |  [Next](manage-ag-templatedbs.html "23.3. Template Databases")  
---|---|---  
23.1. Overview  | [Home](index.html "PostgreSQL 16.9 Documentation") |  23.3. Template Databases  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/manage-ag-createdb.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

