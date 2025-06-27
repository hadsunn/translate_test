PostgreSQL: Documentation: 16: initdb                

[![PostgreSQL Elephant Logo](/media/img/about/press/elephant.png)][1]

*   [Home][2]
*   [About][3]
*   [Download][4]
*   [Documentation][5]
*   [Community][6]
*   [Developers][7]
*   [Support][8]
*   [Donate][9]
*   [Your account][10]

May 8, 2025: [PostgreSQL 17.5, 16.9, 15.13, 14.18, and 13.21 Released!][11] | [PostgreSQL 18 Beta 1 Released!][12]

[Documentation][13] → [PostgreSQL 16][14]

Supported Versions: [Current][15] ([17][16]) / [16][17] / [15][18] / [14][19] / [13][20]

Development Versions: [18][21] / [devel][22]

Unsupported versions: [12][23] / [11][24] / [10][25] / [9.6][26] / [9.5][27] / [9.4][28] / [9.3][29] / [9.2][30] / [9.1][31] / [9.0][32] / [8.4][33] / [8.3][34] / [8.2][35] / [8.1][36] / [8.0][37] / [7.4][38] / [7.3][39] / [7.2][40] / [7.1][41]

| initdb |     |     |     |     |
| --- | --- | --- | --- | --- |
| [Prev][42] | [Up][43] | PostgreSQL Server Applications | [Home][44] | [Next][45] |

- - -

## initdb

initdb — create a new PostgreSQL database cluster

## Synopsis

`initdb` \[_`option`_...\] \[ `--pgdata` | `-D` \] _`directory`_

## Description

`initdb` creates a new PostgreSQL [][46][database cluster][47].

Creating a database cluster consists of creating the [][48][directories][49] in which the cluster data will live, generating the shared catalog tables (tables that belong to the whole cluster rather than to any particular database), and creating the `postgres`, `template1`, and `template0` databases. The `postgres` database is a default database meant for use by users, utilities and third party applications. `template1` and `template0` are meant as source databases to be copied by later `CREATE DATABASE` commands. `template0` should never be modified, but you can add objects to `template1`, which by default will be copied into databases created later. See [Section 23.3][50] for more details.

Although `initdb` will attempt to create the specified data directory, it might not have permission if the parent directory of the desired data directory is root-owned. To initialize in such a setup, create an empty data directory as root, then use `chown` to assign ownership of that directory to the database user account, then `su` to become the database user to run `initdb`.

`initdb` must be run as the user that will own the server process, because the server needs to have access to the files and directories that `initdb` creates. Since the server cannot be run as root, you must not run `initdb` as root either. (It will in fact refuse to do so.)

For security reasons the new cluster created by `initdb` will only be accessible by the cluster owner by default. The `--allow-group-access` option allows any user in the same group as the cluster owner to read files in the cluster. This is useful for performing backups as a non-privileged user.

`initdb` initializes the database cluster's default locale and character set encoding. These can also be set separately for each database when it is created. `initdb` determines those settings for the template databases, which will serve as the default for all other databases.

By default, `initdb` uses the locale provider `libc` (see [Section 24.1.4][51]). The `libc` locale provider takes the locale settings from the environment, and determines the encoding from the locale settings.

To choose a different locale for the cluster, use the option `--locale`. There are also individual options `--lc-*` and `--icu-locale` (see below) to set values for the individual locale categories. Note that inconsistent settings for different locale categories can give nonsensical results, so this should be used with care.

Alternatively, `initdb` can use the ICU library to provide locale services by specifying `--locale-provider=icu`. The server must be built with ICU support. To choose the specific ICU locale ID to apply, use the option `--icu-locale`. Note that for implementation reasons and to support legacy code, `initdb` will still select and initialize libc locale settings when the ICU locale provider is used.

When `initdb` runs, it will print out the locale settings it has chosen. If you have complex requirements or specified multiple options, it is advisable to check that the result matches what was intended.

More details about locale settings can be found in [Section 24.1][52].

