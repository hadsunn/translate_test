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

Supported Versions: [Current](/docs/current/sql-createextension.html
"PostgreSQL 17 - CREATE EXTENSION") ([17](/docs/17/sql-createextension.html
"PostgreSQL 17 - CREATE EXTENSION")) / [16](/docs/16/sql-createextension.html
"PostgreSQL 16 - CREATE EXTENSION") / [15](/docs/15/sql-createextension.html
"PostgreSQL 15 - CREATE EXTENSION") / [14](/docs/14/sql-createextension.html
"PostgreSQL 14 - CREATE EXTENSION") / [13](/docs/13/sql-createextension.html
"PostgreSQL 13 - CREATE EXTENSION")

Development Versions: [18](/docs/18/sql-createextension.html "PostgreSQL 18 -
CREATE EXTENSION") / [devel](/docs/devel/sql-createextension.html "PostgreSQL
devel - CREATE EXTENSION")

Unsupported versions: [12](/docs/12/sql-createextension.html "PostgreSQL 12 -
CREATE EXTENSION") / [11](/docs/11/sql-createextension.html "PostgreSQL 11 -
CREATE EXTENSION") / [10](/docs/10/sql-createextension.html "PostgreSQL 10 -
CREATE EXTENSION") / [9.6](/docs/9.6/sql-createextension.html "PostgreSQL 9.6
- CREATE EXTENSION") / [9.5](/docs/9.5/sql-createextension.html "PostgreSQL
9.5 - CREATE EXTENSION") / [9.4](/docs/9.4/sql-createextension.html
"PostgreSQL 9.4 - CREATE EXTENSION") / [9.3](/docs/9.3/sql-
createextension.html "PostgreSQL 9.3 - CREATE EXTENSION") /
[9.2](/docs/9.2/sql-createextension.html "PostgreSQL 9.2 - CREATE EXTENSION")
/ [9.1](/docs/9.1/sql-createextension.html "PostgreSQL 9.1 - CREATE
EXTENSION")

__

CREATE EXTENSION  
---  
[Prev](sql-createeventtrigger.html "CREATE EVENT TRIGGER")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createforeigndatawrapper.html "CREATE FOREIGN DATA WRAPPER")  
  
* * *

## CREATE EXTENSION

CREATE EXTENSION — install an extension

## Synopsis

    
    
    CREATE EXTENSION [ IF NOT EXISTS ] _extension_name_
        [ WITH ] [ SCHEMA _schema_name_ ]
                 [ VERSION _version_ ]
                 [ CASCADE ]
    

## Description

`CREATE EXTENSION` loads a new extension into the current database. There must
not be an extension of the same name already loaded.

Loading an extension essentially amounts to running the extension's script
file. The script will typically create new SQL objects such as functions, data
types, operators and index support methods. `CREATE EXTENSION` additionally
records the identities of all the created objects, so that they can be dropped
again if `DROP EXTENSION` is issued.

The user who runs `CREATE EXTENSION` becomes the owner of the extension for
purposes of later privilege checks, and normally also becomes the owner of any
objects created by the extension's script.

Loading an extension ordinarily requires the same privileges that would be
required to create its component objects. For many extensions this means
superuser privileges are needed. However, if the extension is marked _trusted_
in its control file, then it can be installed by any user who has `CREATE`
privilege on the current database. In this case the extension object itself
will be owned by the calling user, but the contained objects will be owned by
the bootstrap superuser (unless the extension's script explicitly assigns them
to the calling user). This configuration gives the calling user the right to
drop the extension, but not to modify individual objects within it.

## Parameters

`IF NOT EXISTS`

    

Do not throw an error if an extension with the same name already exists. A
notice is issued in this case. Note that there is no guarantee that the
existing extension is anything like the one that would have been created from
the currently-available script file.

_`extension_name`_

    

The name of the extension to be installed. PostgreSQL will create the
extension using details from the file
`SHAREDIR/extension/`_`extension_name`_`.control`.

_`schema_name`_

    

The name of the schema in which to install the extension's objects, given that
the extension allows its contents to be relocated. The named schema must
already exist. If not specified, and the extension's control file does not
specify a schema either, the current default object creation schema is used.

If the extension specifies a `schema` parameter in its control file, then that
schema cannot be overridden with a `SCHEMA` clause. Normally, an error will be
raised if a `SCHEMA` clause is given and it conflicts with the extension's
`schema` parameter. However, if the `CASCADE` clause is also given, then
_`schema_name`_ is ignored when it conflicts. The given _`schema_name`_ will
be used for installation of any needed extensions that do not specify `schema`
in their control files.

Remember that the extension itself is not considered to be within any schema:
extensions have unqualified names that must be unique database-wide. But
objects belonging to the extension can be within schemas.

_`version`_

    

The version of the extension to install. This can be written as either an
identifier or a string literal. The default version is whatever is specified
in the extension's control file.

`CASCADE`

    

Automatically install any extensions that this extension depends on that are
not already installed. Their dependencies are likewise automatically
installed, recursively. The `SCHEMA` clause, if given, applies to all
extensions that get installed this way. Other options of the statement are not
applied to automatically-installed extensions; in particular, their default
versions are always selected.

## Notes

Before you can use `CREATE EXTENSION` to load an extension into a database,
the extension's supporting files must be installed. Information about
installing the extensions supplied with PostgreSQL can be found in [Additional
Supplied Modules](contrib.html "Appendix F. Additional Supplied Modules and
Extensions").

The extensions currently available for loading can be identified from the
[`pg_available_extensions`](view-pg-available-extensions.html
"54.2. pg_available_extensions") or [`pg_available_extension_versions`](view-
pg-available-extension-versions.html "54.3. pg_available_extension_versions")
system views.

### Caution

Installing an extension as superuser requires trusting that the extension's
author wrote the extension installation script in a secure fashion. It is not
terribly difficult for a malicious user to create trojan-horse objects that
will compromise later execution of a carelessly-written extension script,
allowing that user to acquire superuser privileges. However, trojan-horse
objects are only hazardous if they are in the `search_path` during script
execution, meaning that they are in the extension's installation target schema
or in the schema of some extension it depends on. Therefore, a good rule of
thumb when dealing with extensions whose scripts have not been carefully
vetted is to install them only into schemas for which CREATE privilege has not
been and will not be granted to any untrusted users. Likewise for any
extensions they depend on.

The extensions supplied with PostgreSQL are believed to be secure against
installation-time attacks of this sort, except for a few that depend on other
extensions. As stated in the documentation for those extensions, they should
be installed into secure schemas, or installed into the same schemas as the
extensions they depend on, or both.

For information about writing new extensions, see [Section 38.17](extend-
extensions.html "38.17. Packaging Related Objects into an Extension").

## Examples

Install the [hstore](hstore.html "F.18. hstore — hstore key/value datatype")
extension into the current database, placing its objects in schema `addons`:

    
    
    CREATE EXTENSION hstore SCHEMA addons;
    

Another way to accomplish the same thing:

    
    
    SET search_path = addons;
    CREATE EXTENSION hstore;
    

## Compatibility

`CREATE EXTENSION` is a PostgreSQL extension.

## See Also

[ALTER EXTENSION](sql-alterextension.html "ALTER EXTENSION"), [DROP
EXTENSION](sql-dropextension.html "DROP EXTENSION")

* * *

[Prev](sql-createeventtrigger.html "CREATE EVENT TRIGGER")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createforeigndatawrapper.html "CREATE FOREIGN DATA WRAPPER")  
---|---|---  
CREATE EVENT TRIGGER  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE FOREIGN DATA WRAPPER  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createextension.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

