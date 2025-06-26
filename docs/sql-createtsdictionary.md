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

Supported Versions: [Current](/docs/current/sql-createtsdictionary.html
"PostgreSQL 17 - CREATE TEXT SEARCH DICTIONARY") ([17](/docs/17/sql-
createtsdictionary.html "PostgreSQL 17 - CREATE TEXT SEARCH DICTIONARY")) /
[16](/docs/16/sql-createtsdictionary.html "PostgreSQL 16 - CREATE TEXT SEARCH
DICTIONARY") / [15](/docs/15/sql-createtsdictionary.html "PostgreSQL 15 -
CREATE TEXT SEARCH DICTIONARY") / [14](/docs/14/sql-createtsdictionary.html
"PostgreSQL 14 - CREATE TEXT SEARCH DICTIONARY") / [13](/docs/13/sql-
createtsdictionary.html "PostgreSQL 13 - CREATE TEXT SEARCH DICTIONARY")

Development Versions: [18](/docs/18/sql-createtsdictionary.html "PostgreSQL 18
- CREATE TEXT SEARCH DICTIONARY") / [devel](/docs/devel/sql-
createtsdictionary.html "PostgreSQL devel - CREATE TEXT SEARCH DICTIONARY")

Unsupported versions: [12](/docs/12/sql-createtsdictionary.html "PostgreSQL 12
- CREATE TEXT SEARCH DICTIONARY") / [11](/docs/11/sql-createtsdictionary.html
"PostgreSQL 11 - CREATE TEXT SEARCH DICTIONARY") / [10](/docs/10/sql-
createtsdictionary.html "PostgreSQL 10 - CREATE TEXT SEARCH DICTIONARY") /
[9.6](/docs/9.6/sql-createtsdictionary.html "PostgreSQL 9.6 - CREATE TEXT
SEARCH DICTIONARY") / [9.5](/docs/9.5/sql-createtsdictionary.html "PostgreSQL
9.5 - CREATE TEXT SEARCH DICTIONARY") / [9.4](/docs/9.4/sql-
createtsdictionary.html "PostgreSQL 9.4 - CREATE TEXT SEARCH DICTIONARY") /
[9.3](/docs/9.3/sql-createtsdictionary.html "PostgreSQL 9.3 - CREATE TEXT
SEARCH DICTIONARY") / [9.2](/docs/9.2/sql-createtsdictionary.html "PostgreSQL
9.2 - CREATE TEXT SEARCH DICTIONARY") / [9.1](/docs/9.1/sql-
createtsdictionary.html "PostgreSQL 9.1 - CREATE TEXT SEARCH DICTIONARY") /
[9.0](/docs/9.0/sql-createtsdictionary.html "PostgreSQL 9.0 - CREATE TEXT
SEARCH DICTIONARY") / [8.4](/docs/8.4/sql-createtsdictionary.html "PostgreSQL
8.4 - CREATE TEXT SEARCH DICTIONARY") / [8.3](/docs/8.3/sql-
createtsdictionary.html "PostgreSQL 8.3 - CREATE TEXT SEARCH DICTIONARY")

__

CREATE TEXT SEARCH DICTIONARY  
---  
[Prev](sql-createtsconfig.html "CREATE TEXT SEARCH CONFIGURATION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createtsparser.html "CREATE TEXT SEARCH PARSER")  
  
* * *

## CREATE TEXT SEARCH DICTIONARY

CREATE TEXT SEARCH DICTIONARY — define a new text search dictionary

## Synopsis

    
    
    CREATE TEXT SEARCH DICTIONARY _name_ (
        TEMPLATE = _template_
        [, _option_ = _value_ [, ... ]]
    )
    

## Description

`CREATE TEXT SEARCH DICTIONARY` creates a new text search dictionary. A text
search dictionary specifies a way of recognizing interesting or uninteresting
words for searching. A dictionary depends on a text search template, which
specifies the functions that actually perform the work. Typically the
dictionary provides some options that control the detailed behavior of the
template's functions.

If a schema name is given then the text search dictionary is created in the
specified schema. Otherwise it is created in the current schema.

The user who defines a text search dictionary becomes its owner.

Refer to [Chapter 12](textsearch.html "Chapter 12. Full Text Search") for
further information.

## Parameters

_`name`_

    

The name of the text search dictionary to be created. The name can be schema-
qualified.

_`template`_

    

The name of the text search template that will define the basic behavior of
this dictionary.

_`option`_

    

The name of a template-specific option to be set for this dictionary.

_`value`_

    

The value to use for a template-specific option. If the value is not a simple
identifier or number, it must be quoted (but you can always quote it, if you
wish).

The options can appear in any order.

## Examples

The following example command creates a Snowball-based dictionary with a
nonstandard list of stop words.

    
    
    CREATE TEXT SEARCH DICTIONARY my_russian (
        template = snowball,
        language = russian,
        stopwords = myrussian
    );
    

## Compatibility

There is no `CREATE TEXT SEARCH DICTIONARY` statement in the SQL standard.

## See Also

[ALTER TEXT SEARCH DICTIONARY](sql-altertsdictionary.html "ALTER TEXT SEARCH
DICTIONARY"), [DROP TEXT SEARCH DICTIONARY](sql-droptsdictionary.html "DROP
TEXT SEARCH DICTIONARY")

* * *

[Prev](sql-createtsconfig.html "CREATE TEXT SEARCH CONFIGURATION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createtsparser.html "CREATE TEXT SEARCH PARSER")  
---|---|---  
CREATE TEXT SEARCH CONFIGURATION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE TEXT SEARCH PARSER  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createtsdictionary.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

