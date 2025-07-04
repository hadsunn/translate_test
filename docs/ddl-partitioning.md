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

Supported Versions: [Current](/docs/current/ddl-partitioning.html "PostgreSQL
17 - 5.11. Table Partitioning") ([17](/docs/17/ddl-partitioning.html
"PostgreSQL 17 - 5.11. Table Partitioning")) / [16](/docs/16/ddl-
partitioning.html "PostgreSQL 16 - 5.11. Table Partitioning") /
[15](/docs/15/ddl-partitioning.html "PostgreSQL 15 - 5.11. Table
Partitioning") / [14](/docs/14/ddl-partitioning.html "PostgreSQL 14 -
5.11. Table Partitioning") / [13](/docs/13/ddl-partitioning.html "PostgreSQL
13 - 5.11. Table Partitioning")

Development Versions: [18](/docs/18/ddl-partitioning.html "PostgreSQL 18 -
5.11. Table Partitioning") / [devel](/docs/devel/ddl-partitioning.html
"PostgreSQL devel - 5.11. Table Partitioning")

Unsupported versions: [12](/docs/12/ddl-partitioning.html "PostgreSQL 12 -
5.11. Table Partitioning") / [11](/docs/11/ddl-partitioning.html "PostgreSQL
11 - 5.11. Table Partitioning") / [10](/docs/10/ddl-partitioning.html
"PostgreSQL 10 - 5.11. Table Partitioning") / [9.6](/docs/9.6/ddl-
partitioning.html "PostgreSQL 9.6 - 5.11. Table Partitioning") /
[9.5](/docs/9.5/ddl-partitioning.html "PostgreSQL 9.5 - 5.11. Table
Partitioning") / [9.4](/docs/9.4/ddl-partitioning.html "PostgreSQL 9.4 -
5.11. Table Partitioning") / [9.3](/docs/9.3/ddl-partitioning.html "PostgreSQL
9.3 - 5.11. Table Partitioning") / [9.2](/docs/9.2/ddl-partitioning.html
"PostgreSQL 9.2 - 5.11. Table Partitioning") / [9.1](/docs/9.1/ddl-
partitioning.html "PostgreSQL 9.1 - 5.11. Table Partitioning") /
[9.0](/docs/9.0/ddl-partitioning.html "PostgreSQL 9.0 - 5.11. Table
Partitioning") / [8.4](/docs/8.4/ddl-partitioning.html "PostgreSQL 8.4 -
5.11. Table Partitioning") / [8.3](/docs/8.3/ddl-partitioning.html "PostgreSQL
8.3 - 5.11. Table Partitioning") / [8.2](/docs/8.2/ddl-partitioning.html
"PostgreSQL 8.2 - 5.11. Table Partitioning") / [8.1](/docs/8.1/ddl-
partitioning.html "PostgreSQL 8.1 - 5.11. Table Partitioning")

__

5.11. Table Partitioning  
---  
[Prev](ddl-inherit.html "5.10. Inheritance")  | [Up](ddl.html "Chapter 5. Data Definition") | Chapter 5. Data Definition | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ddl-foreign-data.html "5.12. Foreign Data")  
  
* * *

## 5.11. Table Partitioning #

