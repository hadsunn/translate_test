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

Supported Versions: [Current](/docs/current/contrib-dblink-get-pkey.html
"PostgreSQL 17 - dblink_get_pkey") ([17](/docs/17/contrib-dblink-get-pkey.html
"PostgreSQL 17 - dblink_get_pkey")) / [16](/docs/16/contrib-dblink-get-
pkey.html "PostgreSQL 16 - dblink_get_pkey") / [15](/docs/15/contrib-dblink-
get-pkey.html "PostgreSQL 15 - dblink_get_pkey") / [14](/docs/14/contrib-
dblink-get-pkey.html "PostgreSQL 14 - dblink_get_pkey") /
[13](/docs/13/contrib-dblink-get-pkey.html "PostgreSQL 13 - dblink_get_pkey")

Development Versions: [18](/docs/18/contrib-dblink-get-pkey.html "PostgreSQL
18 - dblink_get_pkey") / [devel](/docs/devel/contrib-dblink-get-pkey.html
"PostgreSQL devel - dblink_get_pkey")

Unsupported versions: [12](/docs/12/contrib-dblink-get-pkey.html "PostgreSQL
12 - dblink_get_pkey") / [11](/docs/11/contrib-dblink-get-pkey.html
"PostgreSQL 11 - dblink_get_pkey") / [10](/docs/10/contrib-dblink-get-
pkey.html "PostgreSQL 10 - dblink_get_pkey") / [9.6](/docs/9.6/contrib-dblink-
get-pkey.html "PostgreSQL 9.6 - dblink_get_pkey") / [9.5](/docs/9.5/contrib-
dblink-get-pkey.html "PostgreSQL 9.5 - dblink_get_pkey") /
[9.4](/docs/9.4/contrib-dblink-get-pkey.html "PostgreSQL 9.4 -
dblink_get_pkey") / [9.3](/docs/9.3/contrib-dblink-get-pkey.html "PostgreSQL
9.3 - dblink_get_pkey") / [9.2](/docs/9.2/contrib-dblink-get-pkey.html
"PostgreSQL 9.2 - dblink_get_pkey") / [9.1](/docs/9.1/contrib-dblink-get-
pkey.html "PostgreSQL 9.1 - dblink_get_pkey") / [9.0](/docs/9.0/contrib-
dblink-get-pkey.html "PostgreSQL 9.0 - dblink_get_pkey") /
[8.4](/docs/8.4/contrib-dblink-get-pkey.html "PostgreSQL 8.4 -
dblink_get_pkey") / [8.3](/docs/8.3/contrib-dblink-get-pkey.html "PostgreSQL
8.3 - dblink_get_pkey")

__

dblink_get_pkey  
---  
[Prev](contrib-dblink-cancel-query.html "dblink_cancel_query")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") | F.12. dblink — connect to other PostgreSQL databases | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-dblink-build-sql-insert.html "dblink_build_sql_insert")  
  
* * *

## dblink_get_pkey

dblink_get_pkey — returns the positions and field names of a relation's
primary key fields

## Synopsis

    
    
    dblink_get_pkey(text relname) returns setof dblink_pkey_results
    

## Description

`dblink_get_pkey` provides information about the primary key of a relation in
the local database. This is sometimes useful in generating queries to be sent
to remote databases.

## Arguments

_`relname`_

    

Name of a local relation, for example `foo` or `myschema.mytab`. Include
double quotes if the name is mixed-case or contains special characters, for
example `"FooBar"`; without quotes, the string will be folded to lower case.

## Return Value

Returns one row for each primary key field, or no rows if the relation has no
primary key. The result row type is defined as

    
    
    CREATE TYPE dblink_pkey_results AS (position int, colname text);
    

The `position` column simply runs from 1 to _`N`_ ; it is the number of the
field within the primary key, not the number within the table's columns.

## Examples

    
    
    CREATE TABLE foobar (
        f1 int,
        f2 int,
        f3 int,
        PRIMARY KEY (f1, f2, f3)
    );
    CREATE TABLE
    
    SELECT * FROM dblink_get_pkey('foobar');
     position | colname
    ----------+---------
            1 | f1
            2 | f2
            3 | f3
    (3 rows)
    

* * *

[Prev](contrib-dblink-cancel-query.html "dblink_cancel_query")  | [Up](dblink.html "F.12. dblink — connect to other PostgreSQL databases") |  [Next](contrib-dblink-build-sql-insert.html "dblink_build_sql_insert")  
---|---|---  
dblink_cancel_query  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dblink_build_sql_insert  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/contrib-dblink-get-pkey.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

