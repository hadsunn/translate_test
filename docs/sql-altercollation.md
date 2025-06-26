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

Supported Versions: [Current](/docs/current/sql-altercollation.html
"PostgreSQL 17 - ALTER COLLATION") ([17](/docs/17/sql-altercollation.html
"PostgreSQL 17 - ALTER COLLATION")) / [16](/docs/16/sql-altercollation.html
"PostgreSQL 16 - ALTER COLLATION") / [15](/docs/15/sql-altercollation.html
"PostgreSQL 15 - ALTER COLLATION") / [14](/docs/14/sql-altercollation.html
"PostgreSQL 14 - ALTER COLLATION") / [13](/docs/13/sql-altercollation.html
"PostgreSQL 13 - ALTER COLLATION")

Development Versions: [18](/docs/18/sql-altercollation.html "PostgreSQL 18 -
ALTER COLLATION") / [devel](/docs/devel/sql-altercollation.html "PostgreSQL
devel - ALTER COLLATION")

Unsupported versions: [12](/docs/12/sql-altercollation.html "PostgreSQL 12 -
ALTER COLLATION") / [11](/docs/11/sql-altercollation.html "PostgreSQL 11 -
ALTER COLLATION") / [10](/docs/10/sql-altercollation.html "PostgreSQL 10 -
ALTER COLLATION") / [9.6](/docs/9.6/sql-altercollation.html "PostgreSQL 9.6 -
ALTER COLLATION") / [9.5](/docs/9.5/sql-altercollation.html "PostgreSQL 9.5 -
ALTER COLLATION") / [9.4](/docs/9.4/sql-altercollation.html "PostgreSQL 9.4 -
ALTER COLLATION") / [9.3](/docs/9.3/sql-altercollation.html "PostgreSQL 9.3 -
ALTER COLLATION") / [9.2](/docs/9.2/sql-altercollation.html "PostgreSQL 9.2 -
ALTER COLLATION") / [9.1](/docs/9.1/sql-altercollation.html "PostgreSQL 9.1 -
ALTER COLLATION")

__

ALTER COLLATION  
---  
[Prev](sql-alteraggregate.html "ALTER AGGREGATE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-alterconversion.html "ALTER CONVERSION")  
  
* * *

## ALTER COLLATION

ALTER COLLATION — change the definition of a collation

## Synopsis

    
    
    ALTER COLLATION _name_ REFRESH VERSION
    
    ALTER COLLATION _name_ RENAME TO _new_name_
    ALTER COLLATION _name_ OWNER TO { _new_owner_ | CURRENT_ROLE | CURRENT_USER | SESSION_USER }
    ALTER COLLATION _name_ SET SCHEMA _new_schema_
    

## Description

`ALTER COLLATION` changes the definition of a collation.

You must own the collation to use `ALTER COLLATION`. To alter the owner, you
must be able to `SET ROLE` to the new owning role, and that role must have
`CREATE` privilege on the collation's schema. (These restrictions enforce that
altering the owner doesn't do anything you couldn't do by dropping and
recreating the collation. However, a superuser can alter ownership of any
collation anyway.)

## Parameters

_`name`_

    

The name (optionally schema-qualified) of an existing collation.

_`new_name`_

    

The new name of the collation.

_`new_owner`_

    

The new owner of the collation.

_`new_schema`_

    

The new schema for the collation.

`REFRESH VERSION`

    

Update the collation's version. See [Notes](sql-altercollation.html#SQL-
ALTERCOLLATION-NOTES "Notes") below.

## Notes

When a collation object is created, the provider-specific version of the
collation is recorded in the system catalog. When the collation is used, the
current version is checked against the recorded version, and a warning is
issued when there is a mismatch, for example:

    
    
    WARNING:  collation "xx-x-icu" has version mismatch
    DETAIL:  The collation in the database was created using version 1.2.3.4, but the operating system provides version 2.3.4.5.
    HINT:  Rebuild all objects affected by this collation and run ALTER COLLATION pg_catalog."xx-x-icu" REFRESH VERSION, or build PostgreSQL with the right library version.
    

A change in collation definitions can lead to corrupt indexes and other
problems because the database system relies on stored objects having a certain
sort order. Generally, this should be avoided, but it can happen in legitimate
circumstances, such as when upgrading the operating system to a new major
version or when using `pg_upgrade` to upgrade to server binaries linked with a
newer version of ICU. When this happens, all objects depending on the
collation should be rebuilt, for example, using `REINDEX`. When that is done,
the collation version can be refreshed using the command `ALTER COLLATION ...
REFRESH VERSION`. This will update the system catalog to record the current
collation version and will make the warning go away. Note that this does not
actually check whether all affected objects have been rebuilt correctly.

When using collations provided by `libc`, version information is recorded on
systems using the GNU C library (most Linux systems), FreeBSD and Windows.
When using collations provided by ICU, the version information is provided by
the ICU library and is available on all platforms.

### Note

When using the GNU C library for collations, the C library's version is used
as a proxy for the collation version. Many Linux distributions change
collation definitions only when upgrading the C library, but this approach is
imperfect as maintainers are free to back-port newer collation definitions to
older C library releases.

When using Windows for collations, version information is only available for
collations defined with BCP 47 language tags such as `en-US`.

For the database default collation, there is an analogous command `ALTER
DATABASE ... REFRESH COLLATION VERSION`.

The following query can be used to identify all collations in the current
database that need to be refreshed and the objects that depend on them:

    
    
    SELECT pg_describe_object(refclassid, refobjid, refobjsubid) AS "Collation",
           pg_describe_object(classid, objid, objsubid) AS "Object"
      FROM pg_depend d JOIN pg_collation c
           ON refclassid = 'pg_collation'::regclass AND refobjid = c.oid
      WHERE c.collversion <> pg_collation_actual_version(c.oid)
      ORDER BY 1, 2;
    

## Examples

To rename the collation `de_DE` to `german`:

    
    
    ALTER COLLATION "de_DE" RENAME TO german;
    

To change the owner of the collation `en_US` to `joe`:

    
    
    ALTER COLLATION "en_US" OWNER TO joe;
    

## Compatibility

There is no `ALTER COLLATION` statement in the SQL standard.

## See Also

[CREATE COLLATION](sql-createcollation.html "CREATE COLLATION"), [DROP
COLLATION](sql-dropcollation.html "DROP COLLATION")

* * *

[Prev](sql-alteraggregate.html "ALTER AGGREGATE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-alterconversion.html "ALTER CONVERSION")  
---|---|---  
ALTER AGGREGATE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER CONVERSION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-altercollation.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

