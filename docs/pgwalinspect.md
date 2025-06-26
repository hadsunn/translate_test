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

Supported Versions: [Current](/docs/current/pgwalinspect.html "PostgreSQL 17 -
F.37. pg_walinspect — low-level WAL inspection")
([17](/docs/17/pgwalinspect.html "PostgreSQL 17 - F.37. pg_walinspect — low-
level WAL inspection")) / [16](/docs/16/pgwalinspect.html "PostgreSQL 16 -
F.37. pg_walinspect — low-level WAL inspection") /
[15](/docs/15/pgwalinspect.html "PostgreSQL 15 - F.37. pg_walinspect — low-
level WAL inspection")

Development Versions: [18](/docs/18/pgwalinspect.html "PostgreSQL 18 -
F.37. pg_walinspect — low-level WAL inspection") /
[devel](/docs/devel/pgwalinspect.html "PostgreSQL devel - F.37. pg_walinspect
— low-level WAL inspection")

__

F.37. pg_walinspect — low-level WAL inspection  
---  
[Prev](pgvisibility.html "F.36. pg_visibility — visibility map information and utilities")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](postgres-fdw.html "F.38. postgres_fdw —  access data stored in external PostgreSQL  servers")  
  
* * *

## F.37. pg_walinspect — low-level WAL inspection #

[F.37.1. General Functions](pgwalinspect.html#PGWALINSPECT-FUNCS)

[F.37.2. Author](pgwalinspect.html#PGWALINSPECT-AUTHOR)

The `pg_walinspect` module provides SQL functions that allow you to inspect
the contents of write-ahead log of a running PostgreSQL database cluster at a
low level, which is useful for debugging, analytical, reporting or educational
purposes. It is similar to [pg_waldump](pgwaldump.html "pg_waldump"), but
accessible through SQL rather than a separate utility.

All the functions of this module will provide the WAL information using the
server's current timeline ID.

### Note

The `pg_walinspect` functions are often called using an LSN argument that
specifies the location at which a known WAL record of interest _begins_.
However, some functions, such as `[pg_logical_emit_message](functions-
admin.html#PG-LOGICAL-EMIT-MESSAGE)`, return the LSN _after_ the record that
was just inserted.

### Tip

All of the `pg_walinspect` functions that show information about records that
fall within a certain LSN range are permissive about accepting _`end_lsn`_
arguments that are after the server's current LSN. Using an _`end_lsn`_ “from
the future” will not raise an error.

It may be convenient to provide the value `FFFFFFFF/FFFFFFFF` (the maximum
valid `pg_lsn` value) as an _`end_lsn`_ argument. This is equivalent to
providing an _`end_lsn`_ argument matching the server's current LSN.

By default, use of these functions is restricted to superusers and members of
the `pg_read_server_files` role. Access may be granted by superusers to others
using `GRANT`.

### F.37.1. General Functions #

`pg_get_wal_record_info(in_lsn pg_lsn) returns record` #

    

Gets WAL record information about a record that is located at or after the
_`in_lsn`_ argument. For example:

    
    
    postgres=# SELECT * FROM pg_get_wal_record_info('0/E419E28');
    -[ RECORD 1 ]----+-------------------------------------------------
    start_lsn        | 0/E419E28
    end_lsn          | 0/E419E68
    prev_lsn         | 0/E419D78
    xid              | 0
    resource_manager | Heap2
    record_type      | VACUUM
    record_length    | 58
    main_data_length | 2
    fpi_length       | 0
    description      | nunused: 5, unused: [1, 2, 3, 4, 5]
    block_ref        | blkref #0: rel 1663/16385/1249 fork main blk 364
    

If _`in_lsn`_ isn't at the start of a WAL record, information about the next
valid WAL record is shown instead. If there is no next valid WAL record, the
function raises an error.

`pg_get_wal_records_info(start_lsn pg_lsn, end_lsn pg_lsn) returns setof
record` #

    

Gets information of all the valid WAL records between _`start_lsn`_ and
_`end_lsn`_. Returns one row per WAL record. For example:

    
    
    postgres=# SELECT * FROM pg_get_wal_records_info('0/1E913618', '0/1E913740') LIMIT 1;
    -[ RECORD 1 ]----+--------------------------------------------------------------
    start_lsn        | 0/1E913618
    end_lsn          | 0/1E913650
    prev_lsn         | 0/1E9135A0
    xid              | 0
    resource_manager | Standby
    record_type      | RUNNING_XACTS
    record_length    | 50
    main_data_length | 24
    fpi_length       | 0
    description      | nextXid 33775 latestCompletedXid 33774 oldestRunningXid 33775
    block_ref        |
    

The function raises an error if _`start_lsn`_ is not available.

`pg_get_wal_block_info(start_lsn pg_lsn, end_lsn pg_lsn, show_data boolean
DEFAULT true) returns setof record` #

    

Gets information about each block reference from all the valid WAL records
between _`start_lsn`_ and _`end_lsn`_ with one or more block references.
Returns one row per block reference per WAL record. For example:

    
    
    postgres=# SELECT * FROM pg_get_wal_block_info('0/1230278', '0/12302B8');
    -[ RECORD 1 ]-----+-----------------------------------
    start_lsn         | 0/1230278
    end_lsn           | 0/12302B8
    prev_lsn          | 0/122FD40
    block_id          | 0
    reltablespace     | 1663
    reldatabase       | 1
    relfilenode       | 2658
    relforknumber     | 0
    relblocknumber    | 11
    xid               | 341
    resource_manager  | Btree
    record_type       | INSERT_LEAF
    record_length     | 64
    main_data_length  | 2
    block_data_length | 16
    block_fpi_length  | 0
    block_fpi_info    |
    description       | off: 46
    block_data        | \x00002a00070010402630000070696400
    block_fpi_data    |
    

This example involves a WAL record that only contains one block reference, but
many WAL records contain several block references. Rows output by
`pg_get_wal_block_info` are guaranteed to have a unique combination of
_`start_lsn`_ and _`block_id`_ values.

Much of the information shown here matches the output that
`pg_get_wal_records_info` would show, given the same arguments. However,
`pg_get_wal_block_info` unnests the information from each WAL record into an
expanded form by outputting one row per block reference, so certain details
are tracked at the block reference level rather than at the whole-record
level. This structure is useful with queries that track how individual blocks
changed over time. Note that records with no block references (e.g., `COMMIT`
WAL records) will have no rows returned, so `pg_get_wal_block_info` may
actually return _fewer_ rows than `pg_get_wal_records_info`.

The `reltablespace`, `reldatabase`, and `relfilenode` parameters reference
[`pg_tablespace`](catalog-pg-tablespace.html "53.56. pg_tablespace").`oid`,
[`pg_database`](catalog-pg-database.html "53.15. pg_database").`oid`, and
[`pg_class`](catalog-pg-class.html "53.11. pg_class").`relfilenode`
respectively. The `relforknumber` field is the fork number within the relation
for the block reference; see `common/relpath.h` for details.

### Tip

The `pg_filenode_relation` function (see [Table 9.97](functions-
admin.html#FUNCTIONS-ADMIN-DBLOCATION "Table 9.97. Database Object Location
Functions")) can help you to determine which relation was modified during
original execution.

It is possible for clients to avoid the overhead of materializing block data.
This may make function execution significantly faster. When _`show_data`_ is
set to `false`, `block_data` and `block_fpi_data` values are omitted (that is,
the `block_data` and `block_fpi_data` `OUT` arguments are `NULL` for all rows
returned). Obviously, this optimization is only feasible with queries where
block data isn't truly required.

The function raises an error if _`start_lsn`_ is not available.

`pg_get_wal_stats(start_lsn pg_lsn, end_lsn pg_lsn, per_record boolean DEFAULT
false) returns setof record` #

    

Gets statistics of all the valid WAL records between _`start_lsn`_ and
_`end_lsn`_. By default, it returns one row per _`resource_manager`_ type.
When _`per_record`_ is set to `true`, it returns one row per _`record_type`_.
For example:

    
    
    postgres=# SELECT * FROM pg_get_wal_stats('0/1E847D00', '0/1E84F500')
               WHERE count > 0 AND
                     "resource_manager/record_type" = 'Transaction'
               LIMIT 1;
    -[ RECORD 1 ]----------------+-------------------
    resource_manager/record_type | Transaction
    count                        | 2
    count_percentage             | 8
    record_size                  | 875
    record_size_percentage       | 41.23468426013195
    fpi_size                     | 0
    fpi_size_percentage          | 0
    combined_size                | 875
    combined_size_percentage     | 2.8634072910530795
    

The function raises an error if _`start_lsn`_ is not available.

### F.37.2. Author #

Bharath Rupireddy
`<[bharath.rupireddyforpostgres@gmail.com](mailto:bharath.rupireddyforpostgres@gmail.com)>`

* * *

[Prev](pgvisibility.html "F.36. pg_visibility — visibility map information and utilities")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](postgres-fdw.html "F.38. postgres_fdw —  access data stored in external PostgreSQL  servers")  
---|---|---  
F.36. pg_visibility — visibility map information and utilities  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.38. postgres_fdw — access data stored in external PostgreSQL servers  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pgwalinspect.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

