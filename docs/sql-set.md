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

Supported Versions: [Current](/docs/current/sql-set.html "PostgreSQL 17 -
SET") ([17](/docs/17/sql-set.html "PostgreSQL 17 - SET")) / [16](/docs/16/sql-
set.html "PostgreSQL 16 - SET") / [15](/docs/15/sql-set.html "PostgreSQL 15 -
SET") / [14](/docs/14/sql-set.html "PostgreSQL 14 - SET") / [13](/docs/13/sql-
set.html "PostgreSQL 13 - SET")

Development Versions: [18](/docs/18/sql-set.html "PostgreSQL 18 - SET") /
[devel](/docs/devel/sql-set.html "PostgreSQL devel - SET")

Unsupported versions: [12](/docs/12/sql-set.html "PostgreSQL 12 - SET") /
[11](/docs/11/sql-set.html "PostgreSQL 11 - SET") / [10](/docs/10/sql-set.html
"PostgreSQL 10 - SET") / [9.6](/docs/9.6/sql-set.html "PostgreSQL 9.6 - SET")
/ [9.5](/docs/9.5/sql-set.html "PostgreSQL 9.5 - SET") / [9.4](/docs/9.4/sql-
set.html "PostgreSQL 9.4 - SET") / [9.3](/docs/9.3/sql-set.html "PostgreSQL
9.3 - SET") / [9.2](/docs/9.2/sql-set.html "PostgreSQL 9.2 - SET") /
[9.1](/docs/9.1/sql-set.html "PostgreSQL 9.1 - SET") / [9.0](/docs/9.0/sql-
set.html "PostgreSQL 9.0 - SET") / [8.4](/docs/8.4/sql-set.html "PostgreSQL
8.4 - SET") / [8.3](/docs/8.3/sql-set.html "PostgreSQL 8.3 - SET") /
[8.2](/docs/8.2/sql-set.html "PostgreSQL 8.2 - SET") / [8.1](/docs/8.1/sql-
set.html "PostgreSQL 8.1 - SET") / [8.0](/docs/8.0/sql-set.html "PostgreSQL
8.0 - SET") / [7.4](/docs/7.4/sql-set.html "PostgreSQL 7.4 - SET") /
[7.3](/docs/7.3/sql-set.html "PostgreSQL 7.3 - SET") / [7.2](/docs/7.2/sql-
set.html "PostgreSQL 7.2 - SET") / [7.1](/docs/7.1/sql-set.html "PostgreSQL
7.1 - SET")

__

SET  
---  
[Prev](sql-selectinto.html "SELECT INTO")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-set-constraints.html "SET CONSTRAINTS")  
  
* * *

## SET

SET — change a run-time parameter

## Synopsis

    
    
    SET [ SESSION | LOCAL ] _configuration_parameter_ { TO | = } { _value_ | '_value_ ' | DEFAULT }
    SET [ SESSION | LOCAL ] TIME ZONE { _value_ | '_value_ ' | LOCAL | DEFAULT }
    

## Description

The `SET` command changes run-time configuration parameters. Many of the run-
time parameters listed in [Chapter 20](runtime-config.html "Chapter 20. Server
Configuration") can be changed on-the-fly with `SET`. (Some parameters can
only be changed by superusers and users who have been granted `SET` privilege
on that parameter. There are also parameters that cannot be changed after
server or session start.) `SET` only affects the value used by the current
session.

If `SET` (or equivalently `SET SESSION`) is issued within a transaction that
is later aborted, the effects of the `SET` command disappear when the
transaction is rolled back. Once the surrounding transaction is committed, the
effects will persist until the end of the session, unless overridden by
another `SET`.

The effects of `SET LOCAL` last only till the end of the current transaction,
whether committed or not. A special case is `SET` followed by `SET LOCAL`
within a single transaction: the `SET LOCAL` value will be seen until the end
of the transaction, but afterwards (if the transaction is committed) the `SET`
value will take effect.

The effects of `SET` or `SET LOCAL` are also canceled by rolling back to a
savepoint that is earlier than the command.

If `SET LOCAL` is used within a function that has a `SET` option for the same
variable (see [CREATE FUNCTION](sql-createfunction.html "CREATE FUNCTION")),
the effects of the `SET LOCAL` command disappear at function exit; that is,
the value in effect when the function was called is restored anyway. This
allows `SET LOCAL` to be used for dynamic or repeated changes of a parameter
within a function, while still having the convenience of using the `SET`
option to save and restore the caller's value. However, a regular `SET`
command overrides any surrounding function's `SET` option; its effects will
persist unless rolled back.

### Note

In PostgreSQL versions 8.0 through 8.2, the effects of a `SET LOCAL` would be
canceled by releasing an earlier savepoint, or by successful exit from a
PL/pgSQL exception block. This behavior has been changed because it was deemed
unintuitive.

## Parameters

`SESSION`

    

Specifies that the command takes effect for the current session. (This is the
default if neither `SESSION` nor `LOCAL` appears.)

`LOCAL`

    

Specifies that the command takes effect for only the current transaction.
After `COMMIT` or `ROLLBACK`, the session-level setting takes effect again.
Issuing this outside of a transaction block emits a warning and otherwise has
no effect.

_`configuration_parameter`_

    

Name of a settable run-time parameter. Available parameters are documented in
[Chapter 20](runtime-config.html "Chapter 20. Server Configuration") and
below.

_`value`_

    

New value of parameter. Values can be specified as string constants,
identifiers, numbers, or comma-separated lists of these, as appropriate for
the particular parameter. `DEFAULT` can be written to specify resetting the
parameter to its default value (that is, whatever value it would have had if
no `SET` had been executed in the current session).

Besides the configuration parameters documented in [Chapter 20](runtime-
config.html "Chapter 20. Server Configuration"), there are a few that can only
be adjusted using the `SET` command or that have a special syntax:

`SCHEMA`

    

`SET SCHEMA '_`value`_ '` is an alias for `SET search_path TO _`value`_`. Only
one schema can be specified using this syntax.

`NAMES`

    

`SET NAMES _`value`_` is an alias for `SET client_encoding TO _`value`_`.

`SEED`

    

Sets the internal seed for the random number generator (the function
`random`). Allowed values are floating-point numbers between -1 and 1
inclusive.

The seed can also be set by invoking the function `setseed`:

    
    
    SELECT setseed(_value_);
    

`TIME ZONE`

    

`SET TIME ZONE '_`value`_ '` is an alias for `SET timezone TO '_`value`_ '`.
The syntax `SET TIME ZONE` allows special syntax for the time zone
specification. Here are examples of valid values:

`'America/Los_Angeles'`

    

The time zone for Berkeley, California.

`'Europe/Rome'`

    

The time zone for Italy.

`-7`

    

The time zone 7 hours west from UTC (equivalent to PDT). Positive values are
east from UTC.

`INTERVAL '-08:00' HOUR TO MINUTE`

    

The time zone 8 hours west from UTC (equivalent to PST).

`LOCAL`  
`DEFAULT`

    

Set the time zone to your local time zone (that is, the server's default value
of `timezone`).

Timezone settings given as numbers or intervals are internally translated to
POSIX timezone syntax. For example, after `SET TIME ZONE -7`, `SHOW TIME ZONE`
would report `<-07>+07`.

Time zone abbreviations are not supported by `SET`; see [Section
8.5.3](datatype-datetime.html#DATATYPE-TIMEZONES "8.5.3. Time Zones") for more
information about time zones.

## Notes

The function `set_config` provides equivalent functionality; see [Section
9.27.1](functions-admin.html#FUNCTIONS-ADMIN-SET "9.27.1. Configuration
Settings Functions"). Also, it is possible to UPDATE the [`pg_settings`](view-
pg-settings.html "54.24. pg_settings") system view to perform the equivalent
of `SET`.

## Examples

Set the schema search path:

    
    
    SET search_path TO my_schema, public;
    

Set the style of date to traditional POSTGRES with “day before month” input
convention:

    
    
    SET datestyle TO postgres, dmy;
    

Set the time zone for Berkeley, California:

    
    
    SET TIME ZONE 'America/Los_Angeles';
    

Set the time zone for Italy:

    
    
    SET TIME ZONE 'Europe/Rome';
    

## Compatibility

`SET TIME ZONE` extends syntax defined in the SQL standard. The standard
allows only numeric time zone offsets while PostgreSQL allows more flexible
time-zone specifications. All other `SET` features are PostgreSQL extensions.

## See Also

[RESET](sql-reset.html "RESET"), [SHOW](sql-show.html "SHOW")

* * *

[Prev](sql-selectinto.html "SELECT INTO")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-set-constraints.html "SET CONSTRAINTS")  
---|---|---  
SELECT INTO  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SET CONSTRAINTS  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-set.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

