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

Supported Versions: [Current](/docs/current/sql-prepare.html "PostgreSQL 17 -
PREPARE") ([17](/docs/17/sql-prepare.html "PostgreSQL 17 - PREPARE")) /
[16](/docs/16/sql-prepare.html "PostgreSQL 16 - PREPARE") / [15](/docs/15/sql-
prepare.html "PostgreSQL 15 - PREPARE") / [14](/docs/14/sql-prepare.html
"PostgreSQL 14 - PREPARE") / [13](/docs/13/sql-prepare.html "PostgreSQL 13 -
PREPARE")

Development Versions: [18](/docs/18/sql-prepare.html "PostgreSQL 18 -
PREPARE") / [devel](/docs/devel/sql-prepare.html "PostgreSQL devel - PREPARE")

Unsupported versions: [12](/docs/12/sql-prepare.html "PostgreSQL 12 -
PREPARE") / [11](/docs/11/sql-prepare.html "PostgreSQL 11 - PREPARE") /
[10](/docs/10/sql-prepare.html "PostgreSQL 10 - PREPARE") /
[9.6](/docs/9.6/sql-prepare.html "PostgreSQL 9.6 - PREPARE") /
[9.5](/docs/9.5/sql-prepare.html "PostgreSQL 9.5 - PREPARE") /
[9.4](/docs/9.4/sql-prepare.html "PostgreSQL 9.4 - PREPARE") /
[9.3](/docs/9.3/sql-prepare.html "PostgreSQL 9.3 - PREPARE") /
[9.2](/docs/9.2/sql-prepare.html "PostgreSQL 9.2 - PREPARE") /
[9.1](/docs/9.1/sql-prepare.html "PostgreSQL 9.1 - PREPARE") /
[9.0](/docs/9.0/sql-prepare.html "PostgreSQL 9.0 - PREPARE") /
[8.4](/docs/8.4/sql-prepare.html "PostgreSQL 8.4 - PREPARE") /
[8.3](/docs/8.3/sql-prepare.html "PostgreSQL 8.3 - PREPARE") /
[8.2](/docs/8.2/sql-prepare.html "PostgreSQL 8.2 - PREPARE") /
[8.1](/docs/8.1/sql-prepare.html "PostgreSQL 8.1 - PREPARE") /
[8.0](/docs/8.0/sql-prepare.html "PostgreSQL 8.0 - PREPARE") /
[7.4](/docs/7.4/sql-prepare.html "PostgreSQL 7.4 - PREPARE") /
[7.3](/docs/7.3/sql-prepare.html "PostgreSQL 7.3 - PREPARE")

__

PREPARE  
---  
[Prev](sql-notify.html "NOTIFY")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-prepare-transaction.html "PREPARE TRANSACTION")  
  
* * *

## PREPARE

PREPARE — prepare a statement for execution

## Synopsis

    
    
    PREPARE _name_ [ ( _data_type_ [, ...] ) ] AS _statement_
    

## Description

`PREPARE` creates a prepared statement. A prepared statement is a server-side
object that can be used to optimize performance. When the `PREPARE` statement
is executed, the specified statement is parsed, analyzed, and rewritten. When
an `EXECUTE` command is subsequently issued, the prepared statement is planned
and executed. This division of labor avoids repetitive parse analysis work,
while allowing the execution plan to depend on the specific parameter values
supplied.

Prepared statements can take parameters: values that are substituted into the
statement when it is executed. When creating the prepared statement, refer to
parameters by position, using `$1`, `$2`, etc. A corresponding list of
parameter data types can optionally be specified. When a parameter's data type
is not specified or is declared as `unknown`, the type is inferred from the
context in which the parameter is first referenced (if possible). When
executing the statement, specify the actual values for these parameters in the
`EXECUTE` statement. Refer to [EXECUTE](sql-execute.html "EXECUTE") for more
information about that.

Prepared statements only last for the duration of the current database
session. When the session ends, the prepared statement is forgotten, so it
must be recreated before being used again. This also means that a single
prepared statement cannot be used by multiple simultaneous database clients;
however, each client can create their own prepared statement to use. Prepared
statements can be manually cleaned up using the [`DEALLOCATE`](sql-
deallocate.html "DEALLOCATE") command.

Prepared statements potentially have the largest performance advantage when a
single session is being used to execute a large number of similar statements.
The performance difference will be particularly significant if the statements
are complex to plan or rewrite, e.g., if the query involves a join of many
tables or requires the application of several rules. If the statement is
relatively simple to plan and rewrite but relatively expensive to execute, the
performance advantage of prepared statements will be less noticeable.

## Parameters

_`name`_

    

An arbitrary name given to this particular prepared statement. It must be
unique within a single session and is subsequently used to execute or
deallocate a previously prepared statement.

_`data_type`_

    

The data type of a parameter to the prepared statement. If the data type of a
particular parameter is unspecified or is specified as `unknown`, it will be
inferred from the context in which the parameter is first referenced. To refer
to the parameters in the prepared statement itself, use `$1`, `$2`, etc.

_`statement`_

    

Any `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `MERGE`, or `VALUES` statement.

## Notes

A prepared statement can be executed with either a _generic plan_ or a _custom
plan_. A generic plan is the same across all executions, while a custom plan
is generated for a specific execution using the parameter values given in that
call. Use of a generic plan avoids planning overhead, but in some situations a
custom plan will be much more efficient to execute because the planner can
make use of knowledge of the parameter values. (Of course, if the prepared
statement has no parameters, then this is moot and a generic plan is always
used.)

By default (that is, when [plan_cache_mode](runtime-config-query.html#GUC-
PLAN-CACHE-MODE) is set to `auto`), the server will automatically choose
whether to use a generic or custom plan for a prepared statement that has
parameters. The current rule for this is that the first five executions are
done with custom plans and the average estimated cost of those plans is
calculated. Then a generic plan is created and its estimated cost is compared
to the average custom-plan cost. Subsequent executions use the generic plan if
its cost is not so much higher than the average custom-plan cost as to make
repeated replanning seem preferable.

This heuristic can be overridden, forcing the server to use either generic or
custom plans, by setting `plan_cache_mode` to `force_generic_plan` or
`force_custom_plan` respectively. This setting is primarily useful if the
generic plan's cost estimate is badly off for some reason, allowing it to be
chosen even though its actual cost is much more than that of a custom plan.

To examine the query plan PostgreSQL is using for a prepared statement, use
[`EXPLAIN`](sql-explain.html "EXPLAIN"), for example

    
    
    EXPLAIN EXECUTE _name_(_parameter_values_);
    

If a generic plan is in use, it will contain parameter symbols `$_`n`_`, while
a custom plan will have the supplied parameter values substituted into it.

For more information on query planning and the statistics collected by
PostgreSQL for that purpose, see the [ANALYZE](sql-analyze.html "ANALYZE")
documentation.

Although the main point of a prepared statement is to avoid repeated parse
analysis and planning of the statement, PostgreSQL will force re-analysis and
re-planning of the statement before using it whenever database objects used in
the statement have undergone definitional (DDL) changes or their planner
statistics have been updated since the previous use of the prepared statement.
Also, if the value of [search_path](runtime-config-client.html#GUC-SEARCH-
PATH) changes from one use to the next, the statement will be re-parsed using
the new `search_path`. (This latter behavior is new as of PostgreSQL 9.3.)
These rules make use of a prepared statement semantically almost equivalent to
re-submitting the same query text over and over, but with a performance
benefit if no object definitions are changed, especially if the best plan
remains the same across uses. An example of a case where the semantic
equivalence is not perfect is that if the statement refers to a table by an
unqualified name, and then a new table of the same name is created in a schema
appearing earlier in the `search_path`, no automatic re-parse will occur since
no object used in the statement changed. However, if some other change forces
a re-parse, the new table will be referenced in subsequent uses.

You can see all prepared statements available in the session by querying the
[`pg_prepared_statements`](view-pg-prepared-statements.html
"54.15. pg_prepared_statements") system view.

## Examples

Create a prepared statement for an `INSERT` statement, and then execute it:

    
    
    PREPARE fooplan (int, text, bool, numeric) AS
        INSERT INTO foo VALUES($1, $2, $3, $4);
    EXECUTE fooplan(1, 'Hunter Valley', 't', 200.00);
    

Create a prepared statement for a `SELECT` statement, and then execute it:

    
    
    PREPARE usrrptplan (int) AS
        SELECT * FROM users u, logs l WHERE u.usrid=$1 AND u.usrid=l.usrid
        AND l.date = $2;
    EXECUTE usrrptplan(1, current_date);
    

In this example, the data type of the second parameter is not specified, so it
is inferred from the context in which `$2` is used.

## Compatibility

The SQL standard includes a `PREPARE` statement, but it is only for use in
embedded SQL. This version of the `PREPARE` statement also uses a somewhat
different syntax.

## See Also

[DEALLOCATE](sql-deallocate.html "DEALLOCATE"), [EXECUTE](sql-execute.html
"EXECUTE")

* * *

[Prev](sql-notify.html "NOTIFY")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-prepare-transaction.html "PREPARE TRANSACTION")  
---|---|---  
NOTIFY  | [Home](index.html "PostgreSQL 16.9 Documentation") |  PREPARE TRANSACTION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-prepare.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

