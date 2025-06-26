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

Supported Versions: [Current](/docs/current/tutorial-sql-intro.html
"PostgreSQL 17 - 2.1. Introduction") ([17](/docs/17/tutorial-sql-intro.html
"PostgreSQL 17 - 2.1. Introduction")) / [16](/docs/16/tutorial-sql-intro.html
"PostgreSQL 16 - 2.1. Introduction") / [15](/docs/15/tutorial-sql-intro.html
"PostgreSQL 15 - 2.1. Introduction") / [14](/docs/14/tutorial-sql-intro.html
"PostgreSQL 14 - 2.1. Introduction") / [13](/docs/13/tutorial-sql-intro.html
"PostgreSQL 13 - 2.1. Introduction")

Development Versions: [18](/docs/18/tutorial-sql-intro.html "PostgreSQL 18 -
2.1. Introduction") / [devel](/docs/devel/tutorial-sql-intro.html "PostgreSQL
devel - 2.1. Introduction")

Unsupported versions: [12](/docs/12/tutorial-sql-intro.html "PostgreSQL 12 -
2.1. Introduction") / [11](/docs/11/tutorial-sql-intro.html "PostgreSQL 11 -
2.1. Introduction") / [10](/docs/10/tutorial-sql-intro.html "PostgreSQL 10 -
2.1. Introduction") / [9.6](/docs/9.6/tutorial-sql-intro.html "PostgreSQL 9.6
- 2.1. Introduction") / [9.5](/docs/9.5/tutorial-sql-intro.html "PostgreSQL
9.5 - 2.1. Introduction") / [9.4](/docs/9.4/tutorial-sql-intro.html
"PostgreSQL 9.4 - 2.1. Introduction") / [9.3](/docs/9.3/tutorial-sql-
intro.html "PostgreSQL 9.3 - 2.1. Introduction") / [9.2](/docs/9.2/tutorial-
sql-intro.html "PostgreSQL 9.2 - 2.1. Introduction") /
[9.1](/docs/9.1/tutorial-sql-intro.html "PostgreSQL 9.1 - 2.1. Introduction")
/ [9.0](/docs/9.0/tutorial-sql-intro.html "PostgreSQL 9.0 -
2.1. Introduction") / [8.4](/docs/8.4/tutorial-sql-intro.html "PostgreSQL 8.4
- 2.1. Introduction") / [8.3](/docs/8.3/tutorial-sql-intro.html "PostgreSQL
8.3 - 2.1. Introduction") / [8.2](/docs/8.2/tutorial-sql-intro.html
"PostgreSQL 8.2 - 2.1. Introduction")

__

2.1. Introduction  
---  
[Prev](tutorial-sql.html "Chapter 2. The SQL Language")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") | Chapter 2. The SQL Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](tutorial-concepts.html "2.2. Concepts")  
  
* * *

## 2.1. Introduction #

This chapter provides an overview of how to use SQL to perform simple
operations. This tutorial is only intended to give you an introduction and is
in no way a complete tutorial on SQL. Numerous books have been written on SQL,
including [[melt93]](biblio.html#MELT93 "Understanding the New SQL") and
[[date97]](biblio.html#DATE97 "A Guide to the SQL Standard"). You should be
aware that some PostgreSQL language features are extensions to the standard.

In the examples that follow, we assume that you have created a database named
`mydb`, as described in the previous chapter, and have been able to start
psql.

Examples in this manual can also be found in the PostgreSQL source
distribution in the directory `src/tutorial/`. (Binary distributions of
PostgreSQL might not provide those files.) To use those files, first change to
that directory and run make:

    
    
    $ **cd _..._ /src/tutorial**
    $ **make**
    

This creates the scripts and compiles the C files containing user-defined
functions and types. Then, to start the tutorial, do the following:

    
    
    $ **psql -s mydb**
    
    ...
    
    mydb=> **\i basics.sql**
    

The `\i` command reads in commands from the specified file. `psql`'s `-s`
option puts you in single step mode which pauses before sending each statement
to the server. The commands used in this section are in the file `basics.sql`.

* * *

[Prev](tutorial-sql.html "Chapter 2. The SQL Language")  | [Up](tutorial-sql.html "Chapter 2. The SQL Language") |  [Next](tutorial-concepts.html "2.2. Concepts")  
---|---|---  
Chapter 2. The SQL Language  | [Home](index.html "PostgreSQL 16.9 Documentation") |  2.2. Concepts  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tutorial-sql-intro.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

