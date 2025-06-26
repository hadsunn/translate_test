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

Supported Versions: [Current](/docs/current/sql-alterpublication.html
"PostgreSQL 17 - ALTER PUBLICATION") ([17](/docs/17/sql-alterpublication.html
"PostgreSQL 17 - ALTER PUBLICATION")) / [16](/docs/16/sql-
alterpublication.html "PostgreSQL 16 - ALTER PUBLICATION") /
[15](/docs/15/sql-alterpublication.html "PostgreSQL 15 - ALTER PUBLICATION") /
[14](/docs/14/sql-alterpublication.html "PostgreSQL 14 - ALTER PUBLICATION") /
[13](/docs/13/sql-alterpublication.html "PostgreSQL 13 - ALTER PUBLICATION")

Development Versions: [18](/docs/18/sql-alterpublication.html "PostgreSQL 18 -
ALTER PUBLICATION") / [devel](/docs/devel/sql-alterpublication.html
"PostgreSQL devel - ALTER PUBLICATION")

Unsupported versions: [12](/docs/12/sql-alterpublication.html "PostgreSQL 12 -
ALTER PUBLICATION") / [11](/docs/11/sql-alterpublication.html "PostgreSQL 11 -
ALTER PUBLICATION") / [10](/docs/10/sql-alterpublication.html "PostgreSQL 10 -
ALTER PUBLICATION")

__

ALTER PUBLICATION  
---  
[Prev](sql-alterprocedure.html "ALTER PROCEDURE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterrole.html "ALTER ROLE")  
  
* * *

## ALTER PUBLICATION

ALTER PUBLICATION — change the definition of a publication

## Synopsis

    
    
    ALTER PUBLICATION _name_ ADD _publication_object_ [, ...]
    ALTER PUBLICATION _name_ SET _publication_object_ [, ...]
    ALTER PUBLICATION _name_ DROP _publication_object_ [, ...]
    ALTER PUBLICATION _name_ SET ( _publication_parameter_ [= _value_] [, ... ] )
    ALTER PUBLICATION _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER PUBLICATION _name_ RENAME TO _new_name_
    
    where _publication_object_ is one of:
    
        TABLE [ ONLY ] _table_name_ [ * ] [ ( _column_name_ [, ... ] ) ] [ WHERE ( _expression_ ) ] [, ... ]
        TABLES IN SCHEMA { _schema_name_ | CURRENT_SCHEMA } [, ... ]
    

## Description

The command `ALTER PUBLICATION` can change the attributes of a publication.

The first three variants change which tables/schemas are part of the
publication. The `SET` clause will replace the list of tables/schemas in the
publication with the specified list; the existing tables/schemas that were
present in the publication will be removed. The `ADD` and `DROP` clauses will
add and remove one or more tables/schemas from the publication. Note that
adding tables/schemas to a publication that is already subscribed to will
require an `ALTER SUBSCRIPTION ... REFRESH PUBLICATION` action on the
subscribing side in order to become effective. Note also that `DROP TABLES IN
SCHEMA` will not drop any schema tables that were specified using [`FOR
TABLE`](sql-createpublication.html#SQL-CREATEPUBLICATION-FOR-TABLE)/ `ADD
TABLE`, and the combination of `DROP` with a `WHERE` clause is not allowed.

The fourth variant of this command listed in the synopsis can change all of
the publication properties specified in [CREATE PUBLICATION](sql-
createpublication.html "CREATE PUBLICATION"). Properties not mentioned in the
command retain their previous settings.

The remaining variants change the owner and the name of the publication.

You must own the publication to use `ALTER PUBLICATION`. Adding a table to a
publication additionally requires owning that table. The `ADD TABLES IN
SCHEMA` and `SET TABLES IN SCHEMA` to a publication requires the invoking user
to be a superuser. To alter the owner, you must be able to `SET ROLE` to the
new owning role, and that role must have `CREATE` privilege on the database.
Also, the new owner of a [`FOR ALL TABLES`](sql-createpublication.html#SQL-
CREATEPUBLICATION-FOR-ALL-TABLES) or [`FOR TABLES IN SCHEMA`](sql-
createpublication.html#SQL-CREATEPUBLICATION-FOR-TABLES-IN-SCHEMA) publication
must be a superuser. However, a superuser can change the ownership of a
publication regardless of these restrictions.

Adding/Setting any schema when the publication also publishes a table with a
column list, and vice versa is not supported.

## Parameters

_`name`_

    

The name of an existing publication whose definition is to be altered.

_`table_name`_

    

Name of an existing table. If `ONLY` is specified before the table name, only
that table is affected. If `ONLY` is not specified, the table and all its
descendant tables (if any) are affected. Optionally, `*` can be specified
after the table name to explicitly indicate that descendant tables are
included.

Optionally, a column list can be specified. See [CREATE PUBLICATION](sql-
createpublication.html "CREATE PUBLICATION") for details. Note that a
subscription having several publications in which the same table has been
published with different column lists is not supported. See [Warning:
Combining Column Lists from Multiple Publications](logical-replication-col-
lists.html#LOGICAL-REPLICATION-COL-LIST-COMBINING "Warning: Combining Column
Lists from Multiple Publications") for details of potential problems when
altering column lists.

If the optional `WHERE` clause is specified, rows for which the _`expression`_
evaluates to false or null will not be published. Note that parentheses are
required around the expression. The _`expression`_ is evaluated with the role
used for the replication connection.

_`schema_name`_

    

Name of an existing schema.

`SET ( _`publication_parameter`_ [= _`value`_] [, ... ] )`

    

This clause alters publication parameters originally set by [CREATE
PUBLICATION](sql-createpublication.html "CREATE PUBLICATION"). See there for
more information.

_`new_owner`_

    

The user name of the new owner of the publication.

_`new_name`_

    

The new name for the publication.

## Examples

Change the publication to publish only deletes and updates:

    
    
    ALTER PUBLICATION noinsert SET (publish = 'update, delete');
    

Add some tables to the publication:

    
    
    ALTER PUBLICATION mypublication ADD TABLE users (user_id, firstname), departments;
    

Change the set of columns published for a table:

    
    
    ALTER PUBLICATION mypublication SET TABLE users (user_id, firstname, lastname), TABLE departments;
    

Add schemas `marketing` and `sales` to the publication `sales_publication`:

    
    
    ALTER PUBLICATION sales_publication ADD TABLES IN SCHEMA marketing, sales;
    

Add tables `users`, `departments` and schema `production` to the publication
`production_publication`:

    
    
    ALTER PUBLICATION production_publication ADD TABLE users, departments, TABLES IN SCHEMA production;
    

## Compatibility

`ALTER PUBLICATION` is a PostgreSQL extension.

## See Also

[CREATE PUBLICATION](sql-createpublication.html "CREATE PUBLICATION"), [DROP
PUBLICATION](sql-droppublication.html "DROP PUBLICATION"), [CREATE
SUBSCRIPTION](sql-createsubscription.html "CREATE SUBSCRIPTION"), [ALTER
SUBSCRIPTION](sql-altersubscription.html "ALTER SUBSCRIPTION")

* * *

[Prev](sql-alterprocedure.html "ALTER PROCEDURE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterrole.html "ALTER ROLE")  
---|---|---  
ALTER PROCEDURE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER ROLE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-alterpublication.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

