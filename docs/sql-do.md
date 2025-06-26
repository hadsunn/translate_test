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

Supported Versions: [Current](/docs/current/sql-do.html "PostgreSQL 17 - DO")
([17](/docs/17/sql-do.html "PostgreSQL 17 - DO")) / [16](/docs/16/sql-do.html
"PostgreSQL 16 - DO") / [15](/docs/15/sql-do.html "PostgreSQL 15 - DO") /
[14](/docs/14/sql-do.html "PostgreSQL 14 - DO") / [13](/docs/13/sql-do.html
"PostgreSQL 13 - DO")

Development Versions: [18](/docs/18/sql-do.html "PostgreSQL 18 - DO") /
[devel](/docs/devel/sql-do.html "PostgreSQL devel - DO")

Unsupported versions: [12](/docs/12/sql-do.html "PostgreSQL 12 - DO") /
[11](/docs/11/sql-do.html "PostgreSQL 11 - DO") / [10](/docs/10/sql-do.html
"PostgreSQL 10 - DO") / [9.6](/docs/9.6/sql-do.html "PostgreSQL 9.6 - DO") /
[9.5](/docs/9.5/sql-do.html "PostgreSQL 9.5 - DO") / [9.4](/docs/9.4/sql-
do.html "PostgreSQL 9.4 - DO") / [9.3](/docs/9.3/sql-do.html "PostgreSQL 9.3 -
DO") / [9.2](/docs/9.2/sql-do.html "PostgreSQL 9.2 - DO") /
[9.1](/docs/9.1/sql-do.html "PostgreSQL 9.1 - DO") / [9.0](/docs/9.0/sql-
do.html "PostgreSQL 9.0 - DO")

__

DO  
---  
[Prev](sql-discard.html "DISCARD")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-drop-access-method.html "DROP ACCESS METHOD")  
  
* * *

## DO

DO — execute an anonymous code block

## Synopsis

    
    
    DO [ LANGUAGE _lang_name_ ] _code_
    

## Description

`DO` executes an anonymous code block, or in other words a transient anonymous
function in a procedural language.

The code block is treated as though it were the body of a function with no
parameters, returning `void`. It is parsed and executed a single time.

The optional `LANGUAGE` clause can be written either before or after the code
block.

## Parameters

_`code`_

    

The procedural language code to be executed. This must be specified as a
string literal, just as in `CREATE FUNCTION`. Use of a dollar-quoted literal
is recommended.

_`lang_name`_

    

The name of the procedural language the code is written in. If omitted, the
default is `plpgsql`.

## Notes

The procedural language to be used must already have been installed into the
current database by means of `CREATE EXTENSION`. `plpgsql` is installed by
default, but other languages are not.

The user must have `USAGE` privilege for the procedural language, or must be a
superuser if the language is untrusted. This is the same privilege requirement
as for creating a function in the language.

If `DO` is executed in a transaction block, then the procedure code cannot
execute transaction control statements. Transaction control statements are
only allowed if `DO` is executed in its own transaction.

## Examples

Grant all privileges on all views in schema `public` to role `webuser`:

    
    
    DO $$DECLARE r record;
    BEGIN
        FOR r IN SELECT table_schema, table_name FROM information_schema.tables
                 WHERE table_type = 'VIEW' AND table_schema = 'public'
        LOOP
            EXECUTE 'GRANT ALL ON ' || quote_ident(r.table_schema) || '.' || quote_ident(r.table_name) || ' TO webuser';
        END LOOP;
    END$$;
    

## Compatibility

There is no `DO` statement in the SQL standard.

## See Also

[CREATE LANGUAGE](sql-createlanguage.html "CREATE LANGUAGE")

* * *

[Prev](sql-discard.html "DISCARD")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-drop-access-method.html "DROP ACCESS METHOD")  
---|---|---  
DISCARD  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DROP ACCESS METHOD  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-do.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

