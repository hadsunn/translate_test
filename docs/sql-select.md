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

Supported Versions: [Current](/docs/current/sql-select.html "PostgreSQL 17 -
SELECT") ([17](/docs/17/sql-select.html "PostgreSQL 17 - SELECT")) /
[16](/docs/16/sql-select.html "PostgreSQL 16 - SELECT") / [15](/docs/15/sql-
select.html "PostgreSQL 15 - SELECT") / [14](/docs/14/sql-select.html
"PostgreSQL 14 - SELECT") / [13](/docs/13/sql-select.html "PostgreSQL 13 -
SELECT")

Development Versions: [18](/docs/18/sql-select.html "PostgreSQL 18 - SELECT")
/ [devel](/docs/devel/sql-select.html "PostgreSQL devel - SELECT")

Unsupported versions: [12](/docs/12/sql-select.html "PostgreSQL 12 - SELECT")
/ [11](/docs/11/sql-select.html "PostgreSQL 11 - SELECT") / [10](/docs/10/sql-
select.html "PostgreSQL 10 - SELECT") / [9.6](/docs/9.6/sql-select.html
"PostgreSQL 9.6 - SELECT") / [9.5](/docs/9.5/sql-select.html "PostgreSQL 9.5 -
SELECT") / [9.4](/docs/9.4/sql-select.html "PostgreSQL 9.4 - SELECT") /
[9.3](/docs/9.3/sql-select.html "PostgreSQL 9.3 - SELECT") /
[9.2](/docs/9.2/sql-select.html "PostgreSQL 9.2 - SELECT") /
[9.1](/docs/9.1/sql-select.html "PostgreSQL 9.1 - SELECT") /
[9.0](/docs/9.0/sql-select.html "PostgreSQL 9.0 - SELECT") /
[8.4](/docs/8.4/sql-select.html "PostgreSQL 8.4 - SELECT") /
[8.3](/docs/8.3/sql-select.html "PostgreSQL 8.3 - SELECT") /
[8.2](/docs/8.2/sql-select.html "PostgreSQL 8.2 - SELECT") /
[8.1](/docs/8.1/sql-select.html "PostgreSQL 8.1 - SELECT") /
[8.0](/docs/8.0/sql-select.html "PostgreSQL 8.0 - SELECT") /
[7.4](/docs/7.4/sql-select.html "PostgreSQL 7.4 - SELECT") /
[7.3](/docs/7.3/sql-select.html "PostgreSQL 7.3 - SELECT") /
[7.2](/docs/7.2/sql-select.html "PostgreSQL 7.2 - SELECT") /
[7.1](/docs/7.1/sql-select.html "PostgreSQL 7.1 - SELECT")

__

SELECT  
---  
[Prev](sql-security-label.html "SECURITY LABEL")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-selectinto.html "SELECT INTO")  
  
* * *

## SELECT

SELECT, TABLE, WITH — retrieve rows from a table or view

## Synopsis

    
    
    [ WITH [ RECURSIVE ] _with_query_ [, ...] ]
    SELECT [ ALL | DISTINCT [ ON ( _expression_ [, ...] ) ] ]
        [ { * | _expression_ [ [ AS ] _output_name_ ] } [, ...] ]
        [ FROM _from_item_ [, ...] ]
        [ WHERE _condition_ ]
        [ GROUP BY [ ALL | DISTINCT ] _grouping_element_ [, ...] ]
        [ HAVING _condition_ ]
        [ WINDOW _window_name_ AS ( _window_definition_ ) [, ...] ]
        [ { UNION | INTERSECT | EXCEPT } [ ALL | DISTINCT ] _select_ ]
        [ ORDER BY _expression_ [ ASC | DESC | USING _operator_ ] [ NULLS { FIRST | LAST } ] [, ...] ]
        [ LIMIT { _count_ | ALL } ]
        [ OFFSET _start_ [ ROW | ROWS ] ]
        [ FETCH { FIRST | NEXT } [ _count_ ] { ROW | ROWS } { ONLY | WITH TIES } ]
        [ FOR { UPDATE | NO KEY UPDATE | SHARE | KEY SHARE } [ OF _table_name_ [, ...] ] [ NOWAIT | SKIP LOCKED ] [...] ]
    
    where _from_item_ can be one of:
    
        [ ONLY ] _table_name_ [ * ] [ [ AS ] _alias_ [ ( _column_alias_ [, ...] ) ] ]
                    [ TABLESAMPLE _sampling_method_ ( _argument_ [, ...] ) [ REPEATABLE ( _seed_ ) ] ]
        [ LATERAL ] ( _select_ ) [ [ AS ] _alias_ [ ( _column_alias_ [, ...] ) ] ]
        _with_query_name_ [ [ AS ] _alias_ [ ( _column_alias_ [, ...] ) ] ]
        [ LATERAL ] _function_name_ ( [ _argument_ [, ...] ] )
                    [ WITH ORDINALITY ] [ [ AS ] _alias_ [ ( _column_alias_ [, ...] ) ] ]
        [ LATERAL ] _function_name_ ( [ _argument_ [, ...] ] ) [ AS ] _alias_ ( _column_definition_ [, ...] )
        [ LATERAL ] _function_name_ ( [ _argument_ [, ...] ] ) AS ( _column_definition_ [, ...] )
        [ LATERAL ] ROWS FROM( _function_name_ ( [ _argument_ [, ...] ] ) [ AS ( _column_definition_ [, ...] ) ] [, ...] )
                    [ WITH ORDINALITY ] [ [ AS ] _alias_ [ ( _column_alias_ [, ...] ) ] ]
        _from_item_ _join_type_ _from_item_ { ON _join_condition_ | USING ( _join_column_ [, ...] ) [ AS _join_using_alias_ ] }
        _from_item_ NATURAL _join_type_ _from_item_
        _from_item_ CROSS JOIN _from_item_
    
    and _grouping_element_ can be one of:
    
        ( )
        _expression_
        ( _expression_ [, ...] )
        ROLLUP ( { _expression_ | ( _expression_ [, ...] ) } [, ...] )
        CUBE ( { _expression_ | ( _expression_ [, ...] ) } [, ...] )
        GROUPING SETS ( _grouping_element_ [, ...] )
    
    and _with_query_ is:
    
        _with_query_name_ [ ( _column_name_ [, ...] ) ] AS [ [ NOT ] MATERIALIZED ] ( _select_ | _values_ | _insert_ | _update_ | _delete_ )
            [ SEARCH { BREADTH | DEPTH } FIRST BY _column_name_ [, ...] SET _search_seq_col_name_ ]
            [ CYCLE _column_name_ [, ...] SET _cycle_mark_col_name_ [ TO _cycle_mark_value_ DEFAULT _cycle_mark_default_ ] USING _cycle_path_col_name_ ]
    
    TABLE [ ONLY ] _table_name_ [ * ]
    

## Description

`SELECT` retrieves rows from zero or more tables. The general processing of
`SELECT` is as follows:

  1. All queries in the `WITH` list are computed. These effectively serve as temporary tables that can be referenced in the `FROM` list. A `WITH` query that is referenced more than once in `FROM` is computed only once, unless specified otherwise with `NOT MATERIALIZED`. (See [WITH Clause](sql-select.html#SQL-WITH "WITH Clause") below.)

  2. All elements in the `FROM` list are computed. (Each element in the `FROM` list is a real or virtual table.) If more than one element is specified in the `FROM` list, they are cross-joined together. (See [FROM Clause](sql-select.html#SQL-FROM "FROM Clause") below.)

  3. If the `WHERE` clause is specified, all rows that do not satisfy the condition are eliminated from the output. (See [WHERE Clause](sql-select.html#SQL-WHERE "WHERE Clause") below.)

  4. If the `GROUP BY` clause is specified, or if there are aggregate function calls, the output is combined into groups of rows that match on one or more values, and the results of aggregate functions are computed. If the `HAVING` clause is present, it eliminates groups that do not satisfy the given condition. (See [GROUP BY Clause](sql-select.html#SQL-GROUPBY "GROUP BY Clause") and [HAVING Clause](sql-select.html#SQL-HAVING "HAVING Clause") below.) Although query output columns are nominally computed in the next step, they can also be referenced (by name or ordinal number) in the `GROUP BY` clause.

  5. The actual output rows are computed using the `SELECT` output expressions for each selected row or row group. (See [SELECT List](sql-select.html#SQL-SELECT-LIST "SELECT List") below.)

  6. `SELECT DISTINCT` eliminates duplicate rows from the result. `SELECT DISTINCT ON` eliminates rows that match on all the specified expressions. `SELECT ALL` (the default) will return all candidate rows, including duplicates. (See [DISTINCT Clause](sql-select.html#SQL-DISTINCT "DISTINCT Clause") below.)

  7. Using the operators `UNION`, `INTERSECT`, and `EXCEPT`, the output of more than one `SELECT` statement can be combined to form a single result set. The `UNION` operator returns all rows that are in one or both of the result sets. The `INTERSECT` operator returns all rows that are strictly in both result sets. The `EXCEPT` operator returns the rows that are in the first result set but not in the second. In all three cases, duplicate rows are eliminated unless `ALL` is specified. The noise word `DISTINCT` can be added to explicitly specify eliminating duplicate rows. Notice that `DISTINCT` is the default behavior here, even though `ALL` is the default for `SELECT` itself. (See [UNION Clause](sql-select.html#SQL-UNION "UNION Clause"), [INTERSECT Clause](sql-select.html#SQL-INTERSECT "INTERSECT Clause"), and [EXCEPT Clause](sql-select.html#SQL-EXCEPT "EXCEPT Clause") below.)

  8. If the `ORDER BY` clause is specified, the returned rows are sorted in the specified order. If `ORDER BY` is not given, the rows are returned in whatever order the system finds fastest to produce. (See [ORDER BY Clause](sql-select.html#SQL-ORDERBY "ORDER BY Clause") below.)

  9. If the `LIMIT` (or `FETCH FIRST`) or `OFFSET` clause is specified, the `SELECT` statement only returns a subset of the result rows. (See [LIMIT Clause](sql-select.html#SQL-LIMIT "LIMIT Clause") below.)

  10. If `FOR UPDATE`, `FOR NO KEY UPDATE`, `FOR SHARE` or `FOR KEY SHARE` is specified, the `SELECT` statement locks the selected rows against concurrent updates. (See [The Locking Clause](sql-select.html#SQL-FOR-UPDATE-SHARE "The Locking Clause") below.)

You must have `SELECT` privilege on each column used in a `SELECT` command.
The use of `FOR NO KEY UPDATE`, `FOR UPDATE`, `FOR SHARE` or `FOR KEY SHARE`
requires `UPDATE` privilege as well (for at least one column of each table so
selected).

## Parameters

### `WITH` Clause

The `WITH` clause allows you to specify one or more subqueries that can be
referenced by name in the primary query. The subqueries effectively act as
temporary tables or views for the duration of the primary query. Each subquery
can be a `SELECT`, `TABLE`, `VALUES`, `INSERT`, `UPDATE` or `DELETE`
statement. When writing a data-modifying statement (`INSERT`, `UPDATE` or
`DELETE`) in `WITH`, it is usual to include a `RETURNING` clause. It is the
output of `RETURNING`, _not_ the underlying table that the statement modifies,
that forms the temporary table that is read by the primary query. If
`RETURNING` is omitted, the statement is still executed, but it produces no
output so it cannot be referenced as a table by the primary query.

A name (without schema qualification) must be specified for each `WITH` query.
Optionally, a list of column names can be specified; if this is omitted, the
column names are inferred from the subquery.

If `RECURSIVE` is specified, it allows a `SELECT` subquery to reference itself
by name. Such a subquery must have the form

    
    
    _non_recursive_term_ UNION [ ALL | DISTINCT ] _recursive_term_
    

where the recursive self-reference must appear on the right-hand side of the
`UNION`. Only one recursive self-reference is permitted per query. Recursive
data-modifying statements are not supported, but you can use the results of a
recursive `SELECT` query in a data-modifying statement. See [Section
7.8](queries-with.html "7.8. WITH Queries \(Common Table Expressions\)") for
an example.

Another effect of `RECURSIVE` is that `WITH` queries need not be ordered: a
query can reference another one that is later in the list. (However, circular
references, or mutual recursion, are not implemented.) Without `RECURSIVE`,
`WITH` queries can only reference sibling `WITH` queries that are earlier in
the `WITH` list.

When there are multiple queries in the `WITH` clause, `RECURSIVE` should be
written only once, immediately after `WITH`. It applies to all queries in the
`WITH` clause, though it has no effect on queries that do not use recursion or
forward references.

The optional `SEARCH` clause computes a _search sequence column_ that can be
used for ordering the results of a recursive query in either breadth-first or
depth-first order. The supplied column name list specifies the row key that is
to be used for keeping track of visited rows. A column named
_`search_seq_col_name`_ will be added to the result column list of the `WITH`
query. This column can be ordered by in the outer query to achieve the
respective ordering. See [Section 7.8.2.1](queries-with.html#QUERIES-WITH-
SEARCH "7.8.2.1. Search Order") for examples.

The optional `CYCLE` clause is used to detect cycles in recursive queries. The
supplied column name list specifies the row key that is to be used for keeping
track of visited rows. A column named _`cycle_mark_col_name`_ will be added to
the result column list of the `WITH` query. This column will be set to
_`cycle_mark_value`_ when a cycle has been detected, else to
_`cycle_mark_default`_. Furthermore, processing of the recursive union will
stop when a cycle has been detected. _`cycle_mark_value`_ and
_`cycle_mark_default`_ must be constants and they must be coercible to a
common data type, and the data type must have an inequality operator. (The SQL
standard requires that they be Boolean constants or character strings, but
PostgreSQL does not require that.) By default, `TRUE` and `FALSE` (of type
`boolean`) are used. Furthermore, a column named _`cycle_path_col_name`_ will
be added to the result column list of the `WITH` query. This column is used
internally for tracking visited rows. See [Section 7.8.2.2](queries-
with.html#QUERIES-WITH-CYCLE "7.8.2.2. Cycle Detection") for examples.

Both the `SEARCH` and the `CYCLE` clause are only valid for recursive `WITH`
queries. The _`with_query`_ must be a `UNION` (or `UNION ALL`) of two `SELECT`
(or equivalent) commands (no nested `UNION`s). If both clauses are used, the
column added by the `SEARCH` clause appears before the columns added by the
`CYCLE` clause.

The primary query and the `WITH` queries are all (notionally) executed at the
same time. This implies that the effects of a data-modifying statement in
`WITH` cannot be seen from other parts of the query, other than by reading its
`RETURNING` output. If two such data-modifying statements attempt to modify
the same row, the results are unspecified.

A key property of `WITH` queries is that they are normally evaluated only once
per execution of the primary query, even if the primary query refers to them
more than once. In particular, data-modifying statements are guaranteed to be
executed once and only once, regardless of whether the primary query reads all
or any of their output.

However, a `WITH` query can be marked `NOT MATERIALIZED` to remove this
guarantee. In that case, the `WITH` query can be folded into the primary query
much as though it were a simple sub-`SELECT` in the primary query's `FROM`
clause. This results in duplicate computations if the primary query refers to
that `WITH` query more than once; but if each such use requires only a few
rows of the `WITH` query's total output, `NOT MATERIALIZED` can provide a net
savings by allowing the queries to be optimized jointly. `NOT MATERIALIZED` is
ignored if it is attached to a `WITH` query that is recursive or is not side-
effect-free (i.e., is not a plain `SELECT` containing no volatile functions).

By default, a side-effect-free `WITH` query is folded into the primary query
if it is used exactly once in the primary query's `FROM` clause. This allows
joint optimization of the two query levels in situations where that should be
semantically invisible. However, such folding can be prevented by marking the
`WITH` query as `MATERIALIZED`. That might be useful, for example, if the
`WITH` query is being used as an optimization fence to prevent the planner
from choosing a bad plan. PostgreSQL versions before v12 never did such
folding, so queries written for older versions might rely on `WITH` to act as
an optimization fence.

See [Section 7.8](queries-with.html "7.8. WITH Queries \(Common Table
Expressions\)") for additional information.

### `FROM` Clause

The `FROM` clause specifies one or more source tables for the `SELECT`. If
multiple sources are specified, the result is the Cartesian product (cross
join) of all the sources. But usually qualification conditions are added (via
`WHERE`) to restrict the returned rows to a small subset of the Cartesian
product.

The `FROM` clause can contain the following elements:

_`table_name`_

    

The name (optionally schema-qualified) of an existing table or view. If `ONLY`
is specified before the table name, only that table is scanned. If `ONLY` is
not specified, the table and all its descendant tables (if any) are scanned.
Optionally, `*` can be specified after the table name to explicitly indicate
that descendant tables are included.

_`alias`_

    

A substitute name for the `FROM` item containing the alias. An alias is used
for brevity or to eliminate ambiguity for self-joins (where the same table is
scanned multiple times). When an alias is provided, it completely hides the
actual name of the table or function; for example given `FROM foo AS f`, the
remainder of the `SELECT` must refer to this `FROM` item as `f` not `foo`. If
an alias is written, a column alias list can also be written to provide
substitute names for one or more columns of the table.

`TABLESAMPLE _`sampling_method`_ ( _`argument`_ [, ...] ) [ REPEATABLE (
_`seed`_ ) ]`

    

A `TABLESAMPLE` clause after a _`table_name`_ indicates that the specified
_`sampling_method`_ should be used to retrieve a subset of the rows in that
table. This sampling precedes the application of any other filters such as
`WHERE` clauses. The standard PostgreSQL distribution includes two sampling
methods, `BERNOULLI` and `SYSTEM`, and other sampling methods can be installed
in the database via extensions.

The `BERNOULLI` and `SYSTEM` sampling methods each accept a single
_`argument`_ which is the fraction of the table to sample, expressed as a
percentage between 0 and 100. This argument can be any `real`-valued
expression. (Other sampling methods might accept more or different arguments.)
These two methods each return a randomly-chosen sample of the table that will
contain approximately the specified percentage of the table's rows. The
`BERNOULLI` method scans the whole table and selects or ignores individual
rows independently with the specified probability. The `SYSTEM` method does
block-level sampling with each block having the specified chance of being
selected; all rows in each selected block are returned. The `SYSTEM` method is
significantly faster than the `BERNOULLI` method when small sampling
percentages are specified, but it may return a less-random sample of the table
as a result of clustering effects.

The optional `REPEATABLE` clause specifies a _`seed`_ number or expression to
use for generating random numbers within the sampling method. The seed value
can be any non-null floating-point value. Two queries that specify the same
seed and _`argument`_ values will select the same sample of the table, if the
table has not been changed meanwhile. But different seed values will usually
produce different samples. If `REPEATABLE` is not given then a new random
sample is selected for each query, based upon a system-generated seed. Note
that some add-on sampling methods do not accept `REPEATABLE`, and will always
produce new samples on each use.

_`select`_

    

A sub-`SELECT` can appear in the `FROM` clause. This acts as though its output
were created as a temporary table for the duration of this single `SELECT`
command. Note that the sub-`SELECT` must be surrounded by parentheses, and an
alias can be provided in the same way as for a table. A [`VALUES`](sql-
values.html "VALUES") command can also be used here.

_`with_query_name`_

    

A `WITH` query is referenced by writing its name, just as though the query's
name were a table name. (In fact, the `WITH` query hides any real table of the
same name for the purposes of the primary query. If necessary, you can refer
to a real table of the same name by schema-qualifying the table's name.) An
alias can be provided in the same way as for a table.

_`function_name`_

    

Function calls can appear in the `FROM` clause. (This is especially useful for
functions that return result sets, but any function can be used.) This acts as
though the function's output were created as a temporary table for the
duration of this single `SELECT` command. If the function's result type is
composite (including the case of a function with multiple `OUT` parameters),
each attribute becomes a separate column in the implicit table.

When the optional `WITH ORDINALITY` clause is added to the function call, an
additional column of type `bigint` will be appended to the function's result
column(s). This column numbers the rows of the function's result set, starting
from 1. By default, this column is named `ordinality`.

An alias can be provided in the same way as for a table. If an alias is
written, a column alias list can also be written to provide substitute names
for one or more attributes of the function's composite return type, including
the ordinality column if present.

Multiple function calls can be combined into a single `FROM`-clause item by
surrounding them with `ROWS FROM( ... )`. The output of such an item is the
concatenation of the first row from each function, then the second row from
each function, etc. If some of the functions produce fewer rows than others,
null values are substituted for the missing data, so that the total number of
rows returned is always the same as for the function that produced the most
rows.

If the function has been defined as returning the `record` data type, then an
alias or the key word `AS` must be present, followed by a column definition
list in the form `( _`column_name`_ _`data_type`_ [, ... ])`. The column
definition list must match the actual number and types of columns returned by
the function.

When using the `ROWS FROM( ... )` syntax, if one of the functions requires a
column definition list, it's preferred to put the column definition list after
the function call inside `ROWS FROM( ... )`. A column definition list can be
placed after the `ROWS FROM( ... )` construct only if there's just a single
function and no `WITH ORDINALITY` clause.

To use `ORDINALITY` together with a column definition list, you must use the
`ROWS FROM( ... )` syntax and put the column definition list inside `ROWS
FROM( ... )`.

_`join_type`_

    

One of

  * `[ INNER ] JOIN`

  * `LEFT [ OUTER ] JOIN`

  * `RIGHT [ OUTER ] JOIN`

  * `FULL [ OUTER ] JOIN`

For the `INNER` and `OUTER` join types, a join condition must be specified,
namely exactly one of `ON _`join_condition`_`, `USING (_`join_column`_ [,
...])`, or `NATURAL`. See below for the meaning.

A `JOIN` clause combines two `FROM` items, which for convenience we will refer
to as “tables”, though in reality they can be any type of `FROM` item. Use
parentheses if necessary to determine the order of nesting. In the absence of
parentheses, `JOIN`s nest left-to-right. In any case `JOIN` binds more tightly
than the commas separating `FROM`-list items. All the `JOIN` options are just
a notational convenience, since they do nothing you couldn't do with plain
`FROM` and `WHERE`.

`LEFT OUTER JOIN` returns all rows in the qualified Cartesian product (i.e.,
all combined rows that pass its join condition), plus one copy of each row in
the left-hand table for which there was no right-hand row that passed the join
condition. This left-hand row is extended to the full width of the joined
table by inserting null values for the right-hand columns. Note that only the
`JOIN` clause's own condition is considered while deciding which rows have
matches. Outer conditions are applied afterwards.

Conversely, `RIGHT OUTER JOIN` returns all the joined rows, plus one row for
each unmatched right-hand row (extended with nulls on the left). This is just
a notational convenience, since you could convert it to a `LEFT OUTER JOIN` by
switching the left and right tables.

`FULL OUTER JOIN` returns all the joined rows, plus one row for each unmatched
left-hand row (extended with nulls on the right), plus one row for each
unmatched right-hand row (extended with nulls on the left).

`ON _`join_condition`_`

    

_`join_condition`_ is an expression resulting in a value of type `boolean`
(similar to a `WHERE` clause) that specifies which rows in a join are
considered to match.

`USING ( _`join_column`_ [, ...] ) [ AS _`join_using_alias`_ ]`

    

A clause of the form `USING ( a, b, ... )` is shorthand for `ON left_table.a =
right_table.a AND left_table.b = right_table.b ...`. Also, `USING` implies
that only one of each pair of equivalent columns will be included in the join
output, not both.

If a _`join_using_alias`_ name is specified, it provides a table alias for the
join columns. Only the join columns listed in the `USING` clause are
addressable by this name. Unlike a regular _`alias`_ , this does not hide the
names of the joined tables from the rest of the query. Also unlike a regular
_`alias`_ , you cannot write a column alias list — the output names of the
join columns are the same as they appear in the `USING` list.

`NATURAL`

    

`NATURAL` is shorthand for a `USING` list that mentions all columns in the two
tables that have matching names. If there are no common column names,
`NATURAL` is equivalent to `ON TRUE`.

`CROSS JOIN`

    

`CROSS JOIN` is equivalent to `INNER JOIN ON (TRUE)`, that is, no rows are
removed by qualification. They produce a simple Cartesian product, the same
result as you get from listing the two tables at the top level of `FROM`, but
restricted by the join condition (if any).

`LATERAL`

    

The `LATERAL` key word can precede a sub-`SELECT` `FROM` item. This allows the
sub-`SELECT` to refer to columns of `FROM` items that appear before it in the
`FROM` list. (Without `LATERAL`, each sub-`SELECT` is evaluated independently
and so cannot cross-reference any other `FROM` item.)

`LATERAL` can also precede a function-call `FROM` item, but in this case it is
a noise word, because the function expression can refer to earlier `FROM`
items in any case.

A `LATERAL` item can appear at top level in the `FROM` list, or within a
`JOIN` tree. In the latter case it can also refer to any items that are on the
left-hand side of a `JOIN` that it is on the right-hand side of.

When a `FROM` item contains `LATERAL` cross-references, evaluation proceeds as
follows: for each row of the `FROM` item providing the cross-referenced
column(s), or set of rows of multiple `FROM` items providing the columns, the
`LATERAL` item is evaluated using that row or row set's values of the columns.
The resulting row(s) are joined as usual with the rows they were computed
from. This is repeated for each row or set of rows from the column source
table(s).

The column source table(s) must be `INNER` or `LEFT` joined to the `LATERAL`
item, else there would not be a well-defined set of rows from which to compute
each set of rows for the `LATERAL` item. Thus, although a construct such as
`_`X`_ RIGHT JOIN LATERAL _`Y`_` is syntactically valid, it is not actually
allowed for _`Y`_ to reference _`X`_.

### `WHERE` Clause

The optional `WHERE` clause has the general form

    
    
    WHERE _condition_
    

where _`condition`_ is any expression that evaluates to a result of type
`boolean`. Any row that does not satisfy this condition will be eliminated
from the output. A row satisfies the condition if it returns true when the
actual row values are substituted for any variable references.

### `GROUP BY` Clause

The optional `GROUP BY` clause has the general form

    
    
    GROUP BY [ ALL | DISTINCT ] _grouping_element_ [, ...]
    

`GROUP BY` will condense into a single row all selected rows that share the
same values for the grouped expressions. An _`expression`_ used inside a
_`grouping_element`_ can be an input column name, or the name or ordinal
number of an output column (`SELECT` list item), or an arbitrary expression
formed from input-column values. In case of ambiguity, a `GROUP BY` name will
be interpreted as an input-column name rather than an output column name.

If any of `GROUPING SETS`, `ROLLUP` or `CUBE` are present as grouping
elements, then the `GROUP BY` clause as a whole defines some number of
independent _`grouping sets`_. The effect of this is equivalent to
constructing a `UNION ALL` between subqueries with the individual grouping
sets as their `GROUP BY` clauses. The optional `DISTINCT` clause removes
duplicate sets before processing; it does _not_ transform the `UNION ALL` into
a `UNION DISTINCT`. For further details on the handling of grouping sets see
[Section 7.2.4](queries-table-expressions.html#QUERIES-GROUPING-SETS
"7.2.4. GROUPING SETS, CUBE, and ROLLUP").

Aggregate functions, if any are used, are computed across all rows making up
each group, producing a separate value for each group. (If there are aggregate
functions but no `GROUP BY` clause, the query is treated as having a single
group comprising all the selected rows.) The set of rows fed to each aggregate
function can be further filtered by attaching a `FILTER` clause to the
aggregate function call; see [Section 4.2.7](sql-expressions.html#SYNTAX-
AGGREGATES "4.2.7. Aggregate Expressions") for more information. When a
`FILTER` clause is present, only those rows matching it are included in the
input to that aggregate function.

When `GROUP BY` is present, or any aggregate functions are present, it is not
valid for the `SELECT` list expressions to refer to ungrouped columns except
within aggregate functions or when the ungrouped column is functionally
dependent on the grouped columns, since there would otherwise be more than one
possible value to return for an ungrouped column. A functional dependency
exists if the grouped columns (or a subset thereof) are the primary key of the
table containing the ungrouped column.

Keep in mind that all aggregate functions are evaluated before evaluating any
“scalar” expressions in the `HAVING` clause or `SELECT` list. This means that,
for example, a `CASE` expression cannot be used to skip evaluation of an
aggregate function; see [Section 4.2.14](sql-expressions.html#SYNTAX-EXPRESS-
EVAL "4.2.14. Expression Evaluation Rules").

Currently, `FOR NO KEY UPDATE`, `FOR UPDATE`, `FOR SHARE` and `FOR KEY SHARE`
cannot be specified with `GROUP BY`.

### `HAVING` Clause

The optional `HAVING` clause has the general form

    
    
    HAVING _condition_
    

where _`condition`_ is the same as specified for the `WHERE` clause.

`HAVING` eliminates group rows that do not satisfy the condition. `HAVING` is
different from `WHERE`: `WHERE` filters individual rows before the application
of `GROUP BY`, while `HAVING` filters group rows created by `GROUP BY`. Each
column referenced in _`condition`_ must unambiguously reference a grouping
column, unless the reference appears within an aggregate function or the
ungrouped column is functionally dependent on the grouping columns.

The presence of `HAVING` turns a query into a grouped query even if there is
no `GROUP BY` clause. This is the same as what happens when the query contains
aggregate functions but no `GROUP BY` clause. All the selected rows are
considered to form a single group, and the `SELECT` list and `HAVING` clause
can only reference table columns from within aggregate functions. Such a query
will emit a single row if the `HAVING` condition is true, zero rows if it is
not true.

Currently, `FOR NO KEY UPDATE`, `FOR UPDATE`, `FOR SHARE` and `FOR KEY SHARE`
cannot be specified with `HAVING`.

### `WINDOW` Clause

The optional `WINDOW` clause has the general form

    
    
    WINDOW _window_name_ AS ( _window_definition_ ) [, ...]
    

where _`window_name`_ is a name that can be referenced from `OVER` clauses or
subsequent window definitions, and _`window_definition`_ is

    
    
    [ _existing_window_name_ ]
    [ PARTITION BY _expression_ [, ...] ]
    [ ORDER BY _expression_ [ ASC | DESC | USING _operator_ ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ _frame_clause_ ]
    

If an _`existing_window_name`_ is specified it must refer to an earlier entry
in the `WINDOW` list; the new window copies its partitioning clause from that
entry, as well as its ordering clause if any. In this case the new window
cannot specify its own `PARTITION BY` clause, and it can specify `ORDER BY`
only if the copied window does not have one. The new window always uses its
own frame clause; the copied window must not specify a frame clause.

The elements of the `PARTITION BY` list are interpreted in much the same
fashion as elements of a [`GROUP BY`](sql-select.html#SQL-GROUPBY "GROUP BY
Clause") clause, except that they are always simple expressions and never the
name or number of an output column. Another difference is that these
expressions can contain aggregate function calls, which are not allowed in a
regular `GROUP BY` clause. They are allowed here because windowing occurs
after grouping and aggregation.

Similarly, the elements of the `ORDER BY` list are interpreted in much the
same fashion as elements of a statement-level [`ORDER BY`](sql-
select.html#SQL-ORDERBY "ORDER BY Clause") clause, except that the expressions
are always taken as simple expressions and never the name or number of an
output column.

The optional _`frame_clause`_ defines the _window frame_ for window functions
that depend on the frame (not all do). The window frame is a set of related
rows for each row of the query (called the _current row_). The
_`frame_clause`_ can be one of

    
    
    { RANGE | ROWS | GROUPS } _frame_start_ [ _frame_exclusion_ ]
    { RANGE | ROWS | GROUPS } BETWEEN _frame_start_ AND _frame_end_ [ _frame_exclusion_ ]
    

where _`frame_start`_ and _`frame_end`_ can be one of

    
    
    UNBOUNDED PRECEDING
    _offset_ PRECEDING
    CURRENT ROW
    _offset_ FOLLOWING
    UNBOUNDED FOLLOWING
    

and _`frame_exclusion`_ can be one of

    
    
    EXCLUDE CURRENT ROW
    EXCLUDE GROUP
    EXCLUDE TIES
    EXCLUDE NO OTHERS
    

If _`frame_end`_ is omitted it defaults to `CURRENT ROW`. Restrictions are
that _`frame_start`_ cannot be `UNBOUNDED FOLLOWING`, _`frame_end`_ cannot be
`UNBOUNDED PRECEDING`, and the _`frame_end`_ choice cannot appear earlier in
the above list of _`frame_start`_ and _`frame_end`_ options than the
_`frame_start`_ choice does — for example `RANGE BETWEEN CURRENT ROW AND
_`offset`_ PRECEDING` is not allowed.

The default framing option is `RANGE UNBOUNDED PRECEDING`, which is the same
as `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`; it sets the frame to
be all rows from the partition start up through the current row's last _peer_
(a row that the window's `ORDER BY` clause considers equivalent to the current
row; all rows are peers if there is no `ORDER BY`). In general, `UNBOUNDED
PRECEDING` means that the frame starts with the first row of the partition,
and similarly `UNBOUNDED FOLLOWING` means that the frame ends with the last
row of the partition, regardless of `RANGE`, `ROWS` or `GROUPS` mode. In
`ROWS` mode, `CURRENT ROW` means that the frame starts or ends with the
current row; but in `RANGE` or `GROUPS` mode it means that the frame starts or
ends with the current row's first or last peer in the `ORDER BY` ordering. The
_`offset`_ `PRECEDING` and _`offset`_ `FOLLOWING` options vary in meaning
depending on the frame mode. In `ROWS` mode, the _`offset`_ is an integer
indicating that the frame starts or ends that many rows before or after the
current row. In `GROUPS` mode, the _`offset`_ is an integer indicating that
the frame starts or ends that many peer groups before or after the current
row's peer group, where a _peer group_ is a group of rows that are equivalent
according to the window's `ORDER BY` clause. In `RANGE` mode, use of an
_`offset`_ option requires that there be exactly one `ORDER BY` column in the
window definition. Then the frame contains those rows whose ordering column
value is no more than _`offset`_ less than (for `PRECEDING`) or more than (for
`FOLLOWING`) the current row's ordering column value. In these cases the data
type of the _`offset`_ expression depends on the data type of the ordering
column. For numeric ordering columns it is typically of the same type as the
ordering column, but for datetime ordering columns it is an `interval`. In all
these cases, the value of the _`offset`_ must be non-null and non-negative.
Also, while the _`offset`_ does not have to be a simple constant, it cannot
contain variables, aggregate functions, or window functions.

The _`frame_exclusion`_ option allows rows around the current row to be
excluded from the frame, even if they would be included according to the frame
start and frame end options. `EXCLUDE CURRENT ROW` excludes the current row
from the frame. `EXCLUDE GROUP` excludes the current row and its ordering
peers from the frame. `EXCLUDE TIES` excludes any peers of the current row
from the frame, but not the current row itself. `EXCLUDE NO OTHERS` simply
specifies explicitly the default behavior of not excluding the current row or
its peers.

Beware that the `ROWS` mode can produce unpredictable results if the `ORDER
BY` ordering does not order the rows uniquely. The `RANGE` and `GROUPS` modes
are designed to ensure that rows that are peers in the `ORDER BY` ordering are
treated alike: all rows of a given peer group will be in the frame or excluded
from it.

The purpose of a `WINDOW` clause is to specify the behavior of _window
functions_ appearing in the query's [`SELECT` list](sql-select.html#SQL-
SELECT-LIST "SELECT List") or [`ORDER BY`](sql-select.html#SQL-ORDERBY "ORDER
BY Clause") clause. These functions can reference the `WINDOW` clause entries
by name in their `OVER` clauses. A `WINDOW` clause entry does not have to be
referenced anywhere, however; if it is not used in the query it is simply
ignored. It is possible to use window functions without any `WINDOW` clause at
all, since a window function call can specify its window definition directly
in its `OVER` clause. However, the `WINDOW` clause saves typing when the same
window definition is needed for more than one window function.

Currently, `FOR NO KEY UPDATE`, `FOR UPDATE`, `FOR SHARE` and `FOR KEY SHARE`
cannot be specified with `WINDOW`.

Window functions are described in detail in [Section 3.5](tutorial-window.html
"3.5. Window Functions"), [Section 4.2.8](sql-expressions.html#SYNTAX-WINDOW-
FUNCTIONS "4.2.8. Window Function Calls"), and [Section 7.2.5](queries-table-
expressions.html#QUERIES-WINDOW "7.2.5. Window Function Processing").

### `SELECT` List

The `SELECT` list (between the key words `SELECT` and `FROM`) specifies
expressions that form the output rows of the `SELECT` statement. The
expressions can (and usually do) refer to columns computed in the `FROM`
clause.

Just as in a table, every output column of a `SELECT` has a name. In a simple
`SELECT` this name is just used to label the column for display, but when the
`SELECT` is a sub-query of a larger query, the name is seen by the larger
query as the column name of the virtual table produced by the sub-query. To
specify the name to use for an output column, write `AS` _`output_name`_ after
the column's expression. (You can omit `AS`, but only if the desired output
name does not match any PostgreSQL keyword (see [Appendix C](sql-keywords-
appendix.html "Appendix C. SQL Key Words")). For protection against possible
future keyword additions, it is recommended that you always either write `AS`
or double-quote the output name.) If you do not specify a column name, a name
is chosen automatically by PostgreSQL. If the column's expression is a simple
column reference then the chosen name is the same as that column's name. In
more complex cases a function or type name may be used, or the system may fall
back on a generated name such as `?column?`.

An output column's name can be used to refer to the column's value in `ORDER
BY` and `GROUP BY` clauses, but not in the `WHERE` or `HAVING` clauses; there
you must write out the expression instead.

Instead of an expression, `*` can be written in the output list as a shorthand
for all the columns of the selected rows. Also, you can write
`_`table_name`_.*` as a shorthand for the columns coming from just that table.
In these cases it is not possible to specify new names with `AS`; the output
column names will be the same as the table columns' names.

According to the SQL standard, the expressions in the output list should be
computed before applying `DISTINCT`, `ORDER BY`, or `LIMIT`. This is obviously
necessary when using `DISTINCT`, since otherwise it's not clear what values
are being made distinct. However, in many cases it is convenient if output
expressions are computed after `ORDER BY` and `LIMIT`; particularly if the
output list contains any volatile or expensive functions. With that behavior,
the order of function evaluations is more intuitive and there will not be
evaluations corresponding to rows that never appear in the output. PostgreSQL
will effectively evaluate output expressions after sorting and limiting, so
long as those expressions are not referenced in `DISTINCT`, `ORDER BY` or
`GROUP BY`. (As a counterexample, `SELECT f(x) FROM tab ORDER BY 1` clearly
must evaluate `f(x)` before sorting.) Output expressions that contain set-
returning functions are effectively evaluated after sorting and before
limiting, so that `LIMIT` will act to cut off the output from a set-returning
function.

### Note

PostgreSQL versions before 9.6 did not provide any guarantees about the timing
of evaluation of output expressions versus sorting and limiting; it depended
on the form of the chosen query plan.

### `DISTINCT` Clause

If `SELECT DISTINCT` is specified, all duplicate rows are removed from the
result set (one row is kept from each group of duplicates). `SELECT ALL`
specifies the opposite: all rows are kept; that is the default.

`SELECT DISTINCT ON ( _`expression`_ [, ...] )` keeps only the first row of
each set of rows where the given expressions evaluate to equal. The `DISTINCT
ON` expressions are interpreted using the same rules as for `ORDER BY` (see
above). Note that the “first row” of each set is unpredictable unless `ORDER
BY` is used to ensure that the desired row appears first. For example:

    
    
    SELECT DISTINCT ON (location) location, time, report
        FROM weather_reports
        ORDER BY location, time DESC;
    

retrieves the most recent weather report for each location. But if we had not
used `ORDER BY` to force descending order of time values for each location,
we'd have gotten a report from an unpredictable time for each location.

The `DISTINCT ON` expression(s) must match the leftmost `ORDER BY`
expression(s). The `ORDER BY` clause will normally contain additional
expression(s) that determine the desired precedence of rows within each
`DISTINCT ON` group.

Currently, `FOR NO KEY UPDATE`, `FOR UPDATE`, `FOR SHARE` and `FOR KEY SHARE`
cannot be specified with `DISTINCT`.

### `UNION` Clause

The `UNION` clause has this general form:

    
    
    _select_statement_ UNION [ ALL | DISTINCT ] _select_statement_
    

_`select_statement`_ is any `SELECT` statement without an `ORDER BY`, `LIMIT`,
`FOR NO KEY UPDATE`, `FOR UPDATE`, `FOR SHARE`, or `FOR KEY SHARE` clause.
(`ORDER BY` and `LIMIT` can be attached to a subexpression if it is enclosed
in parentheses. Without parentheses, these clauses will be taken to apply to
the result of the `UNION`, not to its right-hand input expression.)

The `UNION` operator computes the set union of the rows returned by the
involved `SELECT` statements. A row is in the set union of two result sets if
it appears in at least one of the result sets. The two `SELECT` statements
that represent the direct operands of the `UNION` must produce the same number
of columns, and corresponding columns must be of compatible data types.

The result of `UNION` does not contain any duplicate rows unless the `ALL`
option is specified. `ALL` prevents elimination of duplicates. (Therefore,
`UNION ALL` is usually significantly quicker than `UNION`; use `ALL` when you
can.) `DISTINCT` can be written to explicitly specify the default behavior of
eliminating duplicate rows.

Multiple `UNION` operators in the same `SELECT` statement are evaluated left
to right, unless otherwise indicated by parentheses.

Currently, `FOR NO KEY UPDATE`, `FOR UPDATE`, `FOR SHARE` and `FOR KEY SHARE`
cannot be specified either for a `UNION` result or for any input of a `UNION`.

### `INTERSECT` Clause

The `INTERSECT` clause has this general form:

    
    
    _select_statement_ INTERSECT [ ALL | DISTINCT ] _select_statement_
    

_`select_statement`_ is any `SELECT` statement without an `ORDER BY`, `LIMIT`,
`FOR NO KEY UPDATE`, `FOR UPDATE`, `FOR SHARE`, or `FOR KEY SHARE` clause.

The `INTERSECT` operator computes the set intersection of the rows returned by
the involved `SELECT` statements. A row is in the intersection of two result
sets if it appears in both result sets.

The result of `INTERSECT` does not contain any duplicate rows unless the `ALL`
option is specified. With `ALL`, a row that has _`m`_ duplicates in the left
table and _`n`_ duplicates in the right table will appear min(_`m`_ ,_`n`_)
times in the result set. `DISTINCT` can be written to explicitly specify the
default behavior of eliminating duplicate rows.

Multiple `INTERSECT` operators in the same `SELECT` statement are evaluated
left to right, unless parentheses dictate otherwise. `INTERSECT` binds more
tightly than `UNION`. That is, `A UNION B INTERSECT C` will be read as `A
UNION (B INTERSECT C)`.

Currently, `FOR NO KEY UPDATE`, `FOR UPDATE`, `FOR SHARE` and `FOR KEY SHARE`
cannot be specified either for an `INTERSECT` result or for any input of an
`INTERSECT`.

### `EXCEPT` Clause

The `EXCEPT` clause has this general form:

    
    
    _select_statement_ EXCEPT [ ALL | DISTINCT ] _select_statement_
    

_`select_statement`_ is any `SELECT` statement without an `ORDER BY`, `LIMIT`,
`FOR NO KEY UPDATE`, `FOR UPDATE`, `FOR SHARE`, or `FOR KEY SHARE` clause.

The `EXCEPT` operator computes the set of rows that are in the result of the
left `SELECT` statement but not in the result of the right one.

The result of `EXCEPT` does not contain any duplicate rows unless the `ALL`
option is specified. With `ALL`, a row that has _`m`_ duplicates in the left
table and _`n`_ duplicates in the right table will appear max(_`m`_ -_`n`_ ,0)
times in the result set. `DISTINCT` can be written to explicitly specify the
default behavior of eliminating duplicate rows.

Multiple `EXCEPT` operators in the same `SELECT` statement are evaluated left
to right, unless parentheses dictate otherwise. `EXCEPT` binds at the same
level as `UNION`.

Currently, `FOR NO KEY UPDATE`, `FOR UPDATE`, `FOR SHARE` and `FOR KEY SHARE`
cannot be specified either for an `EXCEPT` result or for any input of an
`EXCEPT`.

### `ORDER BY` Clause

The optional `ORDER BY` clause has this general form:

    
    
    ORDER BY _expression_ [ ASC | DESC | USING _operator_ ] [ NULLS { FIRST | LAST } ] [, ...]
    

The `ORDER BY` clause causes the result rows to be sorted according to the
specified expression(s). If two rows are equal according to the leftmost
expression, they are compared according to the next expression and so on. If
they are equal according to all specified expressions, they are returned in an
implementation-dependent order.

Each _`expression`_ can be the name or ordinal number of an output column
(`SELECT` list item), or it can be an arbitrary expression formed from input-
column values.

The ordinal number refers to the ordinal (left-to-right) position of the
output column. This feature makes it possible to define an ordering on the
basis of a column that does not have a unique name. This is never absolutely
necessary because it is always possible to assign a name to an output column
using the `AS` clause.

It is also possible to use arbitrary expressions in the `ORDER BY` clause,
including columns that do not appear in the `SELECT` output list. Thus the
following statement is valid:

    
    
    SELECT name FROM distributors ORDER BY code;
    

A limitation of this feature is that an `ORDER BY` clause applying to the
result of a `UNION`, `INTERSECT`, or `EXCEPT` clause can only specify an
output column name or number, not an expression.

If an `ORDER BY` expression is a simple name that matches both an output
column name and an input column name, `ORDER BY` will interpret it as the
output column name. This is the opposite of the choice that `GROUP BY` will
make in the same situation. This inconsistency is made to be compatible with
the SQL standard.

Optionally one can add the key word `ASC` (ascending) or `DESC` (descending)
after any expression in the `ORDER BY` clause. If not specified, `ASC` is
assumed by default. Alternatively, a specific ordering operator name can be
specified in the `USING` clause. An ordering operator must be a less-than or
greater-than member of some B-tree operator family. `ASC` is usually
equivalent to `USING <` and `DESC` is usually equivalent to `USING >`. (But
the creator of a user-defined data type can define exactly what the default
sort ordering is, and it might correspond to operators with other names.)

If `NULLS LAST` is specified, null values sort after all non-null values; if
`NULLS FIRST` is specified, null values sort before all non-null values. If
neither is specified, the default behavior is `NULLS LAST` when `ASC` is
specified or implied, and `NULLS FIRST` when `DESC` is specified (thus, the
default is to act as though nulls are larger than non-nulls). When `USING` is
specified, the default nulls ordering depends on whether the operator is a
less-than or greater-than operator.

Note that ordering options apply only to the expression they follow; for
example `ORDER BY x, y DESC` does not mean the same thing as `ORDER BY x DESC,
y DESC`.

Character-string data is sorted according to the collation that applies to the
column being sorted. That can be overridden at need by including a `COLLATE`
clause in the _`expression`_ , for example `ORDER BY mycolumn COLLATE
"en_US"`. For more information see [Section 4.2.10](sql-expressions.html#SQL-
SYNTAX-COLLATE-EXPRS "4.2.10. Collation Expressions") and [Section
24.2](collation.html "24.2. Collation Support").

### `LIMIT` Clause

The `LIMIT` clause consists of two independent sub-clauses:

    
    
    LIMIT { _count_ | ALL }
    OFFSET _start_
    

The parameter _`count`_ specifies the maximum number of rows to return, while
_`start`_ specifies the number of rows to skip before starting to return rows.
When both are specified, _`start`_ rows are skipped before starting to count
the _`count`_ rows to be returned.

If the _`count`_ expression evaluates to NULL, it is treated as `LIMIT ALL`,
i.e., no limit. If _`start`_ evaluates to NULL, it is treated the same as
`OFFSET 0`.

SQL:2008 introduced a different syntax to achieve the same result, which
PostgreSQL also supports. It is:

    
    
    OFFSET _start_ { ROW | ROWS }
    FETCH { FIRST | NEXT } [ _count_ ] { ROW | ROWS } { ONLY | WITH TIES }
    

In this syntax, the _`start`_ or _`count`_ value is required by the standard
to be a literal constant, a parameter, or a variable name; as a PostgreSQL
extension, other expressions are allowed, but will generally need to be
enclosed in parentheses to avoid ambiguity. If _`count`_ is omitted in a
`FETCH` clause, it defaults to 1. The `WITH TIES` option is used to return any
additional rows that tie for the last place in the result set according to the
`ORDER BY` clause; `ORDER BY` is mandatory in this case, and `SKIP LOCKED` is
not allowed. `ROW` and `ROWS` as well as `FIRST` and `NEXT` are noise words
that don't influence the effects of these clauses. According to the standard,
the `OFFSET` clause must come before the `FETCH` clause if both are present;
but PostgreSQL is laxer and allows either order.

When using `LIMIT`, it is a good idea to use an `ORDER BY` clause that
constrains the result rows into a unique order. Otherwise you will get an
unpredictable subset of the query's rows — you might be asking for the tenth
through twentieth rows, but tenth through twentieth in what ordering? You
don't know what ordering unless you specify `ORDER BY`.

The query planner takes `LIMIT` into account when generating a query plan, so
you are very likely to get different plans (yielding different row orders)
depending on what you use for `LIMIT` and `OFFSET`. Thus, using different
`LIMIT`/`OFFSET` values to select different subsets of a query result _will
give inconsistent results_ unless you enforce a predictable result ordering
with `ORDER BY`. This is not a bug; it is an inherent consequence of the fact
that SQL does not promise to deliver the results of a query in any particular
order unless `ORDER BY` is used to constrain the order.

It is even possible for repeated executions of the same `LIMIT` query to
return different subsets of the rows of a table, if there is not an `ORDER BY`
to enforce selection of a deterministic subset. Again, this is not a bug;
determinism of the results is simply not guaranteed in such a case.

### The Locking Clause

`FOR UPDATE`, `FOR NO KEY UPDATE`, `FOR SHARE` and `FOR KEY SHARE` are
_locking clauses_ ; they affect how `SELECT` locks rows as they are obtained
from the table.

The locking clause has the general form

    
    
    FOR _lock_strength_ [ OF _table_name_ [, ...] ] [ NOWAIT | SKIP LOCKED ]
    

where _`lock_strength`_ can be one of

    
    
    UPDATE
    NO KEY UPDATE
    SHARE
    KEY SHARE
    

For more information on each row-level lock mode, refer to [Section
13.3.2](explicit-locking.html#LOCKING-ROWS "13.3.2. Row-Level Locks").

To prevent the operation from waiting for other transactions to commit, use
either the `NOWAIT` or `SKIP LOCKED` option. With `NOWAIT`, the statement
reports an error, rather than waiting, if a selected row cannot be locked
immediately. With `SKIP LOCKED`, any selected rows that cannot be immediately
locked are skipped. Skipping locked rows provides an inconsistent view of the
data, so this is not suitable for general purpose work, but can be used to
avoid lock contention with multiple consumers accessing a queue-like table.
Note that `NOWAIT` and `SKIP LOCKED` apply only to the row-level lock(s) — the
required `ROW SHARE` table-level lock is still taken in the ordinary way (see
[Chapter 13](mvcc.html "Chapter 13. Concurrency Control")). You can use
[`LOCK`](sql-lock.html "LOCK") with the `NOWAIT` option first, if you need to
acquire the table-level lock without waiting.

If specific tables are named in a locking clause, then only rows coming from
those tables are locked; any other tables used in the `SELECT` are simply read
as usual. A locking clause without a table list affects all tables used in the
statement. If a locking clause is applied to a view or sub-query, it affects
all tables used in the view or sub-query. However, these clauses do not apply
to `WITH` queries referenced by the primary query. If you want row locking to
occur within a `WITH` query, specify a locking clause within the `WITH` query.

Multiple locking clauses can be written if it is necessary to specify
different locking behavior for different tables. If the same table is
mentioned (or implicitly affected) by more than one locking clause, then it is
processed as if it was only specified by the strongest one. Similarly, a table
is processed as `NOWAIT` if that is specified in any of the clauses affecting
it. Otherwise, it is processed as `SKIP LOCKED` if that is specified in any of
the clauses affecting it.

The locking clauses cannot be used in contexts where returned rows cannot be
clearly identified with individual table rows; for example they cannot be used
with aggregation.

When a locking clause appears at the top level of a `SELECT` query, the rows
that are locked are exactly those that are returned by the query; in the case
of a join query, the rows locked are those that contribute to returned join
rows. In addition, rows that satisfied the query conditions as of the query
snapshot will be locked, although they will not be returned if they were
updated after the snapshot and no longer satisfy the query conditions. If a
`LIMIT` is used, locking stops once enough rows have been returned to satisfy
the limit (but note that rows skipped over by `OFFSET` will get locked).
Similarly, if a locking clause is used in a cursor's query, only rows actually
fetched or stepped past by the cursor will be locked.

When a locking clause appears in a sub-`SELECT`, the rows locked are those
returned to the outer query by the sub-query. This might involve fewer rows
than inspection of the sub-query alone would suggest, since conditions from
the outer query might be used to optimize execution of the sub-query. For
example,

    
    
    SELECT * FROM (SELECT * FROM mytable FOR UPDATE) ss WHERE col1 = 5;
    

will lock only rows having `col1 = 5`, even though that condition is not
textually within the sub-query.

Previous releases failed to preserve a lock which is upgraded by a later
savepoint. For example, this code:

    
    
    BEGIN;
    SELECT * FROM mytable WHERE key = 1 FOR UPDATE;
    SAVEPOINT s;
    UPDATE mytable SET ... WHERE key = 1;
    ROLLBACK TO s;
    

would fail to preserve the `FOR UPDATE` lock after the `ROLLBACK TO`. This has
been fixed in release 9.3.

### Caution

It is possible for a `SELECT` command running at the `READ COMMITTED`
transaction isolation level and using `ORDER BY` and a locking clause to
return rows out of order. This is because `ORDER BY` is applied first. The
command sorts the result, but might then block trying to obtain a lock on one
or more of the rows. Once the `SELECT` unblocks, some of the ordering column
values might have been modified, leading to those rows appearing to be out of
order (though they are in order in terms of the original column values). This
can be worked around at need by placing the `FOR UPDATE/SHARE` clause in a
sub-query, for example

    
    
    SELECT * FROM (SELECT * FROM mytable FOR UPDATE) ss ORDER BY column1;
    

Note that this will result in locking all rows of `mytable`, whereas `FOR
UPDATE` at the top level would lock only the actually returned rows. This can
make for a significant performance difference, particularly if the `ORDER BY`
is combined with `LIMIT` or other restrictions. So this technique is
recommended only if concurrent updates of the ordering columns are expected
and a strictly sorted result is required.

At the `REPEATABLE READ` or `SERIALIZABLE` transaction isolation level this
would cause a serialization failure (with an `SQLSTATE` of `'40001'`), so
there is no possibility of receiving rows out of order under these isolation
levels.

### `TABLE` Command

The command

    
    
    TABLE _name_
    

is equivalent to

    
    
    SELECT * FROM _name_
    

It can be used as a top-level command or as a space-saving syntax variant in
parts of complex queries. Only the `WITH`, `UNION`, `INTERSECT`, `EXCEPT`,
`ORDER BY`, `LIMIT`, `OFFSET`, `FETCH` and `FOR` locking clauses can be used
with `TABLE`; the `WHERE` clause and any form of aggregation cannot be used.

## Examples

To join the table `films` with the table `distributors`:

    
    
    SELECT f.title, f.did, d.name, f.date_prod, f.kind
        FROM distributors d JOIN films f USING (did);
    
           title       | did |     name     | date_prod  |   kind
    -------------------+-----+--------------+------------+----------
     The Third Man     | 101 | British Lion | 1949-12-23 | Drama
     The African Queen | 101 | British Lion | 1951-08-11 | Romantic
     ...
    

To sum the column `len` of all films and group the results by `kind`:

    
    
    SELECT kind, sum(len) AS total FROM films GROUP BY kind;
    
       kind   | total
    ----------+-------
     Action   | 07:34
     Comedy   | 02:58
     Drama    | 14:28
     Musical  | 06:42
     Romantic | 04:38
    

To sum the column `len` of all films, group the results by `kind` and show
those group totals that are less than 5 hours:

    
    
    SELECT kind, sum(len) AS total
        FROM films
        GROUP BY kind
        HAVING sum(len) < interval '5 hours';
    
       kind   | total
    ----------+-------
     Comedy   | 02:58
     Romantic | 04:38
    

The following two examples are identical ways of sorting the individual
results according to the contents of the second column (`name`):

    
    
    SELECT * FROM distributors ORDER BY name;
    SELECT * FROM distributors ORDER BY 2;
    
     did |       name
    -----+------------------
     109 | 20th Century Fox
     110 | Bavaria Atelier
     101 | British Lion
     107 | Columbia
     102 | Jean Luc Godard
     113 | Luso films
     104 | Mosfilm
     103 | Paramount
     106 | Toho
     105 | United Artists
     111 | Walt Disney
     112 | Warner Bros.
     108 | Westward
    

The next example shows how to obtain the union of the tables `distributors`
and `actors`, restricting the results to those that begin with the letter W in
each table. Only distinct rows are wanted, so the key word `ALL` is omitted.

    
    
    distributors:               actors:
     did |     name              id |     name
    -----+--------------        ----+----------------
     108 | Westward               1 | Woody Allen
     111 | Walt Disney            2 | Warren Beatty
     112 | Warner Bros.           3 | Walter Matthau
     ...                         ...
    
    SELECT distributors.name
        FROM distributors
        WHERE distributors.name LIKE 'W%'
    UNION
    SELECT actors.name
        FROM actors
        WHERE actors.name LIKE 'W%';
    
          name
    ----------------
     Walt Disney
     Walter Matthau
     Warner Bros.
     Warren Beatty
     Westward
     Woody Allen
    

This example shows how to use a function in the `FROM` clause, both with and
without a column definition list:

    
    
    CREATE FUNCTION distributors(int) RETURNS SETOF distributors AS $$
        SELECT * FROM distributors WHERE did = $1;
    $$ LANGUAGE SQL;
    
    SELECT * FROM distributors(111);
     did |    name
    -----+-------------
     111 | Walt Disney
    
    CREATE FUNCTION distributors_2(int) RETURNS SETOF record AS $$
        SELECT * FROM distributors WHERE did = $1;
    $$ LANGUAGE SQL;
    
    SELECT * FROM distributors_2(111) AS (f1 int, f2 text);
     f1  |     f2
    -----+-------------
     111 | Walt Disney
    

Here is an example of a function with an ordinality column added:

    
    
    SELECT * FROM unnest(ARRAY['a','b','c','d','e','f']) WITH ORDINALITY;
     unnest | ordinality
    --------+----------
     a      |        1
     b      |        2
     c      |        3
     d      |        4
     e      |        5
     f      |        6
    (6 rows)
    

This example shows how to use a simple `WITH` clause:

    
    
    WITH t AS (
        SELECT random() as x FROM generate_series(1, 3)
      )
    SELECT * FROM t
    UNION ALL
    SELECT * FROM t;
             x
    --------------------
      0.534150459803641
      0.520092216785997
     0.0735620250925422
      0.534150459803641
      0.520092216785997
     0.0735620250925422
    

Notice that the `WITH` query was evaluated only once, so that we got two sets
of the same three random values.

This example uses `WITH RECURSIVE` to find all subordinates (direct or
indirect) of the employee Mary, and their level of indirectness, from a table
that shows only direct subordinates:

    
    
    WITH RECURSIVE employee_recursive(distance, employee_name, manager_name) AS (
        SELECT 1, employee_name, manager_name
        FROM employee
        WHERE manager_name = 'Mary'
      UNION ALL
        SELECT er.distance + 1, e.employee_name, e.manager_name
        FROM employee_recursive er, employee e
        WHERE er.employee_name = e.manager_name
      )
    SELECT distance, employee_name FROM employee_recursive;
    

Notice the typical form of recursive queries: an initial condition, followed
by `UNION`, followed by the recursive part of the query. Be sure that the
recursive part of the query will eventually return no tuples, or else the
query will loop indefinitely. (See [Section 7.8](queries-with.html "7.8. WITH
Queries \(Common Table Expressions\)") for more examples.)

This example uses `LATERAL` to apply a set-returning function
`get_product_names()` for each row of the `manufacturers` table:

    
    
    SELECT m.name AS mname, pname
    FROM manufacturers m, LATERAL get_product_names(m.id) pname;
    

Manufacturers not currently having any products would not appear in the
result, since it is an inner join. If we wished to include the names of such
manufacturers in the result, we could do:

    
    
    SELECT m.name AS mname, pname
    FROM manufacturers m LEFT JOIN LATERAL get_product_names(m.id) pname ON true;
    

## Compatibility

Of course, the `SELECT` statement is compatible with the SQL standard. But
there are some extensions and some missing features.

### Omitted `FROM` Clauses

PostgreSQL allows one to omit the `FROM` clause. It has a straightforward use
to compute the results of simple expressions:

    
    
    SELECT 2+2;
    
     ?column?
    ----------
            4
    

Some other SQL databases cannot do this except by introducing a dummy one-row
table from which to do the `SELECT`.

### Empty `SELECT` Lists

The list of output expressions after `SELECT` can be empty, producing a zero-
column result table. This is not valid syntax according to the SQL standard.
PostgreSQL allows it to be consistent with allowing zero-column tables.
However, an empty list is not allowed when `DISTINCT` is used.

### Omitting the `AS` Key Word

In the SQL standard, the optional key word `AS` can be omitted before an
output column name whenever the new column name is a valid column name (that
is, not the same as any reserved keyword). PostgreSQL is slightly more
restrictive: `AS` is required if the new column name matches any keyword at
all, reserved or not. Recommended practice is to use `AS` or double-quote
output column names, to prevent any possible conflict against future keyword
additions.

In `FROM` items, both the standard and PostgreSQL allow `AS` to be omitted
before an alias that is an unreserved keyword. But this is impractical for
output column names, because of syntactic ambiguities.

### Omitting Sub-`SELECT` Aliases in `FROM`

According to the SQL standard, a sub-`SELECT` in the `FROM` list must have an
alias. In PostgreSQL, this alias may be omitted.

### `ONLY` and Inheritance

The SQL standard requires parentheses around the table name when writing
`ONLY`, for example `SELECT * FROM ONLY (tab1), ONLY (tab2) WHERE ...`.
PostgreSQL considers these parentheses to be optional.

PostgreSQL allows a trailing `*` to be written to explicitly specify the
non-`ONLY` behavior of including child tables. The standard does not allow
this.

(These points apply equally to all SQL commands supporting the `ONLY` option.)

### `TABLESAMPLE` Clause Restrictions

The `TABLESAMPLE` clause is currently accepted only on regular tables and
materialized views. According to the SQL standard it should be possible to
apply it to any `FROM` item.

### Function Calls in `FROM`

PostgreSQL allows a function call to be written directly as a member of the
`FROM` list. In the SQL standard it would be necessary to wrap such a function
call in a sub-`SELECT`; that is, the syntax `FROM _`func`_(...) _`alias`_` is
approximately equivalent to `FROM LATERAL (SELECT _`func`_(...)) _`alias`_`.
Note that `LATERAL` is considered to be implicit; this is because the standard
requires `LATERAL` semantics for an `UNNEST()` item in `FROM`. PostgreSQL
treats `UNNEST()` the same as other set-returning functions.

### Namespace Available to `GROUP BY` and `ORDER BY`

In the SQL-92 standard, an `ORDER BY` clause can only use output column names
or numbers, while a `GROUP BY` clause can only use expressions based on input
column names. PostgreSQL extends each of these clauses to allow the other
choice as well (but it uses the standard's interpretation if there is
ambiguity). PostgreSQL also allows both clauses to specify arbitrary
expressions. Note that names appearing in an expression will always be taken
as input-column names, not as output-column names.

SQL:1999 and later use a slightly different definition which is not entirely
upward compatible with SQL-92. In most cases, however, PostgreSQL will
interpret an `ORDER BY` or `GROUP BY` expression the same way SQL:1999 does.

### Functional Dependencies

PostgreSQL recognizes functional dependency (allowing columns to be omitted
from `GROUP BY`) only when a table's primary key is included in the `GROUP BY`
list. The SQL standard specifies additional conditions that should be
recognized.

### `LIMIT` and `OFFSET`

The clauses `LIMIT` and `OFFSET` are PostgreSQL-specific syntax, also used by
MySQL. The SQL:2008 standard has introduced the clauses `OFFSET ... FETCH
{FIRST|NEXT} ...` for the same functionality, as shown above in [LIMIT
Clause](sql-select.html#SQL-LIMIT "LIMIT Clause"). This syntax is also used by
IBM DB2. (Applications written for Oracle frequently use a workaround
involving the automatically generated `rownum` column, which is not available
in PostgreSQL, to implement the effects of these clauses.)

### `FOR NO KEY UPDATE`, `FOR UPDATE`, `FOR SHARE`, `FOR KEY SHARE`

Although `FOR UPDATE` appears in the SQL standard, the standard allows it only
as an option of `DECLARE CURSOR`. PostgreSQL allows it in any `SELECT` query
as well as in sub-`SELECT`s, but this is an extension. The `FOR NO KEY
UPDATE`, `FOR SHARE` and `FOR KEY SHARE` variants, as well as the `NOWAIT` and
`SKIP LOCKED` options, do not appear in the standard.

### Data-Modifying Statements in `WITH`

PostgreSQL allows `INSERT`, `UPDATE`, and `DELETE` to be used as `WITH`
queries. This is not found in the SQL standard.

### Nonstandard Clauses

`DISTINCT ON ( ... )` is an extension of the SQL standard.

`ROWS FROM( ... )` is an extension of the SQL standard.

The `MATERIALIZED` and `NOT MATERIALIZED` options of `WITH` are extensions of
the SQL standard.

* * *

[Prev](sql-security-label.html "SECURITY LABEL")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-selectinto.html "SELECT INTO")  
---|---|---  
SECURITY LABEL  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SELECT INTO  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-select.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

