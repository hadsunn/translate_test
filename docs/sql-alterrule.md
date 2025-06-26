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

Supported Versions: [Current](/docs/current/sql-alterrule.html "PostgreSQL 17
- ALTER RULE") ([17](/docs/17/sql-alterrule.html "PostgreSQL 17 - ALTER
RULE")) / [16](/docs/16/sql-alterrule.html "PostgreSQL 16 - ALTER RULE") /
[15](/docs/15/sql-alterrule.html "PostgreSQL 15 - ALTER RULE") /
[14](/docs/14/sql-alterrule.html "PostgreSQL 14 - ALTER RULE") /
[13](/docs/13/sql-alterrule.html "PostgreSQL 13 - ALTER RULE")

Development Versions: [18](/docs/18/sql-alterrule.html "PostgreSQL 18 - ALTER
RULE") / [devel](/docs/devel/sql-alterrule.html "PostgreSQL devel - ALTER
RULE")

Unsupported versions: [12](/docs/12/sql-alterrule.html "PostgreSQL 12 - ALTER
RULE") / [11](/docs/11/sql-alterrule.html "PostgreSQL 11 - ALTER RULE") /
[10](/docs/10/sql-alterrule.html "PostgreSQL 10 - ALTER RULE") /
[9.6](/docs/9.6/sql-alterrule.html "PostgreSQL 9.6 - ALTER RULE") /
[9.5](/docs/9.5/sql-alterrule.html "PostgreSQL 9.5 - ALTER RULE") /
[9.4](/docs/9.4/sql-alterrule.html "PostgreSQL 9.4 - ALTER RULE") /
[9.3](/docs/9.3/sql-alterrule.html "PostgreSQL 9.3 - ALTER RULE")

__

ALTER RULE  
---  
[Prev](sql-alterroutine.html "ALTER ROUTINE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterschema.html "ALTER SCHEMA")  
  
* * *

## ALTER RULE

ALTER RULE — change the definition of a rule

## Synopsis

    
    
    ALTER RULE _name_ ON _table_name_ RENAME TO _new_name_
    

## Description

`ALTER RULE` changes properties of an existing rule. Currently, the only
available action is to change the rule's name.

To use `ALTER RULE`, you must own the table or view that the rule applies to.

## Parameters

_`name`_

    

The name of an existing rule to alter.

_`table_name`_

    

The name (optionally schema-qualified) of the table or view that the rule
applies to.

_`new_name`_

    

The new name for the rule.

## Examples

To rename an existing rule:

    
    
    ALTER RULE notify_all ON emp RENAME TO notify_me;
    

## Compatibility

`ALTER RULE` is a PostgreSQL language extension, as is the entire query
rewrite system.

## See Also

[CREATE RULE](sql-createrule.html "CREATE RULE"), [DROP RULE](sql-
droprule.html "DROP RULE")

* * *

[Prev](sql-alterroutine.html "ALTER ROUTINE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterschema.html "ALTER SCHEMA")  
---|---|---  
ALTER ROUTINE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER SCHEMA  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterrule.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

