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

Supported Versions: [Current](/docs/current/sql-droptsconfig.html "PostgreSQL
17 - DROP TEXT SEARCH CONFIGURATION") ([17](/docs/17/sql-droptsconfig.html
"PostgreSQL 17 - DROP TEXT SEARCH CONFIGURATION")) / [16](/docs/16/sql-
droptsconfig.html "PostgreSQL 16 - DROP TEXT SEARCH CONFIGURATION") /
[15](/docs/15/sql-droptsconfig.html "PostgreSQL 15 - DROP TEXT SEARCH
CONFIGURATION") / [14](/docs/14/sql-droptsconfig.html "PostgreSQL 14 - DROP
TEXT SEARCH CONFIGURATION") / [13](/docs/13/sql-droptsconfig.html "PostgreSQL
13 - DROP TEXT SEARCH CONFIGURATION")

Development Versions: [18](/docs/18/sql-droptsconfig.html "PostgreSQL 18 -
DROP TEXT SEARCH CONFIGURATION") / [devel](/docs/devel/sql-droptsconfig.html
"PostgreSQL devel - DROP TEXT SEARCH CONFIGURATION")

Unsupported versions: [12](/docs/12/sql-droptsconfig.html "PostgreSQL 12 -
DROP TEXT SEARCH CONFIGURATION") / [11](/docs/11/sql-droptsconfig.html
"PostgreSQL 11 - DROP TEXT SEARCH CONFIGURATION") / [10](/docs/10/sql-
droptsconfig.html "PostgreSQL 10 - DROP TEXT SEARCH CONFIGURATION") /
[9.6](/docs/9.6/sql-droptsconfig.html "PostgreSQL 9.6 - DROP TEXT SEARCH
CONFIGURATION") / [9.5](/docs/9.5/sql-droptsconfig.html "PostgreSQL 9.5 - DROP
TEXT SEARCH CONFIGURATION") / [9.4](/docs/9.4/sql-droptsconfig.html
"PostgreSQL 9.4 - DROP TEXT SEARCH CONFIGURATION") / [9.3](/docs/9.3/sql-
droptsconfig.html "PostgreSQL 9.3 - DROP TEXT SEARCH CONFIGURATION") /
[9.2](/docs/9.2/sql-droptsconfig.html "PostgreSQL 9.2 - DROP TEXT SEARCH
CONFIGURATION") / [9.1](/docs/9.1/sql-droptsconfig.html "PostgreSQL 9.1 - DROP
TEXT SEARCH CONFIGURATION") / [9.0](/docs/9.0/sql-droptsconfig.html
"PostgreSQL 9.0 - DROP TEXT SEARCH CONFIGURATION") / [8.4](/docs/8.4/sql-
droptsconfig.html "PostgreSQL 8.4 - DROP TEXT SEARCH CONFIGURATION") /
[8.3](/docs/8.3/sql-droptsconfig.html "PostgreSQL 8.3 - DROP TEXT SEARCH
CONFIGURATION")

__

DROP TEXT SEARCH CONFIGURATION  
---  
[Prev](sql-droptablespace.html "DROP TABLESPACE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-droptsdictionary.html "DROP TEXT SEARCH DICTIONARY")  
  
* * *

## DROP TEXT SEARCH CONFIGURATION

DROP TEXT SEARCH CONFIGURATION — remove a text search configuration

## Synopsis

    
    
    DROP TEXT SEARCH CONFIGURATION [ IF EXISTS ] _name_ [ CASCADE | RESTRICT ]
    

## Description

`DROP TEXT SEARCH CONFIGURATION` drops an existing text search configuration.
To execute this command you must be the owner of the configuration.

## Parameters

`IF EXISTS`

    

Do not throw an error if the text search configuration does not exist. A
notice is issued in this case.

_`name`_

    

The name (optionally schema-qualified) of an existing text search
configuration.

`CASCADE`

    

Automatically drop objects that depend on the text search configuration, and
in turn all objects that depend on those objects (see [Section 5.14](ddl-
depend.html "5.14. Dependency Tracking")).

`RESTRICT`

    

Refuse to drop the text search configuration if any objects depend on it. This
is the default.

## Examples

Remove the text search configuration `my_english`:

    
    
    DROP TEXT SEARCH CONFIGURATION my_english;
    

This command will not succeed if there are any existing indexes that reference
the configuration in `to_tsvector` calls. Add `CASCADE` to drop such indexes
along with the text search configuration.

## Compatibility

There is no `DROP TEXT SEARCH CONFIGURATION` statement in the SQL standard.

## See Also

[ALTER TEXT SEARCH CONFIGURATION](sql-altertsconfig.html "ALTER TEXT SEARCH
CONFIGURATION"), [CREATE TEXT SEARCH CONFIGURATION](sql-createtsconfig.html
"CREATE TEXT SEARCH CONFIGURATION")

* * *

[Prev](sql-droptablespace.html "DROP TABLESPACE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-droptsdictionary.html "DROP TEXT SEARCH DICTIONARY")  
---|---|---  
DROP TABLESPACE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP TEXT SEARCH DICTIONARY  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-droptsconfig.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

