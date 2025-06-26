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

Supported Versions: [Current](/docs/current/sql-droppolicy.html "PostgreSQL 17
- DROP POLICY") ([17](/docs/17/sql-droppolicy.html "PostgreSQL 17 - DROP
POLICY")) / [16](/docs/16/sql-droppolicy.html "PostgreSQL 16 - DROP POLICY") /
[15](/docs/15/sql-droppolicy.html "PostgreSQL 15 - DROP POLICY") /
[14](/docs/14/sql-droppolicy.html "PostgreSQL 14 - DROP POLICY") /
[13](/docs/13/sql-droppolicy.html "PostgreSQL 13 - DROP POLICY")

Development Versions: [18](/docs/18/sql-droppolicy.html "PostgreSQL 18 - DROP
POLICY") / [devel](/docs/devel/sql-droppolicy.html "PostgreSQL devel - DROP
POLICY")

Unsupported versions: [12](/docs/12/sql-droppolicy.html "PostgreSQL 12 - DROP
POLICY") / [11](/docs/11/sql-droppolicy.html "PostgreSQL 11 - DROP POLICY") /
[10](/docs/10/sql-droppolicy.html "PostgreSQL 10 - DROP POLICY") /
[9.6](/docs/9.6/sql-droppolicy.html "PostgreSQL 9.6 - DROP POLICY") /
[9.5](/docs/9.5/sql-droppolicy.html "PostgreSQL 9.5 - DROP POLICY")

__

DROP POLICY  
---  
[Prev](sql-drop-owned.html "DROP OWNED")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropprocedure.html "DROP PROCEDURE")  
  
* * *

## DROP POLICY

DROP POLICY — remove a row-level security policy from a table

## Synopsis

    
    
    DROP POLICY [ IF EXISTS ] _name_ ON _table_name_ [ CASCADE | RESTRICT ]
    

## Description

`DROP POLICY` removes the specified policy from the table. Note that if the
last policy is removed for a table and the table still has row-level security
enabled via `ALTER TABLE`, then the default-deny policy will be used. `ALTER
TABLE ... DISABLE ROW LEVEL SECURITY` can be used to disable row-level
security for a table, whether policies for the table exist or not.

## Parameters

`IF EXISTS`

    

Do not throw an error if the policy does not exist. A notice is issued in this
case.

_`name`_

    

The name of the policy to drop.

_`table_name`_

    

The name (optionally schema-qualified) of the table that the policy is on.

`CASCADE`  
`RESTRICT`

    

These key words do not have any effect, since there are no dependencies on
policies.

## Examples

To drop the policy called `p1` on the table named `my_table`:

    
    
    DROP POLICY p1 ON my_table;
    

## Compatibility

`DROP POLICY` is a PostgreSQL extension.

## See Also

[CREATE POLICY](sql-createpolicy.html "CREATE POLICY"), [ALTER POLICY](sql-
alterpolicy.html "ALTER POLICY")

* * *

[Prev](sql-drop-owned.html "DROP OWNED")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropprocedure.html "DROP PROCEDURE")  
---|---|---  
DROP OWNED  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP PROCEDURE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-droppolicy.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

