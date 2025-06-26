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

Supported Versions: [Current](/docs/current/tutorial-createdb.html "PostgreSQL
17 - 1.3. Creating a Database") ([17](/docs/17/tutorial-createdb.html
"PostgreSQL 17 - 1.3. Creating a Database")) / [16](/docs/16/tutorial-
createdb.html "PostgreSQL 16 - 1.3. Creating a Database") /
[15](/docs/15/tutorial-createdb.html "PostgreSQL 15 - 1.3. Creating a
Database") / [14](/docs/14/tutorial-createdb.html "PostgreSQL 14 -
1.3. Creating a Database") / [13](/docs/13/tutorial-createdb.html "PostgreSQL
13 - 1.3. Creating a Database")

Development Versions: [18](/docs/18/tutorial-createdb.html "PostgreSQL 18 -
1.3. Creating a Database") / [devel](/docs/devel/tutorial-createdb.html
"PostgreSQL devel - 1.3. Creating a Database")

Unsupported versions: [12](/docs/12/tutorial-createdb.html "PostgreSQL 12 -
1.3. Creating a Database") / [11](/docs/11/tutorial-createdb.html "PostgreSQL
11 - 1.3. Creating a Database") / [10](/docs/10/tutorial-createdb.html
"PostgreSQL 10 - 1.3. Creating a Database") / [9.6](/docs/9.6/tutorial-
createdb.html "PostgreSQL 9.6 - 1.3. Creating a Database") /
[9.5](/docs/9.5/tutorial-createdb.html "PostgreSQL 9.5 - 1.3. Creating a
Database") / [9.4](/docs/9.4/tutorial-createdb.html "PostgreSQL 9.4 -
1.3. Creating a Database") / [9.3](/docs/9.3/tutorial-createdb.html
"PostgreSQL 9.3 - 1.3. Creating a Database") / [9.2](/docs/9.2/tutorial-
createdb.html "PostgreSQL 9.2 - 1.3. Creating a Database") /
[9.1](/docs/9.1/tutorial-createdb.html "PostgreSQL 9.1 - 1.3. Creating a
Database") / [9.0](/docs/9.0/tutorial-createdb.html "PostgreSQL 9.0 -
1.3. Creating a Database") / [8.4](/docs/8.4/tutorial-createdb.html
"PostgreSQL 8.4 - 1.3. Creating a Database") / [8.3](/docs/8.3/tutorial-
createdb.html "PostgreSQL 8.3 - 1.3. Creating a Database") /
[8.2](/docs/8.2/tutorial-createdb.html "PostgreSQL 8.2 - 1.3. Creating a
Database") / [8.1](/docs/8.1/tutorial-createdb.html "PostgreSQL 8.1 -
1.3. Creating a Database") / [8.0](/docs/8.0/tutorial-createdb.html
"PostgreSQL 8.0 - 1.3. Creating a Database") / [7.4](/docs/7.4/tutorial-
createdb.html "PostgreSQL 7.4 - 1.3. Creating a Database") /
[7.3](/docs/7.3/tutorial-createdb.html "PostgreSQL 7.3 - 1.3. Creating a
Database") / [7.2](/docs/7.2/tutorial-createdb.html "PostgreSQL 7.2 -
1.3. Creating a Database")

__

1.3. Creating a Database  
---  
[Prev](tutorial-arch.html "1.2. Architectural Fundamentals")  | [Up](tutorial-start.html "Chapter 1. Getting Started") | Chapter 1. Getting Started | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-accessdb.html "1.4. Accessing a Database")  
  
* * *

## 1.3. Creating a Database #

The first test to see whether you can access the database server is to try to
create a database. A running PostgreSQL server can manage many databases.
Typically, a separate database is used for each project or for each user.

Possibly, your site administrator has already created a database for your use.
In that case you can omit this step and skip ahead to the next section.

To create a new database, in this example named `mydb`, you use the following
command:

    
    
    $ **createdb mydb**
    

If this produces no response then this step was successful and you can skip
over the remainder of this section.

If you see a message similar to:

    
    
    createdb: command not found
    

then PostgreSQL was not installed properly. Either it was not installed at all
or your shell's search path was not set to include it. Try calling the command
with an absolute path instead:

    
    
    $ **/usr/local/pgsql/bin/createdb mydb**
    

The path at your site might be different. Contact your site administrator or
check the installation instructions to correct the situation.

Another response could be this:

    
    
    createdb: error: connection to server on socket "/tmp/.s.PGSQL.5432" failed: No such file or directory
            Is the server running locally and accepting connections on that socket?
    

This means that the server was not started, or it is not listening where
`createdb` expects to contact it. Again, check the installation instructions
or consult the administrator.

Another response could be this:

    
    
    createdb: error: connection to server on socket "/tmp/.s.PGSQL.5432" failed: FATAL:  role "joe" does not exist
    

where your own login name is mentioned. This will happen if the administrator
has not created a PostgreSQL user account for you. (PostgreSQL user accounts
are distinct from operating system user accounts.) If you are the
administrator, see [Chapter 22](user-manag.html "Chapter 22. Database Roles")
for help creating accounts. You will need to become the operating system user
under which PostgreSQL was installed (usually `postgres`) to create the first
user account. It could also be that you were assigned a PostgreSQL user name
that is different from your operating system user name; in that case you need
to use the `-U` switch or set the `PGUSER` environment variable to specify
your PostgreSQL user name.

If you have a user account but it does not have the privileges required to
create a database, you will see the following:

    
    
    createdb: error: database creation failed: ERROR:  permission denied to create database
    

Not every user has authorization to create new databases. If PostgreSQL
refuses to create databases for you then the site administrator needs to grant
you permission to create databases. Consult your site administrator if this
occurs. If you installed PostgreSQL yourself then you should log in for the
purposes of this tutorial under the user account that you started the server
as. [1]

You can also create databases with other names. PostgreSQL allows you to
create any number of databases at a given site. Database names must have an
alphabetic first character and are limited to 63 bytes in length. A convenient
choice is to create a database with the same name as your current user name.
Many tools assume that database name as the default, so it can save you some
typing. To create that database, simply type:

    
    
    $ **createdb**
    

If you do not want to use your database anymore you can remove it. For
example, if you are the owner (creator) of the database `mydb`, you can
destroy it using the following command:

    
    
    $ **dropdb mydb**
    

(For this command, the database name does not default to the user account
name. You always need to specify it.) This action physically removes all files
associated with the database and cannot be undone, so this should only be done
with a great deal of forethought.

More about `createdb` and `dropdb` can be found in [createdb](app-
createdb.html "createdb") and [dropdb](app-dropdb.html "dropdb") respectively.

  

* * *

[1] As an explanation for why this works: PostgreSQL user names are separate
from operating system user accounts. When you connect to a database, you can
choose what PostgreSQL user name to connect as; if you don't, it will default
to the same name as your current operating system account. As it happens,
there will always be a PostgreSQL user account that has the same name as the
operating system user that started the server, and it also happens that that
user always has permission to create databases. Instead of logging in as that
user you can also specify the `-U` option everywhere to select a PostgreSQL
user name to connect as.

* * *

[Prev](tutorial-arch.html "1.2. Architectural Fundamentals")  | [Up](tutorial-start.html "Chapter 1. Getting Started") |  [Next](tutorial-accessdb.html "1.4. Accessing a Database")  
---|---|---  
1.2. Architectural Fundamentals  | [Home](index.html "PostgreSQL 16.9 Documentation") |  1.4. Accessing a Database  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-createdb.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

