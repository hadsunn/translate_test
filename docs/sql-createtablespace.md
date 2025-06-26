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

Supported Versions: [Current](/docs/current/sql-createtablespace.html
"PostgreSQL 17 - CREATE TABLESPACE") ([17](/docs/17/sql-createtablespace.html
"PostgreSQL 17 - CREATE TABLESPACE")) / [16](/docs/16/sql-
createtablespace.html "PostgreSQL 16 - CREATE TABLESPACE") /
[15](/docs/15/sql-createtablespace.html "PostgreSQL 15 - CREATE TABLESPACE") /
[14](/docs/14/sql-createtablespace.html "PostgreSQL 14 - CREATE TABLESPACE") /
[13](/docs/13/sql-createtablespace.html "PostgreSQL 13 - CREATE TABLESPACE")

Development Versions: [18](/docs/18/sql-createtablespace.html "PostgreSQL 18 -
CREATE TABLESPACE") / [devel](/docs/devel/sql-createtablespace.html
"PostgreSQL devel - CREATE TABLESPACE")

Unsupported versions: [12](/docs/12/sql-createtablespace.html "PostgreSQL 12 -
CREATE TABLESPACE") / [11](/docs/11/sql-createtablespace.html "PostgreSQL 11 -
CREATE TABLESPACE") / [10](/docs/10/sql-createtablespace.html "PostgreSQL 10 -
CREATE TABLESPACE") / [9.6](/docs/9.6/sql-createtablespace.html "PostgreSQL
9.6 - CREATE TABLESPACE") / [9.5](/docs/9.5/sql-createtablespace.html
"PostgreSQL 9.5 - CREATE TABLESPACE") / [9.4](/docs/9.4/sql-
createtablespace.html "PostgreSQL 9.4 - CREATE TABLESPACE") /
[9.3](/docs/9.3/sql-createtablespace.html "PostgreSQL 9.3 - CREATE
TABLESPACE") / [9.2](/docs/9.2/sql-createtablespace.html "PostgreSQL 9.2 -
CREATE TABLESPACE") / [9.1](/docs/9.1/sql-createtablespace.html "PostgreSQL
9.1 - CREATE TABLESPACE") / [9.0](/docs/9.0/sql-createtablespace.html
"PostgreSQL 9.0 - CREATE TABLESPACE") / [8.4](/docs/8.4/sql-
createtablespace.html "PostgreSQL 8.4 - CREATE TABLESPACE") /
[8.3](/docs/8.3/sql-createtablespace.html "PostgreSQL 8.3 - CREATE
TABLESPACE") / [8.2](/docs/8.2/sql-createtablespace.html "PostgreSQL 8.2 -
CREATE TABLESPACE") / [8.1](/docs/8.1/sql-createtablespace.html "PostgreSQL
8.1 - CREATE TABLESPACE") / [8.0](/docs/8.0/sql-createtablespace.html
"PostgreSQL 8.0 - CREATE TABLESPACE")

__

CREATE TABLESPACE  
---  
[Prev](sql-createtableas.html "CREATE TABLE AS")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createtsconfig.html "CREATE TEXT SEARCH CONFIGURATION")  
  
* * *

## CREATE TABLESPACE

CREATE TABLESPACE — define a new tablespace

## Synopsis

    
    
    CREATE TABLESPACE _tablespace_name_
        [ OWNER { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER } ]
        LOCATION '_directory_ '
        [ WITH ( _tablespace_option_ = _value_ [, ... ] ) ]
    

## Description

`CREATE TABLESPACE` registers a new cluster-wide tablespace. The tablespace
name must be distinct from the name of any existing tablespace in the database
cluster.

A tablespace allows superusers to define an alternative location on the file
system where the data files containing database objects (such as tables and
indexes) can reside.

A user with appropriate privileges can pass _`tablespace_name`_ to `CREATE
DATABASE`, `CREATE TABLE`, `CREATE INDEX` or `ADD CONSTRAINT` to have the data
files for these objects stored within the specified tablespace.

### Warning

A tablespace cannot be used independently of the cluster in which it is
defined; see [Section 23.6](manage-ag-tablespaces.html "23.6. Tablespaces").

## Parameters

_`tablespace_name`_

    

The name of a tablespace to be created. The name cannot begin with `pg_`, as
such names are reserved for system tablespaces.

_`user_name`_

    

The name of the user who will own the tablespace. If omitted, defaults to the
user executing the command. Only superusers can create tablespaces, but they
can assign ownership of tablespaces to non-superusers.

_`directory`_

    

The directory that will be used for the tablespace. The directory must exist
(`CREATE TABLESPACE` will not create it), should be empty, and must be owned
by the PostgreSQL system user. The directory must be specified by an absolute
path name.

_`tablespace_option`_

    

A tablespace parameter to be set or reset. Currently, the only available
parameters are `seq_page_cost`, `random_page_cost`, `effective_io_concurrency`
and `maintenance_io_concurrency`. Setting these values for a particular
tablespace will override the planner's usual estimate of the cost of reading
pages from tables in that tablespace, and the executor's prefetching behavior,
as established by the configuration parameters of the same name (see
[seq_page_cost](runtime-config-query.html#GUC-SEQ-PAGE-COST),
[random_page_cost](runtime-config-query.html#GUC-RANDOM-PAGE-COST),
[effective_io_concurrency](runtime-config-resource.html#GUC-EFFECTIVE-IO-
CONCURRENCY), [maintenance_io_concurrency](runtime-config-resource.html#GUC-
MAINTENANCE-IO-CONCURRENCY)). This may be useful if one tablespace is located
on a disk which is faster or slower than the remainder of the I/O subsystem.

## Notes

`CREATE TABLESPACE` cannot be executed inside a transaction block.

## Examples

To create a tablespace `dbspace` at file system location `/data/dbs`, first
create the directory using operating system facilities and set the correct
ownership:

    
    
    mkdir /data/dbs
    chown postgres:postgres /data/dbs
    

Then issue the tablespace creation command inside PostgreSQL:

    
    
    CREATE TABLESPACE dbspace LOCATION '/data/dbs';
    

To create a tablespace owned by a different database user, use a command like
this:

    
    
    CREATE TABLESPACE indexspace OWNER genevieve LOCATION '/data/indexes';
    

## Compatibility

`CREATE TABLESPACE` is a PostgreSQL extension.

## See Also

[CREATE DATABASE](sql-createdatabase.html "CREATE DATABASE"), [CREATE
TABLE](sql-createtable.html "CREATE TABLE"), [CREATE INDEX](sql-
createindex.html "CREATE INDEX"), [DROP TABLESPACE](sql-droptablespace.html
"DROP TABLESPACE"), [ALTER TABLESPACE](sql-altertablespace.html "ALTER
TABLESPACE")

* * *

[Prev](sql-createtableas.html "CREATE TABLE AS")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createtsconfig.html "CREATE TEXT SEARCH CONFIGURATION")  
---|---|---  
CREATE TABLE AS  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE TEXT SEARCH CONFIGURATION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createtablespace.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

