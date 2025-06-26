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

Supported Versions: [Current](/docs/current/sql-altertsdictionary.html
"PostgreSQL 17 - ALTER TEXT SEARCH DICTIONARY") ([17](/docs/17/sql-
altertsdictionary.html "PostgreSQL 17 - ALTER TEXT SEARCH DICTIONARY")) /
[16](/docs/16/sql-altertsdictionary.html "PostgreSQL 16 - ALTER TEXT SEARCH
DICTIONARY") / [15](/docs/15/sql-altertsdictionary.html "PostgreSQL 15 - ALTER
TEXT SEARCH DICTIONARY") / [14](/docs/14/sql-altertsdictionary.html
"PostgreSQL 14 - ALTER TEXT SEARCH DICTIONARY") / [13](/docs/13/sql-
altertsdictionary.html "PostgreSQL 13 - ALTER TEXT SEARCH DICTIONARY")

Development Versions: [18](/docs/18/sql-altertsdictionary.html "PostgreSQL 18
- ALTER TEXT SEARCH DICTIONARY") / [devel](/docs/devel/sql-
altertsdictionary.html "PostgreSQL devel - ALTER TEXT SEARCH DICTIONARY")

Unsupported versions: [12](/docs/12/sql-altertsdictionary.html "PostgreSQL 12
- ALTER TEXT SEARCH DICTIONARY") / [11](/docs/11/sql-altertsdictionary.html
"PostgreSQL 11 - ALTER TEXT SEARCH DICTIONARY") / [10](/docs/10/sql-
altertsdictionary.html "PostgreSQL 10 - ALTER TEXT SEARCH DICTIONARY") /
[9.6](/docs/9.6/sql-altertsdictionary.html "PostgreSQL 9.6 - ALTER TEXT SEARCH
DICTIONARY") / [9.5](/docs/9.5/sql-altertsdictionary.html "PostgreSQL 9.5 -
ALTER TEXT SEARCH DICTIONARY") / [9.4](/docs/9.4/sql-altertsdictionary.html
"PostgreSQL 9.4 - ALTER TEXT SEARCH DICTIONARY") / [9.3](/docs/9.3/sql-
altertsdictionary.html "PostgreSQL 9.3 - ALTER TEXT SEARCH DICTIONARY") /
[9.2](/docs/9.2/sql-altertsdictionary.html "PostgreSQL 9.2 - ALTER TEXT SEARCH
DICTIONARY") / [9.1](/docs/9.1/sql-altertsdictionary.html "PostgreSQL 9.1 -
ALTER TEXT SEARCH DICTIONARY") / [9.0](/docs/9.0/sql-altertsdictionary.html
"PostgreSQL 9.0 - ALTER TEXT SEARCH DICTIONARY") / [8.4](/docs/8.4/sql-
altertsdictionary.html "PostgreSQL 8.4 - ALTER TEXT SEARCH DICTIONARY") /
[8.3](/docs/8.3/sql-altertsdictionary.html "PostgreSQL 8.3 - ALTER TEXT SEARCH
DICTIONARY")

__

ALTER TEXT SEARCH DICTIONARY  
---  
[Prev](sql-altertsconfig.html "ALTER TEXT SEARCH CONFIGURATION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-altertsparser.html "ALTER TEXT SEARCH PARSER")  
  
* * *

## ALTER TEXT SEARCH DICTIONARY

ALTER TEXT SEARCH DICTIONARY — change the definition of a text search
dictionary

## Synopsis

    
    
    ALTER TEXT SEARCH DICTIONARY _name_ (
        _option_ [ = _value_ ] [, ... ]
    )
    ALTER TEXT SEARCH DICTIONARY _name_ RENAME TO _new_name_
    ALTER TEXT SEARCH DICTIONARY _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER TEXT SEARCH DICTIONARY _name_ SET SCHEMA _new_schema_
    

## Description

`ALTER TEXT SEARCH DICTIONARY` changes the definition of a text search
dictionary. You can change the dictionary's template-specific options, or
change the dictionary's name or owner.

You must be the owner of the dictionary to use `ALTER TEXT SEARCH DICTIONARY`.

## Parameters

_`name`_

    

The name (optionally schema-qualified) of an existing text search dictionary.

_`option`_

    

The name of a template-specific option to be set for this dictionary.

_`value`_

    

The new value to use for a template-specific option. If the equal sign and
value are omitted, then any previous setting for the option is removed from
the dictionary, allowing the default to be used.

_`new_name`_

    

The new name of the text search dictionary.

_`new_owner`_

    

The new owner of the text search dictionary.

_`new_schema`_

    

The new schema for the text search dictionary.

Template-specific options can appear in any order.

## Examples

The following example command changes the stopword list for a Snowball-based
dictionary. Other parameters remain unchanged.

    
    
    ALTER TEXT SEARCH DICTIONARY my_dict ( StopWords = newrussian );
    

The following example command changes the language option to `dutch`, and
removes the stopword option entirely.

    
    
    ALTER TEXT SEARCH DICTIONARY my_dict ( language = dutch, StopWords );
    

The following example command “updates” the dictionary's definition without
actually changing anything.

    
    
    ALTER TEXT SEARCH DICTIONARY my_dict ( dummy );
    

(The reason this works is that the option removal code doesn't complain if
there is no such option.) This trick is useful when changing configuration
files for the dictionary: the `ALTER` will force existing database sessions to
re-read the configuration files, which otherwise they would never do if they
had read them earlier.

## Compatibility

There is no `ALTER TEXT SEARCH DICTIONARY` statement in the SQL standard.

## See Also

[CREATE TEXT SEARCH DICTIONARY](sql-createtsdictionary.html "CREATE TEXT
SEARCH DICTIONARY"), [DROP TEXT SEARCH DICTIONARY](sql-droptsdictionary.html
"DROP TEXT SEARCH DICTIONARY")

* * *

[Prev](sql-altertsconfig.html "ALTER TEXT SEARCH CONFIGURATION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-altertsparser.html "ALTER TEXT SEARCH PARSER")  
---|---|---  
ALTER TEXT SEARCH CONFIGURATION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER TEXT SEARCH PARSER  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-altertsdictionary.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

