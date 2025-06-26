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

Supported Versions: [Current](/docs/current/runtime-config-file-locations.html
"PostgreSQL 17 - 20.2. File Locations") ([17](/docs/17/runtime-config-file-
locations.html "PostgreSQL 17 - 20.2. File Locations")) /
[16](/docs/16/runtime-config-file-locations.html "PostgreSQL 16 - 20.2. File
Locations") / [15](/docs/15/runtime-config-file-locations.html "PostgreSQL 15
- 20.2. File Locations") / [14](/docs/14/runtime-config-file-locations.html
"PostgreSQL 14 - 20.2. File Locations") / [13](/docs/13/runtime-config-file-
locations.html "PostgreSQL 13 - 20.2. File Locations")

Development Versions: [18](/docs/18/runtime-config-file-locations.html
"PostgreSQL 18 - 20.2. File Locations") / [devel](/docs/devel/runtime-config-
file-locations.html "PostgreSQL devel - 20.2. File Locations")

Unsupported versions: [12](/docs/12/runtime-config-file-locations.html
"PostgreSQL 12 - 20.2. File Locations") / [11](/docs/11/runtime-config-file-
locations.html "PostgreSQL 11 - 20.2. File Locations") /
[10](/docs/10/runtime-config-file-locations.html "PostgreSQL 10 - 20.2. File
Locations") / [9.6](/docs/9.6/runtime-config-file-locations.html "PostgreSQL
9.6 - 20.2. File Locations") / [9.5](/docs/9.5/runtime-config-file-
locations.html "PostgreSQL 9.5 - 20.2. File Locations") /
[9.4](/docs/9.4/runtime-config-file-locations.html "PostgreSQL 9.4 -
20.2. File Locations") / [9.3](/docs/9.3/runtime-config-file-locations.html
"PostgreSQL 9.3 - 20.2. File Locations") / [9.2](/docs/9.2/runtime-config-
file-locations.html "PostgreSQL 9.2 - 20.2. File Locations") /
[9.1](/docs/9.1/runtime-config-file-locations.html "PostgreSQL 9.1 -
20.2. File Locations") / [9.0](/docs/9.0/runtime-config-file-locations.html
"PostgreSQL 9.0 - 20.2. File Locations") / [8.4](/docs/8.4/runtime-config-
file-locations.html "PostgreSQL 8.4 - 20.2. File Locations") /
[8.3](/docs/8.3/runtime-config-file-locations.html "PostgreSQL 8.3 -
20.2. File Locations") / [8.2](/docs/8.2/runtime-config-file-locations.html
"PostgreSQL 8.2 - 20.2. File Locations") / [8.1](/docs/8.1/runtime-config-
file-locations.html "PostgreSQL 8.1 - 20.2. File Locations")

__

20.2. File Locations  
---  
[Prev](config-setting.html "20.1. Setting Parameters")  | [Up](runtime-config.html "Chapter 20. Server Configuration") | Chapter 20. Server Configuration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](runtime-config-connection.html "20.3. Connections and Authentication")  
  
* * *

## 20.2. File Locations #

In addition to the `postgresql.conf` file already mentioned, PostgreSQL uses
two other manually-edited configuration files, which control client
authentication (their use is discussed in [Chapter 21](client-
authentication.html "Chapter 21. Client Authentication")). By default, all
three configuration files are stored in the database cluster's data directory.
The parameters described in this section allow the configuration files to be
placed elsewhere. (Doing so can ease administration. In particular it is often
easier to ensure that the configuration files are properly backed-up when they
are kept separate.)

`data_directory` (`string`)  #

    

Specifies the directory to use for data storage. This parameter can only be
set at server start.

`config_file` (`string`)  #

    

Specifies the main server configuration file (customarily called
`postgresql.conf`). This parameter can only be set on the `postgres` command
line.

`hba_file` (`string`)  #

    

Specifies the configuration file for host-based authentication (customarily
called `pg_hba.conf`). This parameter can only be set at server start.

`ident_file` (`string`)  #

    

Specifies the configuration file for user name mapping (customarily called
`pg_ident.conf`). This parameter can only be set at server start. See also
[Section 21.2](auth-username-maps.html "21.2. User Name Maps").

`external_pid_file` (`string`)  #

    

Specifies the name of an additional process-ID (PID) file that the server
should create for use by server administration programs. This parameter can
only be set at server start.

In a default installation, none of the above parameters are set explicitly.
Instead, the data directory is specified by the `-D` command-line option or
the `PGDATA` environment variable, and the configuration files are all found
within the data directory.

If you wish to keep the configuration files elsewhere than the data directory,
the `postgres` `-D` command-line option or `PGDATA` environment variable must
point to the directory containing the configuration files, and the
`data_directory` parameter must be set in `postgresql.conf` (or on the command
line) to show where the data directory is actually located. Notice that
`data_directory` overrides `-D` and `PGDATA` for the location of the data
directory, but not for the location of the configuration files.

If you wish, you can specify the configuration file names and locations
individually using the parameters `config_file`, `hba_file` and/or
`ident_file`. `config_file` can only be specified on the `postgres` command
line, but the others can be set within the main configuration file. If all
three parameters plus `data_directory` are explicitly set, then it is not
necessary to specify `-D` or `PGDATA`.

When setting any of these parameters, a relative path will be interpreted with
respect to the directory in which `postgres` is started.

* * *

[Prev](config-setting.html "20.1. Setting Parameters")  | [Up](runtime-config.html "Chapter 20. Server Configuration") |  [Next](runtime-config-connection.html "20.3. Connections and Authentication")  
---|---|---  
20.1. Setting Parameters  | [Home](index.html "PostgreSQL 16.9 Documentation") |  20.3. Connections and Authentication  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/runtime-config-file-
locations.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

