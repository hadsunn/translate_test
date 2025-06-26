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

Supported Versions: [Current](/docs/current/queries-select-lists.html
"PostgreSQL 17 - 7.3. Select Lists") ([17](/docs/17/queries-select-lists.html
"PostgreSQL 17 - 7.3. Select Lists")) / [16](/docs/16/queries-select-
lists.html "PostgreSQL 16 - 7.3. Select Lists") / [15](/docs/15/queries-
select-lists.html "PostgreSQL 15 - 7.3. Select Lists") /
[14](/docs/14/queries-select-lists.html "PostgreSQL 14 - 7.3. Select Lists") /
[13](/docs/13/queries-select-lists.html "PostgreSQL 13 - 7.3. Select Lists")

Development Versions: [18](/docs/18/queries-select-lists.html "PostgreSQL 18 -
7.3. Select Lists") / [devel](/docs/devel/queries-select-lists.html
"PostgreSQL devel - 7.3. Select Lists")

Unsupported versions: [12](/docs/12/queries-select-lists.html "PostgreSQL 12 -
7.3. Select Lists") / [11](/docs/11/queries-select-lists.html "PostgreSQL 11 -
7.3. Select Lists") / [10](/docs/10/queries-select-lists.html "PostgreSQL 10 -
7.3. Select Lists") / [9.6](/docs/9.6/queries-select-lists.html "PostgreSQL
9.6 - 7.3. Select Lists") / [9.5](/docs/9.5/queries-select-lists.html
"PostgreSQL 9.5 - 7.3. Select Lists") / [9.4](/docs/9.4/queries-select-
lists.html "PostgreSQL 9.4 - 7.3. Select Lists") / [9.3](/docs/9.3/queries-
select-lists.html "PostgreSQL 9.3 - 7.3. Select Lists") /
[9.2](/docs/9.2/queries-select-lists.html "PostgreSQL 9.2 - 7.3. Select
Lists") / [9.1](/docs/9.1/queries-select-lists.html "PostgreSQL 9.1 -
7.3. Select Lists") / [9.0](/docs/9.0/queries-select-lists.html "PostgreSQL
9.0 - 7.3. Select Lists") / [8.4](/docs/8.4/queries-select-lists.html
"PostgreSQL 8.4 - 7.3. Select Lists") / [8.3](/docs/8.3/queries-select-
lists.html "PostgreSQL 8.3 - 7.3. Select Lists") / [8.2](/docs/8.2/queries-
select-lists.html "PostgreSQL 8.2 - 7.3. Select Lists") /
[8.1](/docs/8.1/queries-select-lists.html "PostgreSQL 8.1 - 7.3. Select
Lists") / [8.0](/docs/8.0/queries-select-lists.html "PostgreSQL 8.0 -
7.3. Select Lists") / [7.4](/docs/7.4/queries-select-lists.html "PostgreSQL
7.4 - 7.3. Select Lists") / [7.3](/docs/7.3/queries-select-lists.html
"PostgreSQL 7.3 - 7.3. Select Lists") / [7.2](/docs/7.2/queries-select-
lists.html "PostgreSQL 7.2 - 7.3. Select Lists") / [7.1](/docs/7.1/queries-
select-lists.html "PostgreSQL 7.1 - 7.3. Select Lists")

__

7.3. Select Lists  
---  
[Prev](queries-table-expressions.html "7.2. Table Expressions")  | [Up](queries.html "Chapter 7. Queries") | Chapter 7. Queries | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](queries-union.html "7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)")  
  
* * *

## 7.3. Select Lists #

[7.3.1. Select-List Items](queries-select-lists.html#QUERIES-SELECT-LIST-
ITEMS)

