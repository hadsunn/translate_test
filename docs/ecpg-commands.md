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

Supported Versions: [Current](/docs/current/ecpg-commands.html "PostgreSQL 17
- 36.3. Running SQL Commands") ([17](/docs/17/ecpg-commands.html "PostgreSQL
17 - 36.3. Running SQL Commands")) / [16](/docs/16/ecpg-commands.html
"PostgreSQL 16 - 36.3. Running SQL Commands") / [15](/docs/15/ecpg-
commands.html "PostgreSQL 15 - 36.3. Running SQL Commands") /
[14](/docs/14/ecpg-commands.html "PostgreSQL 14 - 36.3. Running SQL Commands")
/ [13](/docs/13/ecpg-commands.html "PostgreSQL 13 - 36.3. Running SQL
Commands")

Development Versions: [18](/docs/18/ecpg-commands.html "PostgreSQL 18 -
36.3. Running SQL Commands") / [devel](/docs/devel/ecpg-commands.html
"PostgreSQL devel - 36.3. Running SQL Commands")

Unsupported versions: [12](/docs/12/ecpg-commands.html "PostgreSQL 12 -
36.3. Running SQL Commands") / [11](/docs/11/ecpg-commands.html "PostgreSQL 11
- 36.3. Running SQL Commands") / [10](/docs/10/ecpg-commands.html "PostgreSQL
10 - 36.3. Running SQL Commands") / [9.6](/docs/9.6/ecpg-commands.html
"PostgreSQL 9.6 - 36.3. Running SQL Commands") / [9.5](/docs/9.5/ecpg-
commands.html "PostgreSQL 9.5 - 36.3. Running SQL Commands") /
[9.4](/docs/9.4/ecpg-commands.html "PostgreSQL 9.4 - 36.3. Running SQL
Commands") / [9.3](/docs/9.3/ecpg-commands.html "PostgreSQL 9.3 -
36.3. Running SQL Commands") / [9.2](/docs/9.2/ecpg-commands.html "PostgreSQL
9.2 - 36.3. Running SQL Commands") / [9.1](/docs/9.1/ecpg-commands.html
"PostgreSQL 9.1 - 36.3. Running SQL Commands") / [9.0](/docs/9.0/ecpg-
commands.html "PostgreSQL 9.0 - 36.3. Running SQL Commands") /
[8.4](/docs/8.4/ecpg-commands.html "PostgreSQL 8.4 - 36.3. Running SQL
Commands") / [8.3](/docs/8.3/ecpg-commands.html "PostgreSQL 8.3 -
36.3. Running SQL Commands") / [8.2](/docs/8.2/ecpg-commands.html "PostgreSQL
8.2 - 36.3. Running SQL Commands") / [8.1](/docs/8.1/ecpg-commands.html
"PostgreSQL 8.1 - 36.3. Running SQL Commands") / [8.0](/docs/8.0/ecpg-
commands.html "PostgreSQL 8.0 - 36.3. Running SQL Commands") /
[7.4](/docs/7.4/ecpg-commands.html "PostgreSQL 7.4 - 36.3. Running SQL
Commands") / [7.3](/docs/7.3/ecpg-commands.html "PostgreSQL 7.3 -
36.3. Running SQL Commands")

__

36.3. Running SQL Commands  
---  
[Prev](ecpg-connect.html "36.2. Managing Database Connections")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") | Chapter 36. ECPG — Embedded SQL in C | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-variables.html "36.4. Using Host Variables")  
  
* * *

## 36.3. Running SQL Commands #

[36.3.1. Executing SQL Statements](ecpg-commands.html#ECPG-EXECUTING)

[36.3.2. Using Cursors](ecpg-commands.html#ECPG-CURSORS)

[36.3.3. Managing Transactions](ecpg-commands.html#ECPG-TRANSACTIONS)

[36.3.4. Prepared Statements](ecpg-commands.html#ECPG-PREPARED)

Any SQL command can be run from within an embedded SQL application. Below are
some examples of how to do that.

### 36.3.1. Executing SQL Statements #

Creating a table:

    
    
    EXEC SQL CREATE TABLE foo (number integer, ascii char(16));
    EXEC SQL CREATE UNIQUE INDEX num1 ON foo(number);
    EXEC SQL COMMIT;
    

Inserting rows:

    
    
    EXEC SQL INSERT INTO foo (number, ascii) VALUES (9999, 'doodad');
    EXEC SQL COMMIT;
    

Deleting rows:

    
    
    EXEC SQL DELETE FROM foo WHERE number = 9999;
    EXEC SQL COMMIT;
    

Updates:

    
    
    EXEC SQL UPDATE foo
        SET ascii = 'foobar'
        WHERE number = 9999;
    EXEC SQL COMMIT;
    

`SELECT` statements that return a single result row can also be executed using
`EXEC SQL` directly. To handle result sets with multiple rows, an application
has to use a cursor; see [Section 36.3.2](ecpg-commands.html#ECPG-CURSORS
"36.3.2. Using Cursors") below. (As a special case, an application can fetch
multiple rows at once into an array host variable; see [Section
36.4.4.3.1](ecpg-variables.html#ECPG-VARIABLES-ARRAYS "36.4.4.3.1. Arrays").)

Single-row select:

    
    
    EXEC SQL SELECT foo INTO :FooBar FROM table1 WHERE ascii = 'doodad';
    

Also, a configuration parameter can be retrieved with the `SHOW` command:

    
    
    EXEC SQL SHOW search_path INTO :var;
    

The tokens of the form `:_`something`_` are _host variables_ , that is, they
refer to variables in the C program. They are explained in [Section
36.4](ecpg-variables.html "36.4. Using Host Variables").

### 36.3.2. Using Cursors #

To retrieve a result set holding multiple rows, an application has to declare
a cursor and fetch each row from the cursor. The steps to use a cursor are the
following: declare a cursor, open it, fetch a row from the cursor, repeat, and
finally close it.

Select using cursors:

    
    
    EXEC SQL DECLARE foo_bar CURSOR FOR
        SELECT number, ascii FROM foo
        ORDER BY ascii;
    EXEC SQL OPEN foo_bar;
    EXEC SQL FETCH foo_bar INTO :FooBar, DooDad;
    ...
    EXEC SQL CLOSE foo_bar;
    EXEC SQL COMMIT;
    

For more details about declaring a cursor, see [DECLARE](ecpg-sql-declare.html
"DECLARE"); for more details about fetching rows from a cursor, see
[FETCH](sql-fetch.html "FETCH").

### Note

The ECPG `DECLARE` command does not actually cause a statement to be sent to
the PostgreSQL backend. The cursor is opened in the backend (using the
backend's `DECLARE` command) at the point when the `OPEN` command is executed.

### 36.3.3. Managing Transactions #

In the default mode, statements are committed only when `EXEC SQL COMMIT` is
issued. The embedded SQL interface also supports autocommit of transactions
(similar to psql's default behavior) via the `-t` command-line option to
`ecpg` (see [ecpg](app-ecpg.html "ecpg")) or via the `EXEC SQL SET AUTOCOMMIT
TO ON` statement. In autocommit mode, each command is automatically committed
unless it is inside an explicit transaction block. This mode can be explicitly
turned off using `EXEC SQL SET AUTOCOMMIT TO OFF`.

The following transaction management commands are available:

`EXEC SQL COMMIT` #

    

Commit an in-progress transaction.

`EXEC SQL ROLLBACK` #

    

Roll back an in-progress transaction.

`EXEC SQL PREPARE TRANSACTION` _`transaction_id`_ #

    

Prepare the current transaction for two-phase commit.

`EXEC SQL COMMIT PREPARED` _`transaction_id`_ #

    

Commit a transaction that is in prepared state.

`EXEC SQL ROLLBACK PREPARED` _`transaction_id`_ #

    

Roll back a transaction that is in prepared state.

`EXEC SQL SET AUTOCOMMIT TO ON` #

    

Enable autocommit mode.

`EXEC SQL SET AUTOCOMMIT TO OFF` #

    

Disable autocommit mode. This is the default.

### 36.3.4. Prepared Statements #

When the values to be passed to an SQL statement are not known at compile
time, or the same statement is going to be used many times, then prepared
statements can be useful.

The statement is prepared using the command `PREPARE`. For the values that are
not known yet, use the placeholder “`?`”:

    
    
    EXEC SQL PREPARE stmt1 FROM "SELECT oid, datname FROM pg_database WHERE oid = ?";
    

If a statement returns a single row, the application can call `EXECUTE` after
`PREPARE` to execute the statement, supplying the actual values for the
placeholders with a `USING` clause:

    
    
    EXEC SQL EXECUTE stmt1 INTO :dboid, :dbname USING 1;
    

If a statement returns multiple rows, the application can use a cursor
declared based on the prepared statement. To bind input parameters, the cursor
must be opened with a `USING` clause:

    
    
    EXEC SQL PREPARE stmt1 FROM "SELECT oid,datname FROM pg_database WHERE oid > ?";
    EXEC SQL DECLARE foo_bar CURSOR FOR stmt1;
    
    /* when end of result set reached, break out of while loop */
    EXEC SQL WHENEVER NOT FOUND DO BREAK;
    
    EXEC SQL OPEN foo_bar USING 100;
    ...
    while (1)
    {
        EXEC SQL FETCH NEXT FROM foo_bar INTO :dboid, :dbname;
        ...
    }
    EXEC SQL CLOSE foo_bar;
    

When you don't need the prepared statement anymore, you should deallocate it:

    
    
    EXEC SQL DEALLOCATE PREPARE _name_ ;
    

For more details about `PREPARE`, see [PREPARE](ecpg-sql-prepare.html
"PREPARE"). Also see [Section 36.5](ecpg-dynamic.html "36.5. Dynamic SQL") for
more details about using placeholders and input parameters.

* * *

[Prev](ecpg-connect.html "36.2. Managing Database Connections")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") |  [Next](ecpg-variables.html "36.4. Using Host Variables")  
---|---|---  
36.2. Managing Database Connections  | [Home](index.html "PostgreSQL 16.9 Documentation") |  36.4. Using Host Variables  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-commands.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

