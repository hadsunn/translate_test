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

Supported Versions: [Current](/docs/current/contrib-dblink-function.html
"PostgreSQL 17 - dblink") ([17](/docs/17/contrib-dblink-function.html
"PostgreSQL 17 - dblink")) / [16](/docs/16/contrib-dblink-function.html
"PostgreSQL 16 - dblink") / [15](/docs/15/contrib-dblink-function.html
"PostgreSQL 15 - dblink") / [14](/docs/14/contrib-dblink-function.html
"PostgreSQL 14 - dblink") / [13](/docs/13/contrib-dblink-function.html
"PostgreSQL 13 - dblink")

Development Versions: [18](/docs/18/contrib-dblink-function.html "PostgreSQL
18 - dblink") / [devel](/docs/devel/contrib-dblink-function.html "PostgreSQL
devel - dblink")

Unsupported versions: [12](/docs/12/contrib-dblink-function.html "PostgreSQL
12 - dblink") / [11](/docs/11/contrib-dblink-function.html "PostgreSQL 11 -
dblink") / [10](/docs/10/contrib-dblink-function.html "PostgreSQL 10 -
dblink") / [9.6](/docs/9.6/contrib-dblink-function.html "PostgreSQL 9.6 -
dblink") / [9.5](/docs/9.5/contrib-dblink-function.html "PostgreSQL 9.5 -
dblink") / [9.4](/docs/9.4/contrib-dblink-function.html "PostgreSQL 9.4 -
dblink") / [9.3](/docs/9.3/contrib-dblink-function.html "PostgreSQL 9.3 -
dblink") / [9.2](/docs/9.2/contrib-dblink-function.html "PostgreSQL 9.2 -
dblink") / [9.1](/docs/9.1/contrib-dblink-function.html "PostgreSQL 9.1 -
dblink")

__

dblink  
---  
[Prev](contrib-dblink-disconnect.html "dblink_disconnect")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") | F.12. dblink — connect to other PostgreSQL databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-exec.html "dblink_exec")  
  
* * *

## dblink

dblink — executes a query in a remote database

## Synopsis

    
    
    dblink(text connname, text sql [, bool fail_on_error]) returns setof record
    dblink(text connstr, text sql [, bool fail_on_error]) returns setof record
    dblink(text sql [, bool fail_on_error]) returns setof record
    

## Description

`dblink` executes a query (usually a `SELECT`, but it can be any SQL statement
that returns rows) in a remote database.

When two `text` arguments are given, the first one is first looked up as a
persistent connection's name; if found, the command is executed on that
connection. If not found, the first argument is treated as a connection info
string as for `dblink_connect`, and the indicated connection is made just for
the duration of this command.

## Arguments

_`connname`_

    

Name of the connection to use; omit this parameter to use the unnamed
connection.

_`connstr`_

    

A connection info string, as previously described for `dblink_connect`.

_`sql`_

    

The SQL query that you wish to execute in the remote database, for example
`select * from foo`.

_`fail_on_error`_

    

If true (the default when omitted) then an error thrown on the remote side of
the connection causes an error to also be thrown locally. If false, the remote
error is locally reported as a NOTICE, and the function returns no rows.

## Return Value

The function returns the row(s) produced by the query. Since `dblink` can be
used with any query, it is declared to return `record`, rather than specifying
any particular set of columns. This means that you must specify the expected
set of columns in the calling query — otherwise PostgreSQL would not know what
to expect. Here is an example:

    
    
    SELECT *
        FROM dblink('dbname=mydb options=-csearch_path=',
                    'select proname, prosrc from pg_proc')
          AS t1(proname name, prosrc text)
        WHERE proname LIKE 'bytea%';
    

The “alias” part of the `FROM` clause must specify the column names and types
that the function will return. (Specifying column names in an alias is
actually standard SQL syntax, but specifying column types is a PostgreSQL
extension.) This allows the system to understand what `*` should expand to,
and what `proname` in the `WHERE` clause refers to, in advance of trying to
execute the function. At run time, an error will be thrown if the actual query
result from the remote database does not have the same number of columns shown
in the `FROM` clause. The column names need not match, however, and `dblink`
does not insist on exact type matches either. It will succeed so long as the
returned data strings are valid input for the column type declared in the
`FROM` clause.

## Notes

A convenient way to use `dblink` with predetermined queries is to create a
view. This allows the column type information to be buried in the view,
instead of having to spell it out in every query. For example,

    
    
    CREATE VIEW myremote_pg_proc AS
      SELECT *
        FROM dblink('dbname=postgres options=-csearch_path=',
                    'select proname, prosrc from pg_proc')
        AS t1(proname name, prosrc text);
    
    SELECT * FROM myremote_pg_proc WHERE proname LIKE 'bytea%';
    

## Examples

    
    
    SELECT * FROM dblink('dbname=postgres options=-csearch_path=',
                         'select proname, prosrc from pg_proc')
      AS t1(proname name, prosrc text) WHERE proname LIKE 'bytea%';
      proname   |   prosrc
    ------------+------------
     byteacat   | byteacat
     byteaeq    | byteaeq
     bytealt    | bytealt
     byteale    | byteale
     byteagt    | byteagt
     byteage    | byteage
     byteane    | byteane
     byteacmp   | byteacmp
     bytealike  | bytealike
     byteanlike | byteanlike
     byteain    | byteain
     byteaout   | byteaout
    (12 rows)
    
    SELECT dblink_connect('dbname=postgres options=-csearch_path=');
     dblink_connect
    ----------------
     OK
    (1 row)
    
    SELECT * FROM dblink('select proname, prosrc from pg_proc')
      AS t1(proname name, prosrc text) WHERE proname LIKE 'bytea%';
      proname   |   prosrc
    ------------+------------
     byteacat   | byteacat
     byteaeq    | byteaeq
     bytealt    | bytealt
     byteale    | byteale
     byteagt    | byteagt
     byteage    | byteage
     byteane    | byteane
     byteacmp   | byteacmp
     bytealike  | bytealike
     byteanlike | byteanlike
     byteain    | byteain
     byteaout   | byteaout
    (12 rows)
    
    SELECT dblink_connect('myconn', 'dbname=regression options=-csearch_path=');
     dblink_connect
    ----------------
     OK
    (1 row)
    
    SELECT * FROM dblink('myconn', 'select proname, prosrc from pg_proc')
      AS t1(proname name, prosrc text) WHERE proname LIKE 'bytea%';
      proname   |   prosrc
    ------------+------------
     bytearecv  | bytearecv
     byteasend  | byteasend
     byteale    | byteale
     byteagt    | byteagt
     byteage    | byteage
     byteane    | byteane
     byteacmp   | byteacmp
     bytealike  | bytealike
     byteanlike | byteanlike
     byteacat   | byteacat
     byteaeq    | byteaeq
     bytealt    | bytealt
     byteain    | byteain
     byteaout   | byteaout
    (14 rows)
    

* * *

[Prev](contrib-dblink-disconnect.html "dblink_disconnect")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") |  [Next](contrib-dblink-exec.html "dblink_exec")  
---|---|---  
dblink_disconnect  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink_exec  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-dblink-function.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

