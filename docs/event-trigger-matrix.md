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

Supported Versions: [Current](/docs/current/event-trigger-matrix.html
"PostgreSQL 17 - 40.2. Event Trigger Firing Matrix") ([17](/docs/17/event-
trigger-matrix.html "PostgreSQL 17 - 40.2. Event Trigger Firing Matrix")) /
[16](/docs/16/event-trigger-matrix.html "PostgreSQL 16 - 40.2. Event Trigger
Firing Matrix") / [15](/docs/15/event-trigger-matrix.html "PostgreSQL 15 -
40.2. Event Trigger Firing Matrix") / [14](/docs/14/event-trigger-matrix.html
"PostgreSQL 14 - 40.2. Event Trigger Firing Matrix") / [13](/docs/13/event-
trigger-matrix.html "PostgreSQL 13 - 40.2. Event Trigger Firing Matrix")

Unsupported versions: [12](/docs/12/event-trigger-matrix.html "PostgreSQL 12 -
40.2. Event Trigger Firing Matrix") / [11](/docs/11/event-trigger-matrix.html
"PostgreSQL 11 - 40.2. Event Trigger Firing Matrix") / [10](/docs/10/event-
trigger-matrix.html "PostgreSQL 10 - 40.2. Event Trigger Firing Matrix") /
[9.6](/docs/9.6/event-trigger-matrix.html "PostgreSQL 9.6 - 40.2. Event
Trigger Firing Matrix") / [9.5](/docs/9.5/event-trigger-matrix.html
"PostgreSQL 9.5 - 40.2. Event Trigger Firing Matrix") / [9.4](/docs/9.4/event-
trigger-matrix.html "PostgreSQL 9.4 - 40.2. Event Trigger Firing Matrix") /
[9.3](/docs/9.3/event-trigger-matrix.html "PostgreSQL 9.3 - 40.2. Event
Trigger Firing Matrix")

__

40.2. Event Trigger Firing Matrix  
---  
[Prev](event-trigger-definition.html "40.1. Overview of Event Trigger Behavior")  | [Up](event-triggers.html "Chapter 40. Event Triggers") | Chapter 40. Event Triggers | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](event-trigger-interface.html "40.3. Writing Event Trigger Functions in C")  
  
* * *

## 40.2. Event Trigger Firing Matrix #

[Table 40.1](event-trigger-matrix.html#EVENT-TRIGGER-BY-COMMAND-TAG
"Table 40.1. Event Trigger Support by Command Tag") lists all commands for
which event triggers are supported.

**Table  40.1. Event Trigger Support by Command Tag**

