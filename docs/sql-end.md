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

Supported Versions: [Current](/docs/current/sql-end.html "PostgreSQL 17 -
END") ([17](/docs/17/sql-end.html "PostgreSQL 17 - END")) / [16](/docs/16/sql-
end.html "PostgreSQL 16 - END") / [15](/docs/15/sql-end.html "PostgreSQL 15 -
END") / [14](/docs/14/sql-end.html "PostgreSQL 14 - END") / [13](/docs/13/sql-
end.html "PostgreSQL 13 - END")

Development Versions: [18](/docs/18/sql-end.html "PostgreSQL 18 - END") /
[devel](/docs/devel/sql-end.html "PostgreSQL devel - END")

Unsupported versions: [12](/docs/12/sql-end.html "PostgreSQL 12 - END") /
[11](/docs/11/sql-end.html "PostgreSQL 11 - END") / [10](/docs/10/sql-end.html
"PostgreSQL 10 - END") / [9.6](/docs/9.6/sql-end.html "PostgreSQL 9.6 - END")
/ [9.5](/docs/9.5/sql-end.html "PostgreSQL 9.5 - END") / [9.4](/docs/9.4/sql-
end.html "PostgreSQL 9.4 - END") / [9.3](/docs/9.3/sql-end.html "PostgreSQL
9.3 - END") / [9.2](/docs/9.2/sql-end.html "PostgreSQL 9.2 - END") /
[9.1](/docs/9.1/sql-end.html "PostgreSQL 9.1 - END") / [9.0](/docs/9.0/sql-
end.html "PostgreSQL 9.0 - END") / [8.4](/docs/8.4/sql-end.html "PostgreSQL
8.4 - END") / [8.3](/docs/8.3/sql-end.html "PostgreSQL 8.3 - END") /
[8.2](/docs/8.2/sql-end.html "PostgreSQL 8.2 - END") / [8.1](/docs/8.1/sql-
end.html "PostgreSQL 8.1 - END") / [8.0](/docs/8.0/sql-end.html "PostgreSQL
8.0 - END") / [7.4](/docs/7.4/sql-end.html "PostgreSQL 7.4 - END") /
[7.3](/docs/7.3/sql-end.html "PostgreSQL 7.3 - END") / [7.2](/docs/7.2/sql-
end.html "PostgreSQL 7.2 - END") / [7.1](/docs/7.1/sql-end.html "PostgreSQL
7.1 - END")

__

END  
---  
[Prev](sql-dropview.html "DROP VIEW")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-execute.html "EXECUTE")  
  
* * *

## END

END — commit the current transaction

## Synopsis

    
    
    END [ WORK | TRANSACTION ] [ AND [ NO ] CHAIN ]
    

## Description

`END` commits the current transaction. All changes made by the transaction
become visible to others and are guaranteed to be durable if a crash occurs.
This command is a PostgreSQL extension that is equivalent to [`COMMIT`](sql-
commit.html "COMMIT").

## Parameters

`WORK`  
`TRANSACTION`

    

Optional key words. They have no effect.

`AND CHAIN`

    

If `AND CHAIN` is specified, a new transaction is immediately started with the
same transaction characteristics (see [SET TRANSACTION](sql-set-
transaction.html "SET TRANSACTION")) as the just finished one. Otherwise, no
new transaction is started.

## Notes

Use [`ROLLBACK`](sql-rollback.html "ROLLBACK") to abort a transaction.

Issuing `END` when not inside a transaction does no harm, but it will provoke
a warning message.

## Examples

To commit the current transaction and make all changes permanent:

    
    
    END;
    

## Compatibility

`END` is a PostgreSQL extension that provides functionality equivalent to
[`COMMIT`](sql-commit.html "COMMIT"), which is specified in the SQL standard.

## See Also

[BEGIN](sql-begin.html "BEGIN"), [COMMIT](sql-commit.html "COMMIT"),
[ROLLBACK](sql-rollback.html "ROLLBACK")

* * *

[Prev](sql-dropview.html "DROP VIEW")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-execute.html "EXECUTE")  
---|---|---  
DROP VIEW  | [Home](index.html "PostgreSQL 16.9 Documentation") |  EXECUTE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-end.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

