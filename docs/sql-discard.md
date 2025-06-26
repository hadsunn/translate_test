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

Supported Versions: [Current](/docs/current/sql-discard.html "PostgreSQL 17 -
DISCARD") ([17](/docs/17/sql-discard.html "PostgreSQL 17 - DISCARD")) /
[16](/docs/16/sql-discard.html "PostgreSQL 16 - DISCARD") / [15](/docs/15/sql-
discard.html "PostgreSQL 15 - DISCARD") / [14](/docs/14/sql-discard.html
"PostgreSQL 14 - DISCARD") / [13](/docs/13/sql-discard.html "PostgreSQL 13 -
DISCARD")

Development Versions: [18](/docs/18/sql-discard.html "PostgreSQL 18 -
DISCARD") / [devel](/docs/devel/sql-discard.html "PostgreSQL devel - DISCARD")

Unsupported versions: [12](/docs/12/sql-discard.html "PostgreSQL 12 -
DISCARD") / [11](/docs/11/sql-discard.html "PostgreSQL 11 - DISCARD") /
[10](/docs/10/sql-discard.html "PostgreSQL 10 - DISCARD") /
[9.6](/docs/9.6/sql-discard.html "PostgreSQL 9.6 - DISCARD") /
[9.5](/docs/9.5/sql-discard.html "PostgreSQL 9.5 - DISCARD") /
[9.4](/docs/9.4/sql-discard.html "PostgreSQL 9.4 - DISCARD") /
[9.3](/docs/9.3/sql-discard.html "PostgreSQL 9.3 - DISCARD") /
[9.2](/docs/9.2/sql-discard.html "PostgreSQL 9.2 - DISCARD") /
[9.1](/docs/9.1/sql-discard.html "PostgreSQL 9.1 - DISCARD") /
[9.0](/docs/9.0/sql-discard.html "PostgreSQL 9.0 - DISCARD") /
[8.4](/docs/8.4/sql-discard.html "PostgreSQL 8.4 - DISCARD") /
[8.3](/docs/8.3/sql-discard.html "PostgreSQL 8.3 - DISCARD")

__

DISCARD  
---  
[Prev](sql-delete.html "DELETE")  | [Up](sql-commands.html "SQL Commands") | SQL Commands | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-do.html "DO")  
  
* * *

## DISCARD

DISCARD — discard session state

## Synopsis

    
    
    DISCARD { ALL | PLANS | SEQUENCES | TEMPORARY | TEMP }
    

## Description

`DISCARD` releases internal resources associated with a database session. This
command is useful for partially or fully resetting the session's state. There
are several subcommands to release different types of resources; the `DISCARD
ALL` variant subsumes all the others, and also resets additional state.

## Parameters

`PLANS`

    

Releases all cached query plans, forcing re-planning to occur the next time
the associated prepared statement is used.

`SEQUENCES`

    

Discards all cached sequence-related state, including `currval()`/`lastval()`
information and any preallocated sequence values that have not yet been
returned by `nextval()`. (See [CREATE SEQUENCE](sql-createsequence.html
"CREATE SEQUENCE") for a description of preallocated sequence values.)

`TEMPORARY` or `TEMP`

    

Drops all temporary tables created in the current session.

`ALL`

    

Releases all temporary resources associated with the current session and
resets the session to its initial state. Currently, this has the same effect
as executing the following sequence of statements:

    
    
    CLOSE ALL;
    SET SESSION AUTHORIZATION DEFAULT;
    RESET ALL;
    DEALLOCATE ALL;
    UNLISTEN *;
    SELECT pg_advisory_unlock_all();
    DISCARD PLANS;
    DISCARD TEMP;
    DISCARD SEQUENCES;
    

## Notes

`DISCARD ALL` cannot be executed inside a transaction block.

## Compatibility

`DISCARD` is a PostgreSQL extension.

* * *

[Prev](sql-delete.html "DELETE")  | [Up](sql-commands.html "SQL Commands") |  [Next](sql-do.html "DO")  
---|---|---  
DELETE  | [Home](index.html "PostgreSQL 16.9 Documentation") |  DO  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/sql-discard.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

