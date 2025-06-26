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

Supported Versions: [Current](/docs/current/tutorial-accessdb.html "PostgreSQL
17 - 1.4. Accessing a Database") ([17](/docs/17/tutorial-accessdb.html
"PostgreSQL 17 - 1.4. Accessing a Database")) / [16](/docs/16/tutorial-
accessdb.html "PostgreSQL 16 - 1.4. Accessing a Database") /
[15](/docs/15/tutorial-accessdb.html "PostgreSQL 15 - 1.4. Accessing a
Database") / [14](/docs/14/tutorial-accessdb.html "PostgreSQL 14 -
1.4. Accessing a Database") / [13](/docs/13/tutorial-accessdb.html "PostgreSQL
13 - 1.4. Accessing a Database")

Development Versions: [18](/docs/18/tutorial-accessdb.html "PostgreSQL 18 -
1.4. Accessing a Database") / [devel](/docs/devel/tutorial-accessdb.html
"PostgreSQL devel - 1.4. Accessing a Database")

Unsupported versions: [12](/docs/12/tutorial-accessdb.html "PostgreSQL 12 -
1.4. Accessing a Database") / [11](/docs/11/tutorial-accessdb.html "PostgreSQL
11 - 1.4. Accessing a Database") / [10](/docs/10/tutorial-accessdb.html
"PostgreSQL 10 - 1.4. Accessing a Database") / [9.6](/docs/9.6/tutorial-
accessdb.html "PostgreSQL 9.6 - 1.4. Accessing a Database") /
[9.5](/docs/9.5/tutorial-accessdb.html "PostgreSQL 9.5 - 1.4. Accessing a
Database") / [9.4](/docs/9.4/tutorial-accessdb.html "PostgreSQL 9.4 -
1.4. Accessing a Database") / [9.3](/docs/9.3/tutorial-accessdb.html
"PostgreSQL 9.3 - 1.4. Accessing a Database") / [9.2](/docs/9.2/tutorial-
accessdb.html "PostgreSQL 9.2 - 1.4. Accessing a Database") /
[9.1](/docs/9.1/tutorial-accessdb.html "PostgreSQL 9.1 - 1.4. Accessing a
Database") / [9.0](/docs/9.0/tutorial-accessdb.html "PostgreSQL 9.0 -
1.4. Accessing a Database") / [8.4](/docs/8.4/tutorial-accessdb.html
"PostgreSQL 8.4 - 1.4. Accessing a Database") / [8.3](/docs/8.3/tutorial-
accessdb.html "PostgreSQL 8.3 - 1.4. Accessing a Database") /
[8.2](/docs/8.2/tutorial-accessdb.html "PostgreSQL 8.2 - 1.4. Accessing a
Database") / [8.1](/docs/8.1/tutorial-accessdb.html "PostgreSQL 8.1 -
1.4. Accessing a Database") / [8.0](/docs/8.0/tutorial-accessdb.html
"PostgreSQL 8.0 - 1.4. Accessing a Database") / [7.4](/docs/7.4/tutorial-
accessdb.html "PostgreSQL 7.4 - 1.4. Accessing a Database") /
[7.3](/docs/7.3/tutorial-accessdb.html "PostgreSQL 7.3 - 1.4. Accessing a
Database") / [7.2](/docs/7.2/tutorial-accessdb.html "PostgreSQL 7.2 -
1.4. Accessing a Database")

__

1.4. Accessing a Database  
---  
[Prev](tutorial-createdb.html "1.3. Creating a Database")  | [Up](tutorial-start.html "Chapter 1. Getting Started") | Chapter 1. Getting Started | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-sql.html "Chapter 2. The SQL Language")  
  
* * *

## 1.4. Accessing a Database #

Once you have created a database, you can access it by:

  * Running the PostgreSQL interactive terminal program, called _psql_ , which allows you to interactively enter, edit, and execute SQL commands.

  * Using an existing graphical frontend tool like pgAdmin or an office suite with ODBC or JDBC support to create and manipulate a database. These possibilities are not covered in this tutorial.

  * Writing a custom application, using one of the several available language bindings. These possibilities are discussed further in [Part IV](client-interfaces.html "Part IV. Client Interfaces").

You probably want to start up `psql` to try the examples in this tutorial. It
can be activated for the `mydb` database by typing the command:

    
    
    $ **psql mydb**
    

If you do not supply the database name then it will default to your user
account name. You already discovered this scheme in the previous section using
`createdb`.

In `psql`, you will be greeted with the following message:

    
    
    psql (16.9)
    Type "help" for help.
    
    mydb=>
    

The last line could also be:

    
    
    mydb=#
    

That would mean you are a database superuser, which is most likely the case if
you installed the PostgreSQL instance yourself. Being a superuser means that
you are not subject to access controls. For the purposes of this tutorial that
is not important.

If you encounter problems starting `psql` then go back to the previous
section. The diagnostics of `createdb` and `psql` are similar, and if the
former worked the latter should work as well.

The last line printed out by `psql` is the prompt, and it indicates that
`psql` is listening to you and that you can type SQL queries into a work space
maintained by `psql`. Try out these commands:

    
    
    mydb=> **SELECT version();**
                                             version
    -------------------------------------------------------------------​-----------------------
     PostgreSQL 16.9 on x86_64-pc-linux-gnu, compiled by gcc (Debian 4.9.2-10) 4.9.2, 64-bit
    (1 row)
    
    mydb=> **SELECT current_date;**
        date
    ------------
     2016-01-07
    (1 row)
    
    mydb=> **SELECT 2 + 2;**
     ?column?
    ----------
            4
    (1 row)
    

The `psql` program has a number of internal commands that are not SQL
commands. They begin with the backslash character, “`\`”. For example, you can
get help on the syntax of various PostgreSQL SQL commands by typing:

    
    
    mydb=> **\h**
    

To get out of `psql`, type:

    
    
    mydb=> **\q**
    

and `psql` will quit and return you to your command shell. (For more internal
commands, type `\?` at the `psql` prompt.) The full capabilities of `psql` are
documented in [psql](app-psql.html "psql"). In this tutorial we will not use
these features explicitly, but you can use them yourself when it is helpful.

* * *

[Prev](tutorial-createdb.html "1.3. Creating a Database")  | [Up](tutorial-start.html "Chapter 1. Getting Started") |  [Next](tutorial-sql.html "Chapter 2. The SQL Language")  
---|---|---  
1.3. Creating a Database  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 2. The SQL Language  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-accessdb.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

