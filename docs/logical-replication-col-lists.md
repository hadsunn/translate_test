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

Supported Versions: [Current](/docs/current/logical-replication-col-lists.html
"PostgreSQL 17 - 31.4. Column Lists") ([17](/docs/17/logical-replication-col-
lists.html "PostgreSQL 17 - 31.4. Column Lists")) / [16](/docs/16/logical-
replication-col-lists.html "PostgreSQL 16 - 31.4. Column Lists") /
[15](/docs/15/logical-replication-col-lists.html "PostgreSQL 15 - 31.4. Column
Lists")

Development Versions: [18](/docs/18/logical-replication-col-lists.html
"PostgreSQL 18 - 31.4. Column Lists") / [devel](/docs/devel/logical-
replication-col-lists.html "PostgreSQL devel - 31.4. Column Lists")

__

31.4. Column Lists  
---  
[Prev](logical-replication-row-filter.html "31.3. Row Filters")  | [Up](logical-replication.html "Chapter 31. Logical Replication") | Chapter 31. Logical Replication | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logical-replication-conflicts.html "31.5. Conflicts")  
  
* * *

## 31.4. Column Lists #

[31.4.1. Examples](logical-replication-col-lists.html#LOGICAL-REPLICATION-COL-
LIST-EXAMPLES)

Each publication can optionally specify which columns of each table are
replicated to subscribers. The table on the subscriber side must have at least
all the columns that are published. If no column list is specified, then all
columns on the publisher are replicated. See [CREATE PUBLICATION](sql-
createpublication.html "CREATE PUBLICATION") for details on the syntax.

The choice of columns can be based on behavioral or performance reasons.
However, do not rely on this feature for security: a malicious subscriber is
able to obtain data from columns that are not specifically published. If
security is a consideration, protections can be applied at the publisher side.

If no column list is specified, any columns added to the table later are
automatically replicated. This means that having a column list which names all
columns is not the same as having no column list at all.

A column list can contain only simple column references. The order of columns
in the list is not preserved.

Specifying a column list when the publication also publishes [`FOR TABLES IN
SCHEMA`](sql-createpublication.html#SQL-CREATEPUBLICATION-FOR-TABLES-IN-
SCHEMA) is not supported.

For partitioned tables, the publication parameter
[`publish_via_partition_root`](sql-createpublication.html#SQL-
CREATEPUBLICATION-WITH-PUBLISH-VIA-PARTITION-ROOT) determines which column
list is used. If `publish_via_partition_root` is `true`, the root partitioned
table's column list is used. Otherwise, if `publish_via_partition_root` is
`false` (the default), each partition's column list is used.

If a publication publishes `UPDATE` or `DELETE` operations, any column list
must include the table's replica identity columns (see [`REPLICA
IDENTITY`](sql-altertable.html#SQL-ALTERTABLE-REPLICA-IDENTITY)). If a
publication publishes only `INSERT` operations, then the column list may omit
replica identity columns.

Column lists have no effect for the `TRUNCATE` command.

During initial data synchronization, only the published columns are copied.
However, if the subscriber is from a release prior to 15, then all the columns
in the table are copied during initial data synchronization, ignoring any
column lists.

### Warning: Combining Column Lists from Multiple Publications

There's currently no support for subscriptions comprising several publications
where the same table has been published with different column lists. [CREATE
SUBSCRIPTION](sql-createsubscription.html "CREATE SUBSCRIPTION") disallows
creating such subscriptions, but it is still possible to get into that
situation by adding or altering column lists on the publication side after a
subscription has been created.

This means changing the column lists of tables on publications that are
already subscribed could lead to errors being thrown on the subscriber side.

If a subscription is affected by this problem, the only way to resume
replication is to adjust one of the column lists on the publication side so
that they all match; and then either recreate the subscription, or use `ALTER
SUBSCRIPTION ... DROP PUBLICATION` to remove one of the offending publications
and add it again.

### 31.4.1. Examples #

Create a table `t1` to be used in the following example.

    
    
    test_pub=# CREATE TABLE t1(id int, a text, b text, c text, d text, e text, PRIMARY KEY(id));
    CREATE TABLE
    

Create a publication `p1`. A column list is defined for table `t1` to reduce
the number of columns that will be replicated. Notice that the order of column
names in the column list does not matter.

    
    
    test_pub=# CREATE PUBLICATION p1 FOR TABLE t1 (id, b, a, d);
    CREATE PUBLICATION
    

`psql` can be used to show the column lists (if defined) for each publication.

    
    
    test_pub=# \dRp+
                                   Publication p1
      Owner   | All tables | Inserts | Updates | Deletes | Truncates | Via root
    ----------+------------+---------+---------+---------+-----------+----------
     postgres | f          | t       | t       | t       | t         | f
    Tables:
        "public.t1" (id, a, b, d)
    

`psql` can be used to show the column lists (if defined) for each table.

    
    
    test_pub=# \d t1
                     Table "public.t1"
     Column |  Type   | Collation | Nullable | Default
    --------+---------+-----------+----------+---------
     id     | integer |           | not null |
     a      | text    |           |          |
     b      | text    |           |          |
     c      | text    |           |          |
     d      | text    |           |          |
     e      | text    |           |          |
    Indexes:
        "t1_pkey" PRIMARY KEY, btree (id)
    Publications:
        "p1" (id, a, b, d)
    

On the subscriber node, create a table `t1` which now only needs a subset of
the columns that were on the publisher table `t1`, and also create the
subscription `s1` that subscribes to the publication `p1`.

    
    
    test_sub=# CREATE TABLE t1(id int, b text, a text, d text, PRIMARY KEY(id));
    CREATE TABLE
    test_sub=# CREATE SUBSCRIPTION s1
    test_sub-# CONNECTION 'host=localhost dbname=test_pub application_name=s1'
    test_sub-# PUBLICATION p1;
    CREATE SUBSCRIPTION
    

On the publisher node, insert some rows to table `t1`.

    
    
    test_pub=# INSERT INTO t1 VALUES(1, 'a-1', 'b-1', 'c-1', 'd-1', 'e-1');
    INSERT 0 1
    test_pub=# INSERT INTO t1 VALUES(2, 'a-2', 'b-2', 'c-2', 'd-2', 'e-2');
    INSERT 0 1
    test_pub=# INSERT INTO t1 VALUES(3, 'a-3', 'b-3', 'c-3', 'd-3', 'e-3');
    INSERT 0 1
    test_pub=# SELECT * FROM t1 ORDER BY id;
     id |  a  |  b  |  c  |  d  |  e
    ----+-----+-----+-----+-----+-----
      1 | a-1 | b-1 | c-1 | d-1 | e-1
      2 | a-2 | b-2 | c-2 | d-2 | e-2
      3 | a-3 | b-3 | c-3 | d-3 | e-3
    (3 rows)
    

Only data from the column list of publication `p1` is replicated.

    
    
    test_sub=# SELECT * FROM t1 ORDER BY id;
     id |  b  |  a  |  d
    ----+-----+-----+-----
      1 | b-1 | a-1 | d-1
      2 | b-2 | a-2 | d-2
      3 | b-3 | a-3 | d-3
    (3 rows)
    

* * *

[Prev](logical-replication-row-filter.html "31.3. Row Filters")  | [Up](logical-replication.html "Chapter 31. Logical Replication") |  [Next](logical-replication-conflicts.html "31.5. Conflicts")  
---|---|---  
31.3. Row Filters  | [Home](index.html "PostgreSQL 16.9 Documentation") |  31.5. Conflicts  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logical-replication-col-
lists.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

