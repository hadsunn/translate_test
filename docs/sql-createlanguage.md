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

Supported Versions: [Current](/docs/current/sql-createlanguage.html
"PostgreSQL 17 - CREATE LANGUAGE") ([17](/docs/17/sql-createlanguage.html
"PostgreSQL 17 - CREATE LANGUAGE")) / [16](/docs/16/sql-createlanguage.html
"PostgreSQL 16 - CREATE LANGUAGE") / [15](/docs/15/sql-createlanguage.html
"PostgreSQL 15 - CREATE LANGUAGE") / [14](/docs/14/sql-createlanguage.html
"PostgreSQL 14 - CREATE LANGUAGE") / [13](/docs/13/sql-createlanguage.html
"PostgreSQL 13 - CREATE LANGUAGE")

Development Versions: [18](/docs/18/sql-createlanguage.html "PostgreSQL 18 -
CREATE LANGUAGE") / [devel](/docs/devel/sql-createlanguage.html "PostgreSQL
devel - CREATE LANGUAGE")

Unsupported versions: [12](/docs/12/sql-createlanguage.html "PostgreSQL 12 -
CREATE LANGUAGE") / [11](/docs/11/sql-createlanguage.html "PostgreSQL 11 -
CREATE LANGUAGE") / [10](/docs/10/sql-createlanguage.html "PostgreSQL 10 -
CREATE LANGUAGE") / [9.6](/docs/9.6/sql-createlanguage.html "PostgreSQL 9.6 -
CREATE LANGUAGE") / [9.5](/docs/9.5/sql-createlanguage.html "PostgreSQL 9.5 -
CREATE LANGUAGE") / [9.4](/docs/9.4/sql-createlanguage.html "PostgreSQL 9.4 -
CREATE LANGUAGE") / [9.3](/docs/9.3/sql-createlanguage.html "PostgreSQL 9.3 -
CREATE LANGUAGE") / [9.2](/docs/9.2/sql-createlanguage.html "PostgreSQL 9.2 -
CREATE LANGUAGE") / [9.1](/docs/9.1/sql-createlanguage.html "PostgreSQL 9.1 -
CREATE LANGUAGE") / [9.0](/docs/9.0/sql-createlanguage.html "PostgreSQL 9.0 -
CREATE LANGUAGE") / [8.4](/docs/8.4/sql-createlanguage.html "PostgreSQL 8.4 -
CREATE LANGUAGE") / [8.3](/docs/8.3/sql-createlanguage.html "PostgreSQL 8.3 -
CREATE LANGUAGE") / [8.2](/docs/8.2/sql-createlanguage.html "PostgreSQL 8.2 -
CREATE LANGUAGE") / [8.1](/docs/8.1/sql-createlanguage.html "PostgreSQL 8.1 -
CREATE LANGUAGE") / [8.0](/docs/8.0/sql-createlanguage.html "PostgreSQL 8.0 -
CREATE LANGUAGE") / [7.4](/docs/7.4/sql-createlanguage.html "PostgreSQL 7.4 -
CREATE LANGUAGE") / [7.3](/docs/7.3/sql-createlanguage.html "PostgreSQL 7.3 -
CREATE LANGUAGE") / [7.2](/docs/7.2/sql-createlanguage.html "PostgreSQL 7.2 -
CREATE LANGUAGE") / [7.1](/docs/7.1/sql-createlanguage.html "PostgreSQL 7.1 -
CREATE LANGUAGE")

__

CREATE LANGUAGE  
---  
[Prev](sql-createindex.html "CREATE INDEX")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-creatematerializedview.html "CREATE MATERIALIZED VIEW")  
  
* * *

## CREATE LANGUAGE

CREATE LANGUAGE — define a new procedural language

## Synopsis

    
    
    CREATE [ OR REPLACE ] [ TRUSTED ] [ PROCEDURAL ] LANGUAGE _name_
        HANDLER _call_handler_ [ INLINE _inline_handler_ ] [ VALIDATOR _valfunction_ ]
    CREATE [ OR REPLACE ] [ TRUSTED ] [ PROCEDURAL ] LANGUAGE _name_
    

## Description

`CREATE LANGUAGE` registers a new procedural language with a PostgreSQL
database. Subsequently, functions and procedures can be defined in this new
language.

`CREATE LANGUAGE` effectively associates the language name with handler
function(s) that are responsible for executing functions written in the
language. Refer to [Chapter 58](plhandler.html "Chapter 58. Writing a
Procedural Language Handler") for more information about language handlers.

`CREATE OR REPLACE LANGUAGE` will either create a new language, or replace an
existing definition. If the language already exists, its parameters are
updated according to the command, but the language's ownership and permissions
settings do not change, and any existing functions written in the language are
assumed to still be valid.

One must have the PostgreSQL superuser privilege to register a new language or
change an existing language's parameters. However, once the language is
created it is valid to assign ownership of it to a non-superuser, who may then
drop it, change its permissions, rename it, or assign it to a new owner. (Do
not, however, assign ownership of the underlying C functions to a non-
superuser; that would create a privilege escalation path for that user.)

The form of `CREATE LANGUAGE` that does not supply any handler function is
obsolete. For backwards compatibility with old dump files, it is interpreted
as `CREATE EXTENSION`. That will work if the language has been packaged into
an extension of the same name, which is the conventional way to set up
procedural languages.

## Parameters

`TRUSTED`

    

`TRUSTED` specifies that the language does not grant access to data that the
user would not otherwise have. If this key word is omitted when registering
the language, only users with the PostgreSQL superuser privilege can use this
language to create new functions.

`PROCEDURAL`

    

This is a noise word.

_`name`_

    

The name of the new procedural language. The name must be unique among the
languages in the database.

`HANDLER` _`call_handler`_

    

_`call_handler`_ is the name of a previously registered function that will be
called to execute the procedural language's functions. The call handler for a
procedural language must be written in a compiled language such as C with
version 1 call convention and registered with PostgreSQL as a function taking
no arguments and returning the `language_handler` type, a placeholder type
that is simply used to identify the function as a call handler.

`INLINE` _`inline_handler`_

    

_`inline_handler`_ is the name of a previously registered function that will
be called to execute an anonymous code block ([`DO`](sql-do.html "DO")
command) in this language. If no _`inline_handler`_ function is specified, the
language does not support anonymous code blocks. The handler function must
take one argument of type `internal`, which will be the `DO` command's
internal representation, and it will typically return `void`. The return value
of the handler is ignored.

`VALIDATOR` _`valfunction`_

    

_`valfunction`_ is the name of a previously registered function that will be
called when a new function in the language is created, to validate the new
function. If no validator function is specified, then a new function will not
be checked when it is created. The validator function must take one argument
of type `oid`, which will be the OID of the to-be-created function, and will
typically return `void`.

A validator function would typically inspect the function body for syntactical
correctness, but it can also look at other properties of the function, for
example if the language cannot handle certain argument types. To signal an
error, the validator function should use the `ereport()` function. The return
value of the function is ignored.

## Notes

Use [`DROP LANGUAGE`](sql-droplanguage.html "DROP LANGUAGE") to drop
procedural languages.

The system catalog `pg_language` (see [Section 53.29](catalog-pg-language.html
"53.29. pg_language")) records information about the currently installed
languages. Also, the psql command `\dL` lists the installed languages.

To create functions in a procedural language, a user must have the `USAGE`
privilege for the language. By default, `USAGE` is granted to `PUBLIC` (i.e.,
everyone) for trusted languages. This can be revoked if desired.

Procedural languages are local to individual databases. However, a language
can be installed into the `template1` database, which will cause it to be
available automatically in all subsequently-created databases.

## Examples

A minimal sequence for creating a new procedural language is:

    
    
    CREATE FUNCTION plsample_call_handler() RETURNS language_handler
        AS '$libdir/plsample'
        LANGUAGE C;
    CREATE LANGUAGE plsample
        HANDLER plsample_call_handler;
    

Typically that would be written in an extension's creation script, and users
would do this to install the extension:

    
    
    CREATE EXTENSION plsample;
    

## Compatibility

`CREATE LANGUAGE` is a PostgreSQL extension.

## See Also

[ALTER LANGUAGE](sql-alterlanguage.html "ALTER LANGUAGE"), [CREATE
FUNCTION](sql-createfunction.html "CREATE FUNCTION"), [DROP LANGUAGE](sql-
droplanguage.html "DROP LANGUAGE"), [GRANT](sql-grant.html "GRANT"),
[REVOKE](sql-revoke.html "REVOKE")

* * *

[Prev](sql-createindex.html "CREATE INDEX")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-creatematerializedview.html "CREATE MATERIALIZED VIEW")  
---|---|---  
CREATE INDEX  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE MATERIALIZED VIEW  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createlanguage.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

