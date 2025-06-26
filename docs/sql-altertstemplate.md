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

Supported Versions: [Current](/docs/current/sql-altertstemplate.html
"PostgreSQL 17 - ALTER TEXT SEARCH TEMPLATE") ([17](/docs/17/sql-
altertstemplate.html "PostgreSQL 17 - ALTER TEXT SEARCH TEMPLATE")) /
[16](/docs/16/sql-altertstemplate.html "PostgreSQL 16 - ALTER TEXT SEARCH
TEMPLATE") / [15](/docs/15/sql-altertstemplate.html "PostgreSQL 15 - ALTER
TEXT SEARCH TEMPLATE") / [14](/docs/14/sql-altertstemplate.html "PostgreSQL 14
- ALTER TEXT SEARCH TEMPLATE") / [13](/docs/13/sql-altertstemplate.html
"PostgreSQL 13 - ALTER TEXT SEARCH TEMPLATE")

Development Versions: [18](/docs/18/sql-altertstemplate.html "PostgreSQL 18 -
ALTER TEXT SEARCH TEMPLATE") / [devel](/docs/devel/sql-altertstemplate.html
"PostgreSQL devel - ALTER TEXT SEARCH TEMPLATE")

Unsupported versions: [12](/docs/12/sql-altertstemplate.html "PostgreSQL 12 -
ALTER TEXT SEARCH TEMPLATE") / [11](/docs/11/sql-altertstemplate.html
"PostgreSQL 11 - ALTER TEXT SEARCH TEMPLATE") / [10](/docs/10/sql-
altertstemplate.html "PostgreSQL 10 - ALTER TEXT SEARCH TEMPLATE") /
[9.6](/docs/9.6/sql-altertstemplate.html "PostgreSQL 9.6 - ALTER TEXT SEARCH
TEMPLATE") / [9.5](/docs/9.5/sql-altertstemplate.html "PostgreSQL 9.5 - ALTER
TEXT SEARCH TEMPLATE") / [9.4](/docs/9.4/sql-altertstemplate.html "PostgreSQL
9.4 - ALTER TEXT SEARCH TEMPLATE") / [9.3](/docs/9.3/sql-altertstemplate.html
"PostgreSQL 9.3 - ALTER TEXT SEARCH TEMPLATE") / [9.2](/docs/9.2/sql-
altertstemplate.html "PostgreSQL 9.2 - ALTER TEXT SEARCH TEMPLATE") /
[9.1](/docs/9.1/sql-altertstemplate.html "PostgreSQL 9.1 - ALTER TEXT SEARCH
TEMPLATE") / [9.0](/docs/9.0/sql-altertstemplate.html "PostgreSQL 9.0 - ALTER
TEXT SEARCH TEMPLATE") / [8.4](/docs/8.4/sql-altertstemplate.html "PostgreSQL
8.4 - ALTER TEXT SEARCH TEMPLATE") / [8.3](/docs/8.3/sql-altertstemplate.html
"PostgreSQL 8.3 - ALTER TEXT SEARCH TEMPLATE")

__

ALTER TEXT SEARCH TEMPLATE  
---  
[Prev](sql-altertsparser.html "ALTER TEXT SEARCH PARSER")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-altertrigger.html "ALTER TRIGGER")  
  
* * *

## ALTER TEXT SEARCH TEMPLATE

ALTER TEXT SEARCH TEMPLATE — change the definition of a text search template

## Synopsis

    
    
    ALTER TEXT SEARCH TEMPLATE _name_ RENAME TO _new_name_
    ALTER TEXT SEARCH TEMPLATE _name_ SET SCHEMA _new_schema_
    

## Description

`ALTER TEXT SEARCH TEMPLATE` changes the definition of a text search template.
Currently, the only supported functionality is to change the template's name.

You must be a superuser to use `ALTER TEXT SEARCH TEMPLATE`.

## Parameters

_`name`_

    

The name (optionally schema-qualified) of an existing text search template.

_`new_name`_

    

The new name of the text search template.

_`new_schema`_

    

The new schema for the text search template.

## Compatibility

There is no `ALTER TEXT SEARCH TEMPLATE` statement in the SQL standard.

## See Also

[CREATE TEXT SEARCH TEMPLATE](sql-createtstemplate.html "CREATE TEXT SEARCH
TEMPLATE"), [DROP TEXT SEARCH TEMPLATE](sql-droptstemplate.html "DROP TEXT
SEARCH TEMPLATE")

* * *

[Prev](sql-altertsparser.html "ALTER TEXT SEARCH PARSER")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-altertrigger.html "ALTER TRIGGER")  
---|---|---  
ALTER TEXT SEARCH PARSER  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER TRIGGER  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-altertstemplate.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

