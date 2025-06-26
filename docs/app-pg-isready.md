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

Supported Versions: [Current](/docs/current/app-pg-isready.html "PostgreSQL 17
- pg_isready") ([17](/docs/17/app-pg-isready.html "PostgreSQL 17 -
pg_isready")) / [16](/docs/16/app-pg-isready.html "PostgreSQL 16 -
pg_isready") / [15](/docs/15/app-pg-isready.html "PostgreSQL 15 - pg_isready")
/ [14](/docs/14/app-pg-isready.html "PostgreSQL 14 - pg_isready") /
[13](/docs/13/app-pg-isready.html "PostgreSQL 13 - pg_isready")

Development Versions: [18](/docs/18/app-pg-isready.html "PostgreSQL 18 -
pg_isready") / [devel](/docs/devel/app-pg-isready.html "PostgreSQL devel -
pg_isready")

Unsupported versions: [12](/docs/12/app-pg-isready.html "PostgreSQL 12 -
pg_isready") / [11](/docs/11/app-pg-isready.html "PostgreSQL 11 - pg_isready")
/ [10](/docs/10/app-pg-isready.html "PostgreSQL 10 - pg_isready") /
[9.6](/docs/9.6/app-pg-isready.html "PostgreSQL 9.6 - pg_isready") /
[9.5](/docs/9.5/app-pg-isready.html "PostgreSQL 9.5 - pg_isready") /
[9.4](/docs/9.4/app-pg-isready.html "PostgreSQL 9.4 - pg_isready") /
[9.3](/docs/9.3/app-pg-isready.html "PostgreSQL 9.3 - pg_isready")

__

pg_isready  
---  
[Prev](app-pg-dumpall.html "pg_dumpall")  | [Up](reference-client.html "PostgreSQL Client Applications") | PostgreSQL Client Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](app-pgreceivewal.html "pg_receivewal")  
  
* * *

## pg_isready

pg_isready — check the connection status of a PostgreSQL server

## Synopsis

`pg_isready` [_`connection-option`_...] [_`option`_...]

## Description

pg_isready is a utility for checking the connection status of a PostgreSQL
database server. The exit status specifies the result of the connection check.

## Options

`-d _`dbname`_`  
`--dbname=_`dbname`_`

    

Specifies the name of the database to connect to. The _`dbname`_ can be a
[connection string](libpq-connect.html#LIBPQ-CONNSTRING "34.1.1. Connection
Strings"). If so, connection string parameters will override any conflicting
command line options.

`-h _`hostname`_`  
`--host=_`hostname`_`

    

Specifies the host name of the machine on which the server is running. If the
value begins with a slash, it is used as the directory for the Unix-domain
socket.

`-p _`port`_`  
`--port=_`port`_`

    

Specifies the TCP port or the local Unix-domain socket file extension on which
the server is listening for connections. Defaults to the value of the `PGPORT`
environment variable or, if not set, to the port specified at compile time,
usually 5432.

`-q`  
`--quiet`

    

Do not display status message. This is useful when scripting.

`-t _`seconds`_`  
`--timeout=_`seconds`_`

    

The maximum number of seconds to wait when attempting connection before
returning that the server is not responding. Setting to 0 disables. The
default is 3 seconds.

`-U _`username`_`  
`--username=_`username`_`

    

Connect to the database as the user _`username`_ instead of the default.

`-V`  
`--version`

    

Print the pg_isready version and exit.

`-?`  
`--help`

    

Show help about pg_isready command line arguments, and exit.

## Exit Status

pg_isready returns `0` to the shell if the server is accepting connections
normally, `1` if the server is rejecting connections (for example during
startup), `2` if there was no response to the connection attempt, and `3` if
no attempt was made (for example due to invalid parameters).

## Environment

`pg_isready`, like most other PostgreSQL utilities, also uses the environment
variables supported by libpq (see [Section 34.15](libpq-envars.html
"34.15. Environment Variables")).

The environment variable `PG_COLOR` specifies whether to use color in
diagnostic messages. Possible values are `always`, `auto` and `never`.

## Notes

It is not necessary to supply correct user name, password, or database name
values to obtain the server status; however, if incorrect values are provided,
the server will log a failed connection attempt.

## Examples

Standard Usage:

    
    
    $ **pg_isready**
    /tmp:5432 - accepting connections
    $ **echo $?**
    0
    

Running with connection parameters to a PostgreSQL cluster in startup:

    
    
    $ **pg_isready -h localhost -p 5433**
    localhost:5433 - rejecting connections
    $ **echo $?**
    1
    

Running with connection parameters to a non-responsive PostgreSQL cluster:

    
    
    $ **pg_isready -h someremotehost**
    someremotehost:5432 - no response
    $ **echo $?**
    2
    

* * *

[Prev](app-pg-dumpall.html "pg_dumpall")  | [Up](reference-client.html "PostgreSQL Client Applications") |  [Next](app-pgreceivewal.html "pg_receivewal")  
---|---|---  
pg_dumpall  | [Home](index.html "PostgreSQL 16.9 Documentation") |  pg_receivewal  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/app-pg-isready.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

