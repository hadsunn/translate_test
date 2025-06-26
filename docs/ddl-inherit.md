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

Supported Versions: [Current](/docs/current/ddl-inherit.html "PostgreSQL 17 -
5.10. Inheritance") ([17](/docs/17/ddl-inherit.html "PostgreSQL 17 -
5.10. Inheritance")) / [16](/docs/16/ddl-inherit.html "PostgreSQL 16 -
5.10. Inheritance") / [15](/docs/15/ddl-inherit.html "PostgreSQL 15 -
5.10. Inheritance") / [14](/docs/14/ddl-inherit.html "PostgreSQL 14 -
5.10. Inheritance") / [13](/docs/13/ddl-inherit.html "PostgreSQL 13 -
5.10. Inheritance")

Development Versions: [18](/docs/18/ddl-inherit.html "PostgreSQL 18 -
5.10. Inheritance") / [devel](/docs/devel/ddl-inherit.html "PostgreSQL devel -
5.10. Inheritance")

Unsupported versions: [12](/docs/12/ddl-inherit.html "PostgreSQL 12 -
5.10. Inheritance") / [11](/docs/11/ddl-inherit.html "PostgreSQL 11 -
5.10. Inheritance") / [10](/docs/10/ddl-inherit.html "PostgreSQL 10 -
5.10. Inheritance") / [9.6](/docs/9.6/ddl-inherit.html "PostgreSQL 9.6 -
5.10. Inheritance") / [9.5](/docs/9.5/ddl-inherit.html "PostgreSQL 9.5 -
5.10. Inheritance") / [9.4](/docs/9.4/ddl-inherit.html "PostgreSQL 9.4 -
5.10. Inheritance") / [9.3](/docs/9.3/ddl-inherit.html "PostgreSQL 9.3 -
5.10. Inheritance") / [9.2](/docs/9.2/ddl-inherit.html "PostgreSQL 9.2 -
5.10. Inheritance") / [9.1](/docs/9.1/ddl-inherit.html "PostgreSQL 9.1 -
5.10. Inheritance") / [9.0](/docs/9.0/ddl-inherit.html "PostgreSQL 9.0 -
5.10. Inheritance") / [8.4](/docs/8.4/ddl-inherit.html "PostgreSQL 8.4 -
5.10. Inheritance") / [8.3](/docs/8.3/ddl-inherit.html "PostgreSQL 8.3 -
5.10. Inheritance") / [8.2](/docs/8.2/ddl-inherit.html "PostgreSQL 8.2 -
5.10. Inheritance") / [8.1](/docs/8.1/ddl-inherit.html "PostgreSQL 8.1 -
5.10. Inheritance") / [8.0](/docs/8.0/ddl-inherit.html "PostgreSQL 8.0 -
5.10. Inheritance") / [7.4](/docs/7.4/ddl-inherit.html "PostgreSQL 7.4 -
5.10. Inheritance") / [7.3](/docs/7.3/ddl-inherit.html "PostgreSQL 7.3 -
5.10. Inheritance")

__

5.10. Inheritance  
---  
[Prev](ddl-schemas.html "5.9. Schemas")  | [Up](ddl.html "Chapter 5. Data Definition") | Chapter 5. Data Definition | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ddl-partitioning.html "5.11. Table Partitioning")  
  
* * *

## 5.10. Inheritance #

[5.10.1. Caveats](ddl-inherit.html#DDL-INHERIT-CAVEATS)

PostgreSQL implements table inheritance, which can be a useful tool for
database designers. (SQL:1999 and later define a type inheritance feature,
which differs in many respects from the features described here.)

Let's start with an example: suppose we are trying to build a data model for
cities. Each state has many cities, but only one capital. We want to be able
to quickly retrieve the capital city for any particular state. This can be
done by creating two tables, one for state capitals and one for cities that
are not capitals. However, what happens when we want to ask for data about a
city, regardless of whether it is a capital or not? The inheritance feature
can help to resolve this problem. We define the `capitals` table so that it
inherits from `cities`:

    
    
    CREATE TABLE cities (
        name            text,
        population      float,
        elevation       int     -- in feet
    );
    
    CREATE TABLE capitals (
        state           char(2)
    ) INHERITS (cities);
    

In this case, the `capitals` table _inherits_ all the columns of its parent
table, `cities`. State capitals also have an extra column, `state`, that shows
their state.

In PostgreSQL, a table can inherit from zero or more other tables, and a query
can reference either all rows of a table or all rows of a table plus all of
its descendant tables. The latter behavior is the default. For example, the
following query finds the names of all cities, including state capitals, that
are located at an elevation over 500 feet:

    
    
    SELECT name, elevation
        FROM cities
        WHERE elevation > 500;
    

Given the sample data from the PostgreSQL tutorial (see [Section
2.1](tutorial-sql-intro.html "2.1. Introduction")), this returns:

    
    
       name    | elevation
    -----------+-----------
     Las Vegas |      2174
     Mariposa  |      1953
     Madison   |       845
    

On the other hand, the following query finds all the cities that are not state
capitals and are situated at an elevation over 500 feet:

    
    
    SELECT name, elevation
        FROM ONLY cities
        WHERE elevation > 500;
    
       name    | elevation
    -----------+-----------
     Las Vegas |      2174
     Mariposa  |      1953
    

Here the `ONLY` keyword indicates that the query should apply only to
`cities`, and not any tables below `cities` in the inheritance hierarchy. Many
of the commands that we have already discussed — `SELECT`, `UPDATE` and
`DELETE` — support the `ONLY` keyword.

You can also write the table name with a trailing `*` to explicitly specify
that descendant tables are included:

    
    
    SELECT name, elevation
        FROM cities*
        WHERE elevation > 500;
    

Writing `*` is not necessary, since this behavior is always the default.
However, this syntax is still supported for compatibility with older releases
where the default could be changed.

In some cases you might wish to know which table a particular row originated
from. There is a system column called `tableoid` in each table which can tell
you the originating table:

    
    
    SELECT c.tableoid, c.name, c.elevation
    FROM cities c
    WHERE c.elevation > 500;
    

which returns:

    
    
     tableoid |   name    | elevation
    ----------+-----------+-----------
       139793 | Las Vegas |      2174
       139793 | Mariposa  |      1953
       139798 | Madison   |       845
    

(If you try to reproduce this example, you will probably get different numeric
OIDs.) By doing a join with `pg_class` you can see the actual table names:

    
    
    SELECT p.relname, c.name, c.elevation
    FROM cities c, pg_class p
    WHERE c.elevation > 500 AND c.tableoid = p.oid;
    

which returns:

    
    
     relname  |   name    | elevation
    ----------+-----------+-----------
     cities   | Las Vegas |      2174
     cities   | Mariposa  |      1953
     capitals | Madison   |       845
    

Another way to get the same effect is to use the `regclass` alias type, which
will print the table OID symbolically:

    
    
    SELECT c.tableoid::regclass, c.name, c.elevation
    FROM cities c
    WHERE c.elevation > 500;
    

Inheritance does not automatically propagate data from `INSERT` or `COPY`
commands to other tables in the inheritance hierarchy. In our example, the
following `INSERT` statement will fail:

    
    
    INSERT INTO cities (name, population, elevation, state)
    VALUES ('Albany', NULL, NULL, 'NY');
    

We might hope that the data would somehow be routed to the `capitals` table,
but this does not happen: `INSERT` always inserts into exactly the table
specified. In some cases it is possible to redirect the insertion using a rule
(see [Chapter 41](rules.html "Chapter 41. The Rule System")). However that
does not help for the above case because the `cities` table does not contain
the column `state`, and so the command will be rejected before the rule can be
applied.

All check constraints and not-null constraints on a parent table are
automatically inherited by its children, unless explicitly specified otherwise
with `NO INHERIT` clauses. Other types of constraints (unique, primary key,
and foreign key constraints) are not inherited.

A table can inherit from more than one parent table, in which case it has the
union of the columns defined by the parent tables. Any columns declared in the
child table's definition are added to these. If the same column name appears
in multiple parent tables, or in both a parent table and the child's
definition, then these columns are “merged” so that there is only one such
column in the child table. To be merged, columns must have the same data
types, else an error is raised. Inheritable check constraints and not-null
constraints are merged in a similar fashion. Thus, for example, a merged
column will be marked not-null if any one of the column definitions it came
from is marked not-null. Check constraints are merged if they have the same
name, and the merge will fail if their conditions are different.

Table inheritance is typically established when the child table is created,
using the `INHERITS` clause of the [`CREATE TABLE`](sql-createtable.html
"CREATE TABLE") statement. Alternatively, a table which is already defined in
a compatible way can have a new parent relationship added, using the `INHERIT`
variant of [`ALTER TABLE`](sql-altertable.html "ALTER TABLE"). To do this the
new child table must already include columns with the same names and types as
the columns of the parent. It must also include check constraints with the
same names and check expressions as those of the parent. Similarly an
inheritance link can be removed from a child using the `NO INHERIT` variant of
`ALTER TABLE`. Dynamically adding and removing inheritance links like this can
be useful when the inheritance relationship is being used for table
partitioning (see [Section 5.11](ddl-partitioning.html "5.11. Table
Partitioning")).

One convenient way to create a compatible table that will later be made a new
child is to use the `LIKE` clause in `CREATE TABLE`. This creates a new table
with the same columns as the source table. If there are any `CHECK`
constraints defined on the source table, the `INCLUDING CONSTRAINTS` option to
`LIKE` should be specified, as the new child must have constraints matching
the parent to be considered compatible.

A parent table cannot be dropped while any of its children remain. Neither can
columns or check constraints of child tables be dropped or altered if they are
inherited from any parent tables. If you wish to remove a table and all of its
descendants, one easy way is to drop the parent table with the `CASCADE`
option (see [Section 5.14](ddl-depend.html "5.14. Dependency Tracking")).

`ALTER TABLE` will propagate any changes in column data definitions and check
constraints down the inheritance hierarchy. Again, dropping columns that are
depended on by other tables is only possible when using the `CASCADE` option.
`ALTER TABLE` follows the same rules for duplicate column merging and
rejection that apply during `CREATE TABLE`.

Inherited queries perform access permission checks on the parent table only.
Thus, for example, granting `UPDATE` permission on the `cities` table implies
permission to update rows in the `capitals` table as well, when they are
accessed through `cities`. This preserves the appearance that the data is
(also) in the parent table. But the `capitals` table could not be updated
directly without an additional grant. In a similar way, the parent table's row
security policies (see [Section 5.8](ddl-rowsecurity.html "5.8. Row Security
Policies")) are applied to rows coming from child tables during an inherited
query. A child table's policies, if any, are applied only when it is the table
explicitly named in the query; and in that case, any policies attached to its
parent(s) are ignored.

Foreign tables (see [Section 5.12](ddl-foreign-data.html "5.12. Foreign
Data")) can also be part of inheritance hierarchies, either as parent or child
tables, just as regular tables can be. If a foreign table is part of an
inheritance hierarchy then any operations not supported by the foreign table
are not supported on the whole hierarchy either.

### 5.10.1. Caveats #

Note that not all SQL commands are able to work on inheritance hierarchies.
Commands that are used for data querying, data modification, or schema
modification (e.g., `SELECT`, `UPDATE`, `DELETE`, most variants of `ALTER
TABLE`, but not `INSERT` or `ALTER TABLE ... RENAME`) typically default to
including child tables and support the `ONLY` notation to exclude them.
Commands that do database maintenance and tuning (e.g., `REINDEX`, `VACUUM`)
typically only work on individual, physical tables and do not support
recursing over inheritance hierarchies. The respective behavior of each
individual command is documented in its reference page ([SQL Commands](sql-
commands.html "SQL Commands")).

A serious limitation of the inheritance feature is that indexes (including
unique constraints) and foreign key constraints only apply to single tables,
not to their inheritance children. This is true on both the referencing and
referenced sides of a foreign key constraint. Thus, in the terms of the above
example:

  * If we declared `cities`.`name` to be `UNIQUE` or a `PRIMARY KEY`, this would not stop the `capitals` table from having rows with names duplicating rows in `cities`. And those duplicate rows would by default show up in queries from `cities`. In fact, by default `capitals` would have no unique constraint at all, and so could contain multiple rows with the same name. You could add a unique constraint to `capitals`, but this would not prevent duplication compared to `cities`.

  * Similarly, if we were to specify that `cities`.`name` `REFERENCES` some other table, this constraint would not automatically propagate to `capitals`. In this case you could work around it by manually adding the same `REFERENCES` constraint to `capitals`.

  * Specifying that another table's column `REFERENCES cities(name)` would allow the other table to contain city names, but not capital names. There is no good workaround for this case.

Some functionality not implemented for inheritance hierarchies is implemented
for declarative partitioning. Considerable care is needed in deciding whether
partitioning with legacy inheritance is useful for your application.

* * *

[Prev](ddl-schemas.html "5.9. Schemas")  | [Up](ddl.html "Chapter 5. Data Definition") |  [Next](ddl-partitioning.html "5.11. Table Partitioning")  
---|---|---  
5.9. Schemas  | [Home](index.html "PostgreSQL 16.9 Documentation") |  5.11. Table Partitioning  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ddl-inherit.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

