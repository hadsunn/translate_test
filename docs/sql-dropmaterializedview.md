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

Supported Versions: [Current](/docs/current/sql-dropmaterializedview.html
"PostgreSQL 17 - DROP MATERIALIZED VIEW") ([17](/docs/17/sql-
dropmaterializedview.html "PostgreSQL 17 - DROP MATERIALIZED VIEW")) /
[16](/docs/16/sql-dropmaterializedview.html "PostgreSQL 16 - DROP MATERIALIZED
VIEW") / [15](/docs/15/sql-dropmaterializedview.html "PostgreSQL 15 - DROP
MATERIALIZED VIEW") / [14](/docs/14/sql-dropmaterializedview.html "PostgreSQL
14 - DROP MATERIALIZED VIEW") / [13](/docs/13/sql-dropmaterializedview.html
"PostgreSQL 13 - DROP MATERIALIZED VIEW")

Development Versions: [18](/docs/18/sql-dropmaterializedview.html "PostgreSQL
18 - DROP MATERIALIZED VIEW") / [devel](/docs/devel/sql-
dropmaterializedview.html "PostgreSQL devel - DROP MATERIALIZED VIEW")

Unsupported versions: [12](/docs/12/sql-dropmaterializedview.html "PostgreSQL
12 - DROP MATERIALIZED VIEW") / [11](/docs/11/sql-dropmaterializedview.html
"PostgreSQL 11 - DROP MATERIALIZED VIEW") / [10](/docs/10/sql-
dropmaterializedview.html "PostgreSQL 10 - DROP MATERIALIZED VIEW") /
[9.6](/docs/9.6/sql-dropmaterializedview.html "PostgreSQL 9.6 - DROP
MATERIALIZED VIEW") / [9.5](/docs/9.5/sql-dropmaterializedview.html
"PostgreSQL 9.5 - DROP MATERIALIZED VIEW") / [9.4](/docs/9.4/sql-
dropmaterializedview.html "PostgreSQL 9.4 - DROP MATERIALIZED VIEW") /
[9.3](/docs/9.3/sql-dropmaterializedview.html "PostgreSQL 9.3 - DROP
MATERIALIZED VIEW")

__

DROP MATERIALIZED VIEW  
---  
[Prev](sql-droplanguage.html "DROP LANGUAGE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-dropoperator.html "DROP OPERATOR")  
  
* * *

## DROP MATERIALIZED VIEW

DROP MATERIALIZED VIEW — remove a materialized view

## Synopsis

    
    
    DROP MATERIALIZED VIEW [ IF EXISTS ] _name_ [, ...] [ CASCADE | RESTRICT ]
    

## Description

`DROP MATERIALIZED VIEW` drops an existing materialized view. To execute this
command you must be the owner of the materialized view.

## Parameters

`IF EXISTS`

    

Do not throw an error if the materialized view does not exist. A notice is
issued in this case.

_`name`_

    

The name (optionally schema-qualified) of the materialized view to remove.

`CASCADE`

    

Automatically drop objects that depend on the materialized view (such as other
materialized views, or regular views), and in turn all objects that depend on
those objects (see [Section 5.14](ddl-depend.html "5.14. Dependency
Tracking")).

`RESTRICT`

    

Refuse to drop the materialized view if any objects depend on it. This is the
default.

## Examples

This command will remove the materialized view called `order_summary`:

    
    
    DROP MATERIALIZED VIEW order_summary;
    

## Compatibility

`DROP MATERIALIZED VIEW` is a PostgreSQL extension.

## See Also

[CREATE MATERIALIZED VIEW](sql-creatematerializedview.html "CREATE
MATERIALIZED VIEW"), [ALTER MATERIALIZED VIEW](sql-altermaterializedview.html
"ALTER MATERIALIZED VIEW"), [REFRESH MATERIALIZED VIEW](sql-
refreshmaterializedview.html "REFRESH MATERIALIZED VIEW")

* * *

[Prev](sql-droplanguage.html "DROP LANGUAGE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-dropoperator.html "DROP OPERATOR")  
---|---|---  
DROP LANGUAGE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP OPERATOR  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-
dropmaterializedview.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

