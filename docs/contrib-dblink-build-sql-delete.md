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

Supported Versions: [Current](/docs/current/contrib-dblink-build-sql-
delete.html "PostgreSQL 17 - dblink_build_sql_delete") ([17](/docs/17/contrib-
dblink-build-sql-delete.html "PostgreSQL 17 - dblink_build_sql_delete")) /
[16](/docs/16/contrib-dblink-build-sql-delete.html "PostgreSQL 16 -
dblink_build_sql_delete") / [15](/docs/15/contrib-dblink-build-sql-delete.html
"PostgreSQL 15 - dblink_build_sql_delete") / [14](/docs/14/contrib-dblink-
build-sql-delete.html "PostgreSQL 14 - dblink_build_sql_delete") /
[13](/docs/13/contrib-dblink-build-sql-delete.html "PostgreSQL 13 -
dblink_build_sql_delete")

Development Versions: [18](/docs/18/contrib-dblink-build-sql-delete.html
"PostgreSQL 18 - dblink_build_sql_delete") / [devel](/docs/devel/contrib-
dblink-build-sql-delete.html "PostgreSQL devel - dblink_build_sql_delete")

Unsupported versions: [12](/docs/12/contrib-dblink-build-sql-delete.html
"PostgreSQL 12 - dblink_build_sql_delete") / [11](/docs/11/contrib-dblink-
build-sql-delete.html "PostgreSQL 11 - dblink_build_sql_delete") /
[10](/docs/10/contrib-dblink-build-sql-delete.html "PostgreSQL 10 -
dblink_build_sql_delete") / [9.6](/docs/9.6/contrib-dblink-build-sql-
delete.html "PostgreSQL 9.6 - dblink_build_sql_delete") /
[9.5](/docs/9.5/contrib-dblink-build-sql-delete.html "PostgreSQL 9.5 -
dblink_build_sql_delete") / [9.4](/docs/9.4/contrib-dblink-build-sql-
delete.html "PostgreSQL 9.4 - dblink_build_sql_delete") /
[9.3](/docs/9.3/contrib-dblink-build-sql-delete.html "PostgreSQL 9.3 -
dblink_build_sql_delete") / [9.2](/docs/9.2/contrib-dblink-build-sql-
delete.html "PostgreSQL 9.2 - dblink_build_sql_delete") /
[9.1](/docs/9.1/contrib-dblink-build-sql-delete.html "PostgreSQL 9.1 -
dblink_build_sql_delete") / [9.0](/docs/9.0/contrib-dblink-build-sql-
delete.html "PostgreSQL 9.0 - dblink_build_sql_delete") /
[8.4](/docs/8.4/contrib-dblink-build-sql-delete.html "PostgreSQL 8.4 -
dblink_build_sql_delete") / [8.3](/docs/8.3/contrib-dblink-build-sql-
delete.html "PostgreSQL 8.3 - dblink_build_sql_delete")

__

dblink_build_sql_delete  
---  
[Prev](contrib-dblink-build-sql-insert.html "dblink_build_sql_insert")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") | F.12. dblink — connect to other PostgreSQL databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-build-sql-update.html "dblink_build_sql_update")  
  
* * *

## dblink_build_sql_delete

dblink_build_sql_delete — builds a DELETE statement using supplied values for
primary key field values

## Synopsis

    
    
    dblink_build_sql_delete(text relname,
                            int2vector primary_key_attnums,
                            integer num_primary_key_atts,
                            text[] tgt_pk_att_vals_array) returns text
    

## Description

`dblink_build_sql_delete` can be useful in doing selective replication of a
local table to a remote database. It builds an SQL `DELETE` command that will
delete the row with the given primary key values.

## Arguments

_`relname`_

    

Name of a local relation, for example `foo` or `myschema.mytab`. Include
double quotes if the name is mixed-case or contains special characters, for
example `"FooBar"`; without quotes, the string will be folded to lower case.

_`primary_key_attnums`_

    

Attribute numbers (1-based) of the primary key fields, for example `1 2`.

_`num_primary_key_atts`_

    

The number of primary key fields.

_`tgt_pk_att_vals_array`_

    

Values of the primary key fields to be used in the resulting `DELETE` command.
Each field is represented in text form.

## Return Value

Returns the requested SQL statement as text.

## Notes

As of PostgreSQL 9.0, the attribute numbers in _`primary_key_attnums`_ are
interpreted as logical column numbers, corresponding to the column's position
in `SELECT * FROM relname`. Previous versions interpreted the numbers as
physical column positions. There is a difference if any column(s) to the left
of the indicated column have been dropped during the lifetime of the table.

## Examples

    
    
    SELECT dblink_build_sql_delete('"MyFoo"', '1 2', 2, '{"1", "b"}');
               dblink_build_sql_delete
    ---------------------------------------------
     DELETE FROM "MyFoo" WHERE f1='1' AND f2='b'
    (1 row)
    

* * *

[Prev](contrib-dblink-build-sql-insert.html "dblink_build_sql_insert")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") |  [Next](contrib-dblink-build-sql-update.html "dblink_build_sql_update")  
---|---|---  
dblink_build_sql_insert  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink_build_sql_update  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-dblink-build-sql-
delete.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

