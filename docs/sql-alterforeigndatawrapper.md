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

Supported Versions: [Current](/docs/current/sql-alterforeigndatawrapper.html
"PostgreSQL 17 - ALTER FOREIGN DATA WRAPPER") ([17](/docs/17/sql-
alterforeigndatawrapper.html "PostgreSQL 17 - ALTER FOREIGN DATA WRAPPER")) /
[16](/docs/16/sql-alterforeigndatawrapper.html "PostgreSQL 16 - ALTER FOREIGN
DATA WRAPPER") / [15](/docs/15/sql-alterforeigndatawrapper.html "PostgreSQL 15
- ALTER FOREIGN DATA WRAPPER") / [14](/docs/14/sql-
alterforeigndatawrapper.html "PostgreSQL 14 - ALTER FOREIGN DATA WRAPPER") /
[13](/docs/13/sql-alterforeigndatawrapper.html "PostgreSQL 13 - ALTER FOREIGN
DATA WRAPPER")

Development Versions: [18](/docs/18/sql-alterforeigndatawrapper.html
"PostgreSQL 18 - ALTER FOREIGN DATA WRAPPER") / [devel](/docs/devel/sql-
alterforeigndatawrapper.html "PostgreSQL devel - ALTER FOREIGN DATA WRAPPER")

Unsupported versions: [12](/docs/12/sql-alterforeigndatawrapper.html
"PostgreSQL 12 - ALTER FOREIGN DATA WRAPPER") / [11](/docs/11/sql-
alterforeigndatawrapper.html "PostgreSQL 11 - ALTER FOREIGN DATA WRAPPER") /
[10](/docs/10/sql-alterforeigndatawrapper.html "PostgreSQL 10 - ALTER FOREIGN
DATA WRAPPER") / [9.6](/docs/9.6/sql-alterforeigndatawrapper.html "PostgreSQL
9.6 - ALTER FOREIGN DATA WRAPPER") / [9.5](/docs/9.5/sql-
alterforeigndatawrapper.html "PostgreSQL 9.5 - ALTER FOREIGN DATA WRAPPER") /
[9.4](/docs/9.4/sql-alterforeigndatawrapper.html "PostgreSQL 9.4 - ALTER
FOREIGN DATA WRAPPER") / [9.3](/docs/9.3/sql-alterforeigndatawrapper.html
"PostgreSQL 9.3 - ALTER FOREIGN DATA WRAPPER") / [9.2](/docs/9.2/sql-
alterforeigndatawrapper.html "PostgreSQL 9.2 - ALTER FOREIGN DATA WRAPPER") /
[9.1](/docs/9.1/sql-alterforeigndatawrapper.html "PostgreSQL 9.1 - ALTER
FOREIGN DATA WRAPPER") / [9.0](/docs/9.0/sql-alterforeigndatawrapper.html
"PostgreSQL 9.0 - ALTER FOREIGN DATA WRAPPER") / [8.4](/docs/8.4/sql-
alterforeigndatawrapper.html "PostgreSQL 8.4 - ALTER FOREIGN DATA WRAPPER")

__

ALTER FOREIGN DATA WRAPPER  
---  
[Prev](sql-alterextension.html "ALTER EXTENSION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterforeigntable.html "ALTER FOREIGN TABLE")  
  
* * *

## ALTER FOREIGN DATA WRAPPER

ALTER FOREIGN DATA WRAPPER — change the definition of a foreign-data wrapper

## Synopsis

    
    
    ALTER FOREIGN DATA WRAPPER _name_
        [ HANDLER _handler_function_ | NO HANDLER ]
        [ VALIDATOR _validator_function_ | NO VALIDATOR ]
        [ OPTIONS ( [ ADD | SET | DROP ] _option_ ['_value_ '] [, ... ]) ]
    ALTER FOREIGN DATA WRAPPER _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER FOREIGN DATA WRAPPER _name_ RENAME TO _new_name_
    

## Description

`ALTER FOREIGN DATA WRAPPER` changes the definition of a foreign-data wrapper.
The first form of the command changes the support functions or the generic
options of the foreign-data wrapper (at least one clause is required). The
second form changes the owner of the foreign-data wrapper.

Only superusers can alter foreign-data wrappers. Additionally, only superusers
can own foreign-data wrappers.

## Parameters

_`name`_

    

The name of an existing foreign-data wrapper.

`HANDLER _`handler_function`_`

    

Specifies a new handler function for the foreign-data wrapper.

`NO HANDLER`

    

This is used to specify that the foreign-data wrapper should no longer have a
handler function.

Note that foreign tables that use a foreign-data wrapper with no handler
cannot be accessed.

`VALIDATOR _`validator_function`_`

    

Specifies a new validator function for the foreign-data wrapper.

Note that it is possible that pre-existing options of the foreign-data
wrapper, or of dependent servers, user mappings, or foreign tables, are
invalid according to the new validator. PostgreSQL does not check for this. It
is up to the user to make sure that these options are correct before using the
modified foreign-data wrapper. However, any options specified in this `ALTER
FOREIGN DATA WRAPPER` command will be checked using the new validator.

`NO VALIDATOR`

    

This is used to specify that the foreign-data wrapper should no longer have a
validator function.

`OPTIONS ( [ ADD | SET | DROP ] _`option`_ ['_`value`_ '] [, ... ] )`
    

Change options for the foreign-data wrapper. `ADD`, `SET`, and `DROP` specify
the action to be performed. `ADD` is assumed if no operation is explicitly
specified. Option names must be unique; names and values are also validated
using the foreign data wrapper's validator function, if any.

_`new_owner`_

    

The user name of the new owner of the foreign-data wrapper.

_`new_name`_

    

The new name for the foreign-data wrapper.

## Examples

Change a foreign-data wrapper `dbi`, add option `foo`, drop `bar`:

    
    
    ALTER FOREIGN DATA WRAPPER dbi OPTIONS (ADD foo '1', DROP bar);
    

Change the foreign-data wrapper `dbi` validator to `bob.myvalidator`:

    
    
    ALTER FOREIGN DATA WRAPPER dbi VALIDATOR bob.myvalidator;
    

## Compatibility

`ALTER FOREIGN DATA WRAPPER` conforms to ISO/IEC 9075-9 (SQL/MED), except that
the `HANDLER`, `VALIDATOR`, `OWNER TO`, and `RENAME` clauses are extensions.

## See Also

[CREATE FOREIGN DATA WRAPPER](sql-createforeigndatawrapper.html "CREATE
FOREIGN DATA WRAPPER"), [DROP FOREIGN DATA WRAPPER](sql-
dropforeigndatawrapper.html "DROP FOREIGN DATA WRAPPER")

* * *

[Prev](sql-alterextension.html "ALTER EXTENSION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterforeigntable.html "ALTER FOREIGN TABLE")  
---|---|---  
ALTER EXTENSION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER FOREIGN TABLE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-
alterforeigndatawrapper.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

