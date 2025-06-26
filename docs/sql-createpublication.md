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

Supported Versions: [Current](/docs/current/sql-createpublication.html
"PostgreSQL 17 - CREATE PUBLICATION") ([17](/docs/17/sql-
createpublication.html "PostgreSQL 17 - CREATE PUBLICATION")) /
[16](/docs/16/sql-createpublication.html "PostgreSQL 16 - CREATE PUBLICATION")
/ [15](/docs/15/sql-createpublication.html "PostgreSQL 15 - CREATE
PUBLICATION") / [14](/docs/14/sql-createpublication.html "PostgreSQL 14 -
CREATE PUBLICATION") / [13](/docs/13/sql-createpublication.html "PostgreSQL 13
- CREATE PUBLICATION")

Development Versions: [18](/docs/18/sql-createpublication.html "PostgreSQL 18
- CREATE PUBLICATION") / [devel](/docs/devel/sql-createpublication.html
"PostgreSQL devel - CREATE PUBLICATION")

Unsupported versions: [12](/docs/12/sql-createpublication.html "PostgreSQL 12
- CREATE PUBLICATION") / [11](/docs/11/sql-createpublication.html "PostgreSQL
11 - CREATE PUBLICATION") / [10](/docs/10/sql-createpublication.html
"PostgreSQL 10 - CREATE PUBLICATION")

__

CREATE PUBLICATION  
---  
[Prev](sql-createprocedure.html "CREATE PROCEDURE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createrole.html "CREATE ROLE")  
  
* * *

## CREATE PUBLICATION

CREATE PUBLICATION — define a new publication

## Synopsis

    
    
    CREATE PUBLICATION _name_
        [ FOR ALL TABLES
          | FOR _publication_object_ [, ... ] ]
        [ WITH ( _publication_parameter_ [= _value_] [, ... ] ) ]
    
    where _publication_object_ is one of:
    
        TABLE [ ONLY ] _table_name_ [ * ] [ ( _column_name_ [, ... ] ) ] [ WHERE ( _expression_ ) ] [, ... ]
        TABLES IN SCHEMA { _schema_name_ | CURRENT_SCHEMA } [, ... ]
    

## Description

`CREATE PUBLICATION` adds a new publication into the current database. The
publication name must be distinct from the name of any existing publication in
the current database.

A publication is essentially a group of tables whose data changes are intended
to be replicated through logical replication. See [Section 31.1](logical-
replication-publication.html "31.1. Publication") for details about how
publications fit into the logical replication setup.

## Parameters

_`name`_ #

    

The name of the new publication.

`FOR TABLE` #

    

Specifies a list of tables to add to the publication. If `ONLY` is specified
before the table name, only that table is added to the publication. If `ONLY`
is not specified, the table and all its descendant tables (if any) are added.
Optionally, `*` can be specified after the table name to explicitly indicate
that descendant tables are included. This does not apply to a partitioned
table, however. The partitions of a partitioned table are always implicitly
considered part of the publication, so they are never explicitly added to the
publication.

If the optional `WHERE` clause is specified, it defines a _row filter_
expression. Rows for which the _`expression`_ evaluates to false or null will
not be published. Note that parentheses are required around the expression. It
has no effect on `TRUNCATE` commands.

When a column list is specified, only the named columns are replicated. If no
column list is specified, all columns of the table are replicated through this
publication, including any columns added later. It has no effect on `TRUNCATE`
commands. See [Section 31.4](logical-replication-col-lists.html "31.4. Column
Lists") for details about column lists.

Only persistent base tables and partitioned tables can be part of a
publication. Temporary tables, unlogged tables, foreign tables, materialized
views, and regular views cannot be part of a publication.

Specifying a column list when the publication also publishes `FOR TABLES IN
SCHEMA` is not supported.

When a partitioned table is added to a publication, all of its existing and
future partitions are implicitly considered to be part of the publication. So,
even operations that are performed directly on a partition are also published
via publications that its ancestors are part of.

`FOR ALL TABLES` #

    

Marks the publication as one that replicates changes for all tables in the
database, including tables created in the future.

`FOR TABLES IN SCHEMA` #

    

Marks the publication as one that replicates changes for all tables in the
specified list of schemas, including tables created in the future.

Specifying a schema when the publication also publishes a table with a column
list is not supported.

Only persistent base tables and partitioned tables present in the schema will
be included as part of the publication. Temporary tables, unlogged tables,
foreign tables, materialized views, and regular views from the schema will not
be part of the publication.

When a partitioned table is published via schema level publication, all of its
existing and future partitions are implicitly considered to be part of the
publication, regardless of whether they are from the publication schema or
not. So, even operations that are performed directly on a partition are also
published via publications that its ancestors are part of.

`WITH ( _`publication_parameter`_ [= _`value`_] [, ... ] )` #

    

This clause specifies optional parameters for a publication. The following
parameters are supported:

`publish` (`string`) #

    

This parameter determines which DML operations will be published by the new
publication to the subscribers. The value is comma-separated list of
operations. The allowed operations are `insert`, `update`, `delete`, and
`truncate`. The default is to publish all actions, and so the default value
for this option is `'insert, update, delete, truncate'`.

This parameter only affects DML operations. In particular, the initial data
synchronization (see [Section 31.7.1](logical-replication-
architecture.html#LOGICAL-REPLICATION-SNAPSHOT "31.7.1. Initial Snapshot"))
for logical replication does not take this parameter into account when copying
existing table data.

`publish_via_partition_root` (`boolean`) #

    

This parameter determines whether changes in a partitioned table (or on its
partitions) contained in the publication will be published using the identity
and schema of the partitioned table rather than that of the individual
partitions that are actually changed; the latter is the default. Enabling this
allows the changes to be replicated into a non-partitioned table or a
partitioned table consisting of a different set of partitions.

There can be a case where a subscription combines multiple publications. If a
partitioned table is published by any subscribed publications which set
`publish_via_partition_root = true`, changes on this partitioned table (or on
its partitions) will be published using the identity and schema of this
partitioned table rather than that of the individual partitions.

This parameter also affects how row filters and column lists are chosen for
partitions; see below for details.

If this is enabled, `TRUNCATE` operations performed directly on partitions are
not replicated.

When specifying a parameter of type `boolean`, the `=` _`value`_ part can be
omitted, which is equivalent to specifying `TRUE`.

## Notes

If `FOR TABLE`, `FOR ALL TABLES` or `FOR TABLES IN SCHEMA` are not specified,
then the publication starts out with an empty set of tables. That is useful if
tables or schemas are to be added later.

The creation of a publication does not start replication. It only defines a
grouping and filtering logic for future subscribers.

To create a publication, the invoking user must have the `CREATE` privilege
for the current database. (Of course, superusers bypass this check.)

To add a table to a publication, the invoking user must have ownership rights
on the table. The `FOR ALL TABLES` and `FOR TABLES IN SCHEMA` clauses require
the invoking user to be a superuser.

The tables added to a publication that publishes `UPDATE` and/or `DELETE`
operations must have `REPLICA IDENTITY` defined. Otherwise those operations
will be disallowed on those tables.

Any column list must include the `REPLICA IDENTITY` columns in order for
`UPDATE` or `DELETE` operations to be published. There are no column list
restrictions if the publication publishes only `INSERT` operations.

A row filter expression (i.e., the `WHERE` clause) must contain only columns
that are covered by the `REPLICA IDENTITY`, in order for `UPDATE` and `DELETE`
operations to be published. For publication of `INSERT` operations, any column
may be used in the `WHERE` expression. The row filter allows simple
expressions that don't have user-defined functions, user-defined operators,
user-defined types, user-defined collations, non-immutable built-in functions,
or references to system columns.

The row filter on a table becomes redundant if `FOR TABLES IN SCHEMA` is
specified and the table belongs to the referred schema.

For published partitioned tables, the row filter for each partition is taken
from the published partitioned table if the publication parameter
`publish_via_partition_root` is true, or from the partition itself if it is
false (the default). See [Section 31.3](logical-replication-row-filter.html
"31.3. Row Filters") for details about row filters. Similarly, for published
partitioned tables, the column list for each partition is taken from the
published partitioned table if the publication parameter
`publish_via_partition_root` is true, or from the partition itself if it is
false.

For an `INSERT ... ON CONFLICT` command, the publication will publish the
operation that results from the command. Depending on the outcome, it may be
published as either `INSERT` or `UPDATE`, or it may not be published at all.

For a `MERGE` command, the publication will publish an `INSERT`, `UPDATE`, or
`DELETE` for each row inserted, updated, or deleted.

`ATTACH`ing a table into a partition tree whose root is published using a
publication with `publish_via_partition_root` set to `true` does not result in
the table's existing contents being replicated.

`COPY ... FROM` commands are published as `INSERT` operations.

DDL operations are not published.

The `WHERE` clause expression is executed with the role used for the
replication connection.

## Examples

Create a publication that publishes all changes in two tables:

    
    
    CREATE PUBLICATION mypublication FOR TABLE users, departments;
    

Create a publication that publishes all changes from active departments:

    
    
    CREATE PUBLICATION active_departments FOR TABLE departments WHERE (active IS TRUE);
    

Create a publication that publishes all changes in all tables:

    
    
    CREATE PUBLICATION alltables FOR ALL TABLES;
    

Create a publication that only publishes `INSERT` operations in one table:

    
    
    CREATE PUBLICATION insert_only FOR TABLE mydata
        WITH (publish = 'insert');
    

Create a publication that publishes all changes for tables `users`,
`departments` and all changes for all the tables present in the schema
`production`:

    
    
    CREATE PUBLICATION production_publication FOR TABLE users, departments, TABLES IN SCHEMA production;
    

Create a publication that publishes all changes for all the tables present in
the schemas `marketing` and `sales`:

    
    
    CREATE PUBLICATION sales_publication FOR TABLES IN SCHEMA marketing, sales;
    

Create a publication that publishes all changes for table `users`, but
replicates only columns `user_id` and `firstname`:

    
    
    CREATE PUBLICATION users_filtered FOR TABLE users (user_id, firstname);
    

## Compatibility

`CREATE PUBLICATION` is a PostgreSQL extension.

## See Also

[ALTER PUBLICATION](sql-alterpublication.html "ALTER PUBLICATION"), [DROP
PUBLICATION](sql-droppublication.html "DROP PUBLICATION"), [CREATE
SUBSCRIPTION](sql-createsubscription.html "CREATE SUBSCRIPTION"), [ALTER
SUBSCRIPTION](sql-altersubscription.html "ALTER SUBSCRIPTION")

* * *

[Prev](sql-createprocedure.html "CREATE PROCEDURE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createrole.html "CREATE ROLE")  
---|---|---  
CREATE PROCEDURE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE ROLE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createpublication.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

