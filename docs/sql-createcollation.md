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

Supported Versions: [Current](/docs/current/sql-createcollation.html
"PostgreSQL 17 - CREATE COLLATION") ([17](/docs/17/sql-createcollation.html
"PostgreSQL 17 - CREATE COLLATION")) / [16](/docs/16/sql-createcollation.html
"PostgreSQL 16 - CREATE COLLATION") / [15](/docs/15/sql-createcollation.html
"PostgreSQL 15 - CREATE COLLATION") / [14](/docs/14/sql-createcollation.html
"PostgreSQL 14 - CREATE COLLATION") / [13](/docs/13/sql-createcollation.html
"PostgreSQL 13 - CREATE COLLATION")

Development Versions: [18](/docs/18/sql-createcollation.html "PostgreSQL 18 -
CREATE COLLATION") / [devel](/docs/devel/sql-createcollation.html "PostgreSQL
devel - CREATE COLLATION")

Unsupported versions: [12](/docs/12/sql-createcollation.html "PostgreSQL 12 -
CREATE COLLATION") / [11](/docs/11/sql-createcollation.html "PostgreSQL 11 -
CREATE COLLATION") / [10](/docs/10/sql-createcollation.html "PostgreSQL 10 -
CREATE COLLATION") / [9.6](/docs/9.6/sql-createcollation.html "PostgreSQL 9.6
- CREATE COLLATION") / [9.5](/docs/9.5/sql-createcollation.html "PostgreSQL
9.5 - CREATE COLLATION") / [9.4](/docs/9.4/sql-createcollation.html
"PostgreSQL 9.4 - CREATE COLLATION") / [9.3](/docs/9.3/sql-
createcollation.html "PostgreSQL 9.3 - CREATE COLLATION") /
[9.2](/docs/9.2/sql-createcollation.html "PostgreSQL 9.2 - CREATE COLLATION")
/ [9.1](/docs/9.1/sql-createcollation.html "PostgreSQL 9.1 - CREATE
COLLATION")

__

CREATE COLLATION  
---  
[Prev](sql-createcast.html "CREATE CAST")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createconversion.html "CREATE CONVERSION")  
  
* * *

## CREATE COLLATION

CREATE COLLATION — define a new collation

## Synopsis

    
    
    CREATE COLLATION [ IF NOT EXISTS ] _name_ (
        [ LOCALE = _locale_ , ]
        [ LC_COLLATE = _lc_collate_ , ]
        [ LC_CTYPE = _lc_ctype_ , ]
        [ PROVIDER = _provider_ , ]
        [ DETERMINISTIC = _boolean_ , ]
        [ RULES = _rules_ , ]
        [ VERSION = _version_ ]
    )
    CREATE COLLATION [ IF NOT EXISTS ] _name_ FROM _existing_collation_
    

## Description

`CREATE COLLATION` defines a new collation using the specified operating
system locale settings, or by copying an existing collation.

To be able to create a collation, you must have `CREATE` privilege on the
destination schema.

## Parameters

`IF NOT EXISTS`

    

Do not throw an error if a collation with the same name already exists. A
notice is issued in this case. Note that there is no guarantee that the
existing collation is anything like the one that would have been created.

_`name`_

    

The name of the collation. The collation name can be schema-qualified. If it
is not, the collation is defined in the current schema. The collation name
must be unique within that schema. (The system catalogs can contain collations
with the same name for other encodings, but these are ignored if the database
encoding does not match.)

_`locale`_

    

The locale name for this collation. See [Section
24.2.2.3.1](collation.html#COLLATION-MANAGING-CREATE-LIBC "24.2.2.3.1. libc
Collations") and [Section 24.2.2.3.2](collation.html#COLLATION-MANAGING-
CREATE-ICU "24.2.2.3.2. ICU Collations") for details.

If _`provider`_ is `libc`, this is a shortcut for setting `LC_COLLATE` and
`LC_CTYPE` at once. If you specify _`locale`_ , you cannot specify either of
those parameters.

_`lc_collate`_

    

If _`provider`_ is `libc`, use the specified operating system locale for the
`LC_COLLATE` locale category.

_`lc_ctype`_

    

If _`provider`_ is `libc`, use the specified operating system locale for the
`LC_CTYPE` locale category.

_`provider`_

    

Specifies the provider to use for locale services associated with this
collation. Possible values are `icu` (if the server was built with ICU
support) or `libc`. `libc` is the default. See [Section
24.1.4](locale.html#LOCALE-PROVIDERS "24.1.4. Locale Providers") for details.

`DETERMINISTIC`

    

Specifies whether the collation should use deterministic comparisons. The
default is true. A deterministic comparison considers strings that are not
byte-wise equal to be unequal even if they are considered logically equal by
the comparison. PostgreSQL breaks ties using a byte-wise comparison.
Comparison that is not deterministic can make the collation be, say, case- or
accent-insensitive. For that, you need to choose an appropriate `LOCALE`
setting _and_ set the collation to not deterministic here.

Nondeterministic collations are only supported with the ICU provider.

_`rules`_

    

Specifies additional collation rules to customize the behavior of the
collation. This is supported for ICU only. See [Section
24.2.3.4](collation.html#ICU-TAILORING-RULES "24.2.3.4. ICU Tailoring Rules")
for details.

_`version`_

    

Specifies the version string to store with the collation. Normally, this
should be omitted, which will cause the version to be computed from the actual
version of the collation as provided by the operating system. This option is
intended to be used by `pg_upgrade` for copying the version from an existing
installation.

See also [ALTER COLLATION](sql-altercollation.html "ALTER COLLATION") for how
to handle collation version mismatches.

_`existing_collation`_

    

The name of an existing collation to copy. The new collation will have the
same properties as the existing one, but it will be an independent object.

## Notes

`CREATE COLLATION` takes a `SHARE ROW EXCLUSIVE` lock, which is self-
conflicting, on the `pg_collation` system catalog, so only one `CREATE
COLLATION` command can run at a time.

Use `DROP COLLATION` to remove user-defined collations.

See [Section 24.2.2.3](collation.html#COLLATION-CREATE "24.2.2.3. Creating New
Collation Objects") for more information on how to create collations.

When using the `libc` collation provider, the locale must be applicable to the
current database encoding. See [CREATE DATABASE](sql-createdatabase.html
"CREATE DATABASE") for the precise rules.

## Examples

To create a collation from the operating system locale `fr_FR.utf8` (assuming
the current database encoding is `UTF8`):

    
    
    CREATE COLLATION french (locale = 'fr_FR.utf8');
    

To create a collation using the ICU provider using German phone book sort
order:

    
    
    CREATE COLLATION german_phonebook (provider = icu, locale = 'de-u-co-phonebk');
    

To create a collation using the ICU provider, based on the root ICU locale,
with custom rules:

    
    
    CREATE COLLATION custom (provider = icu, locale = 'und', rules = '&V << w <<< W');
    

See [Section 24.2.3.4](collation.html#ICU-TAILORING-RULES "24.2.3.4. ICU
Tailoring Rules") for further details and examples on the rules syntax.

To create a collation from an existing collation:

    
    
    CREATE COLLATION german FROM "de_DE";
    

This can be convenient to be able to use operating-system-independent
collation names in applications.

## Compatibility

There is a `CREATE COLLATION` statement in the SQL standard, but it is limited
to copying an existing collation. The syntax to create a new collation is a
PostgreSQL extension.

## See Also

[ALTER COLLATION](sql-altercollation.html "ALTER COLLATION"), [DROP
COLLATION](sql-dropcollation.html "DROP COLLATION")

* * *

[Prev](sql-createcast.html "CREATE CAST")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createconversion.html "CREATE CONVERSION")  
---|---|---  
CREATE CAST  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE CONVERSION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createcollation.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

