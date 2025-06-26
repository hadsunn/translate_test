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

Supported Versions: [Current](/docs/current/sql-altermaterializedview.html
"PostgreSQL 17 - ALTER MATERIALIZED VIEW") ([17](/docs/17/sql-
altermaterializedview.html "PostgreSQL 17 - ALTER MATERIALIZED VIEW")) /
[16](/docs/16/sql-altermaterializedview.html "PostgreSQL 16 - ALTER
MATERIALIZED VIEW") / [15](/docs/15/sql-altermaterializedview.html "PostgreSQL
15 - ALTER MATERIALIZED VIEW") / [14](/docs/14/sql-altermaterializedview.html
"PostgreSQL 14 - ALTER MATERIALIZED VIEW") / [13](/docs/13/sql-
altermaterializedview.html "PostgreSQL 13 - ALTER MATERIALIZED VIEW")

Development Versions: [18](/docs/18/sql-altermaterializedview.html "PostgreSQL
18 - ALTER MATERIALIZED VIEW") / [devel](/docs/devel/sql-
altermaterializedview.html "PostgreSQL devel - ALTER MATERIALIZED VIEW")

Unsupported versions: [12](/docs/12/sql-altermaterializedview.html "PostgreSQL
12 - ALTER MATERIALIZED VIEW") / [11](/docs/11/sql-altermaterializedview.html
"PostgreSQL 11 - ALTER MATERIALIZED VIEW") / [10](/docs/10/sql-
altermaterializedview.html "PostgreSQL 10 - ALTER MATERIALIZED VIEW") /
[9.6](/docs/9.6/sql-altermaterializedview.html "PostgreSQL 9.6 - ALTER
MATERIALIZED VIEW") / [9.5](/docs/9.5/sql-altermaterializedview.html
"PostgreSQL 9.5 - ALTER MATERIALIZED VIEW") / [9.4](/docs/9.4/sql-
altermaterializedview.html "PostgreSQL 9.4 - ALTER MATERIALIZED VIEW") /
[9.3](/docs/9.3/sql-altermaterializedview.html "PostgreSQL 9.3 - ALTER
MATERIALIZED VIEW")

__

ALTER MATERIALIZED VIEW  
---  
[Prev](sql-alterlargeobject.html "ALTER LARGE OBJECT")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alteroperator.html "ALTER OPERATOR")  
  
* * *

## ALTER MATERIALIZED VIEW

ALTER MATERIALIZED VIEW — change the definition of a materialized view

## Synopsis

    
    
    ALTER MATERIALIZED VIEW [ IF EXISTS ] _name_
        _action_ [, ... ]
    ALTER MATERIALIZED VIEW _name_
        [ NO ] DEPENDS ON EXTENSION _extension_name_
    ALTER MATERIALIZED VIEW [ IF EXISTS ] _name_
        RENAME [ COLUMN ] _column_name_ TO _new_column_name_
    ALTER MATERIALIZED VIEW [ IF EXISTS ] _name_
        RENAME TO _new_name_
    ALTER MATERIALIZED VIEW [ IF EXISTS ] _name_
        SET SCHEMA _new_schema_
    ALTER MATERIALIZED VIEW ALL IN TABLESPACE _name_ [ OWNED BY _role_name_ [, ... ] ]
        SET TABLESPACE _new_tablespace_ [ NOWAIT ]
    
    where _action_ is one of:
    
        ALTER [ COLUMN ] _column_name_ SET STATISTICS _integer_
        ALTER [ COLUMN ] _column_name_ SET ( _attribute_option_ = _value_ [, ... ] )
        ALTER [ COLUMN ] _column_name_ RESET ( _attribute_option_ [, ... ] )
        ALTER [ COLUMN ] _column_name_ SET STORAGE { PLAIN | EXTERNAL | EXTENDED | MAIN | DEFAULT }
        ALTER [ COLUMN ] _column_name_ SET COMPRESSION _compression_method_
        CLUSTER ON _index_name_
        SET WITHOUT CLUSTER
        SET ACCESS METHOD _new_access_method_
        SET TABLESPACE _new_tablespace_
        SET ( _storage_parameter_ [= _value_] [, ... ] )
        RESET ( _storage_parameter_ [, ... ] )
        OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    

## Description

`ALTER MATERIALIZED VIEW` changes various auxiliary properties of an existing
materialized view.

You must own the materialized view to use `ALTER MATERIALIZED VIEW`. To change
a materialized view's schema, you must also have `CREATE` privilege on the new
schema. To alter the owner, you must be able to `SET ROLE` to the new owning
role, and that role must have `CREATE` privilege on the materialized view's
schema. (These restrictions enforce that altering the owner doesn't do
anything you couldn't do by dropping and recreating the materialized view.
However, a superuser can alter ownership of any view anyway.)

The statement subforms and actions available for `ALTER MATERIALIZED VIEW` are
a subset of those available for `ALTER TABLE`, and have the same meaning when
used for materialized views. See the descriptions for [`ALTER TABLE`](sql-
altertable.html "ALTER TABLE") for details.

## Parameters

_`name`_

    

The name (optionally schema-qualified) of an existing materialized view.

_`column_name`_

    

Name of an existing column.

_`extension_name`_

    

The name of the extension that the materialized view is to depend on (or no
longer dependent on, if `NO` is specified). A materialized view that's marked
as dependent on an extension is automatically dropped when the extension is
dropped.

_`new_column_name`_

    

New name for an existing column.

_`new_owner`_

    

The user name of the new owner of the materialized view.

_`new_name`_

    

The new name for the materialized view.

_`new_schema`_

    

The new schema for the materialized view.

## Examples

To rename the materialized view `foo` to `bar`:

    
    
    ALTER MATERIALIZED VIEW foo RENAME TO bar;
    

## Compatibility

`ALTER MATERIALIZED VIEW` is a PostgreSQL extension.

## See Also

[CREATE MATERIALIZED VIEW](sql-creatematerializedview.html "CREATE
MATERIALIZED VIEW"), [DROP MATERIALIZED VIEW](sql-dropmaterializedview.html
"DROP MATERIALIZED VIEW"), [REFRESH MATERIALIZED VIEW](sql-
refreshmaterializedview.html "REFRESH MATERIALIZED VIEW")

* * *

[Prev](sql-alterlargeobject.html "ALTER LARGE OBJECT")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alteroperator.html "ALTER OPERATOR")  
---|---|---  
ALTER LARGE OBJECT  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER OPERATOR  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-
altermaterializedview.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

