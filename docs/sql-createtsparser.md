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

Supported Versions: [Current](/docs/current/sql-createtsparser.html
"PostgreSQL 17 - CREATE TEXT SEARCH PARSER") ([17](/docs/17/sql-
createtsparser.html "PostgreSQL 17 - CREATE TEXT SEARCH PARSER")) /
[16](/docs/16/sql-createtsparser.html "PostgreSQL 16 - CREATE TEXT SEARCH
PARSER") / [15](/docs/15/sql-createtsparser.html "PostgreSQL 15 - CREATE TEXT
SEARCH PARSER") / [14](/docs/14/sql-createtsparser.html "PostgreSQL 14 -
CREATE TEXT SEARCH PARSER") / [13](/docs/13/sql-createtsparser.html
"PostgreSQL 13 - CREATE TEXT SEARCH PARSER")

Development Versions: [18](/docs/18/sql-createtsparser.html "PostgreSQL 18 -
CREATE TEXT SEARCH PARSER") / [devel](/docs/devel/sql-createtsparser.html
"PostgreSQL devel - CREATE TEXT SEARCH PARSER")

Unsupported versions: [12](/docs/12/sql-createtsparser.html "PostgreSQL 12 -
CREATE TEXT SEARCH PARSER") / [11](/docs/11/sql-createtsparser.html
"PostgreSQL 11 - CREATE TEXT SEARCH PARSER") / [10](/docs/10/sql-
createtsparser.html "PostgreSQL 10 - CREATE TEXT SEARCH PARSER") /
[9.6](/docs/9.6/sql-createtsparser.html "PostgreSQL 9.6 - CREATE TEXT SEARCH
PARSER") / [9.5](/docs/9.5/sql-createtsparser.html "PostgreSQL 9.5 - CREATE
TEXT SEARCH PARSER") / [9.4](/docs/9.4/sql-createtsparser.html "PostgreSQL 9.4
- CREATE TEXT SEARCH PARSER") / [9.3](/docs/9.3/sql-createtsparser.html
"PostgreSQL 9.3 - CREATE TEXT SEARCH PARSER") / [9.2](/docs/9.2/sql-
createtsparser.html "PostgreSQL 9.2 - CREATE TEXT SEARCH PARSER") /
[9.1](/docs/9.1/sql-createtsparser.html "PostgreSQL 9.1 - CREATE TEXT SEARCH
PARSER") / [9.0](/docs/9.0/sql-createtsparser.html "PostgreSQL 9.0 - CREATE
TEXT SEARCH PARSER") / [8.4](/docs/8.4/sql-createtsparser.html "PostgreSQL 8.4
- CREATE TEXT SEARCH PARSER") / [8.3](/docs/8.3/sql-createtsparser.html
"PostgreSQL 8.3 - CREATE TEXT SEARCH PARSER")

__

CREATE TEXT SEARCH PARSER  
---  
[Prev](sql-createtsdictionary.html "CREATE TEXT SEARCH DICTIONARY")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createtstemplate.html "CREATE TEXT SEARCH TEMPLATE")  
  
* * *

## CREATE TEXT SEARCH PARSER

CREATE TEXT SEARCH PARSER — define a new text search parser

## Synopsis

    
    
    CREATE TEXT SEARCH PARSER _name_ (
        START = _start_function_ ,
        GETTOKEN = _gettoken_function_ ,
        END = _end_function_ ,
        LEXTYPES = _lextypes_function_
        [, HEADLINE = _headline_function_ ]
    )
    

## Description

`CREATE TEXT SEARCH PARSER` creates a new text search parser. A text search
parser defines a method for splitting a text string into tokens and assigning
types (categories) to the tokens. A parser is not particularly useful by
itself, but must be bound into a text search configuration along with some
text search dictionaries to be used for searching.

If a schema name is given then the text search parser is created in the
specified schema. Otherwise it is created in the current schema.

You must be a superuser to use `CREATE TEXT SEARCH PARSER`. (This restriction
is made because an erroneous text search parser definition could confuse or
even crash the server.)

Refer to [Chapter 12](textsearch.html "Chapter 12. Full Text Search") for
further information.

## Parameters

_`name`_

    

The name of the text search parser to be created. The name can be schema-
qualified.

_`start_function`_

    

The name of the start function for the parser.

_`gettoken_function`_

    

The name of the get-next-token function for the parser.

_`end_function`_

    

The name of the end function for the parser.

_`lextypes_function`_

    

The name of the lextypes function for the parser (a function that returns
information about the set of token types it produces).

_`headline_function`_

    

The name of the headline function for the parser (a function that summarizes a
set of tokens).

The function names can be schema-qualified if necessary. Argument types are
not given, since the argument list for each type of function is predetermined.
All except the headline function are required.

The arguments can appear in any order, not only the one shown above.

## Compatibility

There is no `CREATE TEXT SEARCH PARSER` statement in the SQL standard.

## See Also

[ALTER TEXT SEARCH PARSER](sql-altertsparser.html "ALTER TEXT SEARCH PARSER"),
[DROP TEXT SEARCH PARSER](sql-droptsparser.html "DROP TEXT SEARCH PARSER")

* * *

[Prev](sql-createtsdictionary.html "CREATE TEXT SEARCH DICTIONARY")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createtstemplate.html "CREATE TEXT SEARCH TEMPLATE")  
---|---|---  
CREATE TEXT SEARCH DICTIONARY  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE TEXT SEARCH TEMPLATE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createtsparser.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

