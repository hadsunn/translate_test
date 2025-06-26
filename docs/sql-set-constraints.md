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

Supported Versions: [Current](/docs/current/sql-set-constraints.html
"PostgreSQL 17 - SET CONSTRAINTS") ([17](/docs/17/sql-set-constraints.html
"PostgreSQL 17 - SET CONSTRAINTS")) / [16](/docs/16/sql-set-constraints.html
"PostgreSQL 16 - SET CONSTRAINTS") / [15](/docs/15/sql-set-constraints.html
"PostgreSQL 15 - SET CONSTRAINTS") / [14](/docs/14/sql-set-constraints.html
"PostgreSQL 14 - SET CONSTRAINTS") / [13](/docs/13/sql-set-constraints.html
"PostgreSQL 13 - SET CONSTRAINTS")

Development Versions: [18](/docs/18/sql-set-constraints.html "PostgreSQL 18 -
SET CONSTRAINTS") / [devel](/docs/devel/sql-set-constraints.html "PostgreSQL
devel - SET CONSTRAINTS")

Unsupported versions: [12](/docs/12/sql-set-constraints.html "PostgreSQL 12 -
SET CONSTRAINTS") / [11](/docs/11/sql-set-constraints.html "PostgreSQL 11 -
SET CONSTRAINTS") / [10](/docs/10/sql-set-constraints.html "PostgreSQL 10 -
SET CONSTRAINTS") / [9.6](/docs/9.6/sql-set-constraints.html "PostgreSQL 9.6 -
SET CONSTRAINTS") / [9.5](/docs/9.5/sql-set-constraints.html "PostgreSQL 9.5 -
SET CONSTRAINTS") / [9.4](/docs/9.4/sql-set-constraints.html "PostgreSQL 9.4 -
SET CONSTRAINTS") / [9.3](/docs/9.3/sql-set-constraints.html "PostgreSQL 9.3 -
SET CONSTRAINTS") / [9.2](/docs/9.2/sql-set-constraints.html "PostgreSQL 9.2 -
SET CONSTRAINTS") / [9.1](/docs/9.1/sql-set-constraints.html "PostgreSQL 9.1 -
SET CONSTRAINTS") / [9.0](/docs/9.0/sql-set-constraints.html "PostgreSQL 9.0 -
SET CONSTRAINTS") / [8.4](/docs/8.4/sql-set-constraints.html "PostgreSQL 8.4 -
SET CONSTRAINTS") / [8.3](/docs/8.3/sql-set-constraints.html "PostgreSQL 8.3 -
SET CONSTRAINTS") / [8.2](/docs/8.2/sql-set-constraints.html "PostgreSQL 8.2 -
SET CONSTRAINTS") / [8.1](/docs/8.1/sql-set-constraints.html "PostgreSQL 8.1 -
SET CONSTRAINTS") / [8.0](/docs/8.0/sql-set-constraints.html "PostgreSQL 8.0 -
SET CONSTRAINTS") / [7.4](/docs/7.4/sql-set-constraints.html "PostgreSQL 7.4 -
SET CONSTRAINTS") / [7.3](/docs/7.3/sql-set-constraints.html "PostgreSQL 7.3 -
SET CONSTRAINTS") / [7.2](/docs/7.2/sql-set-constraints.html "PostgreSQL 7.2 -
SET CONSTRAINTS") / [7.1](/docs/7.1/sql-set-constraints.html "PostgreSQL 7.1 -
SET CONSTRAINTS")

__

SET CONSTRAINTS  
---  
[Prev](sql-set.html "SET")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-set-role.html "SET ROLE")  
  
* * *

## SET CONSTRAINTS

SET CONSTRAINTS — set constraint check timing for the current transaction

## Synopsis

    
    
    SET CONSTRAINTS { ALL | _name_ [, ...] } { DEFERRED | IMMEDIATE }
    

## Description

`SET CONSTRAINTS` sets the behavior of constraint checking within the current
transaction. `IMMEDIATE` constraints are checked at the end of each statement.
`DEFERRED` constraints are not checked until transaction commit. Each
constraint has its own `IMMEDIATE` or `DEFERRED` mode.

Upon creation, a constraint is given one of three characteristics: `DEFERRABLE
INITIALLY DEFERRED`, `DEFERRABLE INITIALLY IMMEDIATE`, or `NOT DEFERRABLE`.
The third class is always `IMMEDIATE` and is not affected by the `SET
CONSTRAINTS` command. The first two classes start every transaction in the
indicated mode, but their behavior can be changed within a transaction by `SET
CONSTRAINTS`.

`SET CONSTRAINTS` with a list of constraint names changes the mode of just
those constraints (which must all be deferrable). Each constraint name can be
schema-qualified. The current schema search path is used to find the first
matching name if no schema name is specified. `SET CONSTRAINTS ALL` changes
the mode of all deferrable constraints.

When `SET CONSTRAINTS` changes the mode of a constraint from `DEFERRED` to
`IMMEDIATE`, the new mode takes effect retroactively: any outstanding data
modifications that would have been checked at the end of the transaction are
instead checked during the execution of the `SET CONSTRAINTS` command. If any
such constraint is violated, the `SET CONSTRAINTS` fails (and does not change
the constraint mode). Thus, `SET CONSTRAINTS` can be used to force checking of
constraints to occur at a specific point in a transaction.

Currently, only `UNIQUE`, `PRIMARY KEY`, `REFERENCES` (foreign key), and
`EXCLUDE` constraints are affected by this setting. `NOT NULL` and `CHECK`
constraints are always checked immediately when a row is inserted or modified
(_not_ at the end of the statement). Uniqueness and exclusion constraints that
have not been declared `DEFERRABLE` are also checked immediately.

The firing of triggers that are declared as “constraint triggers” is also
controlled by this setting — they fire at the same time that the associated
constraint should be checked.

## Notes

Because PostgreSQL does not require constraint names to be unique within a
schema (but only per-table), it is possible that there is more than one match
for a specified constraint name. In this case `SET CONSTRAINTS` will act on
all matches. For a non-schema-qualified name, once a match or matches have
been found in some schema in the search path, schemas appearing later in the
path are not searched.

This command only alters the behavior of constraints within the current
transaction. Issuing this outside of a transaction block emits a warning and
otherwise has no effect.

## Compatibility

This command complies with the behavior defined in the SQL standard, except
for the limitation that, in PostgreSQL, it does not apply to `NOT NULL` and
`CHECK` constraints. Also, PostgreSQL checks non-deferrable uniqueness
constraints immediately, not at end of statement as the standard would
suggest.

* * *

[Prev](sql-set.html "SET")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-set-role.html "SET ROLE")  
---|---|---  
SET  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SET ROLE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-set-constraints.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

