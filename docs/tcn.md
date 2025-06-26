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

Supported Versions: [Current](/docs/current/tcn.html "PostgreSQL 17 -
F.44. tcn — a trigger function to notify listeners of changes to table
content") ([17](/docs/17/tcn.html "PostgreSQL 17 - F.44. tcn — a trigger
function to notify listeners of changes to table content")) /
[16](/docs/16/tcn.html "PostgreSQL 16 - F.44. tcn — a trigger function to
notify listeners of changes to table content") / [15](/docs/15/tcn.html
"PostgreSQL 15 - F.44. tcn — a trigger function to notify listeners of changes
to table content") / [14](/docs/14/tcn.html "PostgreSQL 14 - F.44. tcn — a
trigger function to notify listeners of changes to table content") /
[13](/docs/13/tcn.html "PostgreSQL 13 - F.44. tcn — a trigger function to
notify listeners of changes to table content")

Development Versions: [18](/docs/18/tcn.html "PostgreSQL 18 - F.44. tcn — a
trigger function to notify listeners of changes to table content") /
[devel](/docs/devel/tcn.html "PostgreSQL devel - F.44. tcn — a trigger
function to notify listeners of changes to table content")

Unsupported versions: [12](/docs/12/tcn.html "PostgreSQL 12 - F.44. tcn — a
trigger function to notify listeners of changes to table content") /
[11](/docs/11/tcn.html "PostgreSQL 11 - F.44. tcn — a trigger function to
notify listeners of changes to table content") / [10](/docs/10/tcn.html
"PostgreSQL 10 - F.44. tcn — a trigger function to notify listeners of changes
to table content") / [9.6](/docs/9.6/tcn.html "PostgreSQL 9.6 - F.44. tcn — a
trigger function to notify listeners of changes to table content") /
[9.5](/docs/9.5/tcn.html "PostgreSQL 9.5 - F.44. tcn — a trigger function to
notify listeners of changes to table content") / [9.4](/docs/9.4/tcn.html
"PostgreSQL 9.4 - F.44. tcn — a trigger function to notify listeners of
changes to table content") / [9.3](/docs/9.3/tcn.html "PostgreSQL 9.3 -
F.44. tcn — a trigger function to notify listeners of changes to table
content") / [9.2](/docs/9.2/tcn.html "PostgreSQL 9.2 - F.44. tcn — a trigger
function to notify listeners of changes to table content")

__

F.44. tcn — a trigger function to notify listeners of changes to table content  
---  
[Prev](tablefunc.html "F.43. tablefunc — functions that return tables \(crosstab and others\)")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](test-decoding.html "F.45. test_decoding — SQL-based test/example module for WAL logical decoding")  
  
* * *

## F.44. tcn — a trigger function to notify listeners of changes to table
content #

The `tcn` module provides a trigger function that notifies listeners of
changes to any table on which it is attached. It must be used as an `AFTER`
trigger `FOR EACH ROW`.

This module is considered “trusted”, that is, it can be installed by non-
superusers who have `CREATE` privilege on the current database.

Only one parameter may be supplied to the function in a `CREATE TRIGGER`
statement, and that is optional. If supplied it will be used for the channel
name for the notifications. If omitted `tcn` will be used for the channel
name.

The payload of the notifications consists of the table name, a letter to
indicate which type of operation was performed, and column name/value pairs
for primary key columns. Each part is separated from the next by a comma. For
ease of parsing using regular expressions, table and column names are always
wrapped in double quotes, and data values are always wrapped in single quotes.
Embedded quotes are doubled.

A brief example of using the extension follows.

    
    
    test=# create table tcndata
    test-#   (
    test(#     a int not null,
    test(#     b date not null,
    test(#     c text,
    test(#     primary key (a, b)
    test(#   );
    CREATE TABLE
    test=# create trigger tcndata_tcn_trigger
    test-#   after insert or update or delete on tcndata
    test-#   for each row execute function triggered_change_notification();
    CREATE TRIGGER
    test=# listen tcn;
    LISTEN
    test=# insert into tcndata values (1, date '2012-12-22', 'one'),
    test-#                            (1, date '2012-12-23', 'another'),
    test-#                            (2, date '2012-12-23', 'two');
    INSERT 0 3
    Asynchronous notification "tcn" with payload ""tcndata",I,"a"='1',"b"='2012-12-22'" received from server process with PID 22770.
    Asynchronous notification "tcn" with payload ""tcndata",I,"a"='1',"b"='2012-12-23'" received from server process with PID 22770.
    Asynchronous notification "tcn" with payload ""tcndata",I,"a"='2',"b"='2012-12-23'" received from server process with PID 22770.
    test=# update tcndata set c = 'uno' where a = 1;
    UPDATE 2
    Asynchronous notification "tcn" with payload ""tcndata",U,"a"='1',"b"='2012-12-22'" received from server process with PID 22770.
    Asynchronous notification "tcn" with payload ""tcndata",U,"a"='1',"b"='2012-12-23'" received from server process with PID 22770.
    test=# delete from tcndata where a = 1 and b = date '2012-12-22';
    DELETE 1
    Asynchronous notification "tcn" with payload ""tcndata",D,"a"='1',"b"='2012-12-22'" received from server process with PID 22770.
    

* * *

[Prev](tablefunc.html "F.43. tablefunc — functions that return tables \(crosstab and others\)")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](test-decoding.html "F.45. test_decoding — SQL-based test/example module for WAL logical decoding")  
---|---|---  
F.43. tablefunc — functions that return tables (`crosstab` and others)  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.45. test_decoding — SQL-based test/example module for WAL logical decoding  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/tcn.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

