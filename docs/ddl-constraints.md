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

Supported Versions: [Current](/docs/current/ddl-constraints.html "PostgreSQL
17 - 5.4. Constraints") ([17](/docs/17/ddl-constraints.html "PostgreSQL 17 -
5.4. Constraints")) / [16](/docs/16/ddl-constraints.html "PostgreSQL 16 -
5.4. Constraints") / [15](/docs/15/ddl-constraints.html "PostgreSQL 15 -
5.4. Constraints") / [14](/docs/14/ddl-constraints.html "PostgreSQL 14 -
5.4. Constraints") / [13](/docs/13/ddl-constraints.html "PostgreSQL 13 -
5.4. Constraints")

Development Versions: [18](/docs/18/ddl-constraints.html "PostgreSQL 18 -
5.4. Constraints") / [devel](/docs/devel/ddl-constraints.html "PostgreSQL
devel - 5.4. Constraints")

Unsupported versions: [12](/docs/12/ddl-constraints.html "PostgreSQL 12 -
5.4. Constraints") / [11](/docs/11/ddl-constraints.html "PostgreSQL 11 -
5.4. Constraints") / [10](/docs/10/ddl-constraints.html "PostgreSQL 10 -
5.4. Constraints") / [9.6](/docs/9.6/ddl-constraints.html "PostgreSQL 9.6 -
5.4. Constraints") / [9.5](/docs/9.5/ddl-constraints.html "PostgreSQL 9.5 -
5.4. Constraints") / [9.4](/docs/9.4/ddl-constraints.html "PostgreSQL 9.4 -
5.4. Constraints") / [9.3](/docs/9.3/ddl-constraints.html "PostgreSQL 9.3 -
5.4. Constraints") / [9.2](/docs/9.2/ddl-constraints.html "PostgreSQL 9.2 -
5.4. Constraints") / [9.1](/docs/9.1/ddl-constraints.html "PostgreSQL 9.1 -
5.4. Constraints") / [9.0](/docs/9.0/ddl-constraints.html "PostgreSQL 9.0 -
5.4. Constraints") / [8.4](/docs/8.4/ddl-constraints.html "PostgreSQL 8.4 -
5.4. Constraints") / [8.3](/docs/8.3/ddl-constraints.html "PostgreSQL 8.3 -
5.4. Constraints") / [8.2](/docs/8.2/ddl-constraints.html "PostgreSQL 8.2 -
5.4. Constraints") / [8.1](/docs/8.1/ddl-constraints.html "PostgreSQL 8.1 -
5.4. Constraints") / [8.0](/docs/8.0/ddl-constraints.html "PostgreSQL 8.0 -
5.4. Constraints") / [7.4](/docs/7.4/ddl-constraints.html "PostgreSQL 7.4 -
5.4. Constraints") / [7.3](/docs/7.3/ddl-constraints.html "PostgreSQL 7.3 -
5.4. Constraints")

__

5.4. Constraints  
---  
[Prev](ddl-generated-columns.html "5.3. Generated Columns")  | [Up](ddl.html "Chapter 5. Data Definition") | Chapter 5. Data Definition | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ddl-system-columns.html "5.5. System Columns")  
  
* * *

## 5.4. Constraints #

[5.4.1. Check Constraints](ddl-constraints.html#DDL-CONSTRAINTS-CHECK-
CONSTRAINTS)

[5.4.2. Not-Null Constraints](ddl-constraints.html#DDL-CONSTRAINTS-NOT-NULL)

[5.4.3. Unique Constraints](ddl-constraints.html#DDL-CONSTRAINTS-UNIQUE-
CONSTRAINTS)

[5.4.4. Primary Keys](ddl-constraints.html#DDL-CONSTRAINTS-PRIMARY-KEYS)

[5.4.5. Foreign Keys](ddl-constraints.html#DDL-CONSTRAINTS-FK)

[5.4.6. Exclusion Constraints](ddl-constraints.html#DDL-CONSTRAINTS-EXCLUSION)

Data types are a way to limit the kind of data that can be stored in a table.
For many applications, however, the constraint they provide is too coarse. For
example, a column containing a product price should probably only accept
positive values. But there is no standard data type that accepts only positive
numbers. Another issue is that you might want to constrain column data with
respect to other columns or rows. For example, in a table containing product
information, there should be only one row for each product number.

To that end, SQL allows you to define constraints on columns and tables.
Constraints give you as much control over the data in your tables as you wish.
If a user attempts to store data in a column that would violate a constraint,
an error is raised. This applies even if the value came from the default value
definition.

### 5.4.1. Check Constraints #

A check constraint is the most generic constraint type. It allows you to
specify that the value in a certain column must satisfy a Boolean (truth-
value) expression. For instance, to require positive product prices, you could
use:

    
    
    CREATE TABLE products (
        product_no integer,
        name text,
        price numeric **CHECK (price > 0)**
    );
    

As you see, the constraint definition comes after the data type, just like
default value definitions. Default values and constraints can be listed in any
order. A check constraint consists of the key word `CHECK` followed by an
expression in parentheses. The check constraint expression should involve the
column thus constrained, otherwise the constraint would not make too much
sense.

You can also give the constraint a separate name. This clarifies error
messages and allows you to refer to the constraint when you need to change it.
The syntax is:

    
    
    CREATE TABLE products (
        product_no integer,
        name text,
        price numeric **CONSTRAINT positive_price** CHECK (price > 0)
    );
    

So, to specify a named constraint, use the key word `CONSTRAINT` followed by
an identifier followed by the constraint definition. (If you don't specify a
constraint name in this way, the system chooses a name for you.)

A check constraint can also refer to several columns. Say you store a regular
price and a discounted price, and you want to ensure that the discounted price
is lower than the regular price:

    
    
    CREATE TABLE products (
        product_no integer,
        name text,
        price numeric CHECK (price > 0),
        discounted_price numeric CHECK (discounted_price > 0),
        **CHECK (price > discounted_price)**
    );
    

The first two constraints should look familiar. The third one uses a new
syntax. It is not attached to a particular column, instead it appears as a
separate item in the comma-separated column list. Column definitions and these
constraint definitions can be listed in mixed order.

We say that the first two constraints are column constraints, whereas the
third one is a table constraint because it is written separately from any one
column definition. Column constraints can also be written as table
constraints, while the reverse is not necessarily possible, since a column
constraint is supposed to refer to only the column it is attached to.
(PostgreSQL doesn't enforce that rule, but you should follow it if you want
your table definitions to work with other database systems.) The above example
could also be written as:

    
    
    CREATE TABLE products (
        product_no integer,
        name text,
        price numeric,
        CHECK (price > 0),
        discounted_price numeric,
        CHECK (discounted_price > 0),
        CHECK (price > discounted_price)
    );
    

or even:

    
    
    CREATE TABLE products (
        product_no integer,
        name text,
        price numeric CHECK (price > 0),
        discounted_price numeric,
        CHECK (discounted_price > 0 AND price > discounted_price)
    );
    

It's a matter of taste.

Names can be assigned to table constraints in the same way as column
constraints:

    
    
    CREATE TABLE products (
        product_no integer,
        name text,
        price numeric,
        CHECK (price > 0),
        discounted_price numeric,
        CHECK (discounted_price > 0),
        **CONSTRAINT valid_discount** CHECK (price > discounted_price)
    );
    

It should be noted that a check constraint is satisfied if the check
expression evaluates to true or the null value. Since most expressions will
evaluate to the null value if any operand is null, they will not prevent null
values in the constrained columns. To ensure that a column does not contain
null values, the not-null constraint described in the next section can be
used.

### Note

PostgreSQL does not support `CHECK` constraints that reference table data
other than the new or updated row being checked. While a `CHECK` constraint
that violates this rule may appear to work in simple tests, it cannot
guarantee that the database will not reach a state in which the constraint
condition is false (due to subsequent changes of the other row(s) involved).
This would cause a database dump and restore to fail. The restore could fail
even when the complete database state is consistent with the constraint, due
to rows not being loaded in an order that will satisfy the constraint. If
possible, use `UNIQUE`, `EXCLUDE`, or `FOREIGN KEY` constraints to express
cross-row and cross-table restrictions.

If what you desire is a one-time check against other rows at row insertion,
rather than a continuously-maintained consistency guarantee, a custom
[trigger](triggers.html "Chapter 39. Triggers") can be used to implement that.
(This approach avoids the dump/restore problem because pg_dump does not
reinstall triggers until after restoring data, so that the check will not be
enforced during a dump/restore.)

### Note

PostgreSQL assumes that `CHECK` constraints' conditions are immutable, that
is, they will always give the same result for the same input row. This
assumption is what justifies examining `CHECK` constraints only when rows are
inserted or updated, and not at other times. (The warning above about not
referencing other table data is really a special case of this restriction.)

An example of a common way to break this assumption is to reference a user-
defined function in a `CHECK` expression, and then change the behavior of that
function. PostgreSQL does not disallow that, but it will not notice if there
are rows in the table that now violate the `CHECK` constraint. That would
cause a subsequent database dump and restore to fail. The recommended way to
handle such a change is to drop the constraint (using `ALTER TABLE`), adjust
the function definition, and re-add the constraint, thereby rechecking it
against all table rows.

### 5.4.2. Not-Null Constraints #

A not-null constraint simply specifies that a column must not assume the null
value. A syntax example:

    
    
    CREATE TABLE products (
        product_no integer **NOT NULL** ,
        name text **NOT NULL** ,
        price numeric
    );
    

A not-null constraint is always written as a column constraint. A not-null
constraint is functionally equivalent to creating a check constraint `CHECK
(_`column_name`_ IS NOT NULL)`, but in PostgreSQL creating an explicit not-
null constraint is more efficient. The drawback is that you cannot give
explicit names to not-null constraints created this way.

Of course, a column can have more than one constraint. Just write the
constraints one after another:

    
    
    CREATE TABLE products (
        product_no integer NOT NULL,
        name text NOT NULL,
        price numeric NOT NULL CHECK (price > 0)
    );
    

The order doesn't matter. It does not necessarily determine in which order the
constraints are checked.

The `NOT NULL` constraint has an inverse: the `NULL` constraint. This does not
mean that the column must be null, which would surely be useless. Instead,
this simply selects the default behavior that the column might be null. The
`NULL` constraint is not present in the SQL standard and should not be used in
portable applications. (It was only added to PostgreSQL to be compatible with
some other database systems.) Some users, however, like it because it makes it
easy to toggle the constraint in a script file. For example, you could start
with:

    
    
    CREATE TABLE products (
        product_no integer NULL,
        name text NULL,
        price numeric NULL
    );
    

and then insert the `NOT` key word where desired.

### Tip

In most database designs the majority of columns should be marked not null.

### 5.4.3. Unique Constraints #

Unique constraints ensure that the data contained in a column, or a group of
columns, is unique among all the rows in the table. The syntax is:

    
    
    CREATE TABLE products (
        product_no integer **UNIQUE** ,
        name text,
        price numeric
    );
    

when written as a column constraint, and:

    
    
    CREATE TABLE products (
        product_no integer,
        name text,
        price numeric,
        **UNIQUE (product_no)**
    );
    

when written as a table constraint.

To define a unique constraint for a group of columns, write it as a table
constraint with the column names separated by commas:

    
    
    CREATE TABLE example (
        a integer,
        b integer,
        c integer,
        **UNIQUE (a, c)**
    );
    

This specifies that the combination of values in the indicated columns is
unique across the whole table, though any one of the columns need not be (and
ordinarily isn't) unique.

You can assign your own name for a unique constraint, in the usual way:

    
    
    CREATE TABLE products (
        product_no integer **CONSTRAINT must_be_different** UNIQUE,
        name text,
        price numeric
    );
    

Adding a unique constraint will automatically create a unique B-tree index on
the column or group of columns listed in the constraint. A uniqueness
restriction covering only some rows cannot be written as a unique constraint,
but it is possible to enforce such a restriction by creating a unique [partial
index](indexes-partial.html "11.8. Partial Indexes").

In general, a unique constraint is violated if there is more than one row in
the table where the values of all of the columns included in the constraint
are equal. By default, two null values are not considered equal in this
comparison. That means even in the presence of a unique constraint it is
possible to store duplicate rows that contain a null value in at least one of
the constrained columns. This behavior can be changed by adding the clause
`NULLS NOT DISTINCT`, like

    
    
    CREATE TABLE products (
        product_no integer UNIQUE **NULLS NOT DISTINCT** ,
        name text,
        price numeric
    );
    

or

    
    
    CREATE TABLE products (
        product_no integer,
        name text,
        price numeric,
        UNIQUE **NULLS NOT DISTINCT** (product_no)
    );
    

The default behavior can be specified explicitly using `NULLS DISTINCT`. The
default null treatment in unique constraints is implementation-defined
according to the SQL standard, and other implementations have a different
behavior. So be careful when developing applications that are intended to be
portable.

### 5.4.4. Primary Keys #

A primary key constraint indicates that a column, or group of columns, can be
used as a unique identifier for rows in the table. This requires that the
values be both unique and not null. So, the following two table definitions
accept the same data:

    
    
    CREATE TABLE products (
        product_no integer UNIQUE NOT NULL,
        name text,
        price numeric
    );
    
    
    
    CREATE TABLE products (
        product_no integer **PRIMARY KEY** ,
        name text,
        price numeric
    );
    

Primary keys can span more than one column; the syntax is similar to unique
constraints:

    
    
    CREATE TABLE example (
        a integer,
        b integer,
        c integer,
        **PRIMARY KEY (a, c)**
    );
    

Adding a primary key will automatically create a unique B-tree index on the
column or group of columns listed in the primary key, and will force the
column(s) to be marked `NOT NULL`.

A table can have at most one primary key. (There can be any number of unique
and not-null constraints, which are functionally almost the same thing, but
only one can be identified as the primary key.) Relational database theory
dictates that every table must have a primary key. This rule is not enforced
by PostgreSQL, but it is usually best to follow it.

Primary keys are useful both for documentation purposes and for client
applications. For example, a GUI application that allows modifying row values
probably needs to know the primary key of a table to be able to identify rows
uniquely. There are also various ways in which the database system makes use
of a primary key if one has been declared; for example, the primary key
defines the default target column(s) for foreign keys referencing its table.

### 5.4.5. Foreign Keys #

A foreign key constraint specifies that the values in a column (or a group of
columns) must match the values appearing in some row of another table. We say
this maintains the _referential integrity_ between two related tables.

Say you have the product table that we have used several times already:

    
    
    CREATE TABLE products (
        product_no integer PRIMARY KEY,
        name text,
        price numeric
    );
    

Let's also assume you have a table storing orders of those products. We want
to ensure that the orders table only contains orders of products that actually
exist. So we define a foreign key constraint in the orders table that
references the products table:

    
    
    CREATE TABLE orders (
        order_id integer PRIMARY KEY,
        product_no integer **REFERENCES products (product_no)** ,
        quantity integer
    );
    

Now it is impossible to create orders with non-NULL `product_no` entries that
do not appear in the products table.

We say that in this situation the orders table is the _referencing_ table and
the products table is the _referenced_ table. Similarly, there are referencing
and referenced columns.

You can also shorten the above command to:

    
    
    CREATE TABLE orders (
        order_id integer PRIMARY KEY,
        product_no integer **REFERENCES products** ,
        quantity integer
    );
    

because in absence of a column list the primary key of the referenced table is
used as the referenced column(s).

You can assign your own name for a foreign key constraint, in the usual way.

A foreign key can also constrain and reference a group of columns. As usual,
it then needs to be written in table constraint form. Here is a contrived
syntax example:

    
    
    CREATE TABLE t1 (
      a integer PRIMARY KEY,
      b integer,
      c integer,
      **FOREIGN KEY (b, c) REFERENCES other_table (c1, c2)**
    );
    

Of course, the number and type of the constrained columns need to match the
number and type of the referenced columns.

Sometimes it is useful for the “other table” of a foreign key constraint to be
the same table; this is called a _self-referential_ foreign key. For example,
if you want rows of a table to represent nodes of a tree structure, you could
write

    
    
    CREATE TABLE tree (
        node_id integer PRIMARY KEY,
        parent_id integer REFERENCES tree,
        name text,
        ...
    );
    

A top-level node would have NULL `parent_id`, while non-NULL `parent_id`
entries would be constrained to reference valid rows of the table.

A table can have more than one foreign key constraint. This is used to
implement many-to-many relationships between tables. Say you have tables about
products and orders, but now you want to allow one order to contain possibly
many products (which the structure above did not allow). You could use this
table structure:

    
    
    CREATE TABLE products (
        product_no integer PRIMARY KEY,
        name text,
        price numeric
    );
    
    CREATE TABLE orders (
        order_id integer PRIMARY KEY,
        shipping_address text,
        ...
    );
    
    CREATE TABLE order_items (
        product_no integer REFERENCES products,
        order_id integer REFERENCES orders,
        quantity integer,
        PRIMARY KEY (product_no, order_id)
    );
    

Notice that the primary key overlaps with the foreign keys in the last table.

We know that the foreign keys disallow creation of orders that do not relate
to any products. But what if a product is removed after an order is created
that references it? SQL allows you to handle that as well. Intuitively, we
have a few options:

  * Disallow deleting a referenced product

  * Delete the orders as well

  * Something else?

To illustrate this, let's implement the following policy on the many-to-many
relationship example above: when someone wants to remove a product that is
still referenced by an order (via `order_items`), we disallow it. If someone
removes an order, the order items are removed as well:

    
    
    CREATE TABLE products (
        product_no integer PRIMARY KEY,
        name text,
        price numeric
    );
    
    CREATE TABLE orders (
        order_id integer PRIMARY KEY,
        shipping_address text,
        ...
    );
    
    CREATE TABLE order_items (
        product_no integer REFERENCES products **ON DELETE RESTRICT** ,
        order_id integer REFERENCES orders **ON DELETE CASCADE** ,
        quantity integer,
        PRIMARY KEY (product_no, order_id)
    );
    

Restricting and cascading deletes are the two most common options. `RESTRICT`
prevents deletion of a referenced row. `NO ACTION` means that if any
referencing rows still exist when the constraint is checked, an error is
raised; this is the default behavior if you do not specify anything. (The
essential difference between these two choices is that `NO ACTION` allows the
check to be deferred until later in the transaction, whereas `RESTRICT` does
not.) `CASCADE` specifies that when a referenced row is deleted, row(s)
referencing it should be automatically deleted as well. There are two other
options: `SET NULL` and `SET DEFAULT`. These cause the referencing column(s)
in the referencing row(s) to be set to nulls or their default values,
respectively, when the referenced row is deleted. Note that these do not
excuse you from observing any constraints. For example, if an action specifies
`SET DEFAULT` but the default value would not satisfy the foreign key
constraint, the operation will fail.

The appropriate choice of `ON DELETE` action depends on what kinds of objects
the related tables represent. When the referencing table represents something
that is a component of what is represented by the referenced table and cannot
exist independently, then `CASCADE` could be appropriate. If the two tables
represent independent objects, then `RESTRICT` or `NO ACTION` is more
appropriate; an application that actually wants to delete both objects would
then have to be explicit about this and run two delete commands. In the above
example, order items are part of an order, and it is convenient if they are
deleted automatically if an order is deleted. But products and orders are
different things, and so making a deletion of a product automatically cause
the deletion of some order items could be considered problematic. The actions
`SET NULL` or `SET DEFAULT` can be appropriate if a foreign-key relationship
represents optional information. For example, if the products table contained
a reference to a product manager, and the product manager entry gets deleted,
then setting the product's product manager to null or a default might be
useful.

The actions `SET NULL` and `SET DEFAULT` can take a column list to specify
which columns to set. Normally, all columns of the foreign-key constraint are
set; setting only a subset is useful in some special cases. Consider the
following example:

    
    
    CREATE TABLE tenants (
        tenant_id integer PRIMARY KEY
    );
    
    CREATE TABLE users (
        tenant_id integer REFERENCES tenants ON DELETE CASCADE,
        user_id integer NOT NULL,
        PRIMARY KEY (tenant_id, user_id)
    );
    
    CREATE TABLE posts (
        tenant_id integer REFERENCES tenants ON DELETE CASCADE,
        post_id integer NOT NULL,
        author_id integer,
        PRIMARY KEY (tenant_id, post_id),
        FOREIGN KEY (tenant_id, author_id) REFERENCES users ON DELETE SET NULL **(author_id)**
    );
    

Without the specification of the column, the foreign key would also set the
column `tenant_id` to null, but that column is still required as part of the
primary key.

Analogous to `ON DELETE` there is also `ON UPDATE` which is invoked when a
referenced column is changed (updated). The possible actions are the same,
except that column lists cannot be specified for `SET NULL` and `SET DEFAULT`.
In this case, `CASCADE` means that the updated values of the referenced
column(s) should be copied into the referencing row(s).

Normally, a referencing row need not satisfy the foreign key constraint if any
of its referencing columns are null. If `MATCH FULL` is added to the foreign
key declaration, a referencing row escapes satisfying the constraint only if
all its referencing columns are null (so a mix of null and non-null values is
guaranteed to fail a `MATCH FULL` constraint). If you don't want referencing
rows to be able to avoid satisfying the foreign key constraint, declare the
referencing column(s) as `NOT NULL`.

A foreign key must reference columns that either are a primary key or form a
unique constraint, or are columns from a non-partial unique index. This means
that the referenced columns always have an index to allow efficient lookups on
whether a referencing row has a match. Since a `DELETE` of a row from the
referenced table or an `UPDATE` of a referenced column will require a scan of
the referencing table for rows matching the old value, it is often a good idea
to index the referencing columns too. Because this is not always needed, and
there are many choices available on how to index, the declaration of a foreign
key constraint does not automatically create an index on the referencing
columns.

More information about updating and deleting data is in [Chapter 6](dml.html
"Chapter 6. Data Manipulation"). Also see the description of foreign key
constraint syntax in the reference documentation for [CREATE TABLE](sql-
createtable.html "CREATE TABLE").

### 5.4.6. Exclusion Constraints #

Exclusion constraints ensure that if any two rows are compared on the
specified columns or expressions using the specified operators, at least one
of these operator comparisons will return false or null. The syntax is:

    
    
    CREATE TABLE circles (
        c circle,
        EXCLUDE USING gist (c WITH &&)
    );
    

See also [`CREATE TABLE ... CONSTRAINT ... EXCLUDE`](sql-createtable.html#SQL-
CREATETABLE-EXCLUDE) for details.

Adding an exclusion constraint will automatically create an index of the type
specified in the constraint declaration.

* * *

[Prev](ddl-generated-columns.html "5.3. Generated Columns")  | [Up](ddl.html "Chapter 5. Data Definition") |  [Next](ddl-system-columns.html "5.5. System Columns")  
---|---|---  
5.3. Generated Columns  | [Home](index.html "PostgreSQL 16.9 Documentation") |  5.5. System Columns  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ddl-constraints.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

