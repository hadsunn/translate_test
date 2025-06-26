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

Supported Versions: [Current](/docs/current/sql-alterview.html "PostgreSQL 17
- ALTER VIEW") ([17](/docs/17/sql-alterview.html "PostgreSQL 17 - ALTER
VIEW")) / [16](/docs/16/sql-alterview.html "PostgreSQL 16 - ALTER VIEW") /
[15](/docs/15/sql-alterview.html "PostgreSQL 15 - ALTER VIEW") /
[14](/docs/14/sql-alterview.html "PostgreSQL 14 - ALTER VIEW") /
[13](/docs/13/sql-alterview.html "PostgreSQL 13 - ALTER VIEW")

Development Versions: [18](/docs/18/sql-alterview.html "PostgreSQL 18 - ALTER
VIEW") / [devel](/docs/devel/sql-alterview.html "PostgreSQL devel - ALTER
VIEW")

Unsupported versions: [12](/docs/12/sql-alterview.html "PostgreSQL 12 - ALTER
VIEW") / [11](/docs/11/sql-alterview.html "PostgreSQL 11 - ALTER VIEW") /
[10](/docs/10/sql-alterview.html "PostgreSQL 10 - ALTER VIEW") /
[9.6](/docs/9.6/sql-alterview.html "PostgreSQL 9.6 - ALTER VIEW") /
[9.5](/docs/9.5/sql-alterview.html "PostgreSQL 9.5 - ALTER VIEW") /
[9.4](/docs/9.4/sql-alterview.html "PostgreSQL 9.4 - ALTER VIEW") /
[9.3](/docs/9.3/sql-alterview.html "PostgreSQL 9.3 - ALTER VIEW") /
[9.2](/docs/9.2/sql-alterview.html "PostgreSQL 9.2 - ALTER VIEW") /
[9.1](/docs/9.1/sql-alterview.html "PostgreSQL 9.1 - ALTER VIEW") /
[9.0](/docs/9.0/sql-alterview.html "PostgreSQL 9.0 - ALTER VIEW") /
[8.4](/docs/8.4/sql-alterview.html "PostgreSQL 8.4 - ALTER VIEW") /
[8.3](/docs/8.3/sql-alterview.html "PostgreSQL 8.3 - ALTER VIEW")

__

ALTER VIEW  
---  
[Prev](sql-alterusermapping.html "ALTER USER MAPPING")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-analyze.html "ANALYZE")  
  
* * *

## ALTER VIEW

ALTER VIEW — change the definition of a view

## Synopsis

    
    
    ALTER VIEW [ IF EXISTS ] _name_ ALTER [ COLUMN ] _column_name_ SET DEFAULT _expression_
    ALTER VIEW [ IF EXISTS ] _name_ ALTER [ COLUMN ] _column_name_ DROP DEFAULT
    ALTER VIEW [ IF EXISTS ] _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER VIEW [ IF EXISTS ] _name_ RENAME [ COLUMN ] _column_name_ TO _new_column_name_
    ALTER VIEW [ IF EXISTS ] _name_ RENAME TO _new_name_
    ALTER VIEW [ IF EXISTS ] _name_ SET SCHEMA _new_schema_
    ALTER VIEW [ IF EXISTS ] _name_ SET ( _view_option_name_ [= _view_option_value_] [, ... ] )
    ALTER VIEW [ IF EXISTS ] _name_ RESET ( _view_option_name_ [, ... ] )
    

## Description

`ALTER VIEW` changes various auxiliary properties of a view. (If you want to
modify the view's defining query, use `CREATE OR REPLACE VIEW`.)

You must own the view to use `ALTER VIEW`. To change a view's schema, you must
also have `CREATE` privilege on the new schema. To alter the owner, you must
be able to `SET ROLE` to the new owning role, and that role must have `CREATE`
privilege on the view's schema. (These restrictions enforce that altering the
owner doesn't do anything you couldn't do by dropping and recreating the view.
However, a superuser can alter ownership of any view anyway.)

## Parameters

_`name`_

    

The name (optionally schema-qualified) of an existing view.

_`column_name`_

    

Name of an existing column.

_`new_column_name`_

    

New name for an existing column.

`IF EXISTS`

    

Do not throw an error if the view does not exist. A notice is issued in this
case.

`SET`/`DROP DEFAULT`

    

These forms set or remove the default value for a column. A view column's
default value is substituted into any `INSERT` or `UPDATE` command whose
target is the view, before applying any rules or triggers for the view. The
view's default will therefore take precedence over any default values from
underlying relations.

_`new_owner`_

    

The user name of the new owner of the view.

_`new_name`_

    

The new name for the view.

_`new_schema`_

    

The new schema for the view.

`SET ( _`view_option_name`_ [= _`view_option_value`_] [, ... ] )`  
`RESET ( _`view_option_name`_ [, ... ] )`

    

Sets or resets a view option. Currently supported options are:

`check_option` (`enum`)

    

Changes the check option of the view. The value must be `local` or `cascaded`.

`security_barrier` (`boolean`)

    

Changes the security-barrier property of the view. The value must be a Boolean
value, such as `true` or `false`.

`security_invoker` (`boolean`)

    

Changes the security-invoker property of the view. The value must be a Boolean
value, such as `true` or `false`.

## Notes

For historical reasons, `ALTER TABLE` can be used with views too; but the only
variants of `ALTER TABLE` that are allowed with views are equivalent to the
ones shown above.

## Examples

To rename the view `foo` to `bar`:

    
    
    ALTER VIEW foo RENAME TO bar;
    

To attach a default column value to an updatable view:

    
    
    CREATE TABLE base_table (id int, ts timestamptz);
    CREATE VIEW a_view AS SELECT * FROM base_table;
    ALTER VIEW a_view ALTER COLUMN ts SET DEFAULT now();
    INSERT INTO base_table(id) VALUES(1);  -- ts will receive a NULL
    INSERT INTO a_view(id) VALUES(2);  -- ts will receive the current time
    

## Compatibility

`ALTER VIEW` is a PostgreSQL extension of the SQL standard.

## See Also

[CREATE VIEW](sql-createview.html "CREATE VIEW"), [DROP VIEW](sql-
dropview.html "DROP VIEW")

* * *

[Prev](sql-alterusermapping.html "ALTER USER MAPPING")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-analyze.html "ANALYZE")  
---|---|---  
ALTER USER MAPPING  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ANALYZE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterview.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

