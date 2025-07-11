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

Supported Versions: [Current](/docs/current/config-setting.html "PostgreSQL 17
- 20.1. Setting Parameters") ([17](/docs/17/config-setting.html "PostgreSQL 17
- 20.1. Setting Parameters")) / [16](/docs/16/config-setting.html "PostgreSQL
16 - 20.1. Setting Parameters") / [15](/docs/15/config-setting.html
"PostgreSQL 15 - 20.1. Setting Parameters") / [14](/docs/14/config-
setting.html "PostgreSQL 14 - 20.1. Setting Parameters") /
[13](/docs/13/config-setting.html "PostgreSQL 13 - 20.1. Setting Parameters")

Development Versions: [18](/docs/18/config-setting.html "PostgreSQL 18 -
20.1. Setting Parameters") / [devel](/docs/devel/config-setting.html
"PostgreSQL devel - 20.1. Setting Parameters")

Unsupported versions: [12](/docs/12/config-setting.html "PostgreSQL 12 -
20.1. Setting Parameters") / [11](/docs/11/config-setting.html "PostgreSQL 11
- 20.1. Setting Parameters") / [10](/docs/10/config-setting.html "PostgreSQL
10 - 20.1. Setting Parameters") / [9.6](/docs/9.6/config-setting.html
"PostgreSQL 9.6 - 20.1. Setting Parameters") / [9.5](/docs/9.5/config-
setting.html "PostgreSQL 9.5 - 20.1. Setting Parameters") /
[9.4](/docs/9.4/config-setting.html "PostgreSQL 9.4 - 20.1. Setting
Parameters") / [9.3](/docs/9.3/config-setting.html "PostgreSQL 9.3 -
20.1. Setting Parameters") / [9.2](/docs/9.2/config-setting.html "PostgreSQL
9.2 - 20.1. Setting Parameters") / [9.1](/docs/9.1/config-setting.html
"PostgreSQL 9.1 - 20.1. Setting Parameters") / [9.0](/docs/9.0/config-
setting.html "PostgreSQL 9.0 - 20.1. Setting Parameters") /
[8.4](/docs/8.4/config-setting.html "PostgreSQL 8.4 - 20.1. Setting
Parameters") / [8.3](/docs/8.3/config-setting.html "PostgreSQL 8.3 -
20.1. Setting Parameters") / [8.2](/docs/8.2/config-setting.html "PostgreSQL
8.2 - 20.1. Setting Parameters")

__

20.1. Setting Parameters  
---  
[Prev](runtime-config.html "Chapter 20. Server Configuration")  | [Up](runtime-config.html "Chapter 20. Server Configuration") | Chapter 20. Server Configuration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](runtime-config-file-locations.html "20.2. File Locations")  
  
* * *

## 20.1. Setting Parameters #

[20.1.1. Parameter Names and Values](config-setting.html#CONFIG-SETTING-NAMES-
VALUES)

