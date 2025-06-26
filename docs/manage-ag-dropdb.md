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

Supported Versions: [Current](/docs/current/manage-ag-dropdb.html "PostgreSQL
17 - 23.5. Destroying a Database") ([17](/docs/17/manage-ag-dropdb.html
"PostgreSQL 17 - 23.5. Destroying a Database")) / [16](/docs/16/manage-ag-
dropdb.html "PostgreSQL 16 - 23.5. Destroying a Database") /
[15](/docs/15/manage-ag-dropdb.html "PostgreSQL 15 - 23.5. Destroying a
Database") / [14](/docs/14/manage-ag-dropdb.html "PostgreSQL 14 -
23.5. Destroying a Database") / [13](/docs/13/manage-ag-dropdb.html
"PostgreSQL 13 - 23.5. Destroying a Database")

Development Versions: [18](/docs/18/manage-ag-dropdb.html "PostgreSQL 18 -
23.5. Destroying a Database") / [devel](/docs/devel/manage-ag-dropdb.html
"PostgreSQL devel - 23.5. Destroying a Database")

Unsupported versions: [12](/docs/12/manage-ag-dropdb.html "PostgreSQL 12 -
23.5. Destroying a Database") / [11](/docs/11/manage-ag-dropdb.html
"PostgreSQL 11 - 23.5. Destroying a Database") / [10](/docs/10/manage-ag-
dropdb.html "PostgreSQL 10 - 23.5. Destroying a Database") /
[9.6](/docs/9.6/manage-ag-dropdb.html "PostgreSQL 9.6 - 23.5. Destroying a
Database") / [9.5](/docs/9.5/manage-ag-dropdb.html "PostgreSQL 9.5 -
23.5. Destroying a Database") / [9.4](/docs/9.4/manage-ag-dropdb.html
"PostgreSQL 9.4 - 23.5. Destroying a Database") / [9.3](/docs/9.3/manage-ag-
dropdb.html "PostgreSQL 9.3 - 23.5. Destroying a Database") /
[9.2](/docs/9.2/manage-ag-dropdb.html "PostgreSQL 9.2 - 23.5. Destroying a
Database") / [9.1](/docs/9.1/manage-ag-dropdb.html "PostgreSQL 9.1 -
23.5. Destroying a Database") / [9.0](/docs/9.0/manage-ag-dropdb.html
"PostgreSQL 9.0 - 23.5. Destroying a Database") / [8.4](/docs/8.4/manage-ag-
dropdb.html "PostgreSQL 8.4 - 23.5. Destroying a Database") /
[8.3](/docs/8.3/manage-ag-dropdb.html "PostgreSQL 8.3 - 23.5. Destroying a
Database") / [8.2](/docs/8.2/manage-ag-dropdb.html "PostgreSQL 8.2 -
23.5. Destroying a Database") / [8.1](/docs/8.1/manage-ag-dropdb.html
"PostgreSQL 8.1 - 23.5. Destroying a Database") / [8.0](/docs/8.0/manage-ag-
dropdb.html "PostgreSQL 8.0 - 23.5. Destroying a Database") /
[7.4](/docs/7.4/manage-ag-dropdb.html "PostgreSQL 7.4 - 23.5. Destroying a
Database") / [7.3](/docs/7.3/manage-ag-dropdb.html "PostgreSQL 7.3 -
23.5. Destroying a Database") / [7.2](/docs/7.2/manage-ag-dropdb.html
"PostgreSQL 7.2 - 23.5. Destroying a Database") / [7.1](/docs/7.1/manage-ag-
dropdb.html "PostgreSQL 7.1 - 23.5. Destroying a Database")

__

23.5. Destroying a Database  
---  
[Prev](manage-ag-config.html "23.4. Database Configuration")  | [Up](managing-databases.html "Chapter 23. Managing Databases") | Chapter 23. Managing Databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](manage-ag-tablespaces.html "23.6. Tablespaces")  
  
* * *

## 23.5. Destroying a Database #

Databases are destroyed with the command [DROP DATABASE](sql-dropdatabase.html
"DROP DATABASE"):

    
    
    DROP DATABASE _name_ ;
    

Only the owner of the database, or a superuser, can drop a database. Dropping
a database removes all objects that were contained within the database. The
destruction of a database cannot be undone.

You cannot execute the `DROP DATABASE` command while connected to the victim
database. You can, however, be connected to any other database, including the
`template1` database. `template1` would be the only option for dropping the
last user database of a given cluster.

For convenience, there is also a shell program to drop databases,
[dropdb](app-dropdb.html "dropdb"):

    
    
    dropdb _dbname_
    

(Unlike `createdb`, it is not the default action to drop the database with the
current user name.)

* * *

[Prev](manage-ag-config.html "23.4. Database Configuration")  | [Up](managing-databases.html "Chapter 23. Managing Databases") |  [Next](manage-ag-tablespaces.html "23.6. Tablespaces")  
---|---|---  
23.4. Database Configuration  | [Home](index.html "PostgreSQL 16.9 Documentation") |  23.6. Tablespaces  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/manage-ag-dropdb.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

