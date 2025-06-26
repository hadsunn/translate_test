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

Supported Versions: [Current](/docs/current/sql-createtstemplate.html
"PostgreSQL 17 - CREATE TEXT SEARCH TEMPLATE") ([17](/docs/17/sql-
createtstemplate.html "PostgreSQL 17 - CREATE TEXT SEARCH TEMPLATE")) /
[16](/docs/16/sql-createtstemplate.html "PostgreSQL 16 - CREATE TEXT SEARCH
TEMPLATE") / [15](/docs/15/sql-createtstemplate.html "PostgreSQL 15 - CREATE
TEXT SEARCH TEMPLATE") / [14](/docs/14/sql-createtstemplate.html "PostgreSQL
14 - CREATE TEXT SEARCH TEMPLATE") / [13](/docs/13/sql-createtstemplate.html
"PostgreSQL 13 - CREATE TEXT SEARCH TEMPLATE")

Development Versions: [18](/docs/18/sql-createtstemplate.html "PostgreSQL 18 -
CREATE TEXT SEARCH TEMPLATE") / [devel](/docs/devel/sql-createtstemplate.html
"PostgreSQL devel - CREATE TEXT SEARCH TEMPLATE")

Unsupported versions: [12](/docs/12/sql-createtstemplate.html "PostgreSQL 12 -
CREATE TEXT SEARCH TEMPLATE") / [11](/docs/11/sql-createtstemplate.html
"PostgreSQL 11 - CREATE TEXT SEARCH TEMPLATE") / [10](/docs/10/sql-
createtstemplate.html "PostgreSQL 10 - CREATE TEXT SEARCH TEMPLATE") /
[9.6](/docs/9.6/sql-createtstemplate.html "PostgreSQL 9.6 - CREATE TEXT SEARCH
TEMPLATE") / [9.5](/docs/9.5/sql-createtstemplate.html "PostgreSQL 9.5 -
CREATE TEXT SEARCH TEMPLATE") / [9.4](/docs/9.4/sql-createtstemplate.html
"PostgreSQL 9.4 - CREATE TEXT SEARCH TEMPLATE") / [9.3](/docs/9.3/sql-
createtstemplate.html "PostgreSQL 9.3 - CREATE TEXT SEARCH TEMPLATE") /
[9.2](/docs/9.2/sql-createtstemplate.html "PostgreSQL 9.2 - CREATE TEXT SEARCH
TEMPLATE") / [9.1](/docs/9.1/sql-createtstemplate.html "PostgreSQL 9.1 -
CREATE TEXT SEARCH TEMPLATE") / [9.0](/docs/9.0/sql-createtstemplate.html
"PostgreSQL 9.0 - CREATE TEXT SEARCH TEMPLATE") / [8.4](/docs/8.4/sql-
createtstemplate.html "PostgreSQL 8.4 - CREATE TEXT SEARCH TEMPLATE") /
[8.3](/docs/8.3/sql-createtstemplate.html "PostgreSQL 8.3 - CREATE TEXT SEARCH
TEMPLATE")

__

CREATE TEXT SEARCH TEMPLATE  
---  
[Prev](sql-createtsparser.html "CREATE TEXT SEARCH PARSER")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createtransform.html "CREATE TRANSFORM")  
  
* * *

## CREATE TEXT SEARCH TEMPLATE

CREATE TEXT SEARCH TEMPLATE — define a new text search template

## Synopsis

    
    
    CREATE TEXT SEARCH TEMPLATE _name_ (
        [ INIT = _init_function_ , ]
        LEXIZE = _lexize_function_
    )
    

## Description

`CREATE TEXT SEARCH TEMPLATE` creates a new text search template. Text search
templates define the functions that implement text search dictionaries. A
template is not useful by itself, but must be instantiated as a dictionary to
be used. The dictionary typically specifies parameters to be given to the
template functions.

If a schema name is given then the text search template is created in the
specified schema. Otherwise it is created in the current schema.

You must be a superuser to use `CREATE TEXT SEARCH TEMPLATE`. This restriction
is made because an erroneous text search template definition could confuse or
even crash the server. The reason for separating templates from dictionaries
is that a template encapsulates the “unsafe” aspects of defining a dictionary.
The parameters that can be set when defining a dictionary are safe for
unprivileged users to set, and so creating a dictionary need not be a
privileged operation.

Refer to [Chapter 12](textsearch.html "Chapter 12. Full Text Search") for
further information.

## Parameters

_`name`_

    

The name of the text search template to be created. The name can be schema-
qualified.

_`init_function`_

    

The name of the init function for the template.

_`lexize_function`_

    

The name of the lexize function for the template.

The function names can be schema-qualified if necessary. Argument types are
not given, since the argument list for each type of function is predetermined.
The lexize function is required, but the init function is optional.

The arguments can appear in any order, not only the one shown above.

## Compatibility

There is no `CREATE TEXT SEARCH TEMPLATE` statement in the SQL standard.

## See Also

[ALTER TEXT SEARCH TEMPLATE](sql-altertstemplate.html "ALTER TEXT SEARCH
TEMPLATE"), [DROP TEXT SEARCH TEMPLATE](sql-droptstemplate.html "DROP TEXT
SEARCH TEMPLATE")

* * *

[Prev](sql-createtsparser.html "CREATE TEXT SEARCH PARSER")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createtransform.html "CREATE TRANSFORM")  
---|---|---  
CREATE TEXT SEARCH PARSER  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE TRANSFORM  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createtstemplate.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