[20.1.2. Parameter Interaction via the Configuration File](config-
setting.html#CONFIG-SETTING-CONFIGURATION-FILE)

[20.1.3. Parameter Interaction via SQL](config-setting.html#CONFIG-SETTING-
SQL)

[20.1.4. Parameter Interaction via the Shell](config-setting.html#CONFIG-
SETTING-SHELL)

[20.1.5. Managing Configuration File Contents](config-setting.html#CONFIG-
INCLUDES)

### 20.1.1. Parameter Names and Values #

All parameter names are case-insensitive. Every parameter takes a value of one
of five types: boolean, string, integer, floating point, or enumerated (enum).
The type determines the syntax for setting the parameter:

  * _Boolean:_ Values can be written as `on`, `off`, `true`, `false`, `yes`, `no`, `1`, `0` (all case-insensitive) or any unambiguous prefix of one of these.

  * _String:_ In general, enclose the value in single quotes, doubling any single quotes within the value. Quotes can usually be omitted if the value is a simple number or identifier, however. (Values that match an SQL keyword require quoting in some contexts.)

  * _Numeric (integer and floating point):_ Numeric parameters can be specified in the customary integer and floating-point formats; fractional values are rounded to the nearest integer if the parameter is of integer type. Integer parameters additionally accept hexadecimal input (beginning with `0x`) and octal input (beginning with `0`), but these formats cannot have a fraction. Do not use thousands separators. Quotes are not required, except for hexadecimal input.

  * _Numeric with Unit:_ Some numeric parameters have an implicit unit, because they describe quantities of memory or time. The unit might be bytes, kilobytes, blocks (typically eight kilobytes), milliseconds, seconds, or minutes. An unadorned numeric value for one of these settings will use the setting's default unit, which can be learned from `pg_settings`.`unit`. For convenience, settings can be given with a unit specified explicitly, for example `'120 ms'` for a time value, and they will be converted to whatever the parameter's actual unit is. Note that the value must be written as a string (with quotes) to use this feature. The unit name is case-sensitive, and there can be whitespace between the numeric value and the unit.

    * Valid memory units are `B` (bytes), `kB` (kilobytes), `MB` (megabytes), `GB` (gigabytes), and `TB` (terabytes). The multiplier for memory units is 1024, not 1000.

    * Valid time units are `us` (microseconds), `ms` (milliseconds), `s` (seconds), `min` (minutes), `h` (hours), and `d` (days).

If a fractional value is specified with a unit, it will be rounded to a
multiple of the next smaller unit if there is one. For example, `30.1 GB` will
be converted to `30822 MB` not `32319628902 B`. If the parameter is of integer
type, a final rounding to integer occurs after any unit conversion.

  * _Enumerated:_ Enumerated-type parameters are written in the same way as string parameters, but are restricted to have one of a limited set of values. The values allowable for such a parameter can be found from `pg_settings`.`enumvals`. Enum parameter values are case-insensitive.

### 20.1.2. Parameter Interaction via the Configuration File #

The most fundamental way to set these parameters is to edit the file
`postgresql.conf`, which is normally kept in the data directory. A default
copy is installed when the database cluster directory is initialized. An
example of what this file might look like is:

    
    
    # This is a comment
    log_connections = yes
    log_destination = 'syslog'
    search_path = '"$user", public'
    shared_buffers = 128MB
    

One parameter is specified per line. The equal sign between name and value is
optional. Whitespace is insignificant (except within a quoted parameter value)
and blank lines are ignored. Hash marks (`#`) designate the remainder of the
line as a comment. Parameter values that are not simple identifiers or numbers
must be single-quoted. To embed a single quote in a parameter value, write
either two quotes (preferred) or backslash-quote. If the file contains
multiple entries for the same parameter, all but the last one are ignored.

Parameters set in this way provide default values for the cluster. The
settings seen by active sessions will be these values unless they are
overridden. The following sections describe ways in which the administrator or
user can override these defaults.

The configuration file is reread whenever the main server process receives a
SIGHUP signal; this signal is most easily sent by running `pg_ctl reload` from
the command line or by calling the SQL function `pg_reload_conf()`. The main
server process also propagates this signal to all currently running server
processes, so that existing sessions also adopt the new values (this will
happen after they complete any currently-executing client command).
Alternatively, you can send the signal to a single server process directly.
Some parameters can only be set at server start; any changes to their entries
in the configuration file will be ignored until the server is restarted.
Invalid parameter settings in the configuration file are likewise ignored (but
logged) during SIGHUP processing.

In addition to `postgresql.conf`, a PostgreSQL data directory contains a file
`postgresql.auto.conf`, which has the same format as `postgresql.conf` but is
intended to be edited automatically, not manually. This file holds settings
provided through the [`ALTER SYSTEM`](sql-altersystem.html "ALTER SYSTEM")
command. This file is read whenever `postgresql.conf` is, and its settings
take effect in the same way. Settings in `postgresql.auto.conf` override those
in `postgresql.conf`.

External tools may also modify `postgresql.auto.conf`. It is not recommended
to do this while the server is running, since a concurrent `ALTER SYSTEM`
command could overwrite such changes. Such tools might simply append new
settings to the end, or they might choose to remove duplicate settings and/or
comments (as `ALTER SYSTEM` will).

The system view [`pg_file_settings`](view-pg-file-settings.html
"54.7. pg_file_settings") can be helpful for pre-testing changes to the
configuration files, or for diagnosing problems if a SIGHUP signal did not
have the desired effects.

### 20.1.3. Parameter Interaction via SQL #

PostgreSQL provides three SQL commands to establish configuration defaults.
The already-mentioned `ALTER SYSTEM` command provides an SQL-accessible means
of changing global defaults; it is functionally equivalent to editing
`postgresql.conf`. In addition, there are two commands that allow setting of
defaults on a per-database or per-role basis:

  * The [`ALTER DATABASE`](sql-alterdatabase.html "ALTER DATABASE") command allows global settings to be overridden on a per-database basis.

  * The [`ALTER ROLE`](sql-alterrole.html "ALTER ROLE") command allows both global and per-database settings to be overridden with user-specific values.

Values set with `ALTER DATABASE` and `ALTER ROLE` are applied only when
starting a fresh database session. They override values obtained from the
configuration files or server command line, and constitute defaults for the
rest of the session. Note that some settings cannot be changed after server
start, and so cannot be set with these commands (or the ones listed below).

Once a client is connected to the database, PostgreSQL provides two additional
SQL commands (and equivalent functions) to interact with session-local
configuration settings:

  * The [`SHOW`](sql-show.html "SHOW") command allows inspection of the current value of any parameter. The corresponding SQL function is `current_setting(setting_name text)` (see [Section 9.27.1](functions-admin.html#FUNCTIONS-ADMIN-SET "9.27.1. Configuration Settings Functions")).

  * The [`SET`](sql-set.html "SET") command allows modification of the current value of those parameters that can be set locally to a session; it has no effect on other sessions. Many parameters can be set this way by any user, but some can only be set by superusers and users who have been granted `SET` privilege on that parameter. The corresponding SQL function is `set_config(setting_name, new_value, is_local)` (see [Section 9.27.1](functions-admin.html#FUNCTIONS-ADMIN-SET "9.27.1. Configuration Settings Functions")).

In addition, the system view [`pg_settings`](view-pg-settings.html
"54.24. pg_settings") can be used to view and change session-local values:

  * Querying this view is similar to using `SHOW ALL` but provides more detail. It is also more flexible, since it's possible to specify filter conditions or join against other relations.

  * Using `UPDATE` on this view, specifically updating the `setting` column, is the equivalent of issuing `SET` commands. For example, the equivalent of
        
        SET configuration_parameter TO DEFAULT;
        

is:

        
        UPDATE pg_settings SET setting = reset_val WHERE name = 'configuration_parameter';
        

### 20.1.4. Parameter Interaction via the Shell #

In addition to setting global defaults or attaching overrides at the database
or role level, you can pass settings to PostgreSQL via shell facilities. Both
the server and libpq client library accept parameter values via the shell.

  * During server startup, parameter settings can be passed to the `postgres` command via the `-c` command-line parameter. For example,
        
        postgres -c log_connections=yes -c log_destination='syslog'
        

Settings provided in this way override those set via `postgresql.conf` or
`ALTER SYSTEM`, so they cannot be changed globally without restarting the
server.

  * When starting a client session via libpq, parameter settings can be specified using the `PGOPTIONS` environment variable. Settings established in this way constitute defaults for the life of the session, but do not affect other sessions. For historical reasons, the format of `PGOPTIONS` is similar to that used when launching the `postgres` command; specifically, the `-c` flag must be specified. For example,
        
        env PGOPTIONS="-c geqo=off -c statement_timeout=5min" psql
        

Other clients and libraries might provide their own mechanisms, via the shell
or otherwise, that allow the user to alter session settings without direct use
of SQL commands.

### 20.1.5. Managing Configuration File Contents #

PostgreSQL provides several features for breaking down complex
`postgresql.conf` files into sub-files. These features are especially useful
when managing multiple servers with related, but not identical,
configurations.

In addition to individual parameter settings, the `postgresql.conf` file can
contain _include directives_ , which specify another file to read and process
as if it were inserted into the configuration file at this point. This feature
allows a configuration file to be divided into physically separate parts.
Include directives simply look like:

    
    
    include 'filename'
    

If the file name is not an absolute path, it is taken as relative to the
directory containing the referencing configuration file. Inclusions can be
nested.

There is also an `include_if_exists` directive, which acts the same as the
`include` directive, except when the referenced file does not exist or cannot
be read. A regular `include` will consider this an error condition, but
`include_if_exists` merely logs a message and continues processing the
referencing configuration file.

The `postgresql.conf` file can also contain `include_dir` directives, which
specify an entire directory of configuration files to include. These look like

    
    
    include_dir 'directory'
    

Non-absolute directory names are taken as relative to the directory containing
the referencing configuration file. Within the specified directory, only non-
directory files whose names end with the suffix `.conf` will be included. File
names that start with the `.` character are also ignored, to prevent mistakes
since such files are hidden on some platforms. Multiple files within an
include directory are processed in file name order (according to C locale
rules, i.e., numbers before letters, and uppercase letters before lowercase
ones).

Include files or directories can be used to logically separate portions of the
database configuration, rather than having a single large `postgresql.conf`
file. Consider a company that has two database servers, each with a different
amount of memory. There are likely elements of the configuration both will
share, for things such as logging. But memory-related parameters on the server
will vary between the two. And there might be server specific customizations,
too. One way to manage this situation is to break the custom configuration
changes for your site into three files. You could add this to the end of your
`postgresql.conf` file to include them:

    
    
    include 'shared.conf'
    include 'memory.conf'
    include 'server.conf'
    

All systems would have the same `shared.conf`. Each server with a particular
amount of memory could share the same `memory.conf`; you might have one for
all servers with 8GB of RAM, another for those having 16GB. And finally
`server.conf` could have truly server-specific configuration information in
it.

Another possibility is to create a configuration file directory and put this
information into files there. For example, a `conf.d` directory could be
referenced at the end of `postgresql.conf`:

    
    
    include_dir 'conf.d'
    

Then you could name the files in the `conf.d` directory like this:

    
    
    00shared.conf
    01memory.conf
    02server.conf
    

This naming convention establishes a clear order in which these files will be
loaded. This is important because only the last setting encountered for a
particular parameter while the server is reading configuration files will be
used. In this example, something set in `conf.d/02server.conf` would override
a value set in `conf.d/01memory.conf`.

You might instead use this approach to naming the files descriptively:

    
    
    00shared.conf
    01memory-8GB.conf
    02server-foo.conf
    

This sort of arrangement gives a unique name for each configuration file
variation. This can help eliminate ambiguity when several servers have their
configurations all stored in one place, such as in a version control
repository. (Storing database configuration files under version control is
another good practice to consider.)

* * *

[Prev](runtime-config.html "Chapter 20. Server Configuration")  | [Up](runtime-config.html "Chapter 20. Server Configuration") |  [Next](runtime-config-file-locations.html "20.2. File Locations")  
---|---|---  
Chapter 20. Server Configuration  | [Home](index.html "PostgreSQL 16.9 Documentation") |  20.2. File Locations  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/config-setting.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

