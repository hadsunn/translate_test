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

Supported Versions: [Current](/docs/current/contrib-dblink-fetch.html
"PostgreSQL 17 - dblink_fetch") ([17](/docs/17/contrib-dblink-fetch.html
"PostgreSQL 17 - dblink_fetch")) / [16](/docs/16/contrib-dblink-fetch.html
"PostgreSQL 16 - dblink_fetch") / [15](/docs/15/contrib-dblink-fetch.html
"PostgreSQL 15 - dblink_fetch") / [14](/docs/14/contrib-dblink-fetch.html
"PostgreSQL 14 - dblink_fetch") / [13](/docs/13/contrib-dblink-fetch.html
"PostgreSQL 13 - dblink_fetch")

Development Versions: [18](/docs/18/contrib-dblink-fetch.html "PostgreSQL 18 -
dblink_fetch") / [devel](/docs/devel/contrib-dblink-fetch.html "PostgreSQL
devel - dblink_fetch")

Unsupported versions: [12](/docs/12/contrib-dblink-fetch.html "PostgreSQL 12 -
dblink_fetch") / [11](/docs/11/contrib-dblink-fetch.html "PostgreSQL 11 -
dblink_fetch") / [10](/docs/10/contrib-dblink-fetch.html "PostgreSQL 10 -
dblink_fetch") / [9.6](/docs/9.6/contrib-dblink-fetch.html "PostgreSQL 9.6 -
dblink_fetch") / [9.5](/docs/9.5/contrib-dblink-fetch.html "PostgreSQL 9.5 -
dblink_fetch") / [9.4](/docs/9.4/contrib-dblink-fetch.html "PostgreSQL 9.4 -
dblink_fetch") / [9.3](/docs/9.3/contrib-dblink-fetch.html "PostgreSQL 9.3 -
dblink_fetch") / [9.2](/docs/9.2/contrib-dblink-fetch.html "PostgreSQL 9.2 -
dblink_fetch") / [9.1](/docs/9.1/contrib-dblink-fetch.html "PostgreSQL 9.1 -
dblink_fetch") / [9.0](/docs/9.0/contrib-dblink-fetch.html "PostgreSQL 9.0 -
dblink_fetch") / [8.4](/docs/8.4/contrib-dblink-fetch.html "PostgreSQL 8.4 -
dblink_fetch") / [8.3](/docs/8.3/contrib-dblink-fetch.html "PostgreSQL 8.3 -
dblink_fetch")

__

dblink_fetch  
---  
[Prev](contrib-dblink-open.html "dblink_open")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") | F.12. dblink — connect to other PostgreSQL databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-close.html "dblink_close")  
  
* * *

## dblink_fetch

dblink_fetch — returns rows from an open cursor in a remote database

## Synopsis

    
    
    dblink_fetch(text cursorname, int howmany [, bool fail_on_error]) returns setof record
    dblink_fetch(text connname, text cursorname, int howmany [, bool fail_on_error]) returns setof record
    

## Description

`dblink_fetch` fetches rows from a cursor previously established by
`dblink_open`.

## Arguments

_`connname`_

    

Name of the connection to use; omit this parameter to use the unnamed
connection.

_`cursorname`_

    

The name of the cursor to fetch from.

_`howmany`_

    

The maximum number of rows to retrieve. The next _`howmany`_ rows are fetched,
starting at the current cursor position, moving forward. Once the cursor has
reached its end, no more rows are produced.

_`fail_on_error`_

    

If true (the default when omitted) then an error thrown on the remote side of
the connection causes an error to also be thrown locally. If false, the remote
error is locally reported as a NOTICE, and the function returns no rows.

## Return Value

The function returns the row(s) fetched from the cursor. To use this function,
you will need to specify the expected set of columns, as previously discussed
for `dblink`.

## Notes

On a mismatch between the number of return columns specified in the `FROM`
clause, and the actual number of columns returned by the remote cursor, an
error will be thrown. In this event, the remote cursor is still advanced by as
many rows as it would have been if the error had not occurred. The same is
true for any other error occurring in the local query after the remote `FETCH`
has been done.

## Examples

    
    
    SELECT dblink_connect('dbname=postgres options=-csearch_path=');
     dblink_connect
    ----------------
     OK
    (1 row)
    
    SELECT dblink_open('foo', 'select proname, prosrc from pg_proc where proname like ''bytea%''');
     dblink_open
    -------------
     OK
    (1 row)
    
    SELECT * FROM dblink_fetch('foo', 5) AS (funcname name, source text);
     funcname |  source
    ----------+----------
     byteacat | byteacat
     byteacmp | byteacmp
     byteaeq  | byteaeq
     byteage  | byteage
     byteagt  | byteagt
    (5 rows)
    
    SELECT * FROM dblink_fetch('foo', 5) AS (funcname name, source text);
     funcname  |  source
    -----------+-----------
     byteain   | byteain
     byteale   | byteale
     bytealike | bytealike
     bytealt   | bytealt
     byteane   | byteane
    (5 rows)
    
    SELECT * FROM dblink_fetch('foo', 5) AS (funcname name, source text);
      funcname  |   source
    ------------+------------
     byteanlike | byteanlike
     byteaout   | byteaout
    (2 rows)
    
    SELECT * FROM dblink_fetch('foo', 5) AS (funcname name, source text);
     funcname | source
    ----------+--------
    (0 rows)
    

* * *

[Prev](contrib-dblink-open.html "dblink_open")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") |  [Next](contrib-dblink-close.html "dblink_close")  
---|---|---  
dblink_open  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink_close  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-dblink-fetch.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

