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

Supported Versions: [Current](/docs/current/logicaldecoding-example.html
"PostgreSQL 17 - 49.1. Logical Decoding Examples")
([17](/docs/17/logicaldecoding-example.html "PostgreSQL 17 - 49.1. Logical
Decoding Examples")) / [16](/docs/16/logicaldecoding-example.html "PostgreSQL
16 - 49.1. Logical Decoding Examples") / [15](/docs/15/logicaldecoding-
example.html "PostgreSQL 15 - 49.1. Logical Decoding Examples") /
[14](/docs/14/logicaldecoding-example.html "PostgreSQL 14 - 49.1. Logical
Decoding Examples") / [13](/docs/13/logicaldecoding-example.html "PostgreSQL
13 - 49.1. Logical Decoding Examples")

Development Versions: [18](/docs/18/logicaldecoding-example.html "PostgreSQL
18 - 49.1. Logical Decoding Examples") / [devel](/docs/devel/logicaldecoding-
example.html "PostgreSQL devel - 49.1. Logical Decoding Examples")

Unsupported versions: [12](/docs/12/logicaldecoding-example.html "PostgreSQL
12 - 49.1. Logical Decoding Examples") / [11](/docs/11/logicaldecoding-
example.html "PostgreSQL 11 - 49.1. Logical Decoding Examples") /
[10](/docs/10/logicaldecoding-example.html "PostgreSQL 10 - 49.1. Logical
Decoding Examples") / [9.6](/docs/9.6/logicaldecoding-example.html "PostgreSQL
9.6 - 49.1. Logical Decoding Examples") / [9.5](/docs/9.5/logicaldecoding-
example.html "PostgreSQL 9.5 - 49.1. Logical Decoding Examples") /
[9.4](/docs/9.4/logicaldecoding-example.html "PostgreSQL 9.4 - 49.1. Logical
Decoding Examples")

__

49.1. Logical Decoding Examples  
---  
[Prev](logicaldecoding.html "Chapter 49. Logical Decoding")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") | Chapter 49. Logical Decoding | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logicaldecoding-explanation.html "49.2. Logical Decoding Concepts")  
  
* * *

## 49.1. Logical Decoding Examples #

The following example demonstrates controlling logical decoding using the SQL
interface.

Before you can use logical decoding, you must set [wal_level](runtime-config-
wal.html#GUC-WAL-LEVEL) to `logical` and [max_replication_slots](runtime-
config-replication.html#GUC-MAX-REPLICATION-SLOTS) to at least 1. Then, you
should connect to the target database (in the example below, `postgres`) as a
superuser.

    
    
    postgres=# -- Create a slot named 'regression_slot' using the output plugin 'test_decoding'
    postgres=# SELECT * FROM pg_create_logical_replication_slot('regression_slot', 'test_decoding', false, true);
        slot_name    |    lsn
    -----------------+-----------
     regression_slot | 0/16B1970
    (1 row)
    
    postgres=# SELECT slot_name, plugin, slot_type, database, active, restart_lsn, confirmed_flush_lsn FROM pg_replication_slots;
        slot_name    |    plugin     | slot_type | database | active | restart_lsn | confirmed_flush_lsn
    -----------------+---------------+-----------+----------+--------+-------------+-----------------
     regression_slot | test_decoding | logical   | postgres | f      | 0/16A4408   | 0/16A4440
    (1 row)
    
    postgres=# -- There are no changes to see yet
    postgres=# SELECT * FROM pg_logical_slot_get_changes('regression_slot', NULL, NULL);
     lsn | xid | data
    -----+-----+------
    (0 rows)
    
    postgres=# CREATE TABLE data(id serial primary key, data text);
    CREATE TABLE
    
    postgres=# -- DDL isn't replicated, so all you'll see is the transaction
    postgres=# SELECT * FROM pg_logical_slot_get_changes('regression_slot', NULL, NULL);
        lsn    |  xid  |     data
    -----------+-------+--------------
     0/BA2DA58 | 10297 | BEGIN 10297
     0/BA5A5A0 | 10297 | COMMIT 10297
    (2 rows)
    
    postgres=# -- Once changes are read, they're consumed and not emitted
    postgres=# -- in a subsequent call:
    postgres=# SELECT * FROM pg_logical_slot_get_changes('regression_slot', NULL, NULL);
     lsn | xid | data
    -----+-----+------
    (0 rows)
    
    postgres=# BEGIN;
    postgres=*# INSERT INTO data(data) VALUES('1');
    postgres=*# INSERT INTO data(data) VALUES('2');
    postgres=*# COMMIT;
    
    postgres=# SELECT * FROM pg_logical_slot_get_changes('regression_slot', NULL, NULL);
        lsn    |  xid  |                          data
    -----------+-------+---------------------------------------------------------
     0/BA5A688 | 10298 | BEGIN 10298
     0/BA5A6F0 | 10298 | table public.data: INSERT: id[integer]:1 data[text]:'1'
     0/BA5A7F8 | 10298 | table public.data: INSERT: id[integer]:2 data[text]:'2'
     0/BA5A8A8 | 10298 | COMMIT 10298
    (4 rows)
    
    postgres=# INSERT INTO data(data) VALUES('3');
    
    postgres=# -- You can also peek ahead in the change stream without consuming changes
    postgres=# SELECT * FROM pg_logical_slot_peek_changes('regression_slot', NULL, NULL);
        lsn    |  xid  |                          data
    -----------+-------+---------------------------------------------------------
     0/BA5A8E0 | 10299 | BEGIN 10299
     0/BA5A8E0 | 10299 | table public.data: INSERT: id[integer]:3 data[text]:'3'
     0/BA5A990 | 10299 | COMMIT 10299
    (3 rows)
    
    postgres=# -- The next call to pg_logical_slot_peek_changes() returns the same changes again
    postgres=# SELECT * FROM pg_logical_slot_peek_changes('regression_slot', NULL, NULL);
        lsn    |  xid  |                          data
    -----------+-------+---------------------------------------------------------
     0/BA5A8E0 | 10299 | BEGIN 10299
     0/BA5A8E0 | 10299 | table public.data: INSERT: id[integer]:3 data[text]:'3'
     0/BA5A990 | 10299 | COMMIT 10299
    (3 rows)
    
    postgres=# -- options can be passed to output plugin, to influence the formatting
    postgres=# SELECT * FROM pg_logical_slot_peek_changes('regression_slot', NULL, NULL, 'include-timestamp', 'on');
        lsn    |  xid  |                          data
    -----------+-------+---------------------------------------------------------
     0/BA5A8E0 | 10299 | BEGIN 10299
     0/BA5A8E0 | 10299 | table public.data: INSERT: id[integer]:3 data[text]:'3'
     0/BA5A990 | 10299 | COMMIT 10299 (at 2017-05-10 12:07:21.272494-04)
    (3 rows)
    
    postgres=# -- Remember to destroy a slot you no longer need to stop it consuming
    postgres=# -- server resources:
    postgres=# SELECT pg_drop_replication_slot('regression_slot');
     pg_drop_replication_slot
    -----------------------
    
    (1 row)
    

The following examples shows how logical decoding is controlled over the
streaming replication protocol, using the program [pg_recvlogical](app-
pgrecvlogical.html "pg_recvlogical") included in the PostgreSQL distribution.
This requires that client authentication is set up to allow replication
connections (see [Section 27.2.5.1](warm-standby.html#STREAMING-REPLICATION-
AUTHENTICATION "27.2.5.1. Authentication")) and that `max_wal_senders` is set
sufficiently high to allow an additional connection. The second example shows
how to stream two-phase transactions. Before you use two-phase commands, you
must set [max_prepared_transactions](runtime-config-resource.html#GUC-MAX-
PREPARED-TRANSACTIONS) to at least 1.

    
    
    Example 1:
    $ pg_recvlogical -d postgres --slot=test --create-slot
    $ pg_recvlogical -d postgres --slot=test --start -f -
    **Control** +**Z**
    $ psql -d postgres -c "INSERT INTO data(data) VALUES('4');"
    $ fg
    BEGIN 693
    table public.data: INSERT: id[integer]:4 data[text]:'4'
    COMMIT 693
    **Control** +**C**
    $ pg_recvlogical -d postgres --slot=test --drop-slot
    
    Example 2:
    $ pg_recvlogical -d postgres --slot=test --create-slot --two-phase
    $ pg_recvlogical -d postgres --slot=test --start -f -
    **Control** +**Z**
    $ psql -d postgres -c "BEGIN;INSERT INTO data(data) VALUES('5');PREPARE TRANSACTION 'test';"
    $ fg
    BEGIN 694
    table public.data: INSERT: id[integer]:5 data[text]:'5'
    PREPARE TRANSACTION 'test', txid 694
    **Control** +**Z**
    $ psql -d postgres -c "COMMIT PREPARED 'test';"
    $ fg
    COMMIT PREPARED 'test', txid 694
    **Control** +**C**
    $ pg_recvlogical -d postgres --slot=test --drop-slot
    

The following example shows SQL interface that can be used to decode prepared
transactions. Before you use two-phase commit commands, you must set
`max_prepared_transactions` to at least 1. You must also have set the two-
phase parameter as 'true' while creating the slot using
`pg_create_logical_replication_slot` Note that we will stream the entire
transaction after the commit if it is not already decoded.

    
    
    postgres=# BEGIN;
    postgres=*# INSERT INTO data(data) VALUES('5');
    postgres=*# PREPARE TRANSACTION 'test_prepared1';
    
    postgres=# SELECT * FROM pg_logical_slot_get_changes('regression_slot', NULL, NULL);
        lsn    | xid |                          data
    -----------+-----+---------------------------------------------------------
     0/1689DC0 | 529 | BEGIN 529
     0/1689DC0 | 529 | table public.data: INSERT: id[integer]:3 data[text]:'5'
     0/1689FC0 | 529 | PREPARE TRANSACTION 'test_prepared1', txid 529
    (3 rows)
    
    postgres=# COMMIT PREPARED 'test_prepared1';
    postgres=# select * from pg_logical_slot_get_changes('regression_slot', NULL, NULL);
        lsn    | xid |                    data
    -----------+-----+--------------------------------------------
     0/168A060 | 529 | COMMIT PREPARED 'test_prepared1', txid 529
    (4 row)
    
    postgres=#-- you can also rollback a prepared transaction
    postgres=# BEGIN;
    postgres=*# INSERT INTO data(data) VALUES('6');
    postgres=*# PREPARE TRANSACTION 'test_prepared2';
    postgres=# select * from pg_logical_slot_get_changes('regression_slot', NULL, NULL);
        lsn    | xid |                          data
    -----------+-----+---------------------------------------------------------
     0/168A180 | 530 | BEGIN 530
     0/168A1E8 | 530 | table public.data: INSERT: id[integer]:4 data[text]:'6'
     0/168A430 | 530 | PREPARE TRANSACTION 'test_prepared2', txid 530
    (3 rows)
    
    postgres=# ROLLBACK PREPARED 'test_prepared2';
    postgres=# select * from pg_logical_slot_get_changes('regression_slot', NULL, NULL);
        lsn    | xid |                     data
    -----------+-----+----------------------------------------------
     0/168A4B8 | 530 | ROLLBACK PREPARED 'test_prepared2', txid 530
    (1 row)
    

* * *

[Prev](logicaldecoding.html "Chapter 49. Logical Decoding")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") |  [Next](logicaldecoding-explanation.html "49.2. Logical Decoding Concepts")  
---|---|---  
Chapter 49. Logical Decoding  | [Home](index.html "PostgreSQL 16.9 Documentation") |  49.2. Logical Decoding Concepts  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logicaldecoding-example.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

