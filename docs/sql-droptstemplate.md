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

Supported Versions: [Current](/docs/current/sql-droptstemplate.html
"PostgreSQL 17 - DROP TEXT SEARCH TEMPLATE") ([17](/docs/17/sql-
droptstemplate.html "PostgreSQL 17 - DROP TEXT SEARCH TEMPLATE")) /
[16](/docs/16/sql-droptstemplate.html "PostgreSQL 16 - DROP TEXT SEARCH
TEMPLATE") / [15](/docs/15/sql-droptstemplate.html "PostgreSQL 15 - DROP TEXT
SEARCH TEMPLATE") / [14](/docs/14/sql-droptstemplate.html "PostgreSQL 14 -
DROP TEXT SEARCH TEMPLATE") / [13](/docs/13/sql-droptstemplate.html
"PostgreSQL 13 - DROP TEXT SEARCH TEMPLATE")

Development Versions: [18](/docs/18/sql-droptstemplate.html "PostgreSQL 18 -
DROP TEXT SEARCH TEMPLATE") / [devel](/docs/devel/sql-droptstemplate.html
"PostgreSQL devel - DROP TEXT SEARCH TEMPLATE")

Unsupported versions: [12](/docs/12/sql-droptstemplate.html "PostgreSQL 12 -
DROP TEXT SEARCH TEMPLATE") / [11](/docs/11/sql-droptstemplate.html
"PostgreSQL 11 - DROP TEXT SEARCH TEMPLATE") / [10](/docs/10/sql-
droptstemplate.html "PostgreSQL 10 - DROP TEXT SEARCH TEMPLATE") /
[9.6](/docs/9.6/sql-droptstemplate.html "PostgreSQL 9.6 - DROP TEXT SEARCH
TEMPLATE") / [9.5](/docs/9.5/sql-droptstemplate.html "PostgreSQL 9.5 - DROP
TEXT SEARCH TEMPLATE") / [9.4](/docs/9.4/sql-droptstemplate.html "PostgreSQL
9.4 - DROP TEXT SEARCH TEMPLATE") / [9.3](/docs/9.3/sql-droptstemplate.html
"PostgreSQL 9.3 - DROP TEXT SEARCH TEMPLATE") / [9.2](/docs/9.2/sql-
droptstemplate.html "PostgreSQL 9.2 - DROP TEXT SEARCH TEMPLATE") /
[9.1](/docs/9.1/sql-droptstemplate.html "PostgreSQL 9.1 - DROP TEXT SEARCH
TEMPLATE") / [9.0](/docs/9.0/sql-droptstemplate.html "PostgreSQL 9.0 - DROP
TEXT SEARCH TEMPLATE") / [8.4](/docs/8.4/sql-droptstemplate.html "PostgreSQL
8.4 - DROP TEXT SEARCH TEMPLATE") / [8.3](/docs/8.3/sql-droptstemplate.html
"PostgreSQL 8.3 - DROP TEXT SEARCH TEMPLATE")

__

DROP TEXT SEARCH TEMPLATE  
---  
[Prev](sql-droptsparser.html "DROP TEXT SEARCH PARSER")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-droptransform.html "DROP TRANSFORM")  
  
* * *

## DROP TEXT SEARCH TEMPLATE

DROP TEXT SEARCH TEMPLATE — remove a text search template

## Synopsis

    
    
    DROP TEXT SEARCH TEMPLATE [ IF EXISTS ] _name_ [ CASCADE | RESTRICT ]
    

## Description

`DROP TEXT SEARCH TEMPLATE` drops an existing text search template. You must
be a superuser to use this command.

## Parameters

`IF EXISTS`

    

Do not throw an error if the text search template does not exist. A notice is
issued in this case.

_`name`_

    

The name (optionally schema-qualified) of an existing text search template.

`CASCADE`

    

Automatically drop objects that depend on the text search template, and in
turn all objects that depend on those objects (see [Section 5.14](ddl-
depend.html "5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the text search template if any objects depend on it. This is
the default.

## Examples

Remove the text search template `thesaurus`:

    
    
    DROP TEXT SEARCH TEMPLATE thesaurus;
    

This command will not succeed if there are any existing text search
dictionaries that use the template. Add `CASCADE` to drop such dictionaries
along with the template.

## Compatibility

There is no `DROP TEXT SEARCH TEMPLATE` statement in the SQL standard.

## See Also

[ALTER TEXT SEARCH TEMPLATE](sql-altertstemplate.html "ALTER TEXT SEARCH
TEMPLATE"), [CREATE TEXT SEARCH TEMPLATE](sql-createtstemplate.html "CREATE
TEXT SEARCH TEMPLATE")

* * *

[Prev](sql-droptsparser.html "DROP TEXT SEARCH PARSER")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-droptransform.html "DROP TRANSFORM")  
---|---|---  
DROP TEXT SEARCH PARSER  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP TRANSFORM  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-droptstemplate.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