To alter the default encoding, use the `--encoding`. More details can be found in [Section 24.3][53].

## Options

``-A _`authmethod`_``  
``--auth=_`authmethod`_`` [#][54]

This option specifies the default authentication method for local users used in `pg_hba.conf` (`host` and `local` lines). See [Section 21.1][55] for an overview of valid values.

`initdb` will prepopulate `pg_hba.conf` entries using the specified authentication method for non-replication as well as replication connections.

Do not use `trust` unless you trust all local users on your system. `trust` is the default for ease of installation.

``--auth-host=_`authmethod`_`` [#][56]

This option specifies the authentication method for local users via TCP/IP connections used in `pg_hba.conf` (`host` lines).

``--auth-local=_`authmethod`_`` [#][57]

This option specifies the authentication method for local users via Unix-domain socket connections used in `pg_hba.conf` (`local` lines).

``-D _`directory`_``  
``--pgdata=_`directory`_`` [#][58]

This option specifies the directory where the database cluster should be stored. This is the only information required by `initdb`, but you can avoid writing it by setting the `PGDATA` environment variable, which can be convenient since the database server (`postgres`) can find the data directory later by the same variable.

``-E _`encoding`_``  
``--encoding=_`encoding`_`` [#][59]

Selects the encoding of the template databases. This will also be the default encoding of any database you create later, unless you override it then. The character sets supported by the PostgreSQL server are described in [Section 24.3.1][60].

By default, the template database encoding is derived from the locale. If [`--no-locale`][61] is specified (or equivalently, if the locale is `C` or `POSIX`), then the default is `UTF8` for the ICU provider and `SQL_ASCII` for the `libc` provider.

`-g`  
`--allow-group-access` [#][62]

Allows users in the same group as the cluster owner to read all cluster files created by `initdb`. This option is ignored on Windows as it does not support POSIX\-style group permissions.

``--icu-locale=_`locale`_`` [#][63]

Specifies the ICU locale when the ICU provider is used. Locale support is described in [Section 24.1][64].

``--icu-rules=_`rules`_`` [#][65]

Specifies additional collation rules to customize the behavior of the default collation. This is supported for ICU only.

`-k`  
`--data-checksums` [#][66]

Use checksums on data pages to help detect corruption by the I/O system that would otherwise be silent. Enabling checksums may incur a noticeable performance penalty. If set, checksums are calculated for all objects, in all databases. All checksum failures will be reported in the [`pg_stat_database`][67] view. See [Section 30.2][68] for details.

``--locale=_`locale`_`` [#][69]

Sets the default locale for the database cluster. If this option is not specified, the locale is inherited from the environment that `initdb` runs in. Locale support is described in [Section 24.1][70].

``--lc-collate=_`locale`_``  
``--lc-ctype=_`locale`_``  
``--lc-messages=_`locale`_``  
``--lc-monetary=_`locale`_``  
``--lc-numeric=_`locale`_``  
``--lc-time=_`locale`_`` [#][71]

Like `--locale`, but only sets the locale in the specified category.

`--no-locale` [#][72]

Equivalent to `--locale=C`.

``--locale-provider={`libc`|`icu`}`` [#][73]

This option sets the locale provider for databases created in the new cluster. It can be overridden in the `CREATE DATABASE` command when new databases are subsequently created. The default is `libc` (see [Section 24.1.4][74]).

`-N`  
`--no-sync` [#][75]

By default, `initdb` will wait for all files to be written safely to disk. This option causes `initdb` to return without waiting, which is faster, but means that a subsequent operating system crash can leave the data directory corrupt. Generally, this option is useful for testing, but should not be used when creating a production installation.

`--no-instructions` [#][76]

By default, `initdb` will write instructions for how to start the cluster at the end of its output. This option causes those instructions to be left out. This is primarily intended for use by tools that wrap `initdb` in platform-specific behavior, where those instructions are likely to be incorrect.

``--pwfile=_`filename`_`` [#][77]

Makes `initdb` read the bootstrap superuser's password from a file. The first line of the file is taken as the password.

`-S`  
`--sync-only` [#][78]

Safely write all database files to disk and exit. This does not perform any of the normal initdb operations. Generally, this option is useful for ensuring reliable recovery after changing [fsync][79] from `off` to `on`.

``-T _`config`_``  
``--text-search-config=_`config`_`` [#][80]

Sets the default text search configuration. See [default\_text\_search\_config][81] for further information.

``-U _`username`_``  
``--username=_`username`_`` [#][82]

Sets the user name of the [][83][bootstrap superuser][84]. This defaults to the name of the operating-system user running `initdb`.

`-W`  
`--pwprompt` [#][85]

Makes `initdb` prompt for a password to give the bootstrap superuser. If you don't plan on using password authentication, this is not important. Otherwise you won't be able to use password authentication until you have a password set up.

``-X _`directory`_``  
``--waldir=_`directory`_`` [#][86]

This option specifies the directory where the write-ahead log should be stored.

``--wal-segsize=_`size`_`` [#][87]

Set the _WAL segment size_, in megabytes. This is the size of each individual file in the WAL log. The default size is 16 megabytes. The value must be a power of 2 between 1 and 1024 (megabytes). This option can only be set during initialization, and cannot be changed later.

It may be useful to adjust this size to control the granularity of WAL log shipping or archiving. Also, in databases with a high volume of WAL, the sheer number of WAL files per directory can become a performance and management problem. Increasing the WAL file size will reduce the number of WAL files.

Other, less commonly used, options are also available:

``-c _`name`_=_`value`_``  
``--set _`name`_=_`value`_`` [#][88]

Forcibly set the server parameter _`name`_ to _`value`_ during `initdb`, and also install that setting in the generated `postgresql.conf` file, so that it will apply during future server runs. This option can be given more than once to set several parameters. It is primarily useful when the environment is such that the server will not start at all using the default parameters.

`-d`  
`--debug` [#][89]

Print debugging output from the bootstrap backend and a few other messages of lesser interest for the general public. The bootstrap backend is the program `initdb` uses to create the catalog tables. This option generates a tremendous amount of extremely boring output.

`--discard-caches` [#][90]

Run the bootstrap backend with the `debug_discard_caches=1` option. This takes a very long time and is only of use for deep debugging.

``-L _`directory`_`` [#][91]

Specifies where `initdb` should find its input files to initialize the database cluster. This is normally not necessary. You will be told if you need to specify their location explicitly.

`-n`  
`--no-clean` [#][92]

By default, when `initdb` determines that an error prevented it from completely creating the database cluster, it removes any files it might have created before discovering that it cannot finish the job. This option inhibits tidying-up and is thus useful for debugging.

Other options:

`-V`  
`--version` [#][93]

Print the initdb version and exit.

`-?`  
`--help` [#][94]

Show help about initdb command line arguments, and exit.

## Environment

`PGDATA` [#][95]

Specifies the directory where the database cluster is to be stored; can be overridden using the `-D` option.

`PG_COLOR` [#][96]

Specifies whether to use color in diagnostic messages. Possible values are `always`, `auto` and `never`.

`TZ` [#][97]

Specifies the default time zone of the created database cluster. The value should be a full time zone name (see [Section 8.5.3][98]).

## Notes

`initdb` can also be invoked via `pg_ctl initdb`.

## See Also

[pg\_ctl][99], [postgres][100], [Section 21.1][101]

- - -

|     |     |     |
| --- | --- | --- |
| [Prev][102] | [Up][103] | [Next][104] |
| PostgreSQL Server Applications | [Home][105] | pg\_archivecleanup |

## Submit correction

If you see anything in the documentation that is not correct, does not match your experience with the particular feature or requires further clarification, please use [this form][106] to report a documentation issue.

[Privacy Policy][107] | [Code of Conduct][108] | [About PostgreSQL][109] | [Contact][110]  

Copyright © 1996-2025 The PostgreSQL Global Development Group

[1]: /
[2]: / "Home"
[3]: /about/ "About"
[4]: /download/ "Download"
[5]: /docs/ "Documentation"
[6]: /community/ "Community"
[7]: /developer/ "Developers"
[8]: /support/ "Support"
[9]: /about/donate/ "Donate"
[10]: /account/ "Your account"
[11]: /about/news/postgresql-175-169-1513-1418-and-1321-released-3072/
[12]: /about/news/postgresql-18-beta-1-released-3070/
[13]: /docs/ "Documentation"
[14]: /docs/16/index.html
[15]: /docs/current/app-initdb.html "PostgreSQL 17 - initdb"
[16]: /docs/17/app-initdb.html "PostgreSQL 17 - initdb"
[17]: /docs/16/app-initdb.html "PostgreSQL 16 - initdb"
[18]: /docs/15/app-initdb.html "PostgreSQL 15 - initdb"
[19]: /docs/14/app-initdb.html "PostgreSQL 14 - initdb"
[20]: /docs/13/app-initdb.html "PostgreSQL 13 - initdb"
[21]: /docs/18/app-initdb.html "PostgreSQL 18 - initdb"
[22]: /docs/devel/app-initdb.html "PostgreSQL devel - initdb"
[23]: /docs/12/app-initdb.html "PostgreSQL 12 - initdb"
[24]: /docs/11/app-initdb.html "PostgreSQL 11 - initdb"
[25]: /docs/10/app-initdb.html "PostgreSQL 10 - initdb"
[26]: /docs/9.6/app-initdb.html "PostgreSQL 9.6 - initdb"
[27]: /docs/9.5/app-initdb.html "PostgreSQL 9.5 - initdb"
[28]: /docs/9.4/app-initdb.html "PostgreSQL 9.4 - initdb"
[29]: /docs/9.3/app-initdb.html "PostgreSQL 9.3 - initdb"
[30]: /docs/9.2/app-initdb.html "PostgreSQL 9.2 - initdb"
[31]: /docs/9.1/app-initdb.html "PostgreSQL 9.1 - initdb"
[32]: /docs/9.0/app-initdb.html "PostgreSQL 9.0 - initdb"
[33]: /docs/8.4/app-initdb.html "PostgreSQL 8.4 - initdb"
[34]: /docs/8.3/app-initdb.html "PostgreSQL 8.3 - initdb"
[35]: /docs/8.2/app-initdb.html "PostgreSQL 8.2 - initdb"
[36]: /docs/8.1/app-initdb.html "PostgreSQL 8.1 - initdb"
[37]: /docs/8.0/app-initdb.html "PostgreSQL 8.0 - initdb"
[38]: /docs/7.4/app-initdb.html "PostgreSQL 7.4 - initdb"
[39]: /docs/7.3/app-initdb.html "PostgreSQL 7.3 - initdb"
[40]: /docs/7.2/app-initdb.html "PostgreSQL 7.2 - initdb"
[41]: /docs/7.1/app-initdb.html "PostgreSQL 7.1 - initdb"
[42]: reference-server.html "PostgreSQL Server Applications"
[43]: reference-server.html "PostgreSQL Server Applications"
[44]: index.html "PostgreSQL 16.9 Documentation"
[45]: pgarchivecleanup.html "pg_archivecleanup"
[46]: glossary.html#GLOSSARY-DB-CLUSTER
[47]: glossary.html#GLOSSARY-DB-CLUSTER "Database cluster"
[48]: glossary.html#GLOSSARY-DATA-DIRECTORY
[49]: glossary.html#GLOSSARY-DATA-DIRECTORY "Data directory"
[50]: manage-ag-templatedbs.html "23.3. Template Databases"
[51]: locale.html#LOCALE-PROVIDERS "24.1.4. Locale Providers"
[52]: locale.html "24.1. Locale Support"
[53]: multibyte.html "24.3. Character Set Support"
[54]: #APP-INITDB-OPTION-AUTH
[55]: auth-pg-hba-conf.html "21.1. The pg_hba.conf File"
[56]: #APP-INITDB-OPTION-AUTH-HOST
[57]: #APP-INITDB-OPTION-AUTH-LOCAL
[58]: #APP-INITDB-OPTION-PGDATA
[59]: #APP-INITDB-OPTION-ENCODING
[60]: multibyte.html#MULTIBYTE-CHARSET-SUPPORTED "24.3.1. Supported Character Sets"
[61]: app-initdb.html#APP-INITDB-OPTION-NO-LOCALE
[62]: #APP-INITDB-ALLOW-GROUP-ACCESS
[63]: #APP-INITDB-ICU-LOCALE
[64]: locale.html "24.1. Locale Support"
[65]: #APP-INITDB-ICU-RULES
[66]: #APP-INITDB-DATA-CHECKSUMS
[67]: monitoring-stats.html#MONITORING-PG-STAT-DATABASE-VIEW "28.2.16. pg_stat_database"
[68]: checksums.html "30.2. Data Checksums"
[69]: #APP-INITDB-OPTION-LOCALE
[70]: locale.html "24.1. Locale Support"
[71]: #APP-INITDB-OPTION-LC-COLLATE
[72]: #APP-INITDB-OPTION-NO-LOCALE
[73]: #APP-INITDB-OPTION-LOCALE-PROVIDER
[74]: locale.html#LOCALE-PROVIDERS "24.1.4. Locale Providers"
[75]: #APP-INITDB-OPTION-NO-SYNC
[76]: #APP-INITDB-OPTION-NO-INSTRUCTIONS
[77]: #APP-INITDB-OPTION-PWFILE
[78]: #APP-INITDB-OPTION-SYNC-ONLY
[79]: runtime-config-wal.html#GUC-FSYNC
[80]: #APP-INITDB-OPTION-TEXT-SEARCH-CONFIG
[81]: runtime-config-client.html#GUC-DEFAULT-TEXT-SEARCH-CONFIG
[82]: #APP-INITDB-OPTION-USERNAME
[83]: glossary.html#GLOSSARY-BOOTSTRAP-SUPERUSER
[84]: glossary.html#GLOSSARY-BOOTSTRAP-SUPERUSER "Bootstrap superuser"
[85]: #APP-INITDB-OPTION-PWPROMPT
[86]: #APP-INITDB-OPTION-WALDIR
[87]: #APP-INITDB-OPTION-WAL-SEGSIZE
[88]: #APP-INITDB-OPTION-SET
[89]: #APP-INITDB-OPTION-DEBUG
[90]: #APP-INITDB-OPTION-DISCARD-CACHES
[91]: #APP-INITDB-OPTION-L
[92]: #APP-INITDB-OPTION-NO-CLEAN
[93]: #APP-INITDB-OPTION-VERSION
[94]: #APP-INITDB-OPTION-HELP
[95]: #APP-INITDB-ENVIRONMENT-PGDATA
[96]: #APP-INITDB-ENVIRONMENT-PG-COLOR
[97]: #APP-INITDB-ENVIRONMENT-TZ
[98]: datatype-datetime.html#DATATYPE-TIMEZONES "8.5.3. Time Zones"
[99]: app-pg-ctl.html "pg_ctl"
[100]: app-postgres.html "postgres"
[101]: auth-pg-hba-conf.html "21.1. The pg_hba.conf File"
[102]: reference-server.html "PostgreSQL Server Applications"
[103]: reference-server.html "PostgreSQL Server Applications"
[104]: pgarchivecleanup.html "pg_archivecleanup"
[105]: index.html "PostgreSQL 16.9 Documentation"
[106]: /account/comments/new/16/app-initdb.html/
[107]: /about/privacypolicy
[108]: /about/policies/coc/
[109]: /about/
[110]: /about/contact/
