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

Supported Versions: [Current](/docs/current/sql-dropindex.html "PostgreSQL 17
- DROP INDEX") ([17](/docs/17/sql-dropindex.html "PostgreSQL 17 - DROP
INDEX")) / [16](/docs/16/sql-dropindex.html "PostgreSQL 16 - DROP INDEX") /
[15](/docs/15/sql-dropindex.html "PostgreSQL 15 - DROP INDEX") /
[14](/docs/14/sql-dropindex.html "PostgreSQL 14 - DROP INDEX") /
[13](/docs/13/sql-dropindex.html "PostgreSQL 13 - DROP INDEX")

Development Versions: [18](/docs/18/sql-dropindex.html "PostgreSQL 18 - DROP
INDEX") / [devel](/docs/devel/sql-dropindex.html "PostgreSQL devel - DROP
INDEX")

Unsupported versions: [12](/docs/12/sql-dropindex.html "PostgreSQL 12 - DROP
INDEX") / [11](/docs/11/sql-dropindex.html "PostgreSQL 11 - DROP INDEX") /
[10](/docs/10/sql-dropindex.html "PostgreSQL 10 - DROP INDEX") /
[9.6](/docs/9.6/sql-dropindex.html "PostgreSQL 9.6 - DROP INDEX") /
[9.5](/docs/9.5/sql-dropindex.html "PostgreSQL 9.5 - DROP INDEX") /
[9.4](/docs/9.4/sql-dropindex.html "PostgreSQL 9.4 - DROP INDEX") /
[9.3](/docs/9.3/sql-dropindex.html "PostgreSQL 9.3 - DROP INDEX") /
[9.2](/docs/9.2/sql-dropindex.html "PostgreSQL 9.2 - DROP INDEX") /
[9.1](/docs/9.1/sql-dropindex.html "PostgreSQL 9.1 - DROP INDEX") /
[9.0](/docs/9.0/sql-dropindex.html "PostgreSQL 9.0 - DROP INDEX") /
[8.4](/docs/8.4/sql-dropindex.html "PostgreSQL 8.4 - DROP INDEX") /
[8.3](/docs/8.3/sql-dropindex.html "PostgreSQL 8.3 - DROP INDEX") /
[8.2](/docs/8.2/sql-dropindex.html "PostgreSQL 8.2 - DROP INDEX") /
[8.1](/docs/8.1/sql-dropindex.html "PostgreSQL 8.1 - DROP INDEX") /
[8.0](/docs/8.0/sql-dropindex.html "PostgreSQL 8.0 - DROP INDEX") /
[7.4](/docs/7.4/sql-dropindex.html "PostgreSQL 7.4 - DROP INDEX") /
[7.3](/docs/7.3/sql-dropindex.html "PostgreSQL 7.3 - DROP INDEX") /
[7.2](/docs/7.2/sql-dropindex.html "PostgreSQL 7.2 - DROP INDEX") /
[7.1](/docs/7.1/sql-dropindex.html "PostgreSQL 7.1 - DROP INDEX")

__

DROP INDEX  
---  
[Prev](sql-dropgroup.html "DROP GROUP")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-droplanguage.html "DROP LANGUAGE")  
  
* * *

## DROP INDEX

DROP INDEX — remove an index

## Synopsis

    
    
    DROP INDEX [ CONCURRENTLY ] [ IF EXISTS ] _name_ [, ...] [ CASCADE | RESTRICT ]
    

## Description

`DROP INDEX` drops an existing index from the database system. To execute this
command you must be the owner of the index.

## Parameters

`CONCURRENTLY`

    

Drop the index without locking out concurrent selects, inserts, updates, and
deletes on the index's table. A normal `DROP INDEX` acquires an `ACCESS
EXCLUSIVE` lock on the table, blocking other accesses until the index drop can
be completed. With this option, the command instead waits until conflicting
transactions have completed.

There are several caveats to be aware of when using this option. Only one
index name can be specified, and the `CASCADE` option is not supported. (Thus,
an index that supports a `UNIQUE` or `PRIMARY KEY` constraint cannot be
dropped this way.) Also, regular `DROP INDEX` commands can be performed within
a transaction block, but `DROP INDEX CONCURRENTLY` cannot. Lastly, indexes on
partitioned tables cannot be dropped using this option.

For temporary tables, `DROP INDEX` is always non-concurrent, as no other
session can access them, and non-concurrent index drop is cheaper.

`IF EXISTS`

    

Do not throw an error if the index does not exist. A notice is issued in this
case.

_`name`_

    

The name (optionally schema-qualified) of an index to remove.

`CASCADE`

    

Automatically drop objects that depend on the index, and in turn all objects
that depend on those objects (see [Section 5.14](ddl-depend.html
"5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the index if any objects depend on it. This is the default.

## Examples

This command will remove the index `title_idx`:

    
    
    DROP INDEX title_idx;
    

## Compatibility

`DROP INDEX` is a PostgreSQL language extension. There are no provisions for
indexes in the SQL standard.

## See Also

[CREATE INDEX](sql-createindex.html "CREATE INDEX")

* * *

[Prev](sql-dropgroup.html "DROP GROUP")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-droplanguage.html "DROP LANGUAGE")  
---|---|---  
DROP GROUP  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP LANGUAGE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-dropindex.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

