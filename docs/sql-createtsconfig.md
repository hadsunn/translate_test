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

Supported Versions: [Current](/docs/current/sql-createtsconfig.html
"PostgreSQL 17 - CREATE TEXT SEARCH CONFIGURATION") ([17](/docs/17/sql-
createtsconfig.html "PostgreSQL 17 - CREATE TEXT SEARCH CONFIGURATION")) /
[16](/docs/16/sql-createtsconfig.html "PostgreSQL 16 - CREATE TEXT SEARCH
CONFIGURATION") / [15](/docs/15/sql-createtsconfig.html "PostgreSQL 15 -
CREATE TEXT SEARCH CONFIGURATION") / [14](/docs/14/sql-createtsconfig.html
"PostgreSQL 14 - CREATE TEXT SEARCH CONFIGURATION") / [13](/docs/13/sql-
createtsconfig.html "PostgreSQL 13 - CREATE TEXT SEARCH CONFIGURATION")

Development Versions: [18](/docs/18/sql-createtsconfig.html "PostgreSQL 18 -
CREATE TEXT SEARCH CONFIGURATION") / [devel](/docs/devel/sql-
createtsconfig.html "PostgreSQL devel - CREATE TEXT SEARCH CONFIGURATION")

Unsupported versions: [12](/docs/12/sql-createtsconfig.html "PostgreSQL 12 -
CREATE TEXT SEARCH CONFIGURATION") / [11](/docs/11/sql-createtsconfig.html
"PostgreSQL 11 - CREATE TEXT SEARCH CONFIGURATION") / [10](/docs/10/sql-
createtsconfig.html "PostgreSQL 10 - CREATE TEXT SEARCH CONFIGURATION") /
[9.6](/docs/9.6/sql-createtsconfig.html "PostgreSQL 9.6 - CREATE TEXT SEARCH
CONFIGURATION") / [9.5](/docs/9.5/sql-createtsconfig.html "PostgreSQL 9.5 -
CREATE TEXT SEARCH CONFIGURATION") / [9.4](/docs/9.4/sql-createtsconfig.html
"PostgreSQL 9.4 - CREATE TEXT SEARCH CONFIGURATION") / [9.3](/docs/9.3/sql-
createtsconfig.html "PostgreSQL 9.3 - CREATE TEXT SEARCH CONFIGURATION") /
[9.2](/docs/9.2/sql-createtsconfig.html "PostgreSQL 9.2 - CREATE TEXT SEARCH
CONFIGURATION") / [9.1](/docs/9.1/sql-createtsconfig.html "PostgreSQL 9.1 -
CREATE TEXT SEARCH CONFIGURATION") / [9.0](/docs/9.0/sql-createtsconfig.html
"PostgreSQL 9.0 - CREATE TEXT SEARCH CONFIGURATION") / [8.4](/docs/8.4/sql-
createtsconfig.html "PostgreSQL 8.4 - CREATE TEXT SEARCH CONFIGURATION") /
[8.3](/docs/8.3/sql-createtsconfig.html "PostgreSQL 8.3 - CREATE TEXT SEARCH
CONFIGURATION")

__

CREATE TEXT SEARCH CONFIGURATION  
---  
[Prev](sql-createtablespace.html "CREATE TABLESPACE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createtsdictionary.html "CREATE TEXT SEARCH DICTIONARY")  
  
* * *

## CREATE TEXT SEARCH CONFIGURATION

CREATE TEXT SEARCH CONFIGURATION — define a new text search configuration

## Synopsis

    
    
    CREATE TEXT SEARCH CONFIGURATION _name_ (
        PARSER = _parser_name_ |
        COPY = _source_config_
    )
    

## Description

`CREATE TEXT SEARCH CONFIGURATION` creates a new text search configuration. A
text search configuration specifies a text search parser that can divide a
string into tokens, plus dictionaries that can be used to determine which
tokens are of interest for searching.

If only the parser is specified, then the new text search configuration
initially has no mappings from token types to dictionaries, and therefore will
ignore all words. Subsequent `ALTER TEXT SEARCH CONFIGURATION` commands must
be used to create mappings to make the configuration useful. Alternatively, an
existing text search configuration can be copied.

If a schema name is given then the text search configuration is created in the
specified schema. Otherwise it is created in the current schema.

The user who defines a text search configuration becomes its owner.

Refer to [Chapter 12](textsearch.html "Chapter 12. Full Text Search") for
further information.

## Parameters

_`name`_

    

The name of the text search configuration to be created. The name can be
schema-qualified.

_`parser_name`_

    

The name of the text search parser to use for this configuration.

_`source_config`_

    

The name of an existing text search configuration to copy.

## Notes

The `PARSER` and `COPY` options are mutually exclusive, because when an
existing configuration is copied, its parser selection is copied too.

## Compatibility

There is no `CREATE TEXT SEARCH CONFIGURATION` statement in the SQL standard.

## See Also

[ALTER TEXT SEARCH CONFIGURATION](sql-altertsconfig.html "ALTER TEXT SEARCH
CONFIGURATION"), [DROP TEXT SEARCH CONFIGURATION](sql-droptsconfig.html "DROP
TEXT SEARCH CONFIGURATION")

* * *

[Prev](sql-createtablespace.html "CREATE TABLESPACE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createtsdictionary.html "CREATE TEXT SEARCH DICTIONARY")  
---|---|---  
CREATE TABLESPACE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE TEXT SEARCH DICTIONARY  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createtsconfig.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

