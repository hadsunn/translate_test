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

Supported Versions: [Current](/docs/current/querytree.html "PostgreSQL 17 -
41.1. The Query Tree") ([17](/docs/17/querytree.html "PostgreSQL 17 -
41.1. The Query Tree")) / [16](/docs/16/querytree.html "PostgreSQL 16 -
41.1. The Query Tree") / [15](/docs/15/querytree.html "PostgreSQL 15 -
41.1. The Query Tree") / [14](/docs/14/querytree.html "PostgreSQL 14 -
41.1. The Query Tree") / [13](/docs/13/querytree.html "PostgreSQL 13 -
41.1. The Query Tree")

Development Versions: [18](/docs/18/querytree.html "PostgreSQL 18 - 41.1. The
Query Tree") / [devel](/docs/devel/querytree.html "PostgreSQL devel -
41.1. The Query Tree")

Unsupported versions: [12](/docs/12/querytree.html "PostgreSQL 12 - 41.1. The
Query Tree") / [11](/docs/11/querytree.html "PostgreSQL 11 - 41.1. The Query
Tree") / [10](/docs/10/querytree.html "PostgreSQL 10 - 41.1. The Query Tree")
/ [9.6](/docs/9.6/querytree.html "PostgreSQL 9.6 - 41.1. The Query Tree") /
[9.5](/docs/9.5/querytree.html "PostgreSQL 9.5 - 41.1. The Query Tree") /
[9.4](/docs/9.4/querytree.html "PostgreSQL 9.4 - 41.1. The Query Tree") /
[9.3](/docs/9.3/querytree.html "PostgreSQL 9.3 - 41.1. The Query Tree") /
[9.2](/docs/9.2/querytree.html "PostgreSQL 9.2 - 41.1. The Query Tree") /
[9.1](/docs/9.1/querytree.html "PostgreSQL 9.1 - 41.1. The Query Tree") /
[9.0](/docs/9.0/querytree.html "PostgreSQL 9.0 - 41.1. The Query Tree") /
[8.4](/docs/8.4/querytree.html "PostgreSQL 8.4 - 41.1. The Query Tree") /
[8.3](/docs/8.3/querytree.html "PostgreSQL 8.3 - 41.1. The Query Tree") /
[8.2](/docs/8.2/querytree.html "PostgreSQL 8.2 - 41.1. The Query Tree") /
[7.3](/docs/7.3/querytree.html "PostgreSQL 7.3 - 41.1. The Query Tree") /
[7.2](/docs/7.2/querytree.html "PostgreSQL 7.2 - 41.1. The Query Tree")

__

41.1. The Query Tree  
---  
[Prev](rules.html "Chapter 41. The Rule System")  | [Up](rules.html "Chapter 41. The Rule System") | Chapter 41. The Rule System | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](rules-views.html "41.2. Views and the Rule System")  
  
* * *

## 41.1. The Query Tree #

To understand how the rule system works it is necessary to know when it is
invoked and what its input and results are.

The rule system is located between the parser and the planner. It takes the
output of the parser, one query tree, and the user-defined rewrite rules,
which are also query trees with some extra information, and creates zero or
more query trees as result. So its input and output are always things the
parser itself could have produced and thus, anything it sees is basically
representable as an SQL statement.

Now what is a query tree? It is an internal representation of an SQL statement
where the single parts that it is built from are stored separately. These
query trees can be shown in the server log if you set the configuration
parameters `debug_print_parse`, `debug_print_rewritten`, or
`debug_print_plan`. The rule actions are also stored as query trees, in the
system catalog `pg_rewrite`. They are not formatted like the log output, but
they contain exactly the same information.

Reading a raw query tree requires some experience. But since SQL
representations of query trees are sufficient to understand the rule system,
this chapter will not teach how to read them.

When reading the SQL representations of the query trees in this chapter it is
necessary to be able to identify the parts the statement is broken into when
it is in the query tree structure. The parts of a query tree are

the command type

    

This is a simple value telling which command (`SELECT`, `INSERT`, `UPDATE`,
`DELETE`) produced the query tree.

the range table

    

The range table is a list of relations that are used in the query. In a
`SELECT` statement these are the relations given after the `FROM` key word.

Every range table entry identifies a table or view and tells by which name it
is called in the other parts of the query. In the query tree, the range table
entries are referenced by number rather than by name, so here it doesn't
matter if there are duplicate names as it would in an SQL statement. This can
happen after the range tables of rules have been merged in. The examples in
this chapter will not have this situation.

the result relation

    

This is an index into the range table that identifies the relation where the
results of the query go.

`SELECT` queries don't have a result relation. (The special case of `SELECT
INTO` is mostly identical to `CREATE TABLE` followed by `INSERT ... SELECT`,
and is not discussed separately here.)

For `INSERT`, `UPDATE`, and `DELETE` commands, the result relation is the
table (or view!) where the changes are to take effect.

the target list

    

The target list is a list of expressions that define the result of the query.
In the case of a `SELECT`, these expressions are the ones that build the final
output of the query. They correspond to the expressions between the key words
`SELECT` and `FROM`. (`*` is just an abbreviation for all the column names of
a relation. It is expanded by the parser into the individual columns, so the
rule system never sees it.)

`DELETE` commands don't need a normal target list because they don't produce
any result. Instead, the planner adds a special CTID entry to the empty target
list, to allow the executor to find the row to be deleted. (CTID is added when
the result relation is an ordinary table. If it is a view, a whole-row
variable is added instead, by the rule system, as described in [Section
41.2.4](rules-views.html#RULES-VIEWS-UPDATE "41.2.4. Updating a View").)

For `INSERT` commands, the target list describes the new rows that should go
into the result relation. It consists of the expressions in the `VALUES`
clause or the ones from the `SELECT` clause in `INSERT ... SELECT`. The first
step of the rewrite process adds target list entries for any columns that were
not assigned to by the original command but have defaults. Any remaining
columns (with neither a given value nor a default) will be filled in by the
planner with a constant null expression.

For `UPDATE` commands, the target list describes the new rows that should
replace the old ones. In the rule system, it contains just the expressions
from the `SET column = expression` part of the command. The planner will
handle missing columns by inserting expressions that copy the values from the
old row into the new one. Just as for `DELETE`, a CTID or whole-row variable
is added so that the executor can identify the old row to be updated.

Every entry in the target list contains an expression that can be a constant
value, a variable pointing to a column of one of the relations in the range
table, a parameter, or an expression tree made of function calls, constants,
variables, operators, etc.

the qualification

    

The query's qualification is an expression much like one of those contained in
the target list entries. The result value of this expression is a Boolean that
tells whether the operation (`INSERT`, `UPDATE`, `DELETE`, or `SELECT`) for
the final result row should be executed or not. It corresponds to the `WHERE`
clause of an SQL statement.

the join tree

    

The query's join tree shows the structure of the `FROM` clause. For a simple
query like `SELECT ... FROM a, b, c`, the join tree is just a list of the
`FROM` items, because we are allowed to join them in any order. But when
`JOIN` expressions, particularly outer joins, are used, we have to join in the
order shown by the joins. In that case, the join tree shows the structure of
the `JOIN` expressions. The restrictions associated with particular `JOIN`
clauses (from `ON` or `USING` expressions) are stored as qualification
expressions attached to those join-tree nodes. It turns out to be convenient
to store the top-level `WHERE` expression as a qualification attached to the
top-level join-tree item, too. So really the join tree represents both the
`FROM` and `WHERE` clauses of a `SELECT`.

the others

    

The other parts of the query tree like the `ORDER BY` clause aren't of
interest here. The rule system substitutes some entries there while applying
rules, but that doesn't have much to do with the fundamentals of the rule
system.

* * *

[Prev](rules.html "Chapter 41. The Rule System")  | [Up](rules.html "Chapter 41. The Rule System") |  [Next](rules-views.html "41.2. Views and the Rule System")  
---|---|---  
Chapter 41. The Rule System  | [Home](index.html "PostgreSQL 16.9 Documentation") |  41.2. Views and the Rule System  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/querytree.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

