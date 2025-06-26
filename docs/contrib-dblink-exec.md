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

Supported Versions: [Current](/docs/current/contrib-dblink-exec.html
"PostgreSQL 17 - dblink_exec") ([17](/docs/17/contrib-dblink-exec.html
"PostgreSQL 17 - dblink_exec")) / [16](/docs/16/contrib-dblink-exec.html
"PostgreSQL 16 - dblink_exec") / [15](/docs/15/contrib-dblink-exec.html
"PostgreSQL 15 - dblink_exec") / [14](/docs/14/contrib-dblink-exec.html
"PostgreSQL 14 - dblink_exec") / [13](/docs/13/contrib-dblink-exec.html
"PostgreSQL 13 - dblink_exec")

Development Versions: [18](/docs/18/contrib-dblink-exec.html "PostgreSQL 18 -
dblink_exec") / [devel](/docs/devel/contrib-dblink-exec.html "PostgreSQL devel
- dblink_exec")

Unsupported versions: [12](/docs/12/contrib-dblink-exec.html "PostgreSQL 12 -
dblink_exec") / [11](/docs/11/contrib-dblink-exec.html "PostgreSQL 11 -
dblink_exec") / [10](/docs/10/contrib-dblink-exec.html "PostgreSQL 10 -
dblink_exec") / [9.6](/docs/9.6/contrib-dblink-exec.html "PostgreSQL 9.6 -
dblink_exec") / [9.5](/docs/9.5/contrib-dblink-exec.html "PostgreSQL 9.5 -
dblink_exec") / [9.4](/docs/9.4/contrib-dblink-exec.html "PostgreSQL 9.4 -
dblink_exec") / [9.3](/docs/9.3/contrib-dblink-exec.html "PostgreSQL 9.3 -
dblink_exec") / [9.2](/docs/9.2/contrib-dblink-exec.html "PostgreSQL 9.2 -
dblink_exec") / [9.1](/docs/9.1/contrib-dblink-exec.html "PostgreSQL 9.1 -
dblink_exec") / [9.0](/docs/9.0/contrib-dblink-exec.html "PostgreSQL 9.0 -
dblink_exec") / [8.4](/docs/8.4/contrib-dblink-exec.html "PostgreSQL 8.4 -
dblink_exec") / [8.3](/docs/8.3/contrib-dblink-exec.html "PostgreSQL 8.3 -
dblink_exec")

__

dblink_exec  
---  
[Prev](contrib-dblink-function.html "dblink")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") | F.12. dblink — connect to other PostgreSQL databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-open.html "dblink_open")  
  
* * *

## dblink_exec

dblink_exec — executes a command in a remote database

## Synopsis

    
    
    dblink_exec(text connname, text sql [, bool fail_on_error]) returns text
    dblink_exec(text connstr, text sql [, bool fail_on_error]) returns text
    dblink_exec(text sql [, bool fail_on_error]) returns text
    

## Description

`dblink_exec` executes a command (that is, any SQL statement that doesn't
return rows) in a remote database.

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

    

The SQL command that you wish to execute in the remote database, for example
`insert into foo values(0, 'a', '{"a0","b0","c0"}')`.

_`fail_on_error`_

    

If true (the default when omitted) then an error thrown on the remote side of
the connection causes an error to also be thrown locally. If false, the remote
error is locally reported as a NOTICE, and the function's return value is set
to `ERROR`.

## Return Value

Returns status, either the command's status string or `ERROR`.

## Examples

    
    
    SELECT dblink_connect('dbname=dblink_test_standby');
     dblink_connect
    ----------------
     OK
    (1 row)
    
    SELECT dblink_exec('insert into foo values(21, ''z'', ''{"a0","b0","c0"}'');');
       dblink_exec
    -----------------
     INSERT 943366 1
    (1 row)
    
    SELECT dblink_connect('myconn', 'dbname=regression');
     dblink_connect
    ----------------
     OK
    (1 row)
    
    SELECT dblink_exec('myconn', 'insert into foo values(21, ''z'', ''{"a0","b0","c0"}'');');
       dblink_exec
    ------------------
     INSERT 6432584 1
    (1 row)
    
    SELECT dblink_exec('myconn', 'insert into pg_class values (''foo'')',false);
    NOTICE:  sql error
    DETAIL:  ERROR:  null value in column "relnamespace" violates not-null constraint
    
     dblink_exec
    -------------
     ERROR
    (1 row)
    

* * *

[Prev](contrib-dblink-function.html "dblink")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") |  [Next](contrib-dblink-open.html "dblink_open")  
---|---|---  
dblink  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink_open  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-dblink-exec.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

