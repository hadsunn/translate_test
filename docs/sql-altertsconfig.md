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

Supported Versions: [Current](/docs/current/sql-altertsconfig.html "PostgreSQL
17 - ALTER TEXT SEARCH CONFIGURATION") ([17](/docs/17/sql-altertsconfig.html
"PostgreSQL 17 - ALTER TEXT SEARCH CONFIGURATION")) / [16](/docs/16/sql-
altertsconfig.html "PostgreSQL 16 - ALTER TEXT SEARCH CONFIGURATION") /
[15](/docs/15/sql-altertsconfig.html "PostgreSQL 15 - ALTER TEXT SEARCH
CONFIGURATION") / [14](/docs/14/sql-altertsconfig.html "PostgreSQL 14 - ALTER
TEXT SEARCH CONFIGURATION") / [13](/docs/13/sql-altertsconfig.html "PostgreSQL
13 - ALTER TEXT SEARCH CONFIGURATION")

Development Versions: [18](/docs/18/sql-altertsconfig.html "PostgreSQL 18 -
ALTER TEXT SEARCH CONFIGURATION") / [devel](/docs/devel/sql-altertsconfig.html
"PostgreSQL devel - ALTER TEXT SEARCH CONFIGURATION")

Unsupported versions: [12](/docs/12/sql-altertsconfig.html "PostgreSQL 12 -
ALTER TEXT SEARCH CONFIGURATION") / [11](/docs/11/sql-altertsconfig.html
"PostgreSQL 11 - ALTER TEXT SEARCH CONFIGURATION") / [10](/docs/10/sql-
altertsconfig.html "PostgreSQL 10 - ALTER TEXT SEARCH CONFIGURATION") /
[9.6](/docs/9.6/sql-altertsconfig.html "PostgreSQL 9.6 - ALTER TEXT SEARCH
CONFIGURATION") / [9.5](/docs/9.5/sql-altertsconfig.html "PostgreSQL 9.5 -
ALTER TEXT SEARCH CONFIGURATION") / [9.4](/docs/9.4/sql-altertsconfig.html
"PostgreSQL 9.4 - ALTER TEXT SEARCH CONFIGURATION") / [9.3](/docs/9.3/sql-
altertsconfig.html "PostgreSQL 9.3 - ALTER TEXT SEARCH CONFIGURATION") /
[9.2](/docs/9.2/sql-altertsconfig.html "PostgreSQL 9.2 - ALTER TEXT SEARCH
CONFIGURATION") / [9.1](/docs/9.1/sql-altertsconfig.html "PostgreSQL 9.1 -
ALTER TEXT SEARCH CONFIGURATION") / [9.0](/docs/9.0/sql-altertsconfig.html
"PostgreSQL 9.0 - ALTER TEXT SEARCH CONFIGURATION") / [8.4](/docs/8.4/sql-
altertsconfig.html "PostgreSQL 8.4 - ALTER TEXT SEARCH CONFIGURATION") /
[8.3](/docs/8.3/sql-altertsconfig.html "PostgreSQL 8.3 - ALTER TEXT SEARCH
CONFIGURATION")

__

ALTER TEXT SEARCH CONFIGURATION  
---  
[Prev](sql-altertablespace.html "ALTER TABLESPACE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-altertsdictionary.html "ALTER TEXT SEARCH DICTIONARY")  
  
* * *

## ALTER TEXT SEARCH CONFIGURATION

ALTER TEXT SEARCH CONFIGURATION — change the definition of a text search
configuration

## Synopsis

    
    
    ALTER TEXT SEARCH CONFIGURATION _name_
        ADD MAPPING FOR _token_type_ [, ... ] WITH _dictionary_name_ [, ... ]
    ALTER TEXT SEARCH CONFIGURATION _name_
        ALTER MAPPING FOR _token_type_ [, ... ] WITH _dictionary_name_ [, ... ]
    ALTER TEXT SEARCH CONFIGURATION _name_
        ALTER MAPPING REPLACE _old_dictionary_ WITH _new_dictionary_
    ALTER TEXT SEARCH CONFIGURATION _name_
        ALTER MAPPING FOR _token_type_ [, ... ] REPLACE _old_dictionary_ WITH _new_dictionary_
    ALTER TEXT SEARCH CONFIGURATION _name_
        DROP MAPPING [ IF EXISTS ] FOR _token_type_ [, ... ]
    ALTER TEXT SEARCH CONFIGURATION _name_ RENAME TO _new_name_
    ALTER TEXT SEARCH CONFIGURATION _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER TEXT SEARCH CONFIGURATION _name_ SET SCHEMA _new_schema_
    

## Description

`ALTER TEXT SEARCH CONFIGURATION` changes the definition of a text search
configuration. You can modify its mappings from token types to dictionaries,
or change the configuration's name or owner.

You must be the owner of the configuration to use `ALTER TEXT SEARCH
CONFIGURATION`.

## Parameters

_`name`_

    

The name (optionally schema-qualified) of an existing text search
configuration.

_`token_type`_

    

The name of a token type that is emitted by the configuration's parser.

_`dictionary_name`_

    

The name of a text search dictionary to be consulted for the specified token
type(s). If multiple dictionaries are listed, they are consulted in the
specified order.

_`old_dictionary`_

    

The name of a text search dictionary to be replaced in the mapping.

_`new_dictionary`_

    

The name of a text search dictionary to be substituted for _`old_dictionary`_.

_`new_name`_

    

The new name of the text search configuration.

_`new_owner`_

    

The new owner of the text search configuration.

_`new_schema`_

    

The new schema for the text search configuration.

The `ADD MAPPING FOR` form installs a list of dictionaries to be consulted for
the specified token type(s); it is an error if there is already a mapping for
any of the token types. The `ALTER MAPPING FOR` form does the same, but first
removing any existing mapping for those token types. The `ALTER MAPPING
REPLACE` forms substitute _`new_dictionary`_ for _`old_dictionary`_ anywhere
the latter appears. This is done for only the specified token types when `FOR`
appears, or for all mappings of the configuration when it doesn't. The `DROP
MAPPING` form removes all dictionaries for the specified token type(s),
causing tokens of those types to be ignored by the text search configuration.
It is an error if there is no mapping for the token types, unless `IF EXISTS`
appears.

## Examples

The following example replaces the `english` dictionary with the `swedish`
dictionary anywhere that `english` is used within `my_config`.

    
    
    ALTER TEXT SEARCH CONFIGURATION my_config
      ALTER MAPPING REPLACE english WITH swedish;
    

## Compatibility

There is no `ALTER TEXT SEARCH CONFIGURATION` statement in the SQL standard.

## See Also

[CREATE TEXT SEARCH CONFIGURATION](sql-createtsconfig.html "CREATE TEXT SEARCH
CONFIGURATION"), [DROP TEXT SEARCH CONFIGURATION](sql-droptsconfig.html "DROP
TEXT SEARCH CONFIGURATION")

* * *

[Prev](sql-altertablespace.html "ALTER TABLESPACE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-altertsdictionary.html "ALTER TEXT SEARCH DICTIONARY")  
---|---|---  
ALTER TABLESPACE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER TEXT SEARCH DICTIONARY  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-altertsconfig.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

