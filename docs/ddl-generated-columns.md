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

Supported Versions: [Current](/docs/current/ddl-generated-columns.html
"PostgreSQL 17 - 5.3. Generated Columns") ([17](/docs/17/ddl-generated-
columns.html "PostgreSQL 17 - 5.3. Generated Columns")) / [16](/docs/16/ddl-
generated-columns.html "PostgreSQL 16 - 5.3. Generated Columns") /
[15](/docs/15/ddl-generated-columns.html "PostgreSQL 15 - 5.3. Generated
Columns") / [14](/docs/14/ddl-generated-columns.html "PostgreSQL 14 -
5.3. Generated Columns") / [13](/docs/13/ddl-generated-columns.html
"PostgreSQL 13 - 5.3. Generated Columns")

Development Versions: [18](/docs/18/ddl-generated-columns.html "PostgreSQL 18
- 5.3. Generated Columns") / [devel](/docs/devel/ddl-generated-columns.html
"PostgreSQL devel - 5.3. Generated Columns")

Unsupported versions: [12](/docs/12/ddl-generated-columns.html "PostgreSQL 12
- 5.3. Generated Columns")

__

5.3. Generated Columns  
---  
[Prev](ddl-default.html "5.2. Default Values")  | [Up](ddl.html "Chapter 5. Data Definition") | Chapter 5. Data Definition | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ddl-constraints.html "5.4. Constraints")  
  
* * *

## 5.3. Generated Columns #

A generated column is a special column that is always computed from other
columns. Thus, it is for columns what a view is for tables. There are two
kinds of generated columns: stored and virtual. A stored generated column is
computed when it is written (inserted or updated) and occupies storage as if
it were a normal column. A virtual generated column occupies no storage and is
computed when it is read. Thus, a virtual generated column is similar to a
view and a stored generated column is similar to a materialized view (except
that it is always updated automatically). PostgreSQL currently implements only
stored generated columns.

To create a generated column, use the `GENERATED ALWAYS AS` clause in `CREATE
TABLE`, for example:

    
    
    CREATE TABLE people (
        ...,
        height_cm numeric,
        height_in numeric **GENERATED ALWAYS AS (height_cm / 2.54) STORED**
    );
    

The keyword `STORED` must be specified to choose the stored kind of generated
column. See [CREATE TABLE](sql-createtable.html "CREATE TABLE") for more
details.

A generated column cannot be written to directly. In `INSERT` or `UPDATE`
commands, a value cannot be specified for a generated column, but the keyword
`DEFAULT` may be specified.

Consider the differences between a column with a default and a generated
column. The column default is evaluated once when the row is first inserted if
no other value was provided; a generated column is updated whenever the row
changes and cannot be overridden. A column default may not refer to other
columns of the table; a generation expression would normally do so. A column
default can use volatile functions, for example `random()` or functions
referring to the current time; this is not allowed for generated columns.

Several restrictions apply to the definition of generated columns and tables
involving generated columns:

  * The generation expression can only use immutable functions and cannot use subqueries or reference anything other than the current row in any way.

  * A generation expression cannot reference another generated column.

  * A generation expression cannot reference a system column, except `tableoid`.

  * A generated column cannot have a column default or an identity definition.

  * A generated column cannot be part of a partition key.

  * Foreign tables can have generated columns. See [CREATE FOREIGN TABLE](sql-createforeigntable.html "CREATE FOREIGN TABLE") for details.

  * For inheritance and partitioning:

    * If a parent column is a generated column, its child column must also be a generated column; however, the child column can have a different generation expression. The generation expression that is actually applied during insert or update of a row is the one associated with the table that the row is physically in. (This is unlike the behavior for column defaults: for those, the default value associated with the table named in the query applies.)

    * If a parent column is not a generated column, its child column must not be generated either.

    * For inherited tables, if you write a child column definition without any `GENERATED` clause in `CREATE TABLE ... INHERITS`, then its `GENERATED` clause will automatically be copied from the parent. `ALTER TABLE ... INHERIT` will insist that parent and child columns already match as to generation status, but it will not require their generation expressions to match.

    * Similarly for partitioned tables, if you write a child column definition without any `GENERATED` clause in `CREATE TABLE ... PARTITION OF`, then its `GENERATED` clause will automatically be copied from the parent. `ALTER TABLE ... ATTACH PARTITION` will insist that parent and child columns already match as to generation status, but it will not require their generation expressions to match.

    * In case of multiple inheritance, if one parent column is a generated column, then all parent columns must be generated columns. If they do not all have the same generation expression, then the desired expression for the child must be specified explicitly.

Additional considerations apply to the use of generated columns.

  * Generated columns maintain access privileges separately from their underlying base columns. So, it is possible to arrange it so that a particular role can read from a generated column but not from the underlying base columns.

  * Generated columns are, conceptually, updated after `BEFORE` triggers have run. Therefore, changes made to base columns in a `BEFORE` trigger will be reflected in generated columns. But conversely, it is not allowed to access generated columns in `BEFORE` triggers.

  * Generated columns are skipped for logical replication and cannot be specified in a `CREATE PUBLICATION` column list.

* * *

[Prev](ddl-default.html "5.2. Default Values")  | [Up](ddl.html "Chapter 5. Data Definition") |  [Next](ddl-constraints.html "5.4. Constraints")  
---|---|---  
5.2. Default Values  | [Home](index.html "PostgreSQL 16.9 Documentation") |  5.4. Constraints  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ddl-generated-columns.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

