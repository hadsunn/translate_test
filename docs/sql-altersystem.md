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

Supported Versions: [Current](/docs/current/sql-altersystem.html "PostgreSQL
17 - ALTER SYSTEM") ([17](/docs/17/sql-altersystem.html "PostgreSQL 17 - ALTER
SYSTEM")) / [16](/docs/16/sql-altersystem.html "PostgreSQL 16 - ALTER SYSTEM")
/ [15](/docs/15/sql-altersystem.html "PostgreSQL 15 - ALTER SYSTEM") /
[14](/docs/14/sql-altersystem.html "PostgreSQL 14 - ALTER SYSTEM") /
[13](/docs/13/sql-altersystem.html "PostgreSQL 13 - ALTER SYSTEM")

Development Versions: [18](/docs/18/sql-altersystem.html "PostgreSQL 18 -
ALTER SYSTEM") / [devel](/docs/devel/sql-altersystem.html "PostgreSQL devel -
ALTER SYSTEM")

Unsupported versions: [12](/docs/12/sql-altersystem.html "PostgreSQL 12 -
ALTER SYSTEM") / [11](/docs/11/sql-altersystem.html "PostgreSQL 11 - ALTER
SYSTEM") / [10](/docs/10/sql-altersystem.html "PostgreSQL 10 - ALTER SYSTEM")
/ [9.6](/docs/9.6/sql-altersystem.html "PostgreSQL 9.6 - ALTER SYSTEM") /
[9.5](/docs/9.5/sql-altersystem.html "PostgreSQL 9.5 - ALTER SYSTEM") /
[9.4](/docs/9.4/sql-altersystem.html "PostgreSQL 9.4 - ALTER SYSTEM")

__

ALTER SYSTEM  
---  
[Prev](sql-altersubscription.html "ALTER SUBSCRIPTION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-altertable.html "ALTER TABLE")  
  
* * *

## ALTER SYSTEM

ALTER SYSTEM — change a server configuration parameter

## Synopsis

    
    
    ALTER SYSTEM SET _configuration_parameter_ { TO | = } { _value_ [, ...] | DEFAULT }
    
    ALTER SYSTEM RESET _configuration_parameter_
    ALTER SYSTEM RESET ALL
    

## Description

`ALTER SYSTEM` is used for changing server configuration parameters across the
entire database cluster. It can be more convenient than the traditional method
of manually editing the `postgresql.conf` file. `ALTER SYSTEM` writes the
given parameter setting to the `postgresql.auto.conf` file, which is read in
addition to `postgresql.conf`. Setting a parameter to `DEFAULT`, or using the
`RESET` variant, removes that configuration entry from the
`postgresql.auto.conf` file. Use `RESET ALL` to remove all such configuration
entries.

Values set with `ALTER SYSTEM` will be effective after the next server
configuration reload, or after the next server restart in the case of
parameters that can only be changed at server start. A server configuration
reload can be commanded by calling the SQL function `pg_reload_conf()`,
running `pg_ctl reload`, or sending a SIGHUP signal to the main server
process.

Only superusers and users granted `ALTER SYSTEM` privilege on a parameter can
change it using `ALTER SYSTEM`. Also, since this command acts directly on the
file system and cannot be rolled back, it is not allowed inside a transaction
block or function.

## Parameters

_`configuration_parameter`_

    

Name of a settable configuration parameter. Available parameters are
documented in [Chapter 20](runtime-config.html "Chapter 20. Server
Configuration").

_`value`_

    

New value of the parameter. Values can be specified as string constants,
identifiers, numbers, or comma-separated lists of these, as appropriate for
the particular parameter. Values that are neither numbers nor valid
identifiers must be quoted. `DEFAULT` can be written to specify removing the
parameter and its value from `postgresql.auto.conf`.

For some list-accepting parameters, quoted values will produce double-quoted
output to preserve whitespace and commas; for others, double-quotes must be
used inside single-quoted strings to get this effect.

## Notes

This command can't be used to set [data_directory](runtime-config-file-
locations.html#GUC-DATA-DIRECTORY), nor parameters that are not allowed in
`postgresql.conf` (e.g., [preset options](runtime-config-preset.html
"20.15. Preset Options")).

See [Section 20.1](config-setting.html "20.1. Setting Parameters") for other
ways to set the parameters.

## Examples

Set the `wal_level`:

    
    
    ALTER SYSTEM SET wal_level = replica;
    

Undo that, restoring whatever setting was effective in `postgresql.conf`:

    
    
    ALTER SYSTEM RESET wal_level;
    

## Compatibility

The `ALTER SYSTEM` statement is a PostgreSQL extension.

## See Also

[SET](sql-set.html "SET"), [SHOW](sql-show.html "SHOW")

* * *

[Prev](sql-altersubscription.html "ALTER SUBSCRIPTION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-altertable.html "ALTER TABLE")  
---|---|---  
ALTER SUBSCRIPTION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ALTER TABLE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-altersystem.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

