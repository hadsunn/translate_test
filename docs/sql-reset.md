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

Supported Versions: [Current](/docs/current/sql-reset.html "PostgreSQL 17 -
RESET") ([17](/docs/17/sql-reset.html "PostgreSQL 17 - RESET")) /
[16](/docs/16/sql-reset.html "PostgreSQL 16 - RESET") / [15](/docs/15/sql-
reset.html "PostgreSQL 15 - RESET") / [14](/docs/14/sql-reset.html "PostgreSQL
14 - RESET") / [13](/docs/13/sql-reset.html "PostgreSQL 13 - RESET")

Development Versions: [18](/docs/18/sql-reset.html "PostgreSQL 18 - RESET") /
[devel](/docs/devel/sql-reset.html "PostgreSQL devel - RESET")

Unsupported versions: [12](/docs/12/sql-reset.html "PostgreSQL 12 - RESET") /
[11](/docs/11/sql-reset.html "PostgreSQL 11 - RESET") / [10](/docs/10/sql-
reset.html "PostgreSQL 10 - RESET") / [9.6](/docs/9.6/sql-reset.html
"PostgreSQL 9.6 - RESET") / [9.5](/docs/9.5/sql-reset.html "PostgreSQL 9.5 -
RESET") / [9.4](/docs/9.4/sql-reset.html "PostgreSQL 9.4 - RESET") /
[9.3](/docs/9.3/sql-reset.html "PostgreSQL 9.3 - RESET") /
[9.2](/docs/9.2/sql-reset.html "PostgreSQL 9.2 - RESET") /
[9.1](/docs/9.1/sql-reset.html "PostgreSQL 9.1 - RESET") /
[9.0](/docs/9.0/sql-reset.html "PostgreSQL 9.0 - RESET") /
[8.4](/docs/8.4/sql-reset.html "PostgreSQL 8.4 - RESET") /
[8.3](/docs/8.3/sql-reset.html "PostgreSQL 8.3 - RESET") /
[8.2](/docs/8.2/sql-reset.html "PostgreSQL 8.2 - RESET") /
[8.1](/docs/8.1/sql-reset.html "PostgreSQL 8.1 - RESET") /
[8.0](/docs/8.0/sql-reset.html "PostgreSQL 8.0 - RESET") /
[7.4](/docs/7.4/sql-reset.html "PostgreSQL 7.4 - RESET") /
[7.3](/docs/7.3/sql-reset.html "PostgreSQL 7.3 - RESET") /
[7.2](/docs/7.2/sql-reset.html "PostgreSQL 7.2 - RESET") /
[7.1](/docs/7.1/sql-reset.html "PostgreSQL 7.1 - RESET")

__

RESET  
---  
[Prev](sql-release-savepoint.html "RELEASE SAVEPOINT")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-revoke.html "REVOKE")  
  
* * *

## RESET

RESET — restore the value of a run-time parameter to the default value

## Synopsis

    
    
    RESET _configuration_parameter_
    RESET ALL
    

## Description

`RESET` restores run-time parameters to their default values. `RESET` is an
alternative spelling for

    
    
    SET _configuration_parameter_ TO DEFAULT
    

Refer to [SET](sql-set.html "SET") for details.

The default value is defined as the value that the parameter would have had,
if no `SET` had ever been issued for it in the current session. The actual
source of this value might be a compiled-in default, the configuration file,
command-line options, or per-database or per-user default settings. This is
subtly different from defining it as “the value that the parameter had at
session start”, because if the value came from the configuration file, it will
be reset to whatever is specified by the configuration file now. See [Chapter
20](runtime-config.html "Chapter 20. Server Configuration") for details.

The transactional behavior of `RESET` is the same as `SET`: its effects will
be undone by transaction rollback.

## Parameters

_`configuration_parameter`_

    

Name of a settable run-time parameter. Available parameters are documented in
[Chapter 20](runtime-config.html "Chapter 20. Server Configuration") and on
the [SET](sql-set.html "SET") reference page.

`ALL`

    

Resets all settable run-time parameters to default values.

## Examples

Set the `timezone` configuration variable to its default value:

    
    
    RESET timezone;
    

## Compatibility

`RESET` is a PostgreSQL extension.

## See Also

[SET](sql-set.html "SET"), [SHOW](sql-show.html "SHOW")

* * *

[Prev](sql-release-savepoint.html "RELEASE SAVEPOINT")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-revoke.html "REVOKE")  
---|---|---  
RELEASE SAVEPOINT  | [Home](index.html "PostgreSQL 16.9 Documentation") |  REVOKE  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-reset.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

