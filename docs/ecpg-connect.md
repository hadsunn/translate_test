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

Supported Versions: [Current](/docs/current/ecpg-connect.html "PostgreSQL 17 -
36.2. Managing Database Connections") ([17](/docs/17/ecpg-connect.html
"PostgreSQL 17 - 36.2. Managing Database Connections")) / [16](/docs/16/ecpg-
connect.html "PostgreSQL 16 - 36.2. Managing Database Connections") /
[15](/docs/15/ecpg-connect.html "PostgreSQL 15 - 36.2. Managing Database
Connections") / [14](/docs/14/ecpg-connect.html "PostgreSQL 14 -
36.2. Managing Database Connections") / [13](/docs/13/ecpg-connect.html
"PostgreSQL 13 - 36.2. Managing Database Connections")

Development Versions: [18](/docs/18/ecpg-connect.html "PostgreSQL 18 -
36.2. Managing Database Connections") / [devel](/docs/devel/ecpg-connect.html
"PostgreSQL devel - 36.2. Managing Database Connections")

Unsupported versions: [12](/docs/12/ecpg-connect.html "PostgreSQL 12 -
36.2. Managing Database Connections") / [11](/docs/11/ecpg-connect.html
"PostgreSQL 11 - 36.2. Managing Database Connections") / [10](/docs/10/ecpg-
connect.html "PostgreSQL 10 - 36.2. Managing Database Connections") /
[9.6](/docs/9.6/ecpg-connect.html "PostgreSQL 9.6 - 36.2. Managing Database
Connections") / [9.5](/docs/9.5/ecpg-connect.html "PostgreSQL 9.5 -
36.2. Managing Database Connections") / [9.4](/docs/9.4/ecpg-connect.html
"PostgreSQL 9.4 - 36.2. Managing Database Connections") /
[9.3](/docs/9.3/ecpg-connect.html "PostgreSQL 9.3 - 36.2. Managing Database
Connections") / [9.2](/docs/9.2/ecpg-connect.html "PostgreSQL 9.2 -
36.2. Managing Database Connections") / [9.1](/docs/9.1/ecpg-connect.html
"PostgreSQL 9.1 - 36.2. Managing Database Connections") /
[9.0](/docs/9.0/ecpg-connect.html "PostgreSQL 9.0 - 36.2. Managing Database
Connections") / [8.4](/docs/8.4/ecpg-connect.html "PostgreSQL 8.4 -
36.2. Managing Database Connections") / [8.3](/docs/8.3/ecpg-connect.html
"PostgreSQL 8.3 - 36.2. Managing Database Connections") /
[8.2](/docs/8.2/ecpg-connect.html "PostgreSQL 8.2 - 36.2. Managing Database
Connections") / [8.1](/docs/8.1/ecpg-connect.html "PostgreSQL 8.1 -
36.2. Managing Database Connections") / [8.0](/docs/8.0/ecpg-connect.html
"PostgreSQL 8.0 - 36.2. Managing Database Connections") /
[7.4](/docs/7.4/ecpg-connect.html "PostgreSQL 7.4 - 36.2. Managing Database
Connections") / [7.3](/docs/7.3/ecpg-connect.html "PostgreSQL 7.3 -
36.2. Managing Database Connections")

__

36.2. Managing Database Connections  
---  
[Prev](ecpg-concept.html "36.1. The Concept")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") | Chapter 36. ECPG — Embedded SQL in C | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-commands.html "36.3. Running SQL Commands")  
  
* * *

## 36.2. Managing Database Connections #

[36.2.1. Connecting to the Database Server](ecpg-connect.html#ECPG-CONNECTING)

[36.2.2. Choosing a Connection](ecpg-connect.html#ECPG-SET-CONNECTION)

[36.2.3. Closing a Connection](ecpg-connect.html#ECPG-DISCONNECT)

This section describes how to open, close, and switch database connections.

### 36.2.1. Connecting to the Database Server #

One connects to a database using the following statement:

    
    
    EXEC SQL CONNECT TO _target_ [AS _connection-name_] [USER _user-name_];
    

The _`target`_ can be specified in the following ways:

  * `_`dbname`_[@_`hostname`_][:_`port`_]`
  * `tcp:postgresql://_`hostname`_[:_`port`_][/_`dbname`_][?_`options`_]`
  * `unix:postgresql://localhost[:_`port`_][/_`dbname`_][?_`options`_]`
  * an SQL string literal containing one of the above forms
  * a reference to a character variable containing one of the above forms (see examples)
  * `DEFAULT`

The connection target `DEFAULT` initiates a connection to the default database
under the default user name. No separate user name or connection name can be
specified in that case.

If you specify the connection target directly (that is, not as a string
literal or variable reference), then the components of the target are passed
through normal SQL parsing; this means that, for example, the _`hostname`_
must look like one or more SQL identifiers separated by dots, and those
identifiers will be case-folded unless double-quoted. Values of any
_`options`_ must be SQL identifiers, integers, or variable references. Of
course, you can put nearly anything into an SQL identifier by double-quoting
it. In practice, it is probably less error-prone to use a (single-quoted)
string literal or a variable reference than to write the connection target
directly.

There are also different ways to specify the user name:

  * `_`username`_`
  * `_`username`_ /_`password`_`
  * `_`username`_ IDENTIFIED BY _`password`_`
  * `_`username`_ USING _`password`_`

As above, the parameters _`username`_ and _`password`_ can be an SQL
identifier, an SQL string literal, or a reference to a character variable.

If the connection target includes any _`options`_ , those consist of
`_`keyword`_ =_`value`_` specifications separated by ampersands (`&`). The
allowed key words are the same ones recognized by libpq (see [Section
34.1.2](libpq-connect.html#LIBPQ-PARAMKEYWORDS "34.1.2. Parameter Key
Words")). Spaces are ignored before any _`keyword`_ or _`value`_ , though not
within or after one. Note that there is no way to write `&` within a
_`value`_.

Notice that when specifying a socket connection (with the `unix:` prefix), the
host name must be exactly `localhost`. To select a non-default socket
directory, write the directory's pathname as the value of a `host` option in
the _`options`_ part of the target.

The _`connection-name`_ is used to handle multiple connections in one program.
It can be omitted if a program uses only one connection. The most recently
opened connection becomes the current connection, which is used by default
when an SQL statement is to be executed (see later in this chapter).

Here are some examples of `CONNECT` statements:

    
    
    EXEC SQL CONNECT TO mydb@sql.mydomain.com;
    
    EXEC SQL CONNECT TO tcp:postgresql://sql.mydomain.com/mydb AS myconnection USER john;
    
    EXEC SQL BEGIN DECLARE SECTION;
    const char *target = "mydb@sql.mydomain.com";
    const char *user = "john";
    const char *passwd = "secret";
    EXEC SQL END DECLARE SECTION;
     ...
    EXEC SQL CONNECT TO :target USER :user USING :passwd;
    /* or EXEC SQL CONNECT TO :target USER :user/:passwd; */
    

The last example makes use of the feature referred to above as character
variable references. You will see in later sections how C variables can be
used in SQL statements when you prefix them with a colon.

Be advised that the format of the connection target is not specified in the
SQL standard. So if you want to develop portable applications, you might want
to use something based on the last example above to encapsulate the connection
target string somewhere.

If untrusted users have access to a database that has not adopted a [secure
schema usage pattern](ddl-schemas.html#DDL-SCHEMAS-PATTERNS "5.9.6. Usage
Patterns"), begin each session by removing publicly-writable schemas from
`search_path`. For example, add `options=-c search_path=` to `_`options`_`, or
issue `EXEC SQL SELECT pg_catalog.set_config('search_path', '', false);` after
connecting. This consideration is not specific to ECPG; it applies to every
interface for executing arbitrary SQL commands.

### 36.2.2. Choosing a Connection #

SQL statements in embedded SQL programs are by default executed on the current
connection, that is, the most recently opened one. If an application needs to
manage multiple connections, then there are three ways to handle this.

The first option is to explicitly choose a connection for each SQL statement,
for example:

    
    
    EXEC SQL AT _connection-name_ SELECT ...;
    

This option is particularly suitable if the application needs to use several
connections in mixed order.

If your application uses multiple threads of execution, they cannot share a
connection concurrently. You must either explicitly control access to the
connection (using mutexes) or use a connection for each thread.

The second option is to execute a statement to switch the current connection.
That statement is:

    
    
    EXEC SQL SET CONNECTION _connection-name_ ;
    

This option is particularly convenient if many statements are to be executed
on the same connection.

Here is an example program managing multiple database connections:

    
    
    #include <stdio.h>
    
    EXEC SQL BEGIN DECLARE SECTION;
        char dbname[1024];
    EXEC SQL END DECLARE SECTION;
    
    int
    main()
    {
        EXEC SQL CONNECT TO testdb1 AS con1 USER testuser;
        EXEC SQL SELECT pg_catalog.set_config('search_path', '', false); EXEC SQL COMMIT;
        EXEC SQL CONNECT TO testdb2 AS con2 USER testuser;
        EXEC SQL SELECT pg_catalog.set_config('search_path', '', false); EXEC SQL COMMIT;
        EXEC SQL CONNECT TO testdb3 AS con3 USER testuser;
        EXEC SQL SELECT pg_catalog.set_config('search_path', '', false); EXEC SQL COMMIT;
    
        /* This query would be executed in the last opened database "testdb3". */
        EXEC SQL SELECT current_database() INTO :dbname;
        printf("current=%s (should be testdb3)\n", dbname);
    
        /* Using "AT" to run a query in "testdb2" */
        EXEC SQL AT con2 SELECT current_database() INTO :dbname;
        printf("current=%s (should be testdb2)\n", dbname);
    
        /* Switch the current connection to "testdb1". */
        EXEC SQL SET CONNECTION con1;
    
        EXEC SQL SELECT current_database() INTO :dbname;
        printf("current=%s (should be testdb1)\n", dbname);
    
        EXEC SQL DISCONNECT ALL;
        return 0;
    }
    

This example would produce this output:

    
    
    current=testdb3 (should be testdb3)
    current=testdb2 (should be testdb2)
    current=testdb1 (should be testdb1)
    

The third option is to declare an SQL identifier linked to the connection, for
example:

    
    
    EXEC SQL AT _connection-name_ DECLARE _statement-name_ STATEMENT;
    EXEC SQL PREPARE _statement-name_ FROM :_dyn-string_ ;
    

Once you link an SQL identifier to a connection, you execute dynamic SQL
without an AT clause. Note that this option behaves like preprocessor
directives, therefore the link is enabled only in the file.

Here is an example program using this option:

    
    
    #include <stdio.h>
    
    EXEC SQL BEGIN DECLARE SECTION;
    char dbname[128];
    char *dyn_sql = "SELECT current_database()";
    EXEC SQL END DECLARE SECTION;
    
    int main(){
      EXEC SQL CONNECT TO postgres AS con1;
      EXEC SQL CONNECT TO testdb AS con2;
      EXEC SQL AT con1 DECLARE stmt STATEMENT;
      EXEC SQL PREPARE stmt FROM :dyn_sql;
      EXEC SQL EXECUTE stmt INTO :dbname;
      printf("%s\n", dbname);
    
      EXEC SQL DISCONNECT ALL;
      return 0;
    }
    

This example would produce this output, even if the default connection is
testdb:

    
    
    postgres
    

### 36.2.3. Closing a Connection #

To close a connection, use the following statement:

    
    
    EXEC SQL DISCONNECT [_connection_];
    

The _`connection`_ can be specified in the following ways:

  * `_`connection-name`_`
  * `CURRENT`
  * `ALL`

If no connection name is specified, the current connection is closed.

It is good style that an application always explicitly disconnect from every
connection it opened.

* * *

[Prev](ecpg-concept.html "36.1. The Concept")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") |  [Next](ecpg-commands.html "36.3. Running SQL Commands")  
---|---|---  
36.1. The Concept  | [Home](index.html "PostgreSQL 16.9 Documentation") |  36.3. Running SQL Commands  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-connect.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