[5.11.1. Overview](ddl-partitioning.html#DDL-PARTITIONING-OVERVIEW)

[5.11.2. Declarative Partitioning](ddl-partitioning.html#DDL-PARTITIONING-
DECLARATIVE)

[5.11.3. Partitioning Using Inheritance](ddl-partitioning.html#DDL-
PARTITIONING-USING-INHERITANCE)

[5.11.4. Partition Pruning](ddl-partitioning.html#DDL-PARTITION-PRUNING)

[5.11.5. Partitioning and Constraint Exclusion](ddl-partitioning.html#DDL-
PARTITIONING-CONSTRAINT-EXCLUSION)

[5.11.6. Best Practices for Declarative Partitioning](ddl-
partitioning.html#DDL-PARTITIONING-DECLARATIVE-BEST-PRACTICES)

PostgreSQL supports basic table partitioning. This section describes why and
how to implement partitioning as part of your database design.

### 5.11.1. Overview #

Partitioning refers to splitting what is logically one large table into
smaller physical pieces. Partitioning can provide several benefits:

  * Query performance can be improved dramatically in certain situations, particularly when most of the heavily accessed rows of the table are in a single partition or a small number of partitions. Partitioning effectively substitutes for the upper tree levels of indexes, making it more likely that the heavily-used parts of the indexes fit in memory.

  * When queries or updates access a large percentage of a single partition, performance can be improved by using a sequential scan of that partition instead of using an index, which would require random-access reads scattered across the whole table.

  * Bulk loads and deletes can be accomplished by adding or removing partitions, if the usage pattern is accounted for in the partitioning design. Dropping an individual partition using `DROP TABLE`, or doing `ALTER TABLE DETACH PARTITION`, is far faster than a bulk operation. These commands also entirely avoid the `VACUUM` overhead caused by a bulk `DELETE`.

  * Seldom-used data can be migrated to cheaper and slower storage media.

These benefits will normally be worthwhile only when a table would otherwise
be very large. The exact point at which a table will benefit from partitioning
depends on the application, although a rule of thumb is that the size of the
table should exceed the physical memory of the database server.

PostgreSQL offers built-in support for the following forms of partitioning:

Range Partitioning #

    

The table is partitioned into “ranges” defined by a key column or set of
columns, with no overlap between the ranges of values assigned to different
partitions. For example, one might partition by date ranges, or by ranges of
identifiers for particular business objects. Each range's bounds are
understood as being inclusive at the lower end and exclusive at the upper end.
For example, if one partition's range is from `1` to `10`, and the next one's
range is from `10` to `20`, then value `10` belongs to the second partition
not the first.

List Partitioning #

    

The table is partitioned by explicitly listing which key value(s) appear in
each partition.

Hash Partitioning #

    

The table is partitioned by specifying a modulus and a remainder for each
partition. Each partition will hold the rows for which the hash value of the
partition key divided by the specified modulus will produce the specified
remainder.

If your application needs to use other forms of partitioning not listed above,
alternative methods such as inheritance and `UNION ALL` views can be used
instead. Such methods offer flexibility but do not have some of the
performance benefits of built-in declarative partitioning.

### 5.11.2. Declarative Partitioning #

PostgreSQL allows you to declare that a table is divided into partitions. The
table that is divided is referred to as a _partitioned table_. The declaration
includes the _partitioning method_ as described above, plus a list of columns
or expressions to be used as the _partition key_.

The partitioned table itself is a “virtual” table having no storage of its
own. Instead, the storage belongs to _partitions_ , which are otherwise-
ordinary tables associated with the partitioned table. Each partition stores a
subset of the data as defined by its _partition bounds_. All rows inserted
into a partitioned table will be routed to the appropriate one of the
partitions based on the values of the partition key column(s). Updating the
partition key of a row will cause it to be moved into a different partition if
it no longer satisfies the partition bounds of its original partition.

Partitions may themselves be defined as partitioned tables, resulting in _sub-
partitioning_. Although all partitions must have the same columns as their
partitioned parent, partitions may have their own indexes, constraints and
default values, distinct from those of other partitions. See [CREATE
TABLE](sql-createtable.html "CREATE TABLE") for more details on creating
partitioned tables and partitions.

It is not possible to turn a regular table into a partitioned table or vice
versa. However, it is possible to add an existing regular or partitioned table
as a partition of a partitioned table, or remove a partition from a
partitioned table turning it into a standalone table; this can simplify and
speed up many maintenance processes. See [ALTER TABLE](sql-altertable.html
"ALTER TABLE") to learn more about the `ATTACH PARTITION` and `DETACH
PARTITION` sub-commands.

Partitions can also be [foreign tables](ddl-foreign-data.html "5.12. Foreign
Data"), although considerable care is needed because it is then the user's
responsibility that the contents of the foreign table satisfy the partitioning
rule. There are some other restrictions as well. See [CREATE FOREIGN
TABLE](sql-createforeigntable.html "CREATE FOREIGN TABLE") for more
information.

#### 5.11.2.1. Example #

Suppose we are constructing a database for a large ice cream company. The
company measures peak temperatures every day as well as ice cream sales in
each region. Conceptually, we want a table like:

    
    
    CREATE TABLE measurement (
        city_id         int not null,
        logdate         date not null,
        peaktemp        int,
        unitsales       int
    );
    

We know that most queries will access just the last week's, month's or
quarter's data, since the main use of this table will be to prepare online
reports for management. To reduce the amount of old data that needs to be
stored, we decide to keep only the most recent 3 years worth of data. At the
beginning of each month we will remove the oldest month's data. In this
situation we can use partitioning to help us meet all of our different
requirements for the measurements table.

To use declarative partitioning in this case, use the following steps:

  1. Create the `measurement` table as a partitioned table by specifying the `PARTITION BY` clause, which includes the partitioning method (`RANGE` in this case) and the list of column(s) to use as the partition key.
         
         CREATE TABLE measurement (
             city_id         int not null,
             logdate         date not null,
             peaktemp        int,
             unitsales       int
         ) PARTITION BY RANGE (logdate);
         

  2. Create partitions. Each partition's definition must specify bounds that correspond to the partitioning method and partition key of the parent. Note that specifying bounds such that the new partition's values would overlap with those in one or more existing partitions will cause an error.

Partitions thus created are in every way normal PostgreSQL tables (or,
possibly, foreign tables). It is possible to specify a tablespace and storage
parameters for each partition separately.

For our example, each partition should hold one month's worth of data, to
match the requirement of deleting one month's data at a time. So the commands
might look like:

         
         CREATE TABLE measurement_y2006m02 PARTITION OF measurement
             FOR VALUES FROM ('2006-02-01') TO ('2006-03-01');
         
         CREATE TABLE measurement_y2006m03 PARTITION OF measurement
             FOR VALUES FROM ('2006-03-01') TO ('2006-04-01');
         
         ...
         CREATE TABLE measurement_y2007m11 PARTITION OF measurement
             FOR VALUES FROM ('2007-11-01') TO ('2007-12-01');
         
         CREATE TABLE measurement_y2007m12 PARTITION OF measurement
             FOR VALUES FROM ('2007-12-01') TO ('2008-01-01')
             TABLESPACE fasttablespace;
         
         CREATE TABLE measurement_y2008m01 PARTITION OF measurement
             FOR VALUES FROM ('2008-01-01') TO ('2008-02-01')
             WITH (parallel_workers = 4)
             TABLESPACE fasttablespace;
         

(Recall that adjacent partitions can share a bound value, since range upper
bounds are treated as exclusive bounds.)

If you wish to implement sub-partitioning, again specify the `PARTITION BY`
clause in the commands used to create individual partitions, for example:

         
         CREATE TABLE measurement_y2006m02 PARTITION OF measurement
             FOR VALUES FROM ('2006-02-01') TO ('2006-03-01')
             PARTITION BY RANGE (peaktemp);
         

After creating partitions of `measurement_y2006m02`, any data inserted into
`measurement` that is mapped to `measurement_y2006m02` (or data that is
directly inserted into `measurement_y2006m02`, which is allowed provided its
partition constraint is satisfied) will be further redirected to one of its
partitions based on the `peaktemp` column. The partition key specified may
overlap with the parent's partition key, although care should be taken when
specifying the bounds of a sub-partition such that the set of data it accepts
constitutes a subset of what the partition's own bounds allow; the system does
not try to check whether that's really the case.

Inserting data into the parent table that does not map to one of the existing
partitions will cause an error; an appropriate partition must be added
manually.

It is not necessary to manually create table constraints describing the
partition boundary conditions for partitions. Such constraints will be created
automatically.

  3. Create an index on the key column(s), as well as any other indexes you might want, on the partitioned table. (The key index is not strictly necessary, but in most scenarios it is helpful.) This automatically creates a matching index on each partition, and any partitions you create or attach later will also have such an index. An index or unique constraint declared on a partitioned table is “virtual” in the same way that the partitioned table is: the actual data is in child indexes on the individual partition tables.
         
         CREATE INDEX ON measurement (logdate);
         

  4. Ensure that the [enable_partition_pruning](runtime-config-query.html#GUC-ENABLE-PARTITION-PRUNING) configuration parameter is not disabled in `postgresql.conf`. If it is, queries will not be optimized as desired.

In the above example we would be creating a new partition each month, so it
might be wise to write a script that generates the required DDL automatically.

#### 5.11.2.2. Partition Maintenance #

Normally the set of partitions established when initially defining the table
is not intended to remain static. It is common to want to remove partitions
holding old data and periodically add new partitions for new data. One of the
most important advantages of partitioning is precisely that it allows this
otherwise painful task to be executed nearly instantaneously by manipulating
the partition structure, rather than physically moving large amounts of data
around.

The simplest option for removing old data is to drop the partition that is no
longer necessary:

    
    
    DROP TABLE measurement_y2006m02;
    

This can very quickly delete millions of records because it doesn't have to
individually delete every record. Note however that the above command requires
taking an `ACCESS EXCLUSIVE` lock on the parent table.

Another option that is often preferable is to remove the partition from the
partitioned table but retain access to it as a table in its own right. This
has two forms:

    
    
    ALTER TABLE measurement DETACH PARTITION measurement_y2006m02;
    ALTER TABLE measurement DETACH PARTITION measurement_y2006m02 CONCURRENTLY;
    

These allow further operations to be performed on the data before it is
dropped. For example, this is often a useful time to back up the data using
`COPY`, pg_dump, or similar tools. It might also be a useful time to aggregate
data into smaller formats, perform other data manipulations, or run reports.
The first form of the command requires an `ACCESS EXCLUSIVE` lock on the
parent table. Adding the `CONCURRENTLY` qualifier as in the second form allows
the detach operation to require only `SHARE UPDATE EXCLUSIVE` lock on the
parent table, but see [`ALTER TABLE ... DETACH PARTITION`](sql-
altertable.html#SQL-ALTERTABLE-DETACH-PARTITION) for details on the
restrictions.

Similarly we can add a new partition to handle new data. We can create an
empty partition in the partitioned table just as the original partitions were
created above:

    
    
    CREATE TABLE measurement_y2008m02 PARTITION OF measurement
        FOR VALUES FROM ('2008-02-01') TO ('2008-03-01')
        TABLESPACE fasttablespace;
    

As an alternative, it is sometimes more convenient to create the new table
outside the partition structure, and attach it as a partition later. This
allows new data to be loaded, checked, and transformed prior to it appearing
in the partitioned table. Moreover, the `ATTACH PARTITION` operation requires
only `SHARE UPDATE EXCLUSIVE` lock on the partitioned table, as opposed to the
`ACCESS EXCLUSIVE` lock that is required by `CREATE TABLE ... PARTITION OF`,
so it is more friendly to concurrent operations on the partitioned table. The
`CREATE TABLE ... LIKE` option is helpful to avoid tediously repeating the
parent table's definition:

    
    
    CREATE TABLE measurement_y2008m02
      (LIKE measurement INCLUDING DEFAULTS INCLUDING CONSTRAINTS)
      TABLESPACE fasttablespace;
    
    ALTER TABLE measurement_y2008m02 ADD CONSTRAINT y2008m02
       CHECK ( logdate >= DATE '2008-02-01' AND logdate < DATE '2008-03-01' );
    
    \copy measurement_y2008m02 from 'measurement_y2008m02'
    -- possibly some other data preparation work
    
    ALTER TABLE measurement ATTACH PARTITION measurement_y2008m02
        FOR VALUES FROM ('2008-02-01') TO ('2008-03-01' );
    

Before running the `ATTACH PARTITION` command, it is recommended to create a
`CHECK` constraint on the table to be attached that matches the expected
partition constraint, as illustrated above. That way, the system will be able
to skip the scan which is otherwise needed to validate the implicit partition
constraint. Without the `CHECK` constraint, the table will be scanned to
validate the partition constraint while holding an `ACCESS EXCLUSIVE` lock on
that partition. It is recommended to drop the now-redundant `CHECK` constraint
after the `ATTACH PARTITION` is complete. If the table being attached is
itself a partitioned table, then each of its sub-partitions will be
recursively locked and scanned until either a suitable `CHECK` constraint is
encountered or the leaf partitions are reached.

Similarly, if the partitioned table has a `DEFAULT` partition, it is
recommended to create a `CHECK` constraint which excludes the to-be-attached
partition's constraint. If this is not done then the `DEFAULT` partition will
be scanned to verify that it contains no records which should be located in
the partition being attached. This operation will be performed whilst holding
an `ACCESS EXCLUSIVE` lock on the `DEFAULT` partition. If the `DEFAULT`
partition is itself a partitioned table, then each of its partitions will be
recursively checked in the same way as the table being attached, as mentioned
above.

As explained above, it is possible to create indexes on partitioned tables so
that they are applied automatically to the entire hierarchy. This is very
convenient, as not only will the existing partitions become indexed, but also
any partitions that are created in the future will. One limitation is that
it's not possible to use the `CONCURRENTLY` qualifier when creating such a
partitioned index. To avoid long lock times, it is possible to use `CREATE
INDEX ON ONLY` the partitioned table; such an index is marked invalid, and the
partitions do not get the index applied automatically. The indexes on
partitions can be created individually using `CONCURRENTLY`, and then
_attached_ to the index on the parent using `ALTER INDEX .. ATTACH PARTITION`.
Once indexes for all partitions are attached to the parent index, the parent
index is marked valid automatically. Example:

    
    
    CREATE INDEX measurement_usls_idx ON ONLY measurement (unitsales);
    
    CREATE INDEX CONCURRENTLY measurement_usls_200602_idx
        ON measurement_y2006m02 (unitsales);
    ALTER INDEX measurement_usls_idx
        ATTACH PARTITION measurement_usls_200602_idx;
    ...
    

This technique can be used with `UNIQUE` and `PRIMARY KEY` constraints too;
the indexes are created implicitly when the constraint is created. Example:

    
    
    ALTER TABLE ONLY measurement ADD UNIQUE (city_id, logdate);
    
    ALTER TABLE measurement_y2006m02 ADD UNIQUE (city_id, logdate);
    ALTER INDEX measurement_city_id_logdate_key
        ATTACH PARTITION measurement_y2006m02_city_id_logdate_key;
    ...
    

#### 5.11.2.3. Limitations #

The following limitations apply to partitioned tables:

  * To create a unique or primary key constraint on a partitioned table, the partition keys must not include any expressions or function calls and the constraint's columns must include all of the partition key columns. This limitation exists because the individual indexes making up the constraint can only directly enforce uniqueness within their own partitions; therefore, the partition structure itself must guarantee that there are not duplicates in different partitions.

  * There is no way to create an exclusion constraint spanning the whole partitioned table. It is only possible to put such a constraint on each leaf partition individually. Again, this limitation stems from not being able to enforce cross-partition restrictions.

  * `BEFORE ROW` triggers on `INSERT` cannot change which partition is the final destination for a new row.

  * Mixing temporary and permanent relations in the same partition tree is not allowed. Hence, if the partitioned table is permanent, so must be its partitions and likewise if the partitioned table is temporary. When using temporary relations, all members of the partition tree have to be from the same session.

Individual partitions are linked to their partitioned table using inheritance
behind-the-scenes. However, it is not possible to use all of the generic
features of inheritance with declaratively partitioned tables or their
partitions, as discussed below. Notably, a partition cannot have any parents
other than the partitioned table it is a partition of, nor can a table inherit
from both a partitioned table and a regular table. That means partitioned
tables and their partitions never share an inheritance hierarchy with regular
tables.

Since a partition hierarchy consisting of the partitioned table and its
partitions is still an inheritance hierarchy, `tableoid` and all the normal
rules of inheritance apply as described in [Section 5.10](ddl-inherit.html
"5.10. Inheritance"), with a few exceptions:

  * Partitions cannot have columns that are not present in the parent. It is not possible to specify columns when creating partitions with `CREATE TABLE`, nor is it possible to add columns to partitions after-the-fact using `ALTER TABLE`. Tables may be added as a partition with `ALTER TABLE ... ATTACH PARTITION` only if their columns exactly match the parent.

  * Both `CHECK` and `NOT NULL` constraints of a partitioned table are always inherited by all its partitions. `CHECK` constraints that are marked `NO INHERIT` are not allowed to be created on partitioned tables. You cannot drop a `NOT NULL` constraint on a partition's column if the same constraint is present in the parent table.

  * Using `ONLY` to add or drop a constraint on only the partitioned table is supported as long as there are no partitions. Once partitions exist, using `ONLY` will result in an error for any constraints other than `UNIQUE` and `PRIMARY KEY`. Instead, constraints on the partitions themselves can be added and (if they are not present in the parent table) dropped.

  * As a partitioned table does not have any data itself, attempts to use `TRUNCATE` `ONLY` on a partitioned table will always return an error.

### 5.11.3. Partitioning Using Inheritance #

While the built-in declarative partitioning is suitable for most common use
cases, there are some circumstances where a more flexible approach may be
useful. Partitioning can be implemented using table inheritance, which allows
for several features not supported by declarative partitioning, such as:

  * For declarative partitioning, partitions must have exactly the same set of columns as the partitioned table, whereas with table inheritance, child tables may have extra columns not present in the parent.

  * Table inheritance allows for multiple inheritance.

  * Declarative partitioning only supports range, list and hash partitioning, whereas table inheritance allows data to be divided in a manner of the user's choosing. (Note, however, that if constraint exclusion is unable to prune child tables effectively, query performance might be poor.)

#### 5.11.3.1. Example #

This example builds a partitioning structure equivalent to the declarative
partitioning example above. Use the following steps:

  1. Create the “root” table, from which all of the “child” tables will inherit. This table will contain no data. Do not define any check constraints on this table, unless you intend them to be applied equally to all child tables. There is no point in defining any indexes or unique constraints on it, either. For our example, the root table is the `measurement` table as originally defined:
         
         CREATE TABLE measurement (
             city_id         int not null,
             logdate         date not null,
             peaktemp        int,
             unitsales       int
         );
         

  2. Create several “child” tables that each inherit from the root table. Normally, these tables will not add any columns to the set inherited from the root. Just as with declarative partitioning, these tables are in every way normal PostgreSQL tables (or foreign tables).
         
         CREATE TABLE measurement_y2006m02 () INHERITS (measurement);
         CREATE TABLE measurement_y2006m03 () INHERITS (measurement);
         ...
         CREATE TABLE measurement_y2007m11 () INHERITS (measurement);
         CREATE TABLE measurement_y2007m12 () INHERITS (measurement);
         CREATE TABLE measurement_y2008m01 () INHERITS (measurement);
         

  3. Add non-overlapping table constraints to the child tables to define the allowed key values in each.

Typical examples would be:

         
         CHECK ( x = 1 )
         CHECK ( county IN ( 'Oxfordshire', 'Buckinghamshire', 'Warwickshire' ))
         CHECK ( outletID >= 100 AND outletID < 200 )
         

Ensure that the constraints guarantee that there is no overlap between the key
values permitted in different child tables. A common mistake is to set up
range constraints like:

         
         CHECK ( outletID BETWEEN 100 AND 200 )
         CHECK ( outletID BETWEEN 200 AND 300 )
         

This is wrong since it is not clear which child table the key value 200
belongs in. Instead, ranges should be defined in this style:

         
         CREATE TABLE measurement_y2006m02 (
             CHECK ( logdate >= DATE '2006-02-01' AND logdate < DATE '2006-03-01' )
         ) INHERITS (measurement);
         
         CREATE TABLE measurement_y2006m03 (
             CHECK ( logdate >= DATE '2006-03-01' AND logdate < DATE '2006-04-01' )
         ) INHERITS (measurement);
         
         ...
         CREATE TABLE measurement_y2007m11 (
             CHECK ( logdate >= DATE '2007-11-01' AND logdate < DATE '2007-12-01' )
         ) INHERITS (measurement);
         
         CREATE TABLE measurement_y2007m12 (
             CHECK ( logdate >= DATE '2007-12-01' AND logdate < DATE '2008-01-01' )
         ) INHERITS (measurement);
         
         CREATE TABLE measurement_y2008m01 (
             CHECK ( logdate >= DATE '2008-01-01' AND logdate < DATE '2008-02-01' )
         ) INHERITS (measurement);
         

  4. For each child table, create an index on the key column(s), as well as any other indexes you might want.
         
         CREATE INDEX measurement_y2006m02_logdate ON measurement_y2006m02 (logdate);
         CREATE INDEX measurement_y2006m03_logdate ON measurement_y2006m03 (logdate);
         CREATE INDEX measurement_y2007m11_logdate ON measurement_y2007m11 (logdate);
         CREATE INDEX measurement_y2007m12_logdate ON measurement_y2007m12 (logdate);
         CREATE INDEX measurement_y2008m01_logdate ON measurement_y2008m01 (logdate);
         

  5. We want our application to be able to say `INSERT INTO measurement ...` and have the data be redirected into the appropriate child table. We can arrange that by attaching a suitable trigger function to the root table. If data will be added only to the latest child, we can use a very simple trigger function:
         
         CREATE OR REPLACE FUNCTION measurement_insert_trigger()
         RETURNS TRIGGER AS $$
         BEGIN
             INSERT INTO measurement_y2008m01 VALUES (NEW.*);
             RETURN NULL;
         END;
         $$
         LANGUAGE plpgsql;
         

After creating the function, we create a trigger which calls the trigger
function:

         
         CREATE TRIGGER insert_measurement_trigger
             BEFORE INSERT ON measurement
             FOR EACH ROW EXECUTE FUNCTION measurement_insert_trigger();
         

We must redefine the trigger function each month so that it always inserts
into the current child table. The trigger definition does not need to be
updated, however.

We might want to insert data and have the server automatically locate the
child table into which the row should be added. We could do this with a more
complex trigger function, for example:

         
         CREATE OR REPLACE FUNCTION measurement_insert_trigger()
         RETURNS TRIGGER AS $$
         BEGIN
             IF ( NEW.logdate >= DATE '2006-02-01' AND
                  NEW.logdate < DATE '2006-03-01' ) THEN
                 INSERT INTO measurement_y2006m02 VALUES (NEW.*);
             ELSIF ( NEW.logdate >= DATE '2006-03-01' AND
                     NEW.logdate < DATE '2006-04-01' ) THEN
                 INSERT INTO measurement_y2006m03 VALUES (NEW.*);
             ...
             ELSIF ( NEW.logdate >= DATE '2008-01-01' AND
                     NEW.logdate < DATE '2008-02-01' ) THEN
                 INSERT INTO measurement_y2008m01 VALUES (NEW.*);
             ELSE
                 RAISE EXCEPTION 'Date out of range.  Fix the measurement_insert_trigger() function!';
             END IF;
             RETURN NULL;
         END;
         $$
         LANGUAGE plpgsql;
         

The trigger definition is the same as before. Note that each `IF` test must
exactly match the `CHECK` constraint for its child table.

While this function is more complex than the single-month case, it doesn't
need to be updated as often, since branches can be added in advance of being
needed.

### Note

In practice, it might be best to check the newest child first, if most inserts
go into that child. For simplicity, we have shown the trigger's tests in the
same order as in other parts of this example.

A different approach to redirecting inserts into the appropriate child table
is to set up rules, instead of a trigger, on the root table. For example:

         
         CREATE RULE measurement_insert_y2006m02 AS
         ON INSERT TO measurement WHERE
             ( logdate >= DATE '2006-02-01' AND logdate < DATE '2006-03-01' )
         DO INSTEAD
             INSERT INTO measurement_y2006m02 VALUES (NEW.*);
         ...
         CREATE RULE measurement_insert_y2008m01 AS
         ON INSERT TO measurement WHERE
             ( logdate >= DATE '2008-01-01' AND logdate < DATE '2008-02-01' )
         DO INSTEAD
             INSERT INTO measurement_y2008m01 VALUES (NEW.*);
         

A rule has significantly more overhead than a trigger, but the overhead is
paid once per query rather than once per row, so this method might be
advantageous for bulk-insert situations. In most cases, however, the trigger
method will offer better performance.

Be aware that `COPY` ignores rules. If you want to use `COPY` to insert data,
you'll need to copy into the correct child table rather than directly into the
root. `COPY` does fire triggers, so you can use it normally if you use the
trigger approach.

Another disadvantage of the rule approach is that there is no simple way to
force an error if the set of rules doesn't cover the insertion date; the data
will silently go into the root table instead.

  6. Ensure that the [constraint_exclusion](runtime-config-query.html#GUC-CONSTRAINT-EXCLUSION) configuration parameter is not disabled in `postgresql.conf`; otherwise child tables may be accessed unnecessarily.

As we can see, a complex table hierarchy could require a substantial amount of
DDL. In the above example we would be creating a new child table each month,
so it might be wise to write a script that generates the required DDL
automatically.

#### 5.11.3.2. Maintenance for Inheritance Partitioning #

To remove old data quickly, simply drop the child table that is no longer
necessary:

    
    
    DROP TABLE measurement_y2006m02;
    

To remove the child table from the inheritance hierarchy table but retain
access to it as a table in its own right:

    
    
    ALTER TABLE measurement_y2006m02 NO INHERIT measurement;
    

To add a new child table to handle new data, create an empty child table just
as the original children were created above:

    
    
    CREATE TABLE measurement_y2008m02 (
        CHECK ( logdate >= DATE '2008-02-01' AND logdate < DATE '2008-03-01' )
    ) INHERITS (measurement);
    

Alternatively, one may want to create and populate the new child table before
adding it to the table hierarchy. This could allow data to be loaded, checked,
and transformed before being made visible to queries on the parent table.

    
    
    CREATE TABLE measurement_y2008m02
      (LIKE measurement INCLUDING DEFAULTS INCLUDING CONSTRAINTS);
    ALTER TABLE measurement_y2008m02 ADD CONSTRAINT y2008m02
       CHECK ( logdate >= DATE '2008-02-01' AND logdate < DATE '2008-03-01' );
    \copy measurement_y2008m02 from 'measurement_y2008m02'
    -- possibly some other data preparation work
    ALTER TABLE measurement_y2008m02 INHERIT measurement;
    

#### 5.11.3.3. Caveats #

The following caveats apply to partitioning implemented using inheritance:

  * There is no automatic way to verify that all of the `CHECK` constraints are mutually exclusive. It is safer to create code that generates child tables and creates and/or modifies associated objects than to write each by hand.

  * Indexes and foreign key constraints apply to single tables and not to their inheritance children, hence they have some [caveats](ddl-inherit.html#DDL-INHERIT-CAVEATS "5.10.1. Caveats") to be aware of.

  * The schemes shown here assume that the values of a row's key column(s) never change, or at least do not change enough to require it to move to another partition. An `UPDATE` that attempts to do that will fail because of the `CHECK` constraints. If you need to handle such cases, you can put suitable update triggers on the child tables, but it makes management of the structure much more complicated.

  * If you are using manual `VACUUM` or `ANALYZE` commands, don't forget that you need to run them on each child table individually. A command like:
        
        ANALYZE measurement;
        

will only process the root table.

  * `INSERT` statements with `ON CONFLICT` clauses are unlikely to work as expected, as the `ON CONFLICT` action is only taken in case of unique violations on the specified target relation, not its child relations.

  * Triggers or rules will be needed to route rows to the desired child table, unless the application is explicitly aware of the partitioning scheme. Triggers may be complicated to write, and will be much slower than the tuple routing performed internally by declarative partitioning.

### 5.11.4. Partition Pruning #

_Partition pruning_ is a query optimization technique that improves
performance for declaratively partitioned tables. As an example:

    
    
    SET enable_partition_pruning = on;                 -- the default
    SELECT count(*) FROM measurement WHERE logdate >= DATE '2008-01-01';
    

Without partition pruning, the above query would scan each of the partitions
of the `measurement` table. With partition pruning enabled, the planner will
examine the definition of each partition and prove that the partition need not
be scanned because it could not contain any rows meeting the query's `WHERE`
clause. When the planner can prove this, it excludes (_prunes_) the partition
from the query plan.

By using the EXPLAIN command and the [enable_partition_pruning](runtime-
config-query.html#GUC-ENABLE-PARTITION-PRUNING) configuration parameter, it's
possible to show the difference between a plan for which partitions have been
pruned and one for which they have not. A typical unoptimized plan for this
type of table setup is:

    
    
    SET enable_partition_pruning = off;
    EXPLAIN SELECT count(*) FROM measurement WHERE logdate >= DATE '2008-01-01';
                                        QUERY PLAN
    -------------------------------------------------------------------​----------------
     Aggregate  (cost=188.76..188.77 rows=1 width=8)
       ->  Append  (cost=0.00..181.05 rows=3085 width=0)
             ->  Seq Scan on measurement_y2006m02  (cost=0.00..33.12 rows=617 width=0)
                   Filter: (logdate >= '2008-01-01'::date)
             ->  Seq Scan on measurement_y2006m03  (cost=0.00..33.12 rows=617 width=0)
                   Filter: (logdate >= '2008-01-01'::date)
    ...
             ->  Seq Scan on measurement_y2007m11  (cost=0.00..33.12 rows=617 width=0)
                   Filter: (logdate >= '2008-01-01'::date)
             ->  Seq Scan on measurement_y2007m12  (cost=0.00..33.12 rows=617 width=0)
                   Filter: (logdate >= '2008-01-01'::date)
             ->  Seq Scan on measurement_y2008m01  (cost=0.00..33.12 rows=617 width=0)
                   Filter: (logdate >= '2008-01-01'::date)
    

Some or all of the partitions might use index scans instead of full-table
sequential scans, but the point here is that there is no need to scan the
older partitions at all to answer this query. When we enable partition
pruning, we get a significantly cheaper plan that will deliver the same
answer:

    
    
    SET enable_partition_pruning = on;
    EXPLAIN SELECT count(*) FROM measurement WHERE logdate >= DATE '2008-01-01';
                                        QUERY PLAN
    -------------------------------------------------------------------​----------------
     Aggregate  (cost=37.75..37.76 rows=1 width=8)
       ->  Seq Scan on measurement_y2008m01  (cost=0.00..33.12 rows=617 width=0)
             Filter: (logdate >= '2008-01-01'::date)
    

Note that partition pruning is driven only by the constraints defined
implicitly by the partition keys, not by the presence of indexes. Therefore it
isn't necessary to define indexes on the key columns. Whether an index needs
to be created for a given partition depends on whether you expect that queries
that scan the partition will generally scan a large part of the partition or
just a small part. An index will be helpful in the latter case but not the
former.

Partition pruning can be performed not only during the planning of a given
query, but also during its execution. This is useful as it can allow more
partitions to be pruned when clauses contain expressions whose values are not
known at query planning time, for example, parameters defined in a `PREPARE`
statement, using a value obtained from a subquery, or using a parameterized
value on the inner side of a nested loop join. Partition pruning during
execution can be performed at any of the following times:

  * During initialization of the query plan. Partition pruning can be performed here for parameter values which are known during the initialization phase of execution. Partitions which are pruned during this stage will not show up in the query's `EXPLAIN` or `EXPLAIN ANALYZE`. It is possible to determine the number of partitions which were removed during this phase by observing the “Subplans Removed” property in the `EXPLAIN` output. It's important to note that any partitions removed by the partition pruning done at this stage are still locked at the beginning of execution.

  * During actual execution of the query plan. Partition pruning may also be performed here to remove partitions using values which are only known during actual query execution. This includes values from subqueries and values from execution-time parameters such as those from parameterized nested loop joins. Since the value of these parameters may change many times during the execution of the query, partition pruning is performed whenever one of the execution parameters being used by partition pruning changes. Determining if partitions were pruned during this phase requires careful inspection of the `loops` property in the `EXPLAIN ANALYZE` output. Subplans corresponding to different partitions may have different values for it depending on how many times each of them was pruned during execution. Some may be shown as `(never executed)` if they were pruned every time.

Partition pruning can be disabled using the
[enable_partition_pruning](runtime-config-query.html#GUC-ENABLE-PARTITION-
PRUNING) setting.

### 5.11.5. Partitioning and Constraint Exclusion #

_Constraint exclusion_ is a query optimization technique similar to partition
pruning. While it is primarily used for partitioning implemented using the
legacy inheritance method, it can be used for other purposes, including with
declarative partitioning.

Constraint exclusion works in a very similar way to partition pruning, except
that it uses each table's `CHECK` constraints — which gives it its name —
whereas partition pruning uses the table's partition bounds, which exist only
in the case of declarative partitioning. Another difference is that constraint
exclusion is only applied at plan time; there is no attempt to remove
partitions at execution time.

The fact that constraint exclusion uses `CHECK` constraints, which makes it
slow compared to partition pruning, can sometimes be used as an advantage:
because constraints can be defined even on declaratively-partitioned tables,
in addition to their internal partition bounds, constraint exclusion may be
able to elide additional partitions from the query plan.

The default (and recommended) setting of [constraint_exclusion](runtime-
config-query.html#GUC-CONSTRAINT-EXCLUSION) is neither `on` nor `off`, but an
intermediate setting called `partition`, which causes the technique to be
applied only to queries that are likely to be working on inheritance
partitioned tables. The `on` setting causes the planner to examine `CHECK`
constraints in all queries, even simple ones that are unlikely to benefit.

The following caveats apply to constraint exclusion:

  * Constraint exclusion is only applied during query planning, unlike partition pruning, which can also be applied during query execution.

  * Constraint exclusion only works when the query's `WHERE` clause contains constants (or externally supplied parameters). For example, a comparison against a non-immutable function such as `CURRENT_TIMESTAMP` cannot be optimized, since the planner cannot know which child table the function's value might fall into at run time.

  * Keep the partitioning constraints simple, else the planner may not be able to prove that child tables might not need to be visited. Use simple equality conditions for list partitioning, or simple range tests for range partitioning, as illustrated in the preceding examples. A good rule of thumb is that partitioning constraints should contain only comparisons of the partitioning column(s) to constants using B-tree-indexable operators, because only B-tree-indexable column(s) are allowed in the partition key.

  * All constraints on all children of the parent table are examined during constraint exclusion, so large numbers of children are likely to increase query planning time considerably. So the legacy inheritance based partitioning will work well with up to perhaps a hundred child tables; don't try to use many thousands of children.

### 5.11.6. Best Practices for Declarative Partitioning #

The choice of how to partition a table should be made carefully, as the
performance of query planning and execution can be negatively affected by poor
design.

One of the most critical design decisions will be the column or columns by
which you partition your data. Often the best choice will be to partition by
the column or set of columns which most commonly appear in `WHERE` clauses of
queries being executed on the partitioned table. `WHERE` clauses that are
compatible with the partition bound constraints can be used to prune unneeded
partitions. However, you may be forced into making other decisions by
requirements for the `PRIMARY KEY` or a `UNIQUE` constraint. Removal of
unwanted data is also a factor to consider when planning your partitioning
strategy. An entire partition can be detached fairly quickly, so it may be
beneficial to design the partition strategy in such a way that all data to be
removed at once is located in a single partition.

Choosing the target number of partitions that the table should be divided into
is also a critical decision to make. Not having enough partitions may mean
that indexes remain too large and that data locality remains poor which could
result in low cache hit ratios. However, dividing the table into too many
partitions can also cause issues. Too many partitions can mean longer query
planning times and higher memory consumption during both query planning and
execution, as further described below. When choosing how to partition your
table, it's also important to consider what changes may occur in the future.
For example, if you choose to have one partition per customer and you
currently have a small number of large customers, consider the implications if
in several years you instead find yourself with a large number of small
customers. In this case, it may be better to choose to partition by `HASH` and
choose a reasonable number of partitions rather than trying to partition by
`LIST` and hoping that the number of customers does not increase beyond what
it is practical to partition the data by.

Sub-partitioning can be useful to further divide partitions that are expected
to become larger than other partitions. Another option is to use range
partitioning with multiple columns in the partition key. Either of these can
easily lead to excessive numbers of partitions, so restraint is advisable.

It is important to consider the overhead of partitioning during query planning
and execution. The query planner is generally able to handle partition
hierarchies with up to a few thousand partitions fairly well, provided that
typical queries allow the query planner to prune all but a small number of
partitions. Planning times become longer and memory consumption becomes higher
when more partitions remain after the planner performs partition pruning.
Another reason to be concerned about having a large number of partitions is
that the server's memory consumption may grow significantly over time,
especially if many sessions touch large numbers of partitions. That's because
each partition requires its metadata to be loaded into the local memory of
each session that touches it.

With data warehouse type workloads, it can make sense to use a larger number
of partitions than with an OLTP type workload. Generally, in data warehouses,
query planning time is less of a concern as the majority of processing time is
spent during query execution. With either of these two types of workload, it
is important to make the right decisions early, as re-partitioning large
quantities of data can be painfully slow. Simulations of the intended workload
are often beneficial for optimizing the partitioning strategy. Never just
assume that more partitions are better than fewer partitions, nor vice-versa.

* * *

[Prev](ddl-inherit.html "5.10. Inheritance")  | [Up](ddl.html "Chapter 5. Data Definition") |  [Next](ddl-foreign-data.html "5.12. Foreign Data")  
---|---|---  
5.10. Inheritance  | [Home](index.html "PostgreSQL 16.9 Documentation") |  5.12. Foreign Data  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ddl-partitioning.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

