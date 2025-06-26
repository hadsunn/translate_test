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

Supported Versions: [Current](/docs/current/ddl-alter.html "PostgreSQL 17 -
5.6. Modifying Tables") ([17](/docs/17/ddl-alter.html "PostgreSQL 17 -
5.6. Modifying Tables")) / [16](/docs/16/ddl-alter.html "PostgreSQL 16 -
5.6. Modifying Tables") / [15](/docs/15/ddl-alter.html "PostgreSQL 15 -
5.6. Modifying Tables") / [14](/docs/14/ddl-alter.html "PostgreSQL 14 -
5.6. Modifying Tables") / [13](/docs/13/ddl-alter.html "PostgreSQL 13 -
5.6. Modifying Tables")

Development Versions: [18](/docs/18/ddl-alter.html "PostgreSQL 18 -
5.6. Modifying Tables") / [devel](/docs/devel/ddl-alter.html "PostgreSQL devel
- 5.6. Modifying Tables")

Unsupported versions: [12](/docs/12/ddl-alter.html "PostgreSQL 12 -
5.6. Modifying Tables") / [11](/docs/11/ddl-alter.html "PostgreSQL 11 -
5.6. Modifying Tables") / [10](/docs/10/ddl-alter.html "PostgreSQL 10 -
5.6. Modifying Tables") / [9.6](/docs/9.6/ddl-alter.html "PostgreSQL 9.6 -
5.6. Modifying Tables") / [9.5](/docs/9.5/ddl-alter.html "PostgreSQL 9.5 -
5.6. Modifying Tables") / [9.4](/docs/9.4/ddl-alter.html "PostgreSQL 9.4 -
5.6. Modifying Tables") / [9.3](/docs/9.3/ddl-alter.html "PostgreSQL 9.3 -
5.6. Modifying Tables") / [9.2](/docs/9.2/ddl-alter.html "PostgreSQL 9.2 -
5.6. Modifying Tables") / [9.1](/docs/9.1/ddl-alter.html "PostgreSQL 9.1 -
5.6. Modifying Tables") / [9.0](/docs/9.0/ddl-alter.html "PostgreSQL 9.0 -
5.6. Modifying Tables") / [8.4](/docs/8.4/ddl-alter.html "PostgreSQL 8.4 -
5.6. Modifying Tables") / [8.3](/docs/8.3/ddl-alter.html "PostgreSQL 8.3 -
5.6. Modifying Tables") / [8.2](/docs/8.2/ddl-alter.html "PostgreSQL 8.2 -
5.6. Modifying Tables") / [8.1](/docs/8.1/ddl-alter.html "PostgreSQL 8.1 -
5.6. Modifying Tables") / [8.0](/docs/8.0/ddl-alter.html "PostgreSQL 8.0 -
5.6. Modifying Tables") / [7.4](/docs/7.4/ddl-alter.html "PostgreSQL 7.4 -
5.6. Modifying Tables") / [7.3](/docs/7.3/ddl-alter.html "PostgreSQL 7.3 -
5.6. Modifying Tables")

__

5.6. Modifying Tables  
---  
[Prev](ddl-system-columns.html "5.5. System Columns")  | [Up](ddl.html "Chapter 5. Data Definition") | Chapter 5. Data Definition | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ddl-priv.html "5.7. Privileges")  
  
* * *

## 5.6. Modifying Tables #

[5.6.1. Adding a Column](ddl-alter.html#DDL-ALTER-ADDING-A-COLUMN)

[5.6.2. Removing a Column](ddl-alter.html#DDL-ALTER-REMOVING-A-COLUMN)

[5.6.3. Adding a Constraint](ddl-alter.html#DDL-ALTER-ADDING-A-CONSTRAINT)

[5.6.4. Removing a Constraint](ddl-alter.html#DDL-ALTER-REMOVING-A-CONSTRAINT)

[5.6.5. Changing a Column's Default Value](ddl-alter.html#DDL-ALTER-COLUMN-
DEFAULT)

[5.6.6. Changing a Column's Data Type](ddl-alter.html#DDL-ALTER-COLUMN-TYPE)

[5.6.7. Renaming a Column](ddl-alter.html#DDL-ALTER-RENAMING-COLUMN)

[5.6.8. Renaming a Table](ddl-alter.html#DDL-ALTER-RENAMING-TABLE)

When you create a table and you realize that you made a mistake, or the
requirements of the application change, you can drop the table and create it
again. But this is not a convenient option if the table is already filled with
data, or if the table is referenced by other database objects (for instance a
foreign key constraint). Therefore PostgreSQL provides a family of commands to
make modifications to existing tables. Note that this is conceptually distinct
from altering the data contained in the table: here we are interested in
altering the definition, or structure, of the table.

You can:

  * Add columns

  * Remove columns

  * Add constraints

  * Remove constraints

  * Change default values

  * Change column data types

  * Rename columns

  * Rename tables

All these actions are performed using the [ALTER TABLE](sql-altertable.html
"ALTER TABLE") command, whose reference page contains details beyond those
given here.

### 5.6.1. Adding a Column #

To add a column, use a command like:

    
    
    ALTER TABLE products ADD COLUMN description text;
    

The new column is initially filled with whatever default value is given (null
if you don't specify a `DEFAULT` clause).

### Tip

From PostgreSQL 11, adding a column with a constant default value no longer
means that each row of the table needs to be updated when the `ALTER TABLE`
statement is executed. Instead, the default value will be returned the next
time the row is accessed, and applied when the table is rewritten, making the
`ALTER TABLE` very fast even on large tables.

However, if the default value is volatile (e.g., `clock_timestamp()`) each row
will need to be updated with the value calculated at the time `ALTER TABLE` is
executed. To avoid a potentially lengthy update operation, particularly if you
intend to fill the column with mostly nondefault values anyway, it may be
preferable to add the column with no default, insert the correct values using
`UPDATE`, and then add any desired default as described below.

You can also define constraints on the column at the same time, using the
usual syntax:

    
    
    ALTER TABLE products ADD COLUMN description text CHECK (description <> '');
    

In fact all the options that can be applied to a column description in `CREATE
TABLE` can be used here. Keep in mind however that the default value must
satisfy the given constraints, or the `ADD` will fail. Alternatively, you can
add constraints later (see below) after you've filled in the new column
correctly.

### 5.6.2. Removing a Column #

To remove a column, use a command like:

    
    
    ALTER TABLE products DROP COLUMN description;
    

Whatever data was in the column disappears. Table constraints involving the
column are dropped, too. However, if the column is referenced by a foreign key
constraint of another table, PostgreSQL will not silently drop that
constraint. You can authorize dropping everything that depends on the column
by adding `CASCADE`:

    
    
    ALTER TABLE products DROP COLUMN description CASCADE;
    

See [Section 5.14](ddl-depend.html "5.14. Dependency Tracking") for a
description of the general mechanism behind this.

### 5.6.3. Adding a Constraint #

To add a constraint, the table constraint syntax is used. For example:

    
    
    ALTER TABLE products ADD CHECK (name <> '');
    ALTER TABLE products ADD CONSTRAINT some_name UNIQUE (product_no);
    ALTER TABLE products ADD FOREIGN KEY (product_group_id) REFERENCES product_groups;
    

To add a not-null constraint, which cannot be written as a table constraint,
use this syntax:

    
    
    ALTER TABLE products ALTER COLUMN product_no SET NOT NULL;
    

The constraint will be checked immediately, so the table data must satisfy the
constraint before it can be added.

### 5.6.4. Removing a Constraint #

To remove a constraint you need to know its name. If you gave it a name then
that's easy. Otherwise the system assigned a generated name, which you need to
find out. The psql command `\d _`tablename`_` can be helpful here; other
interfaces might also provide a way to inspect table details. Then the command
is:

    
    
    ALTER TABLE products DROP CONSTRAINT some_name;
    

As with dropping a column, you need to add `CASCADE` if you want to drop a
constraint that something else depends on. An example is that a foreign key
constraint depends on a unique or primary key constraint on the referenced
column(s).

This works the same for all constraint types except not-null constraints. To
drop a not null constraint use:

    
    
    ALTER TABLE products ALTER COLUMN product_no DROP NOT NULL;
    

(Recall that not-null constraints do not have names.)

### 5.6.5. Changing a Column's Default Value #

To set a new default for a column, use a command like:

    
    
    ALTER TABLE products ALTER COLUMN price SET DEFAULT 7.77;
    

Note that this doesn't affect any existing rows in the table, it just changes
the default for future `INSERT` commands.

To remove any default value, use:

    
    
    ALTER TABLE products ALTER COLUMN price DROP DEFAULT;
    

This is effectively the same as setting the default to null. As a consequence,
it is not an error to drop a default where one hadn't been defined, because
the default is implicitly the null value.

### 5.6.6. Changing a Column's Data Type #

To convert a column to a different data type, use a command like:

    
    
    ALTER TABLE products ALTER COLUMN price TYPE numeric(10,2);
    

This will succeed only if each existing entry in the column can be converted
to the new type by an implicit cast. If a more complex conversion is needed,
you can add a `USING` clause that specifies how to compute the new values from
the old.

PostgreSQL will attempt to convert the column's default value (if any) to the
new type, as well as any constraints that involve the column. But these
conversions might fail, or might produce surprising results. It's often best
to drop any constraints on the column before altering its type, and then add
back suitably modified constraints afterwards.

### 5.6.7. Renaming a Column #

To rename a column:

    
    
    ALTER TABLE products RENAME COLUMN product_no TO product_number;
    

### 5.6.8. Renaming a Table #

To rename a table:

    
    
    ALTER TABLE products RENAME TO items;
    

* * *

[Prev](ddl-system-columns.html "5.5. System Columns")  | [Up](ddl.html "Chapter 5. Data Definition") |  [Next](ddl-priv.html "5.7. Privileges")  
---|---|---  
5.5. System Columns  | [Home](index.html "PostgreSQL 16.9 Documentation") |  5.7. Privileges  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ddl-alter.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

