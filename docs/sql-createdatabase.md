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

Supported Versions: [Current](/docs/current/sql-createdatabase.html
"PostgreSQL 17 - CREATE DATABASE") ([17](/docs/17/sql-createdatabase.html
"PostgreSQL 17 - CREATE DATABASE")) / [16](/docs/16/sql-createdatabase.html
"PostgreSQL 16 - CREATE DATABASE") / [15](/docs/15/sql-createdatabase.html
"PostgreSQL 15 - CREATE DATABASE") / [14](/docs/14/sql-createdatabase.html
"PostgreSQL 14 - CREATE DATABASE") / [13](/docs/13/sql-createdatabase.html
"PostgreSQL 13 - CREATE DATABASE")

Development Versions: [18](/docs/18/sql-createdatabase.html "PostgreSQL 18 -
CREATE DATABASE") / [devel](/docs/devel/sql-createdatabase.html "PostgreSQL
devel - CREATE DATABASE")

Unsupported versions: [12](/docs/12/sql-createdatabase.html "PostgreSQL 12 -
CREATE DATABASE") / [11](/docs/11/sql-createdatabase.html "PostgreSQL 11 -
CREATE DATABASE") / [10](/docs/10/sql-createdatabase.html "PostgreSQL 10 -
CREATE DATABASE") / [9.6](/docs/9.6/sql-createdatabase.html "PostgreSQL 9.6 -
CREATE DATABASE") / [9.5](/docs/9.5/sql-createdatabase.html "PostgreSQL 9.5 -
CREATE DATABASE") / [9.4](/docs/9.4/sql-createdatabase.html "PostgreSQL 9.4 -
CREATE DATABASE") / [9.3](/docs/9.3/sql-createdatabase.html "PostgreSQL 9.3 -
CREATE DATABASE") / [9.2](/docs/9.2/sql-createdatabase.html "PostgreSQL 9.2 -
CREATE DATABASE") / [9.1](/docs/9.1/sql-createdatabase.html "PostgreSQL 9.1 -
CREATE DATABASE") / [9.0](/docs/9.0/sql-createdatabase.html "PostgreSQL 9.0 -
CREATE DATABASE") / [8.4](/docs/8.4/sql-createdatabase.html "PostgreSQL 8.4 -
CREATE DATABASE") / [8.3](/docs/8.3/sql-createdatabase.html "PostgreSQL 8.3 -
CREATE DATABASE") / [8.2](/docs/8.2/sql-createdatabase.html "PostgreSQL 8.2 -
CREATE DATABASE") / [8.1](/docs/8.1/sql-createdatabase.html "PostgreSQL 8.1 -
CREATE DATABASE") / [8.0](/docs/8.0/sql-createdatabase.html "PostgreSQL 8.0 -
CREATE DATABASE") / [7.4](/docs/7.4/sql-createdatabase.html "PostgreSQL 7.4 -
CREATE DATABASE") / [7.3](/docs/7.3/sql-createdatabase.html "PostgreSQL 7.3 -
CREATE DATABASE") / [7.2](/docs/7.2/sql-createdatabase.html "PostgreSQL 7.2 -
CREATE DATABASE") / [7.1](/docs/7.1/sql-createdatabase.html "PostgreSQL 7.1 -
CREATE DATABASE")

__

CREATE DATABASE  
---  
[Prev](sql-createconversion.html "CREATE CONVERSION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-createdomain.html "CREATE DOMAIN")  
  
* * *

## CREATE DATABASE

CREATE DATABASE — create a new database

## Synopsis

    
    
    CREATE DATABASE _name_
        [ WITH ] [ OWNER [=] _user_name_ ]
               [ TEMPLATE [=] _template_ ]
               [ ENCODING [=] _encoding_ ]
               [ STRATEGY [=] _strategy_ ]
               [ LOCALE [=] _locale_ ]
               [ LC_COLLATE [=] _lc_collate_ ]
               [ LC_CTYPE [=] _lc_ctype_ ]
               [ ICU_LOCALE [=] _icu_locale_ ]
               [ ICU_RULES [=] _icu_rules_ ]
               [ LOCALE_PROVIDER [=] _locale_provider_ ]
               [ COLLATION_VERSION = _collation_version_ ]
               [ TABLESPACE [=] _tablespace_name_ ]
               [ ALLOW_CONNECTIONS [=] _allowconn_ ]
               [ CONNECTION LIMIT [=] _connlimit_ ]
               [ IS_TEMPLATE [=] _istemplate_ ]
               [ OID [=] _oid_ ]
    

## Description

`CREATE DATABASE` creates a new PostgreSQL database.

To create a database, you must be a superuser or have the special `CREATEDB`
privilege. See [CREATE ROLE](sql-createrole.html "CREATE ROLE").

By default, the new database will be created by cloning the standard system
database `template1`. A different template can be specified by writing
`TEMPLATE _`name`_`. In particular, by writing `TEMPLATE template0`, you can
create a pristine database (one where no user-defined objects exist and where
the system objects have not been altered) containing only the standard objects
predefined by your version of PostgreSQL. This is useful if you wish to avoid
copying any installation-local objects that might have been added to
`template1`.

## Parameters

_`name`_ #

    

The name of a database to create.

_`user_name`_ #

    

The role name of the user who will own the new database, or `DEFAULT` to use
the default (namely, the user executing the command). To create a database
owned by another role, you must be able to `SET ROLE` to that role.

_`template`_ #

    

The name of the template from which to create the new database, or `DEFAULT`
to use the default template (`template1`).

_`encoding`_ #

    

Character set encoding to use in the new database. Specify a string constant
(e.g., `'SQL_ASCII'`), or an integer encoding number, or `DEFAULT` to use the
default encoding (namely, the encoding of the template database). The
character sets supported by the PostgreSQL server are described in [Section
24.3.1](multibyte.html#MULTIBYTE-CHARSET-SUPPORTED "24.3.1. Supported
Character Sets"). See below for additional restrictions.

_`strategy`_ #

    

Strategy to be used in creating the new database. If the `WAL_LOG` strategy is
used, the database will be copied block by block and each block will be
separately written to the write-ahead log. This is the most efficient strategy
in cases where the template database is small, and therefore it is the
default. The older `FILE_COPY` strategy is also available. This strategy
writes a small record to the write-ahead log for each tablespace used by the
target database. Each such record represents copying an entire directory to a
new location at the filesystem level. While this does reduce the write-ahead
log volume substantially, especially if the template database is large, it
also forces the system to perform a checkpoint both before and after the
creation of the new database. In some situations, this may have a noticeable
negative impact on overall system performance.

_`locale`_ #

    

Sets the default collation order and character classification in the new
database. Collation affects the sort order applied to strings, e.g., in
queries with `ORDER BY`, as well as the order used in indexes on text columns.
Character classification affects the categorization of characters, e.g.,
lower, upper, and digit. Also sets the associated aspects of the operating
system environment, `LC_COLLATE` and `LC_CTYPE`. The default is the same
setting as the template database. See [Section
24.2.2.3.1](collation.html#COLLATION-MANAGING-CREATE-LIBC "24.2.2.3.1. libc
Collations") and [Section 24.2.2.3.2](collation.html#COLLATION-MANAGING-
CREATE-ICU "24.2.2.3.2. ICU Collations") for details.

Can be overridden by setting [_`lc_collate`_](sql-createdatabase.html#CREATE-
DATABASE-LC-COLLATE), [_`lc_ctype`_](sql-createdatabase.html#CREATE-DATABASE-
LC-CTYPE), or [_`icu_locale`_](sql-createdatabase.html#CREATE-DATABASE-ICU-
LOCALE) individually.

### Tip

The other locale settings [lc_messages](runtime-config-client.html#GUC-LC-
MESSAGES), [lc_monetary](runtime-config-client.html#GUC-LC-MONETARY),
[lc_numeric](runtime-config-client.html#GUC-LC-NUMERIC), and
[lc_time](runtime-config-client.html#GUC-LC-TIME) are not fixed per database
and are not set by this command. If you want to make them the default for a
specific database, you can use `ALTER DATABASE ... SET`.

_`lc_collate`_ #

    

Sets `LC_COLLATE` in the database server's operating system environment. The
default is the setting of [_`locale`_](sql-createdatabase.html#CREATE-
DATABASE-LOCALE) if specified, otherwise the same setting as the template
database. See below for additional restrictions.

If [_`locale_provider`_](sql-createdatabase.html#CREATE-DATABASE-LOCALE-
PROVIDER) is `libc`, also sets the default collation order to use in the new
database, overriding the setting [_`locale`_](sql-createdatabase.html#CREATE-
DATABASE-LOCALE).

_`lc_ctype`_ #

    

Sets `LC_CTYPE` in the database server's operating system environment. The
default is the setting of [_`locale`_](sql-createdatabase.html#CREATE-
DATABASE-LOCALE) if specified, otherwise the same setting as the template
database. See below for additional restrictions.

If [_`locale_provider`_](sql-createdatabase.html#CREATE-DATABASE-LOCALE-
PROVIDER) is `libc`, also sets the default character classification to use in
the new database, overriding the setting [_`locale`_](sql-
createdatabase.html#CREATE-DATABASE-LOCALE).

_`icu_locale`_ #

    

Specifies the ICU locale (see [Section 24.2.2.3.2](collation.html#COLLATION-
MANAGING-CREATE-ICU "24.2.2.3.2. ICU Collations")) for the database default
collation order and character classification, overriding the setting
[_`locale`_](sql-createdatabase.html#CREATE-DATABASE-LOCALE). The [locale
provider](sql-createdatabase.html#CREATE-DATABASE-LOCALE-PROVIDER) must be
ICU. The default is the setting of [_`locale`_](sql-
createdatabase.html#CREATE-DATABASE-LOCALE) if specified; otherwise the same
setting as the template database.

_`icu_rules`_ #

    

Specifies additional collation rules to customize the behavior of the default
collation of this database. This is supported for ICU only. See [Section
24.2.3.4](collation.html#ICU-TAILORING-RULES "24.2.3.4. ICU Tailoring Rules")
for details.

_`locale_provider`_ #

    

Specifies the provider to use for the default collation in this database.
Possible values are `icu` (if the server was built with ICU support) or
`libc`. By default, the provider is the same as that of the
[_`template`_](sql-createdatabase.html#CREATE-DATABASE-TEMPLATE). See [Section
24.1.4](locale.html#LOCALE-PROVIDERS "24.1.4. Locale Providers") for details.

_`collation_version`_ #

    

Specifies the collation version string to store with the database. Normally,
this should be omitted, which will cause the version to be computed from the
actual version of the database collation as provided by the operating system.
This option is intended to be used by `pg_upgrade` for copying the version
from an existing installation.

See also [ALTER DATABASE](sql-alterdatabase.html "ALTER DATABASE") for how to
handle database collation version mismatches.

_`tablespace_name`_ #

    

The name of the tablespace that will be associated with the new database, or
`DEFAULT` to use the template database's tablespace. This tablespace will be
the default tablespace used for objects created in this database. See [CREATE
TABLESPACE](sql-createtablespace.html "CREATE TABLESPACE") for more
information.

_`allowconn`_ #

    

If false then no one can connect to this database. The default is true,
allowing connections (except as restricted by other mechanisms, such as
`GRANT`/`REVOKE CONNECT`).

_`connlimit`_ #

    

How many concurrent connections can be made to this database. -1 (the default)
means no limit.

_`istemplate`_ #

    

If true, then this database can be cloned by any user with `CREATEDB`
privileges; if false (the default), then only superusers or the owner of the
database can clone it.

_`oid`_ #

    

The object identifier to be used for the new database. If this parameter is
not specified, PostgreSQL will choose a suitable OID automatically. This
parameter is primarily intended for internal use by pg_upgrade, and only
pg_upgrade can specify a value less than 16384.

Optional parameters can be written in any order, not only the order
illustrated above.

## Notes

`CREATE DATABASE` cannot be executed inside a transaction block.

Errors along the line of “could not initialize database directory” are most
likely related to insufficient permissions on the data directory, a full disk,
or other file system problems.

Use [`DROP DATABASE`](sql-dropdatabase.html "DROP DATABASE") to remove a
database.

The program [createdb](app-createdb.html "createdb") is a wrapper program
around this command, provided for convenience.

Database-level configuration parameters (set via [`ALTER DATABASE`](sql-
alterdatabase.html "ALTER DATABASE")) and database-level permissions (set via
[`GRANT`](sql-grant.html "GRANT")) are not copied from the template database.

Although it is possible to copy a database other than `template1` by
specifying its name as the template, this is not (yet) intended as a general-
purpose “`COPY DATABASE`” facility. The principal limitation is that no other
sessions can be connected to the template database while it is being copied.
`CREATE DATABASE` will fail if any other connection exists when it starts;
otherwise, new connections to the template database are locked out until
`CREATE DATABASE` completes. See [Section 23.3](manage-ag-templatedbs.html
"23.3. Template Databases") for more information.

The character set encoding specified for the new database must be compatible
with the chosen locale settings (`LC_COLLATE` and `LC_CTYPE`). If the locale
is `C` (or equivalently `POSIX`), then all encodings are allowed, but for
other locale settings there is only one encoding that will work properly. (On
Windows, however, UTF-8 encoding can be used with any locale.) `CREATE
DATABASE` will allow superusers to specify `SQL_ASCII` encoding regardless of
the locale settings, but this choice is deprecated and may result in
misbehavior of character-string functions if data that is not encoding-
compatible with the locale is stored in the database.

The encoding and locale settings must match those of the template database,
except when `template0` is used as template. This is because other databases
might contain data that does not match the specified encoding, or might
contain indexes whose sort ordering is affected by `LC_COLLATE` and
`LC_CTYPE`. Copying such data would result in a database that is corrupt
according to the new settings. `template0`, however, is known to not contain
any data or indexes that would be affected.

There is currently no option to use a database locale with nondeterministic
comparisons (see [`CREATE COLLATION`](sql-createcollation.html "CREATE
COLLATION") for an explanation). If this is needed, then per-column collations
would need to be used.

The `CONNECTION LIMIT` option is only enforced approximately; if two new
sessions start at about the same time when just one connection “slot” remains
for the database, it is possible that both will fail. Also, the limit is not
enforced against superusers or background worker processes.

## Examples

To create a new database:

    
    
    CREATE DATABASE lusiadas;
    

To create a database `sales` owned by user `salesapp` with a default
tablespace of `salesspace`:

    
    
    CREATE DATABASE sales OWNER salesapp TABLESPACE salesspace;
    

To create a database `music` with a different locale:

    
    
    CREATE DATABASE music
        LOCALE 'sv_SE.utf8'
        TEMPLATE template0;
    

In this example, the `TEMPLATE template0` clause is required if the specified
locale is different from the one in `template1`. (If it is not, then
specifying the locale explicitly is redundant.)

To create a database `music2` with a different locale and a different
character set encoding:

    
    
    CREATE DATABASE music2
        LOCALE 'sv_SE.iso885915'
        ENCODING LATIN9
        TEMPLATE template0;
    

The specified locale and encoding settings must match, or an error will be
reported.

Note that locale names are specific to the operating system, so that the above
commands might not work in the same way everywhere.

## Compatibility

There is no `CREATE DATABASE` statement in the SQL standard. Databases are
equivalent to catalogs, whose creation is implementation-defined.

## See Also

[ALTER DATABASE](sql-alterdatabase.html "ALTER DATABASE"), [DROP
DATABASE](sql-dropdatabase.html "DROP DATABASE")

* * *

[Prev](sql-createconversion.html "CREATE CONVERSION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-createdomain.html "CREATE DOMAIN")  
---|---|---  
CREATE CONVERSION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  CREATE DOMAIN  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-createdatabase.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