[7.3.2. Column Labels](queries-select-lists.html#QUERIES-COLUMN-LABELS)

[7.3.3. `DISTINCT`](queries-select-lists.html#QUERIES-DISTINCT)

As shown in the previous section, the table expression in the `SELECT` command
constructs an intermediate virtual table by possibly combining tables, views,
eliminating rows, grouping, etc. This table is finally passed on to processing
by the _select list_. The select list determines which _columns_ of the
intermediate table are actually output.

### 7.3.1. Select-List Items #

The simplest kind of select list is `*` which emits all columns that the table
expression produces. Otherwise, a select list is a comma-separated list of
value expressions (as defined in [Section 4.2](sql-expressions.html
"4.2. Value Expressions")). For instance, it could be a list of column names:

    
    
    SELECT a, b, c FROM ...
    

The columns names `a`, `b`, and `c` are either the actual names of the columns
of tables referenced in the `FROM` clause, or the aliases given to them as
explained in [Section 7.2.1.2](queries-table-expressions.html#QUERIES-TABLE-
ALIASES "7.2.1.2. Table and Column Aliases"). The name space available in the
select list is the same as in the `WHERE` clause, unless grouping is used, in
which case it is the same as in the `HAVING` clause.

If more than one table has a column of the same name, the table name must also
be given, as in:

    
    
    SELECT tbl1.a, tbl2.a, tbl1.b FROM ...
    

When working with multiple tables, it can also be useful to ask for all the
columns of a particular table:

    
    
    SELECT tbl1.*, tbl2.a FROM ...
    

See [Section 8.16.5](rowtypes.html#ROWTYPES-USAGE "8.16.5. Using Composite
Types in Queries") for more about the _`table_name`_`.*` notation.

If an arbitrary value expression is used in the select list, it conceptually
adds a new virtual column to the returned table. The value expression is
evaluated once for each result row, with the row's values substituted for any
column references. But the expressions in the select list do not have to
reference any columns in the table expression of the `FROM` clause; they can
be constant arithmetic expressions, for instance.

### 7.3.2. Column Labels #

The entries in the select list can be assigned names for subsequent
processing, such as for use in an `ORDER BY` clause or for display by the
client application. For example:

    
    
    SELECT a AS value, b + c AS sum FROM ...
    

If no output column name is specified using `AS`, the system assigns a default
column name. For simple column references, this is the name of the referenced
column. For function calls, this is the name of the function. For complex
expressions, the system will generate a generic name.

The `AS` key word is usually optional, but in some cases where the desired
column name matches a PostgreSQL key word, you must write `AS` or double-quote
the column name in order to avoid ambiguity. ([Appendix C](sql-keywords-
appendix.html "Appendix C. SQL Key Words") shows which key words require `AS`
to be used as a column label.) For example, `FROM` is one such key word, so
this does not work:

    
    
    SELECT a from, b + c AS sum FROM ...
    

but either of these do:

    
    
    SELECT a AS from, b + c AS sum FROM ...
    SELECT a "from", b + c AS sum FROM ...
    

For greatest safety against possible future key word additions, it is
recommended that you always either write `AS` or double-quote the output
column name.

### Note

The naming of output columns here is different from that done in the `FROM`
clause (see [Section 7.2.1.2](queries-table-expressions.html#QUERIES-TABLE-
ALIASES "7.2.1.2. Table and Column Aliases")). It is possible to rename the
same column twice, but the name assigned in the select list is the one that
will be passed on.

### 7.3.3. `DISTINCT` #

After the select list has been processed, the result table can optionally be
subject to the elimination of duplicate rows. The `DISTINCT` key word is
written directly after `SELECT` to specify this:

    
    
    SELECT DISTINCT _select_list_ ...
    

(Instead of `DISTINCT` the key word `ALL` can be used to specify the default
behavior of retaining all rows.)

Obviously, two rows are considered distinct if they differ in at least one
column value. Null values are considered equal in this comparison.

Alternatively, an arbitrary expression can determine what rows are to be
considered distinct:

    
    
    SELECT DISTINCT ON (_expression_ [, _expression_ ...]) _select_list_ ...
    

Here _`expression`_ is an arbitrary value expression that is evaluated for all
rows. A set of rows for which all the expressions are equal are considered
duplicates, and only the first row of the set is kept in the output. Note that
the “first row” of a set is unpredictable unless the query is sorted on enough
columns to guarantee a unique ordering of the rows arriving at the `DISTINCT`
filter. (`DISTINCT ON` processing occurs after `ORDER BY` sorting.)

The `DISTINCT ON` clause is not part of the SQL standard and is sometimes
considered bad style because of the potentially indeterminate nature of its
results. With judicious use of `GROUP BY` and subqueries in `FROM`, this
construct can be avoided, but it is often the most convenient alternative.

* * *

[Prev](queries-table-expressions.html "7.2. Table Expressions")  | [Up](queries.html "Chapter 7. Queries") |  [Next](queries-union.html "7.4. Combining Queries \(UNION, INTERSECT, EXCEPT\)")  
---|---|---  
7.2. Table Expressions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  7.4. Combining Queries (`UNION`, `INTERSECT`, `EXCEPT`)  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/queries-select-lists.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

