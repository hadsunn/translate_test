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

Supported Versions: [Current](/docs/current/pgrowlocks.html "PostgreSQL 17 -
F.31. pgrowlocks — show a table's row locking information")
([17](/docs/17/pgrowlocks.html "PostgreSQL 17 - F.31. pgrowlocks — show a
table's row locking information")) / [16](/docs/16/pgrowlocks.html "PostgreSQL
16 - F.31. pgrowlocks — show a table's row locking information") /
[15](/docs/15/pgrowlocks.html "PostgreSQL 15 - F.31. pgrowlocks — show a
table's row locking information") / [14](/docs/14/pgrowlocks.html "PostgreSQL
14 - F.31. pgrowlocks — show a table's row locking information") /
[13](/docs/13/pgrowlocks.html "PostgreSQL 13 - F.31. pgrowlocks — show a
table's row locking information")

Development Versions: [18](/docs/18/pgrowlocks.html "PostgreSQL 18 -
F.31. pgrowlocks — show a table's row locking information") /
[devel](/docs/devel/pgrowlocks.html "PostgreSQL devel - F.31. pgrowlocks —
show a table's row locking information")

Unsupported versions: [12](/docs/12/pgrowlocks.html "PostgreSQL 12 -
F.31. pgrowlocks — show a table's row locking information") /
[11](/docs/11/pgrowlocks.html "PostgreSQL 11 - F.31. pgrowlocks — show a
table's row locking information") / [10](/docs/10/pgrowlocks.html "PostgreSQL
10 - F.31. pgrowlocks — show a table's row locking information") /
[9.6](/docs/9.6/pgrowlocks.html "PostgreSQL 9.6 - F.31. pgrowlocks — show a
table's row locking information") / [9.5](/docs/9.5/pgrowlocks.html
"PostgreSQL 9.5 - F.31. pgrowlocks — show a table's row locking information")
/ [9.4](/docs/9.4/pgrowlocks.html "PostgreSQL 9.4 - F.31. pgrowlocks — show a
table's row locking information") / [9.3](/docs/9.3/pgrowlocks.html
"PostgreSQL 9.3 - F.31. pgrowlocks — show a table's row locking information")
/ [9.2](/docs/9.2/pgrowlocks.html "PostgreSQL 9.2 - F.31. pgrowlocks — show a
table's row locking information") / [9.1](/docs/9.1/pgrowlocks.html
"PostgreSQL 9.1 - F.31. pgrowlocks — show a table's row locking information")
/ [9.0](/docs/9.0/pgrowlocks.html "PostgreSQL 9.0 - F.31. pgrowlocks — show a
table's row locking information") / [8.4](/docs/8.4/pgrowlocks.html
"PostgreSQL 8.4 - F.31. pgrowlocks — show a table's row locking information")
/ [8.3](/docs/8.3/pgrowlocks.html "PostgreSQL 8.3 - F.31. pgrowlocks — show a
table's row locking information")

__

F.31. pgrowlocks — show a table's row locking information  
---  
[Prev](pgprewarm.html "F.30. pg_prewarm — preload relation data into buffer caches")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pgstatstatements.html "F.32. pg_stat_statements — track statistics of SQL planning and execution")  
  
* * *

## F.31. pgrowlocks — show a table's row locking information #

[F.31.1. Overview](pgrowlocks.html#PGROWLOCKS-OVERVIEW)

[F.31.2. Sample Output](pgrowlocks.html#PGROWLOCKS-SAMPLE-OUTPUT)

[F.31.3. Author](pgrowlocks.html#PGROWLOCKS-AUTHOR)

The `pgrowlocks` module provides a function to show row locking information
for a specified table.

By default use is restricted to superusers, roles with privileges of the
`pg_stat_scan_tables` role, and users with `SELECT` permissions on the table.

### F.31.1. Overview #

    
    
    pgrowlocks(text) returns setof record
    

The parameter is the name of a table. The result is a set of records, with one
row for each locked row within the table. The output columns are shown in
[Table F.21](pgrowlocks.html#PGROWLOCKS-COLUMNS "Table F.21. pgrowlocks Output
Columns").

**Table  F.21. `pgrowlocks` Output Columns**

Name | Type | Description  
---|---|---  
`locked_row` | `tid` | Tuple ID (TID) of locked row  
`locker` | `xid` | Transaction ID of locker, or multixact ID if multitransaction; see [Section 74.1](transaction-id.html "74.1. Transactions and Identifiers")  
`multi` | `boolean` | True if locker is a multitransaction  
`xids` | `xid[]` | Transaction IDs of lockers (more than one if multitransaction)  
`modes` | `text[]` | Lock mode of lockers (more than one if multitransaction), an array of `Key Share`, `Share`, `For No Key Update`, `No Key Update`, `For Update`, `Update`.  
`pids` | `integer[]` | Process IDs of locking backends (more than one if multitransaction)  
  
  

`pgrowlocks` takes `AccessShareLock` for the target table and reads each row
one by one to collect the row locking information. This is not very speedy for
a large table. Note that:

  1. If an `ACCESS EXCLUSIVE` lock is taken on the table, `pgrowlocks` will be blocked.

  2. `pgrowlocks` is not guaranteed to produce a self-consistent snapshot. It is possible that a new row lock is taken, or an old lock is freed, during its execution.

`pgrowlocks` does not show the contents of locked rows. If you want to take a
look at the row contents at the same time, you could do something like this:

    
    
    SELECT * FROM accounts AS a, pgrowlocks('accounts') AS p
      WHERE p.locked_row = a.ctid;
    

Be aware however that such a query will be very inefficient.

### F.31.2. Sample Output #

    
    
    =# SELECT * FROM pgrowlocks('t1');
     locked_row | locker | multi | xids  |     modes      |  pids
    ------------+--------+-------+-------+----------------+--------
     (0,1)      |    609 | f     | {609} | {"For Share"}  | {3161}
     (0,2)      |    609 | f     | {609} | {"For Share"}  | {3161}
     (0,3)      |    607 | f     | {607} | {"For Update"} | {3107}
     (0,4)      |    607 | f     | {607} | {"For Update"} | {3107}
    (4 rows)
    

### F.31.3. Author #

Tatsuo Ishii

* * *

[Prev](pgprewarm.html "F.30. pg_prewarm — preload relation data into buffer caches")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](pgstatstatements.html "F.32. pg_stat_statements — track statistics of SQL planning and execution")  
---|---|---  
F.30. pg_prewarm — preload relation data into buffer caches  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.32. pg_stat_statements — track statistics of SQL planning and execution  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pgrowlocks.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

