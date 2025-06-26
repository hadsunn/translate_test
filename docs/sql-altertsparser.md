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

Supported Versions: [Current](/docs/current/sql-altertsparser.html "PostgreSQL
17 - ALTER TEXT SEARCH PARSER") ([17](/docs/17/sql-altertsparser.html
"PostgreSQL 17 - ALTER TEXT SEARCH PARSER")) / [16](/docs/16/sql-
altertsparser.html "PostgreSQL 16 - ALTER TEXT SEARCH PARSER") /
[15](/docs/15/sql-altertsparser.html "PostgreSQL 15 - ALTER TEXT SEARCH
PARSER") / [14](/docs/14/sql-altertsparser.html "PostgreSQL 14 - ALTER TEXT
SEARCH PARSER") / [13](/docs/13/sql-altertsparser.html "PostgreSQL 13 - ALTER
TEXT SEARCH PARSER")

Development Versions: [18](/docs/18/sql-altertsparser.html "PostgreSQL 18 -
ALTER TEXT SEARCH PARSER") / [devel](/docs/devel/sql-altertsparser.html
"PostgreSQL devel - ALTER TEXT SEARCH PARSER")

Unsupported versions: [12](/docs/12/sql-altertsparser.html "PostgreSQL 12 -
ALTER TEXT SEARCH PARSER") / [11](/docs/11/sql-altertsparser.html "PostgreSQL
11 - ALTER TEXT SEARCH PARSER") / [10](/docs/10/sql-altertsparser.html
"PostgreSQL 10 - ALTER TEXT SEARCH PARSER") / [9.6](/docs/9.6/sql-
altertsparser.html "PostgreSQL 9.6 - ALTER TEXT SEARCH PARSER") /
[9.5](/docs/9.5/sql-altertsparser.html "PostgreSQL 9.5 - ALTER TEXT SEARCH
PARSER") / [9.4](/docs/9.4/sql-altertsparser.html "PostgreSQL 9.4 - ALTER TEXT
SEARCH PARSER") / [9.3](/docs/9.3/sql-altertsparser.html "PostgreSQL 9.3 -
ALTER TEXT SEARCH PARSER") / [9.2](/docs/9.2/sql-altertsparser.html
"PostgreSQL 9.2 - ALTER TEXT SEARCH PARSER") / [9.1](/docs/9.1/sql-
altertsparser.html "PostgreSQL 9.1 - ALTER TEXT SEARCH PARSER") /
[9.0](/docs/9.0/sql-altertsparser.html "PostgreSQL 9.0 - ALTER TEXT SEARCH
PARSER") / [8.4](/docs/8.4/sql-altertsparser.html "PostgreSQL 8.4 - ALTER TEXT
SEARCH PARSER") / [8.3](/docs/8.3/sql-altertsparser.html "PostgreSQL 8.3 -
ALTER TEXT SEARCH PARSER")

__

ALTER TEXT SEARCH PARSER  
---  
[Prev](sql-altertsdictionary.html "ALTER TEXT SEARCH DICTIONARY")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-altertstemplate.html "ALTER TEXT SEARCH TEMPLATE")  
  
* * *

## ALTER TEXT SEARCH PARSER

ALTER TEXT SEARCH PARSER — change the definition of a text search parser

## Synopsis

    
    
    ALTER TEXT SEARCH PARSER _name_ RENAME TO _new_name_
    ALTER TEXT SEARCH PARSER _name_ SET SCHEMA _new_schema_
    

## Description

`ALTER TEXT SEARCH PARSER` changes the definition of a text search parser.
Currently, the only supported functionality is to change the parser's name.

You must be a superuser to use `ALTER TEXT SEARCH PARSER`.

## Parameters

_`name`_

    

The name (optionally schema-qualified) of an existing text search parser.

_`new_name`_

    

The new name of the text search parser.

_`new_schema`_

    

The new schema for the text search parser.

## Compatibility

There is no `ALTER TEXT SEARCH PARSER` statement in the SQL standard.

## See Also

[CREATE TEXT SEARCH PARSER](sql-createtsparser.html "CREATE TEXT SEARCH
PARSER"), [DROP TEXT SEARCH PARSER](sql-droptsparser.html "DROP TEXT SEARCH
PARSER")

* * *

[Prev](sql-altertsdictionary.html "ALTER TEXT SEARCH DICTIONARY")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-altertstemplate.html "ALTER TEXT SEARCH TEMPLATE")  
---|---|---  
ALTER TEXT SEARCH DICTIONARY  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER TEXT SEARCH TEMPLATE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-altertsparser.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

