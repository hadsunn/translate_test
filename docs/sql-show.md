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

Supported Versions: [Current](/docs/current/sql-show.html "PostgreSQL 17 -
SHOW") ([17](/docs/17/sql-show.html "PostgreSQL 17 - SHOW")) /
[16](/docs/16/sql-show.html "PostgreSQL 16 - SHOW") / [15](/docs/15/sql-
show.html "PostgreSQL 15 - SHOW") / [14](/docs/14/sql-show.html "PostgreSQL 14
- SHOW") / [13](/docs/13/sql-show.html "PostgreSQL 13 - SHOW")

Development Versions: [18](/docs/18/sql-show.html "PostgreSQL 18 - SHOW") /
[devel](/docs/devel/sql-show.html "PostgreSQL devel - SHOW")

Unsupported versions: [12](/docs/12/sql-show.html "PostgreSQL 12 - SHOW") /
[11](/docs/11/sql-show.html "PostgreSQL 11 - SHOW") / [10](/docs/10/sql-
show.html "PostgreSQL 10 - SHOW") / [9.6](/docs/9.6/sql-show.html "PostgreSQL
9.6 - SHOW") / [9.5](/docs/9.5/sql-show.html "PostgreSQL 9.5 - SHOW") /
[9.4](/docs/9.4/sql-show.html "PostgreSQL 9.4 - SHOW") / [9.3](/docs/9.3/sql-
show.html "PostgreSQL 9.3 - SHOW") / [9.2](/docs/9.2/sql-show.html "PostgreSQL
9.2 - SHOW") / [9.1](/docs/9.1/sql-show.html "PostgreSQL 9.1 - SHOW") /
[9.0](/docs/9.0/sql-show.html "PostgreSQL 9.0 - SHOW") / [8.4](/docs/8.4/sql-
show.html "PostgreSQL 8.4 - SHOW") / [8.3](/docs/8.3/sql-show.html "PostgreSQL
8.3 - SHOW") / [8.2](/docs/8.2/sql-show.html "PostgreSQL 8.2 - SHOW") /
[8.1](/docs/8.1/sql-show.html "PostgreSQL 8.1 - SHOW") / [8.0](/docs/8.0/sql-
show.html "PostgreSQL 8.0 - SHOW") / [7.4](/docs/7.4/sql-show.html "PostgreSQL
7.4 - SHOW") / [7.3](/docs/7.3/sql-show.html "PostgreSQL 7.3 - SHOW") /
[7.2](/docs/7.2/sql-show.html "PostgreSQL 7.2 - SHOW") / [7.1](/docs/7.1/sql-
show.html "PostgreSQL 7.1 - SHOW")

__

SHOW  
---  
[Prev](sql-set-transaction.html "SET TRANSACTION")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-start-transaction.html "START TRANSACTION")  
  
* * *

## SHOW

SHOW — show the value of a run-time parameter

## Synopsis

    
    
    SHOW _name_
    SHOW ALL
    

## Description

`SHOW` will display the current setting of run-time parameters. These
variables can be set using the `SET` statement, by editing the
`postgresql.conf` configuration file, through the `PGOPTIONS` environmental
variable (when using libpq or a libpq-based application), or through command-
line flags when starting the `postgres` server. See [Chapter 20](runtime-
config.html "Chapter 20. Server Configuration") for details.

## Parameters

_`name`_

    

The name of a run-time parameter. Available parameters are documented in
[Chapter 20](runtime-config.html "Chapter 20. Server Configuration") and on
the [SET](sql-set.html "SET") reference page. In addition, there are a few
parameters that can be shown but not set:

`SERVER_VERSION`

    

Shows the server's version number.

`SERVER_ENCODING`

    

Shows the server-side character set encoding. At present, this parameter can
be shown but not set, because the encoding is determined at database creation
time.

`IS_SUPERUSER`

    

True if the current role has superuser privileges.

`ALL`

    

Show the values of all configuration parameters, with descriptions.

## Notes

The function `current_setting` produces equivalent output; see [Section
9.27.1](functions-admin.html#FUNCTIONS-ADMIN-SET "9.27.1. Configuration
Settings Functions"). Also, the [`pg_settings`](view-pg-settings.html
"54.24. pg_settings") system view produces the same information.

## Examples

Show the current setting of the parameter `DateStyle`:

    
    
    SHOW DateStyle;
     DateStyle
    -----------
     ISO, MDY
    (1 row)
    

Show the current setting of the parameter `geqo`:

    
    
    SHOW geqo;
     geqo
    ------
     on
    (1 row)
    

Show all settings:

    
    
    SHOW ALL;
                name         | setting |                description
    -------------------------+---------+-------------------------------------------------
     allow_system_table_mods | off     | Allows modifications of the structure of ...
        .
        .
        .
     xmloption               | content | Sets whether XML data in implicit parsing ...
     zero_damaged_pages      | off     | Continues processing past damaged page headers.
    (196 rows)
    

## Compatibility

The `SHOW` command is a PostgreSQL extension.

## See Also

[SET](sql-set.html "SET"), [RESET](sql-reset.html "RESET")

* * *

[Prev](sql-set-transaction.html "SET TRANSACTION")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-start-transaction.html "START TRANSACTION")  
---|---|---  
SET TRANSACTION  | [Home](index.html "PostgreSQL 16.9 Documentation") |  START TRANSACTION  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-show.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

