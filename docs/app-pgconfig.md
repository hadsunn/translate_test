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

Supported Versions: [Current](/docs/current/app-pgconfig.html "PostgreSQL 17 -
pg_config") ([17](/docs/17/app-pgconfig.html "PostgreSQL 17 - pg_config")) /
[16](/docs/16/app-pgconfig.html "PostgreSQL 16 - pg_config") /
[15](/docs/15/app-pgconfig.html "PostgreSQL 15 - pg_config") /
[14](/docs/14/app-pgconfig.html "PostgreSQL 14 - pg_config") /
[13](/docs/13/app-pgconfig.html "PostgreSQL 13 - pg_config")

Development Versions: [18](/docs/18/app-pgconfig.html "PostgreSQL 18 -
pg_config") / [devel](/docs/devel/app-pgconfig.html "PostgreSQL devel -
pg_config")

Unsupported versions: [12](/docs/12/app-pgconfig.html "PostgreSQL 12 -
pg_config") / [11](/docs/11/app-pgconfig.html "PostgreSQL 11 - pg_config") /
[10](/docs/10/app-pgconfig.html "PostgreSQL 10 - pg_config") /
[9.6](/docs/9.6/app-pgconfig.html "PostgreSQL 9.6 - pg_config") /
[9.5](/docs/9.5/app-pgconfig.html "PostgreSQL 9.5 - pg_config") /
[9.4](/docs/9.4/app-pgconfig.html "PostgreSQL 9.4 - pg_config") /
[9.3](/docs/9.3/app-pgconfig.html "PostgreSQL 9.3 - pg_config") /
[9.2](/docs/9.2/app-pgconfig.html "PostgreSQL 9.2 - pg_config") /
[9.1](/docs/9.1/app-pgconfig.html "PostgreSQL 9.1 - pg_config") /
[9.0](/docs/9.0/app-pgconfig.html "PostgreSQL 9.0 - pg_config") /
[8.4](/docs/8.4/app-pgconfig.html "PostgreSQL 8.4 - pg_config") /
[8.3](/docs/8.3/app-pgconfig.html "PostgreSQL 8.3 - pg_config") /
[8.2](/docs/8.2/app-pgconfig.html "PostgreSQL 8.2 - pg_config") /
[8.1](/docs/8.1/app-pgconfig.html "PostgreSQL 8.1 - pg_config") /
[8.0](/docs/8.0/app-pgconfig.html "PostgreSQL 8.0 - pg_config") /
[7.4](/docs/7.4/app-pgconfig.html "PostgreSQL 7.4 - pg_config") /
[7.3](/docs/7.3/app-pgconfig.html "PostgreSQL 7.3 - pg_config") /
[7.2](/docs/7.2/app-pgconfig.html "PostgreSQL 7.2 - pg_config") /
[7.1](/docs/7.1/app-pgconfig.html "PostgreSQL 7.1 - pg_config")

__

pg_config  
---  
[Prev](pgbench.html "pgbench")  | [Up](reference-client.html "PostgreSQL Client Applications") | PostgreSQL Client Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](app-pgdump.html "pg_dump")  
  
* * *

## pg_config

pg_config — retrieve information about the installed version of PostgreSQL

## Synopsis

`pg_config` [_`option`_...]

## Description

The pg_config utility prints configuration parameters of the currently
installed version of PostgreSQL. It is intended, for example, to be used by
software packages that want to interface to PostgreSQL to facilitate finding
the required header files and libraries.

## Options

To use pg_config, supply one or more of the following options:

`--bindir`

    

Print the location of user executables. Use this, for example, to find the
`psql` program. This is normally also the location where the `pg_config`
program resides.

`--docdir`

    

Print the location of documentation files.

`--htmldir`

    

Print the location of HTML documentation files.

`--includedir`

    

Print the location of C header files of the client interfaces.

`--pkgincludedir`

    

Print the location of other C header files.

`--includedir-server`

    

Print the location of C header files for server programming.

`--libdir`

    

Print the location of object code libraries.

`--pkglibdir`

    

Print the location of dynamically loadable modules, or where the server would
search for them. (Other architecture-dependent data files might also be
installed in this directory.)

`--localedir`

    

Print the location of locale support files. (This will be an empty string if
locale support was not configured when PostgreSQL was built.)

`--mandir`

    

Print the location of manual pages.

`--sharedir`

    

Print the location of architecture-independent support files.

`--sysconfdir`

    

Print the location of system-wide configuration files.

`--pgxs`

    

Print the location of extension makefiles.

`--configure`

    

Print the options that were given to the `configure` script when PostgreSQL
was configured for building. This can be used to reproduce the identical
configuration, or to find out with what options a binary package was built.
(Note however that binary packages often contain vendor-specific custom
patches.) See also the examples below.

`--cc`

    

Print the value of the `CC` variable that was used for building PostgreSQL.
This shows the C compiler used.

`--cppflags`

    

Print the value of the `CPPFLAGS` variable that was used for building
PostgreSQL. This shows C compiler switches needed at preprocessing time
(typically, `-I` switches).

`--cflags`

    

Print the value of the `CFLAGS` variable that was used for building
PostgreSQL. This shows C compiler switches.

`--cflags_sl`

    

Print the value of the `CFLAGS_SL` variable that was used for building
PostgreSQL. This shows extra C compiler switches used for building shared
libraries.

`--ldflags`

    

Print the value of the `LDFLAGS` variable that was used for building
PostgreSQL. This shows linker switches.

`--ldflags_ex`

    

Print the value of the `LDFLAGS_EX` variable that was used for building
PostgreSQL. This shows linker switches used for building executables only.

`--ldflags_sl`

    

Print the value of the `LDFLAGS_SL` variable that was used for building
PostgreSQL. This shows linker switches used for building shared libraries
only.

`--libs`

    

Print the value of the `LIBS` variable that was used for building PostgreSQL.
This normally contains `-l` switches for external libraries linked into
PostgreSQL.

`--version`

    

Print the version of PostgreSQL.

`-?`  
`--help`

    

Show help about pg_config command line arguments, and exit.

If more than one option is given, the information is printed in that order,
one item per line. If no options are given, all available information is
printed, with labels.

## Notes

The options `--docdir`, `--pkgincludedir`, `--localedir`, `--mandir`,
`--sharedir`, `--sysconfdir`, `--cc`, `--cppflags`, `--cflags`, `--cflags_sl`,
`--ldflags`, `--ldflags_sl`, and `--libs` were added in PostgreSQL 8.1. The
option `--htmldir` was added in PostgreSQL 8.4. The option `--ldflags_ex` was
added in PostgreSQL 9.0.

## Example

To reproduce the build configuration of the current PostgreSQL installation,
run the following command:

    
    
    eval ./configure `pg_config --configure`
    

The output of `pg_config --configure` contains shell quotation marks so
arguments with spaces are represented correctly. Therefore, using `eval` is
required for proper results.

* * *

[Prev](pgbench.html "pgbench")  | [Up](reference-client.html "PostgreSQL Client Applications") |  [Next](app-pgdump.html "pg_dump")  
---|---|---  
pgbench  | [Home](index.html "PostgreSQL 16.9 Documentation") |  pg_dump  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/app-pgconfig.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

