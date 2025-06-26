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

Supported Versions: [Current](/docs/current/app-pgcontroldata.html "PostgreSQL
17 - pg_controldata") ([17](/docs/17/app-pgcontroldata.html "PostgreSQL 17 -
pg_controldata")) / [16](/docs/16/app-pgcontroldata.html "PostgreSQL 16 -
pg_controldata") / [15](/docs/15/app-pgcontroldata.html "PostgreSQL 15 -
pg_controldata") / [14](/docs/14/app-pgcontroldata.html "PostgreSQL 14 -
pg_controldata") / [13](/docs/13/app-pgcontroldata.html "PostgreSQL 13 -
pg_controldata")

Development Versions: [18](/docs/18/app-pgcontroldata.html "PostgreSQL 18 -
pg_controldata") / [devel](/docs/devel/app-pgcontroldata.html "PostgreSQL
devel - pg_controldata")

Unsupported versions: [12](/docs/12/app-pgcontroldata.html "PostgreSQL 12 -
pg_controldata") / [11](/docs/11/app-pgcontroldata.html "PostgreSQL 11 -
pg_controldata") / [10](/docs/10/app-pgcontroldata.html "PostgreSQL 10 -
pg_controldata") / [9.6](/docs/9.6/app-pgcontroldata.html "PostgreSQL 9.6 -
pg_controldata") / [9.5](/docs/9.5/app-pgcontroldata.html "PostgreSQL 9.5 -
pg_controldata") / [9.4](/docs/9.4/app-pgcontroldata.html "PostgreSQL 9.4 -
pg_controldata") / [9.3](/docs/9.3/app-pgcontroldata.html "PostgreSQL 9.3 -
pg_controldata") / [9.2](/docs/9.2/app-pgcontroldata.html "PostgreSQL 9.2 -
pg_controldata") / [9.1](/docs/9.1/app-pgcontroldata.html "PostgreSQL 9.1 -
pg_controldata") / [9.0](/docs/9.0/app-pgcontroldata.html "PostgreSQL 9.0 -
pg_controldata") / [8.4](/docs/8.4/app-pgcontroldata.html "PostgreSQL 8.4 -
pg_controldata") / [8.3](/docs/8.3/app-pgcontroldata.html "PostgreSQL 8.3 -
pg_controldata") / [8.2](/docs/8.2/app-pgcontroldata.html "PostgreSQL 8.2 -
pg_controldata") / [8.1](/docs/8.1/app-pgcontroldata.html "PostgreSQL 8.1 -
pg_controldata") / [8.0](/docs/8.0/app-pgcontroldata.html "PostgreSQL 8.0 -
pg_controldata") / [7.4](/docs/7.4/app-pgcontroldata.html "PostgreSQL 7.4 -
pg_controldata") / [7.3](/docs/7.3/app-pgcontroldata.html "PostgreSQL 7.3 -
pg_controldata")

__

pg_controldata  
---  
[Prev](app-pgchecksums.html "pg_checksums")  | [Up](reference-server.html "PostgreSQL Server Applications") | PostgreSQL Server Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](app-pg-ctl.html "pg_ctl")  
  
* * *

## pg_controldata

pg_controldata — display control information of a PostgreSQL database cluster

## Synopsis

`pg_controldata` [_`option`_] [[ `-D` | `--pgdata` ]_`datadir`_]

## Description

`pg_controldata` prints information initialized during `initdb`, such as the
catalog version. It also shows information about write-ahead logging and
checkpoint processing. This information is cluster-wide, and not specific to
any one database.

This utility can only be run by the user who initialized the cluster because
it requires read access to the data directory. You can specify the data
directory on the command line, or use the environment variable `PGDATA`. This
utility supports the options `-V` and `--version`, which print the
pg_controldata version and exit. It also supports options `-?` and `--help`,
which output the supported arguments.

## Environment

`PGDATA`

    

Default data directory location

`PG_COLOR`

    

Specifies whether to use color in diagnostic messages. Possible values are
`always`, `auto` and `never`.

* * *

[Prev](app-pgchecksums.html "pg_checksums")  | [Up](reference-server.html "PostgreSQL Server Applications") |  [Next](app-pg-ctl.html "pg_ctl")  
---|---|---  
pg_checksums  | [Home](index.html "PostgreSQL 16.9 Documentation") |  pg_ctl  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/app-pgcontroldata.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

