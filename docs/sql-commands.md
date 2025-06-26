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

Supported Versions: [Current](/docs/current/sql-commands.html "PostgreSQL 17 -
SQL Commands") ([17](/docs/17/sql-commands.html "PostgreSQL 17 - SQL
Commands")) / [16](/docs/16/sql-commands.html "PostgreSQL 16 - SQL Commands")
/ [15](/docs/15/sql-commands.html "PostgreSQL 15 - SQL Commands") /
[14](/docs/14/sql-commands.html "PostgreSQL 14 - SQL Commands") /
[13](/docs/13/sql-commands.html "PostgreSQL 13 - SQL Commands")

Development Versions: [18](/docs/18/sql-commands.html "PostgreSQL 18 - SQL
Commands") / [devel](/docs/devel/sql-commands.html "PostgreSQL devel - SQL
Commands")

Unsupported versions: [12](/docs/12/sql-commands.html "PostgreSQL 12 - SQL
Commands") / [11](/docs/11/sql-commands.html "PostgreSQL 11 - SQL Commands") /
[10](/docs/10/sql-commands.html "PostgreSQL 10 - SQL Commands") /
[9.6](/docs/9.6/sql-commands.html "PostgreSQL 9.6 - SQL Commands") /
[9.5](/docs/9.5/sql-commands.html "PostgreSQL 9.5 - SQL Commands") /
[9.4](/docs/9.4/sql-commands.html "PostgreSQL 9.4 - SQL Commands") /
[9.3](/docs/9.3/sql-commands.html "PostgreSQL 9.3 - SQL Commands") /
[9.2](/docs/9.2/sql-commands.html "PostgreSQL 9.2 - SQL Commands") /
[9.1](/docs/9.1/sql-commands.html "PostgreSQL 9.1 - SQL Commands") /
[9.0](/docs/9.0/sql-commands.html "PostgreSQL 9.0 - SQL Commands") /
[8.4](/docs/8.4/sql-commands.html "PostgreSQL 8.4 - SQL Commands") /
[8.3](/docs/8.3/sql-commands.html "PostgreSQL 8.3 - SQL Commands") /
[8.2](/docs/8.2/sql-commands.html "PostgreSQL 8.2 - SQL Commands") /
[8.1](/docs/8.1/sql-commands.html "PostgreSQL 8.1 - SQL Commands") /
[8.0](/docs/8.0/sql-commands.html "PostgreSQL 8.0 - SQL Commands") /
[7.4](/docs/7.4/sql-commands.html "PostgreSQL 7.4 - SQL Commands") /
[7.3](/docs/7.3/sql-commands.html "PostgreSQL 7.3 - SQL Commands") /
[7.2](/docs/7.2/sql-commands.html "PostgreSQL 7.2 - SQL Commands") /
[7.1](/docs/7.1/sql-commands.html "PostgreSQL 7.1 - SQL Commands")

__

SQL Commands  
---  
[Prev](reference.html "Part VI. Reference")  | [Up](reference.html "Part VI. Reference") | Part VI. Reference | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-abort.html "ABORT")  
  
* * *

# SQL Commands

* * *

This part contains reference information for the SQL commands supported by
PostgreSQL. By “SQL” the language in general is meant; information about the
standards conformance and compatibility of each command can be found on the
respective reference page.

**Table of Contents**

[ABORT](sql-abort.html) — abort the current transaction

[ALTER AGGREGATE](sql-alteraggregate.html) — change the definition of an
aggregate function

[ALTER COLLATION](sql-altercollation.html) — change the definition of a
collation

[ALTER CONVERSION](sql-alterconversion.html) — change the definition of a
conversion

[ALTER DATABASE](sql-alterdatabase.html) — change a database

[ALTER DEFAULT PRIVILEGES](sql-alterdefaultprivileges.html) — define default
access privileges

[ALTER DOMAIN](sql-alterdomain.html) — change the definition of a domain

[ALTER EVENT TRIGGER](sql-altereventtrigger.html) — change the definition of
an event trigger

[ALTER EXTENSION](sql-alterextension.html) — change the definition of an
extension

[ALTER FOREIGN DATA WRAPPER](sql-alterforeigndatawrapper.html) — change the
definition of a foreign-data wrapper

[ALTER FOREIGN TABLE](sql-alterforeigntable.html) — change the definition of a
foreign table

[ALTER FUNCTION](sql-alterfunction.html) — change the definition of a function

[ALTER GROUP](sql-altergroup.html) — change role name or membership

[ALTER INDEX](sql-alterindex.html) — change the definition of an index

[ALTER LANGUAGE](sql-alterlanguage.html) — change the definition of a
procedural language

[ALTER LARGE OBJECT](sql-alterlargeobject.html) — change the definition of a
large object

[ALTER MATERIALIZED VIEW](sql-altermaterializedview.html) — change the
definition of a materialized view

[ALTER OPERATOR](sql-alteroperator.html) — change the definition of an
operator

[ALTER OPERATOR CLASS](sql-alteropclass.html) — change the definition of an
operator class

[ALTER OPERATOR FAMILY](sql-alteropfamily.html) — change the definition of an
operator family

[ALTER POLICY](sql-alterpolicy.html) — change the definition of a row-level
security policy

[ALTER PROCEDURE](sql-alterprocedure.html) — change the definition of a
procedure

[ALTER PUBLICATION](sql-alterpublication.html) — change the definition of a
publication

[ALTER ROLE](sql-alterrole.html) — change a database role

[ALTER ROUTINE](sql-alterroutine.html) — change the definition of a routine

[ALTER RULE](sql-alterrule.html) — change the definition of a rule

[ALTER SCHEMA](sql-alterschema.html) — change the definition of a schema

[ALTER SEQUENCE](sql-altersequence.html) — change the definition of a sequence
generator

[ALTER SERVER](sql-alterserver.html) — change the definition of a foreign
server

[ALTER STATISTICS](sql-alterstatistics.html) — change the definition of an
extended statistics object

[ALTER SUBSCRIPTION](sql-altersubscription.html) — change the definition of a
subscription

[ALTER SYSTEM](sql-altersystem.html) — change a server configuration parameter

[ALTER TABLE](sql-altertable.html) — change the definition of a table

[ALTER TABLESPACE](sql-altertablespace.html) — change the definition of a
tablespace

[ALTER TEXT SEARCH CONFIGURATION](sql-altertsconfig.html) — change the
definition of a text search configuration

[ALTER TEXT SEARCH DICTIONARY](sql-altertsdictionary.html) — change the
definition of a text search dictionary

[ALTER TEXT SEARCH PARSER](sql-altertsparser.html) — change the definition of
a text search parser

[ALTER TEXT SEARCH TEMPLATE](sql-altertstemplate.html) — change the definition
of a text search template

[ALTER TRIGGER](sql-altertrigger.html) — change the definition of a trigger

[ALTER TYPE](sql-altertype.html) — change the definition of a type

[ALTER USER](sql-alteruser.html) — change a database role

[ALTER USER MAPPING](sql-alterusermapping.html) — change the definition of a
user mapping

[ALTER VIEW](sql-alterview.html) — change the definition of a view

[ANALYZE](sql-analyze.html) — collect statistics about a database

[BEGIN](sql-begin.html) — start a transaction block

[CALL](sql-call.html) — invoke a procedure

[CHECKPOINT](sql-checkpoint.html) — force a write-ahead log checkpoint

[CLOSE](sql-close.html) — close a cursor

[CLUSTER](sql-cluster.html) — cluster a table according to an index

[COMMENT](sql-comment.html) — define or change the comment of an object

[COMMIT](sql-commit.html) — commit the current transaction

[COMMIT PREPARED](sql-commit-prepared.html) — commit a transaction that was
earlier prepared for two-phase commit

[COPY](sql-copy.html) — copy data between a file and a table

[CREATE ACCESS METHOD](sql-create-access-method.html) — define a new access
method

[CREATE AGGREGATE](sql-createaggregate.html) — define a new aggregate function

[CREATE CAST](sql-createcast.html) — define a new cast

[CREATE COLLATION](sql-createcollation.html) — define a new collation

[CREATE CONVERSION](sql-createconversion.html) — define a new encoding
conversion

[CREATE DATABASE](sql-createdatabase.html) — create a new database

[CREATE DOMAIN](sql-createdomain.html) — define a new domain

[CREATE EVENT TRIGGER](sql-createeventtrigger.html) — define a new event
trigger

[CREATE EXTENSION](sql-createextension.html) — install an extension

[CREATE FOREIGN DATA WRAPPER](sql-createforeigndatawrapper.html) — define a
new foreign-data wrapper

[CREATE FOREIGN TABLE](sql-createforeigntable.html) — define a new foreign
table

[CREATE FUNCTION](sql-createfunction.html) — define a new function

[CREATE GROUP](sql-creategroup.html) — define a new database role

[CREATE INDEX](sql-createindex.html) — define a new index

[CREATE LANGUAGE](sql-createlanguage.html) — define a new procedural language

[CREATE MATERIALIZED VIEW](sql-creatematerializedview.html) — define a new
materialized view

[CREATE OPERATOR](sql-createoperator.html) — define a new operator

[CREATE OPERATOR CLASS](sql-createopclass.html) — define a new operator class

[CREATE OPERATOR FAMILY](sql-createopfamily.html) — define a new operator
family

[CREATE POLICY](sql-createpolicy.html) — define a new row-level security
policy for a table

[CREATE PROCEDURE](sql-createprocedure.html) — define a new procedure

[CREATE PUBLICATION](sql-createpublication.html) — define a new publication

[CREATE ROLE](sql-createrole.html) — define a new database role

[CREATE RULE](sql-createrule.html) — define a new rewrite rule

[CREATE SCHEMA](sql-createschema.html) — define a new schema

[CREATE SEQUENCE](sql-createsequence.html) — define a new sequence generator

[CREATE SERVER](sql-createserver.html) — define a new foreign server

[CREATE STATISTICS](sql-createstatistics.html) — define extended statistics

[CREATE SUBSCRIPTION](sql-createsubscription.html) — define a new subscription

[CREATE TABLE](sql-createtable.html) — define a new table

[CREATE TABLE AS](sql-createtableas.html) — define a new table from the
results of a query

[CREATE TABLESPACE](sql-createtablespace.html) — define a new tablespace

[CREATE TEXT SEARCH CONFIGURATION](sql-createtsconfig.html) — define a new
text search configuration

[CREATE TEXT SEARCH DICTIONARY](sql-createtsdictionary.html) — define a new
text search dictionary

[CREATE TEXT SEARCH PARSER](sql-createtsparser.html) — define a new text
search parser

[CREATE TEXT SEARCH TEMPLATE](sql-createtstemplate.html) — define a new text
search template

[CREATE TRANSFORM](sql-createtransform.html) — define a new transform

[CREATE TRIGGER](sql-createtrigger.html) — define a new trigger

[CREATE TYPE](sql-createtype.html) — define a new data type

[CREATE USER](sql-createuser.html) — define a new database role

[CREATE USER MAPPING](sql-createusermapping.html) — define a new mapping of a
user to a foreign server

[CREATE VIEW](sql-createview.html) — define a new view

[DEALLOCATE](sql-deallocate.html) — deallocate a prepared statement

[DECLARE](sql-declare.html) — define a cursor

[DELETE](sql-delete.html) — delete rows of a table

[DISCARD](sql-discard.html) — discard session state

[DO](sql-do.html) — execute an anonymous code block

[DROP ACCESS METHOD](sql-drop-access-method.html) — remove an access method

[DROP AGGREGATE](sql-dropaggregate.html) — remove an aggregate function

[DROP CAST](sql-dropcast.html) — remove a cast

[DROP COLLATION](sql-dropcollation.html) — remove a collation

[DROP CONVERSION](sql-dropconversion.html) — remove a conversion

[DROP DATABASE](sql-dropdatabase.html) — remove a database

[DROP DOMAIN](sql-dropdomain.html) — remove a domain

[DROP EVENT TRIGGER](sql-dropeventtrigger.html) — remove an event trigger

[DROP EXTENSION](sql-dropextension.html) — remove an extension

[DROP FOREIGN DATA WRAPPER](sql-dropforeigndatawrapper.html) — remove a
foreign-data wrapper

[DROP FOREIGN TABLE](sql-dropforeigntable.html) — remove a foreign table

[DROP FUNCTION](sql-dropfunction.html) — remove a function

[DROP GROUP](sql-dropgroup.html) — remove a database role

[DROP INDEX](sql-dropindex.html) — remove an index

[DROP LANGUAGE](sql-droplanguage.html) — remove a procedural language

[DROP MATERIALIZED VIEW](sql-dropmaterializedview.html) — remove a
materialized view

[DROP OPERATOR](sql-dropoperator.html) — remove an operator

[DROP OPERATOR CLASS](sql-dropopclass.html) — remove an operator class

[DROP OPERATOR FAMILY](sql-dropopfamily.html) — remove an operator family

[DROP OWNED](sql-drop-owned.html) — remove database objects owned by a
database role

[DROP POLICY](sql-droppolicy.html) — remove a row-level security policy from a
table

[DROP PROCEDURE](sql-dropprocedure.html) — remove a procedure

[DROP PUBLICATION](sql-droppublication.html) — remove a publication

[DROP ROLE](sql-droprole.html) — remove a database role

[DROP ROUTINE](sql-droproutine.html) — remove a routine

[DROP RULE](sql-droprule.html) — remove a rewrite rule

[DROP SCHEMA](sql-dropschema.html) — remove a schema

[DROP SEQUENCE](sql-dropsequence.html) — remove a sequence

[DROP SERVER](sql-dropserver.html) — remove a foreign server descriptor

[DROP STATISTICS](sql-dropstatistics.html) — remove extended statistics

[DROP SUBSCRIPTION](sql-dropsubscription.html) — remove a subscription

[DROP TABLE](sql-droptable.html) — remove a table

[DROP TABLESPACE](sql-droptablespace.html) — remove a tablespace

[DROP TEXT SEARCH CONFIGURATION](sql-droptsconfig.html) — remove a text search
configuration

[DROP TEXT SEARCH DICTIONARY](sql-droptsdictionary.html) — remove a text
search dictionary

[DROP TEXT SEARCH PARSER](sql-droptsparser.html) — remove a text search parser

[DROP TEXT SEARCH TEMPLATE](sql-droptstemplate.html) — remove a text search
template

[DROP TRANSFORM](sql-droptransform.html) — remove a transform

[DROP TRIGGER](sql-droptrigger.html) — remove a trigger

[DROP TYPE](sql-droptype.html) — remove a data type

[DROP USER](sql-dropuser.html) — remove a database role

[DROP USER MAPPING](sql-dropusermapping.html) — remove a user mapping for a
foreign server

[DROP VIEW](sql-dropview.html) — remove a view

[END](sql-end.html) — commit the current transaction

[EXECUTE](sql-execute.html) — execute a prepared statement

[EXPLAIN](sql-explain.html) — show the execution plan of a statement

[FETCH](sql-fetch.html) — retrieve rows from a query using a cursor

[GRANT](sql-grant.html) — define access privileges

[IMPORT FOREIGN SCHEMA](sql-importforeignschema.html) — import table
definitions from a foreign server

[INSERT](sql-insert.html) — create new rows in a table

[LISTEN](sql-listen.html) — listen for a notification

[LOAD](sql-load.html) — load a shared library file

[LOCK](sql-lock.html) — lock a table

[MERGE](sql-merge.html) — conditionally insert, update, or delete rows of a
table

[MOVE](sql-move.html) — position a cursor

[NOTIFY](sql-notify.html) — generate a notification

[PREPARE](sql-prepare.html) — prepare a statement for execution

[PREPARE TRANSACTION](sql-prepare-transaction.html) — prepare the current
transaction for two-phase commit

[REASSIGN OWNED](sql-reassign-owned.html) — change the ownership of database
objects owned by a database role

[REFRESH MATERIALIZED VIEW](sql-refreshmaterializedview.html) — replace the
contents of a materialized view

[REINDEX](sql-reindex.html) — rebuild indexes

[RELEASE SAVEPOINT](sql-release-savepoint.html) — release a previously defined
savepoint

[RESET](sql-reset.html) — restore the value of a run-time parameter to the
default value

[REVOKE](sql-revoke.html) — remove access privileges

[ROLLBACK](sql-rollback.html) — abort the current transaction

[ROLLBACK PREPARED](sql-rollback-prepared.html) — cancel a transaction that
was earlier prepared for two-phase commit

[ROLLBACK TO SAVEPOINT](sql-rollback-to.html) — roll back to a savepoint

[SAVEPOINT](sql-savepoint.html) — define a new savepoint within the current
transaction

[SECURITY LABEL](sql-security-label.html) — define or change a security label
applied to an object

[SELECT](sql-select.html) — retrieve rows from a table or view

[SELECT INTO](sql-selectinto.html) — define a new table from the results of a
query

[SET](sql-set.html) — change a run-time parameter

[SET CONSTRAINTS](sql-set-constraints.html) — set constraint check timing for
the current transaction

[SET ROLE](sql-set-role.html) — set the current user identifier of the current
session

[SET SESSION AUTHORIZATION](sql-set-session-authorization.html) — set the
session user identifier and the current user identifier of the current session

[SET TRANSACTION](sql-set-transaction.html) — set the characteristics of the
current transaction

[SHOW](sql-show.html) — show the value of a run-time parameter

[START TRANSACTION](sql-start-transaction.html) — start a transaction block

[TRUNCATE](sql-truncate.html) — empty a table or set of tables

[UNLISTEN](sql-unlisten.html) — stop listening for a notification

[UPDATE](sql-update.html) — update rows of a table

[VACUUM](sql-vacuum.html) — garbage-collect and optionally analyze a database

[VALUES](sql-values.html) — compute a set of rows

* * *

[Prev](reference.html "Part VI. Reference")  | [Up](reference.html "Part VI. Reference") |  [Next](sql-abort.html "ABORT")  
---|---|---  
Part VI. Reference  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ABORT  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-commands.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

