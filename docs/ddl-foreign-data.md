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

Supported Versions: [Current](/docs/current/ddl-foreign-data.html "PostgreSQL
17 - 5.12. Foreign Data") ([17](/docs/17/ddl-foreign-data.html "PostgreSQL 17
- 5.12. Foreign Data")) / [16](/docs/16/ddl-foreign-data.html "PostgreSQL 16 -
5.12. Foreign Data") / [15](/docs/15/ddl-foreign-data.html "PostgreSQL 15 -
5.12. Foreign Data") / [14](/docs/14/ddl-foreign-data.html "PostgreSQL 14 -
5.12. Foreign Data") / [13](/docs/13/ddl-foreign-data.html "PostgreSQL 13 -
5.12. Foreign Data")

Development Versions: [18](/docs/18/ddl-foreign-data.html "PostgreSQL 18 -
5.12. Foreign Data") / [devel](/docs/devel/ddl-foreign-data.html "PostgreSQL
devel - 5.12. Foreign Data")

Unsupported versions: [12](/docs/12/ddl-foreign-data.html "PostgreSQL 12 -
5.12. Foreign Data") / [11](/docs/11/ddl-foreign-data.html "PostgreSQL 11 -
5.12. Foreign Data") / [10](/docs/10/ddl-foreign-data.html "PostgreSQL 10 -
5.12. Foreign Data") / [9.6](/docs/9.6/ddl-foreign-data.html "PostgreSQL 9.6 -
5.12. Foreign Data") / [9.5](/docs/9.5/ddl-foreign-data.html "PostgreSQL 9.5 -
5.12. Foreign Data") / [9.4](/docs/9.4/ddl-foreign-data.html "PostgreSQL 9.4 -
5.12. Foreign Data") / [9.3](/docs/9.3/ddl-foreign-data.html "PostgreSQL 9.3 -
5.12. Foreign Data") / [9.2](/docs/9.2/ddl-foreign-data.html "PostgreSQL 9.2 -
5.12. Foreign Data") / [9.1](/docs/9.1/ddl-foreign-data.html "PostgreSQL 9.1 -
5.12. Foreign Data")

__

5.12. Foreign Data  
---  
[Prev](ddl-partitioning.html "5.11. Table Partitioning")  | [Up](ddl.html "Chapter 5. Data Definition") | Chapter 5. Data Definition | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ddl-others.html "5.13. Other Database Objects")  
  
* * *

## 5.12. Foreign Data #

PostgreSQL implements portions of the SQL/MED specification, allowing you to
access data that resides outside PostgreSQL using regular SQL queries. Such
data is referred to as _foreign data_. (Note that this usage is not to be
confused with foreign keys, which are a type of constraint within the
database.)

Foreign data is accessed with help from a _foreign data wrapper_. A foreign
data wrapper is a library that can communicate with an external data source,
hiding the details of connecting to the data source and obtaining data from
it. There are some foreign data wrappers available as `contrib` modules; see
[Appendix F](contrib.html "Appendix F. Additional Supplied Modules and
Extensions"). Other kinds of foreign data wrappers might be found as third
party products. If none of the existing foreign data wrappers suit your needs,
you can write your own; see [Chapter 59](fdwhandler.html "Chapter 59. Writing
a Foreign Data Wrapper").

To access foreign data, you need to create a _foreign server_ object, which
defines how to connect to a particular external data source according to the
set of options used by its supporting foreign data wrapper. Then you need to
create one or more _foreign tables_ , which define the structure of the remote
data. A foreign table can be used in queries just like a normal table, but a
foreign table has no storage in the PostgreSQL server. Whenever it is used,
PostgreSQL asks the foreign data wrapper to fetch data from the external
source, or transmit data to the external source in the case of update
commands.

Accessing remote data may require authenticating to the external data source.
This information can be provided by a _user mapping_ , which can provide
additional data such as user names and passwords based on the current
PostgreSQL role.

For additional information, see [CREATE FOREIGN DATA WRAPPER](sql-
createforeigndatawrapper.html "CREATE FOREIGN DATA WRAPPER"), [CREATE
SERVER](sql-createserver.html "CREATE SERVER"), [CREATE USER MAPPING](sql-
createusermapping.html "CREATE USER MAPPING"), [CREATE FOREIGN TABLE](sql-
createforeigntable.html "CREATE FOREIGN TABLE"), and [IMPORT FOREIGN
SCHEMA](sql-importforeignschema.html "IMPORT FOREIGN SCHEMA").

* * *

[Prev](ddl-partitioning.html "5.11. Table Partitioning")  | [Up](ddl.html "Chapter 5. Data Definition") |  [Next](ddl-others.html "5.13. Other Database Objects")  
---|---|---  
5.11. Table Partitioning  | [Home](index.html "PostgreSQL 16.9 Documentation") |  5.13. Other Database Objects  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ddl-foreign-data.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