Command Tag | `ddl_​command_​start` | `ddl_​command_​end` | `sql_​drop` | `table_​rewrite` | Notes  
---|---|---|---|---|---  
`ALTER AGGREGATE` | `X` | `X` | `-` | `-` |    
`ALTER COLLATION` | `X` | `X` | `-` | `-` |    
`ALTER CONVERSION` | `X` | `X` | `-` | `-` |    
`ALTER DOMAIN` | `X` | `X` | `-` | `-` |    
`ALTER DEFAULT PRIVILEGES` | `X` | `X` | `-` | `-` |    
`ALTER EXTENSION` | `X` | `X` | `-` | `-` |    
`ALTER FOREIGN DATA WRAPPER` | `X` | `X` | `-` | `-` |    
`ALTER FOREIGN TABLE` | `X` | `X` | `X` | `-` |    
`ALTER FUNCTION` | `X` | `X` | `-` | `-` |    
`ALTER LANGUAGE` | `X` | `X` | `-` | `-` |    
`ALTER LARGE OBJECT` | `X` | `X` | `-` | `-` |    
`ALTER MATERIALIZED VIEW` | `X` | `X` | `-` | `X` |    
`ALTER OPERATOR` | `X` | `X` | `-` | `-` |    
`ALTER OPERATOR CLASS` | `X` | `X` | `-` | `-` |    
`ALTER OPERATOR FAMILY` | `X` | `X` | `-` | `-` |    
`ALTER POLICY` | `X` | `X` | `-` | `-` |    
`ALTER PROCEDURE` | `X` | `X` | `-` | `-` |    
`ALTER PUBLICATION` | `X` | `X` | `-` | `-` |    
`ALTER ROUTINE` | `X` | `X` | `-` | `-` |    
`ALTER SCHEMA` | `X` | `X` | `-` | `-` |    
`ALTER SEQUENCE` | `X` | `X` | `-` | `-` |    
`ALTER SERVER` | `X` | `X` | `-` | `-` |    
`ALTER STATISTICS` | `X` | `X` | `-` | `-` |    
`ALTER SUBSCRIPTION` | `X` | `X` | `-` | `-` |    
`ALTER TABLE` | `X` | `X` | `X` | `X` |    
`ALTER TEXT SEARCH CONFIGURATION` | `X` | `X` | `-` | `-` |    
`ALTER TEXT SEARCH DICTIONARY` | `X` | `X` | `-` | `-` |    
`ALTER TEXT SEARCH PARSER` | `X` | `X` | `-` | `-` |    
`ALTER TEXT SEARCH TEMPLATE` | `X` | `X` | `-` | `-` |    
`ALTER TRIGGER` | `X` | `X` | `-` | `-` |    
`ALTER TYPE` | `X` | `X` | `-` | `X` |    
`ALTER USER MAPPING` | `X` | `X` | `-` | `-` |    
`ALTER VIEW` | `X` | `X` | `-` | `-` |    
`COMMENT` | `X` | `X` | `-` | `-` | Only for local objects  
`CREATE ACCESS METHOD` | `X` | `X` | `-` | `-` |    
`CREATE AGGREGATE` | `X` | `X` | `-` | `-` |    
`CREATE CAST` | `X` | `X` | `-` | `-` |    
`CREATE COLLATION` | `X` | `X` | `-` | `-` |    
`CREATE CONVERSION` | `X` | `X` | `-` | `-` |    
`CREATE DOMAIN` | `X` | `X` | `-` | `-` |    
`CREATE EXTENSION` | `X` | `X` | `-` | `-` |    
`CREATE FOREIGN DATA WRAPPER` | `X` | `X` | `-` | `-` |    
`CREATE FOREIGN TABLE` | `X` | `X` | `-` | `-` |    
`CREATE FUNCTION` | `X` | `X` | `-` | `-` |    
`CREATE INDEX` | `X` | `X` | `-` | `-` |    
`CREATE LANGUAGE` | `X` | `X` | `-` | `-` |    
`CREATE MATERIALIZED VIEW` | `X` | `X` | `-` | `-` |    
`CREATE OPERATOR` | `X` | `X` | `-` | `-` |    
`CREATE OPERATOR CLASS` | `X` | `X` | `-` | `-` |    
`CREATE OPERATOR FAMILY` | `X` | `X` | `-` | `-` |    
`CREATE POLICY` | `X` | `X` | `-` | `-` |    
`CREATE PROCEDURE` | `X` | `X` | `-` | `-` |    
`CREATE PUBLICATION` | `X` | `X` | `-` | `-` |    
`CREATE RULE` | `X` | `X` | `-` | `-` |    
`CREATE SCHEMA` | `X` | `X` | `-` | `-` |    
`CREATE SEQUENCE` | `X` | `X` | `-` | `-` |    
`CREATE SERVER` | `X` | `X` | `-` | `-` |    
`CREATE STATISTICS` | `X` | `X` | `-` | `-` |    
`CREATE SUBSCRIPTION` | `X` | `X` | `-` | `-` |    
`CREATE TABLE` | `X` | `X` | `-` | `-` |    
`CREATE TABLE AS` | `X` | `X` | `-` | `-` |    
`CREATE TEXT SEARCH CONFIGURATION` | `X` | `X` | `-` | `-` |    
`CREATE TEXT SEARCH DICTIONARY` | `X` | `X` | `-` | `-` |    
`CREATE TEXT SEARCH PARSER` | `X` | `X` | `-` | `-` |    
`CREATE TEXT SEARCH TEMPLATE` | `X` | `X` | `-` | `-` |    
`CREATE TRIGGER` | `X` | `X` | `-` | `-` |    
`CREATE TYPE` | `X` | `X` | `-` | `-` |    
`CREATE USER MAPPING` | `X` | `X` | `-` | `-` |    
`CREATE VIEW` | `X` | `X` | `-` | `-` |    
`DROP ACCESS METHOD` | `X` | `X` | `X` | `-` |    
`DROP AGGREGATE` | `X` | `X` | `X` | `-` |    
`DROP CAST` | `X` | `X` | `X` | `-` |    
`DROP COLLATION` | `X` | `X` | `X` | `-` |    
`DROP CONVERSION` | `X` | `X` | `X` | `-` |    
`DROP DOMAIN` | `X` | `X` | `X` | `-` |    
`DROP EXTENSION` | `X` | `X` | `X` | `-` |    
`DROP FOREIGN DATA WRAPPER` | `X` | `X` | `X` | `-` |    
`DROP FOREIGN TABLE` | `X` | `X` | `X` | `-` |    
`DROP FUNCTION` | `X` | `X` | `X` | `-` |    
`DROP INDEX` | `X` | `X` | `X` | `-` |    
`DROP LANGUAGE` | `X` | `X` | `X` | `-` |    
`DROP MATERIALIZED VIEW` | `X` | `X` | `X` | `-` |    
`DROP OPERATOR` | `X` | `X` | `X` | `-` |    
`DROP OPERATOR CLASS` | `X` | `X` | `X` | `-` |    
`DROP OPERATOR FAMILY` | `X` | `X` | `X` | `-` |    
`DROP OWNED` | `X` | `X` | `X` | `-` |    
`DROP POLICY` | `X` | `X` | `X` | `-` |    
`DROP PROCEDURE` | `X` | `X` | `X` | `-` |    
`DROP PUBLICATION` | `X` | `X` | `X` | `-` |    
`DROP ROUTINE` | `X` | `X` | `X` | `-` |    
`DROP RULE` | `X` | `X` | `X` | `-` |    
`DROP SCHEMA` | `X` | `X` | `X` | `-` |    
`DROP SEQUENCE` | `X` | `X` | `X` | `-` |    
`DROP SERVER` | `X` | `X` | `X` | `-` |    
`DROP STATISTICS` | `X` | `X` | `X` | `-` |    
`DROP SUBSCRIPTION` | `X` | `X` | `X` | `-` |    
`DROP TABLE` | `X` | `X` | `X` | `-` |    
`DROP TEXT SEARCH CONFIGURATION` | `X` | `X` | `X` | `-` |    
`DROP TEXT SEARCH DICTIONARY` | `X` | `X` | `X` | `-` |    
`DROP TEXT SEARCH PARSER` | `X` | `X` | `X` | `-` |    
`DROP TEXT SEARCH TEMPLATE` | `X` | `X` | `X` | `-` |    
`DROP TRIGGER` | `X` | `X` | `X` | `-` |    
`DROP TYPE` | `X` | `X` | `X` | `-` |    
`DROP USER MAPPING` | `X` | `X` | `X` | `-` |    
`DROP VIEW` | `X` | `X` | `X` | `-` |    
`GRANT` | `X` | `X` | `-` | `-` | Only for local objects  
`IMPORT FOREIGN SCHEMA` | `X` | `X` | `-` | `-` |    
`REFRESH MATERIALIZED VIEW` | `X` | `X` | `-` | `-` |    
`REVOKE` | `X` | `X` | `-` | `-` | Only for local objects  
`SECURITY LABEL` | `X` | `X` | `-` | `-` | Only for local objects  
`SELECT INTO` | `X` | `X` | `-` | `-` |    
  
  

* * *

[Prev](event-trigger-definition.html "40.1. Overview of Event Trigger Behavior")  | [Up](event-triggers.html "Chapter 40. Event Triggers") |  [Next](event-trigger-interface.html "40.3. Writing Event Trigger Functions in C")  
---|---|---  
40.1. Overview of Event Trigger Behavior  | [Home](index.html "PostgreSQL 16.9 Documentation") |  40.3. Writing Event Trigger Functions in C  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/event-trigger-matrix.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

