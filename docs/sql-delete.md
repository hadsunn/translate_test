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

Supported Versions: [Current](/docs/current/sql-delete.html "PostgreSQL 17 -
DELETE") ([17](/docs/17/sql-delete.html "PostgreSQL 17 - DELETE")) /
[16](/docs/16/sql-delete.html "PostgreSQL 16 - DELETE") / [15](/docs/15/sql-
delete.html "PostgreSQL 15 - DELETE") / [14](/docs/14/sql-delete.html
"PostgreSQL 14 - DELETE") / [13](/docs/13/sql-delete.html "PostgreSQL 13 -
DELETE")

Development Versions: [18](/docs/18/sql-delete.html "PostgreSQL 18 - DELETE")
/ [devel](/docs/devel/sql-delete.html "PostgreSQL devel - DELETE")

Unsupported versions: [12](/docs/12/sql-delete.html "PostgreSQL 12 - DELETE")
/ [11](/docs/11/sql-delete.html "PostgreSQL 11 - DELETE") / [10](/docs/10/sql-
delete.html "PostgreSQL 10 - DELETE") / [9.6](/docs/9.6/sql-delete.html
"PostgreSQL 9.6 - DELETE") / [9.5](/docs/9.5/sql-delete.html "PostgreSQL 9.5 -
DELETE") / [9.4](/docs/9.4/sql-delete.html "PostgreSQL 9.4 - DELETE") /
[9.3](/docs/9.3/sql-delete.html "PostgreSQL 9.3 - DELETE") /
[9.2](/docs/9.2/sql-delete.html "PostgreSQL 9.2 - DELETE") /
[9.1](/docs/9.1/sql-delete.html "PostgreSQL 9.1 - DELETE") /
[9.0](/docs/9.0/sql-delete.html "PostgreSQL 9.0 - DELETE") /
[8.4](/docs/8.4/sql-delete.html "PostgreSQL 8.4 - DELETE") /
[8.3](/docs/8.3/sql-delete.html "PostgreSQL 8.3 - DELETE") /
[8.2](/docs/8.2/sql-delete.html "PostgreSQL 8.2 - DELETE") /
[8.1](/docs/8.1/sql-delete.html "PostgreSQL 8.1 - DELETE") /
[8.0](/docs/8.0/sql-delete.html "PostgreSQL 8.0 - DELETE") /
[7.4](/docs/7.4/sql-delete.html "PostgreSQL 7.4 - DELETE") /
[7.3](/docs/7.3/sql-delete.html "PostgreSQL 7.3 - DELETE") /
[7.2](/docs/7.2/sql-delete.html "PostgreSQL 7.2 - DELETE") /
[7.1](/docs/7.1/sql-delete.html "PostgreSQL 7.1 - DELETE")

__

DELETE  
---  
[Prev](sql-declare.html "DECLARE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-discard.html "DISCARD")  
  
* * *

## DELETE

DELETE — delete rows of a table

## Synopsis

    
    
    [ WITH [ RECURSIVE ] _with_query_ [, ...] ]
    DELETE FROM [ ONLY ] _table_name_ [ * ] [ [ AS ] _alias_ ]
        [ USING _from_item_ [, ...] ]
        [ WHERE _condition_ | WHERE CURRENT OF _cursor_name_ ]
        [ RETURNING { * | _output_expression_ [ [ AS ] _output_name_ ] } [, ...] ]
    

## Description

`DELETE` deletes rows that satisfy the `WHERE` clause from the specified
table. If the `WHERE` clause is absent, the effect is to delete all rows in
the table. The result is a valid, but empty table.

### Tip

[`TRUNCATE`](sql-truncate.html "TRUNCATE") provides a faster mechanism to
remove all rows from a table.

There are two ways to delete rows in a table using information contained in
other tables in the database: using sub-selects, or specifying additional
tables in the `USING` clause. Which technique is more appropriate depends on
the specific circumstances.

The optional `RETURNING` clause causes `DELETE` to compute and return value(s)
based on each row actually deleted. Any expression using the table's columns,
and/or columns of other tables mentioned in `USING`, can be computed. The
syntax of the `RETURNING` list is identical to that of the output list of
`SELECT`.

You must have the `DELETE` privilege on the table to delete from it, as well
as the `SELECT` privilege for any table in the `USING` clause or whose values
are read in the _`condition`_.

## Parameters

_`with_query`_

    

The `WITH` clause allows you to specify one or more subqueries that can be
referenced by name in the `DELETE` query. See [Section 7.8](queries-with.html
"7.8. WITH Queries \(Common Table Expressions\)") and [SELECT](sql-select.html
"SELECT") for details.

_`table_name`_

    

The name (optionally schema-qualified) of the table to delete rows from. If
`ONLY` is specified before the table name, matching rows are deleted from the
named table only. If `ONLY` is not specified, matching rows are also deleted
from any tables inheriting from the named table. Optionally, `*` can be
specified after the table name to explicitly indicate that descendant tables
are included.

_`alias`_

    

A substitute name for the target table. When an alias is provided, it
completely hides the actual name of the table. For example, given `DELETE FROM
foo AS f`, the remainder of the `DELETE` statement must refer to this table as
`f` not `foo`.

_`from_item`_

    

A table expression allowing columns from other tables to appear in the `WHERE`
condition. This uses the same syntax as the [`FROM`](sql-select.html#SQL-FROM
"FROM Clause") clause of a `SELECT` statement; for example, an alias for the
table name can be specified. Do not repeat the target table as a _`from_item`_
unless you wish to set up a self-join (in which case it must appear with an
alias in the _`from_item`_).

_`condition`_

    

An expression that returns a value of type `boolean`. Only rows for which this
expression returns `true` will be deleted.

_`cursor_name`_

    

The name of the cursor to use in a `WHERE CURRENT OF` condition. The row to be
deleted is the one most recently fetched from this cursor. The cursor must be
a non-grouping query on the `DELETE`'s target table. Note that `WHERE CURRENT
OF` cannot be specified together with a Boolean condition. See [DECLARE](sql-
declare.html "DECLARE") for more information about using cursors with `WHERE
CURRENT OF`.

_`output_expression`_

    

An expression to be computed and returned by the `DELETE` command after each
row is deleted. The expression can use any column names of the table named by
_`table_name`_ or table(s) listed in `USING`. Write `*` to return all columns.

_`output_name`_

    

A name to use for a returned column.

## Outputs

On successful completion, a `DELETE` command returns a command tag of the form

    
    
    DELETE _count_
    

The _`count`_ is the number of rows deleted. Note that the number may be less
than the number of rows that matched the _`condition`_ when deletes were
suppressed by a `BEFORE DELETE` trigger. If _`count`_ is 0, no rows were
deleted by the query (this is not considered an error).

If the `DELETE` command contains a `RETURNING` clause, the result will be
similar to that of a `SELECT` statement containing the columns and values
defined in the `RETURNING` list, computed over the row(s) deleted by the
command.

## Notes

PostgreSQL lets you reference columns of other tables in the `WHERE` condition
by specifying the other tables in the `USING` clause. For example, to delete
all films produced by a given producer, one can do:

    
    
    DELETE FROM films USING producers
      WHERE producer_id = producers.id AND producers.name = 'foo';
    

What is essentially happening here is a join between `films` and `producers`,
with all successfully joined `films` rows being marked for deletion. This
syntax is not standard. A more standard way to do it is:

    
    
    DELETE FROM films
      WHERE producer_id IN (SELECT id FROM producers WHERE name = 'foo');
    

In some cases the join style is easier to write or faster to execute than the
sub-select style.

## Examples

Delete all films but musicals:

    
    
    DELETE FROM films WHERE kind <> 'Musical';
    

Clear the table `films`:

    
    
    DELETE FROM films;
    

Delete completed tasks, returning full details of the deleted rows:

    
    
    DELETE FROM tasks WHERE status = 'DONE' RETURNING *;
    

Delete the row of `tasks` on which the cursor `c_tasks` is currently
positioned:

    
    
    DELETE FROM tasks WHERE CURRENT OF c_tasks;
    

## Compatibility

This command conforms to the SQL standard, except that the `USING` and
`RETURNING` clauses are PostgreSQL extensions, as is the ability to use `WITH`
with `DELETE`.

## See Also

[TRUNCATE](sql-truncate.html "TRUNCATE")

* * *

[Prev](sql-declare.html "DECLARE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-discard.html "DISCARD")  
---|---|---  
DECLARE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DISCARD  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-delete.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

