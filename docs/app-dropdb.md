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

Supported Versions: [Current](/docs/current/app-dropdb.html "PostgreSQL 17 -
dropdb") ([17](/docs/17/app-dropdb.html "PostgreSQL 17 - dropdb")) /
[16](/docs/16/app-dropdb.html "PostgreSQL 16 - dropdb") / [15](/docs/15/app-
dropdb.html "PostgreSQL 15 - dropdb") / [14](/docs/14/app-dropdb.html
"PostgreSQL 14 - dropdb") / [13](/docs/13/app-dropdb.html "PostgreSQL 13 -
dropdb")

Development Versions: [18](/docs/18/app-dropdb.html "PostgreSQL 18 - dropdb")
/ [devel](/docs/devel/app-dropdb.html "PostgreSQL devel - dropdb")

Unsupported versions: [12](/docs/12/app-dropdb.html "PostgreSQL 12 - dropdb")
/ [11](/docs/11/app-dropdb.html "PostgreSQL 11 - dropdb") / [10](/docs/10/app-
dropdb.html "PostgreSQL 10 - dropdb") / [9.6](/docs/9.6/app-dropdb.html
"PostgreSQL 9.6 - dropdb") / [9.5](/docs/9.5/app-dropdb.html "PostgreSQL 9.5 -
dropdb") / [9.4](/docs/9.4/app-dropdb.html "PostgreSQL 9.4 - dropdb") /
[9.3](/docs/9.3/app-dropdb.html "PostgreSQL 9.3 - dropdb") /
[9.2](/docs/9.2/app-dropdb.html "PostgreSQL 9.2 - dropdb") /
[9.1](/docs/9.1/app-dropdb.html "PostgreSQL 9.1 - dropdb") /
[9.0](/docs/9.0/app-dropdb.html "PostgreSQL 9.0 - dropdb") /
[8.4](/docs/8.4/app-dropdb.html "PostgreSQL 8.4 - dropdb") /
[8.3](/docs/8.3/app-dropdb.html "PostgreSQL 8.3 - dropdb") /
[8.2](/docs/8.2/app-dropdb.html "PostgreSQL 8.2 - dropdb") /
[8.1](/docs/8.1/app-dropdb.html "PostgreSQL 8.1 - dropdb") /
[8.0](/docs/8.0/app-dropdb.html "PostgreSQL 8.0 - dropdb") /
[7.4](/docs/7.4/app-dropdb.html "PostgreSQL 7.4 - dropdb") /
[7.3](/docs/7.3/app-dropdb.html "PostgreSQL 7.3 - dropdb") /
[7.2](/docs/7.2/app-dropdb.html "PostgreSQL 7.2 - dropdb") /
[7.1](/docs/7.1/app-dropdb.html "PostgreSQL 7.1 - dropdb")

__

dropdb  
---  
[Prev](app-createuser.html "createuser")  | [Up](reference-client.html "PostgreSQL Client Applications") | PostgreSQL Client Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](app-dropuser.html "dropuser")  
  
* * *

## dropdb

dropdb — remove a PostgreSQL database

## Synopsis

`dropdb` [_`connection-option`_...] [_`option`_...] _`dbname`_

## Description

dropdb destroys an existing PostgreSQL database. The user who executes this
command must be a database superuser or the owner of the database.

dropdb is a wrapper around the SQL command [`DROP DATABASE`](sql-
dropdatabase.html "DROP DATABASE"). There is no effective difference between
dropping databases via this utility and via other methods for accessing the
server.

## Options

dropdb accepts the following command-line arguments:

_`dbname`_

    

Specifies the name of the database to be removed.

`-e`  
`--echo`

    

Echo the commands that dropdb generates and sends to the server.

`-f`  
`--force`

    

Attempt to terminate all existing connections to the target database before
dropping it. See [DROP DATABASE](sql-dropdatabase.html "DROP DATABASE") for
more information on this option.

`-i`  
`--interactive`

    

Issues a verification prompt before doing anything destructive.

`-V`  
`--version`

    

Print the dropdb version and exit.

`--if-exists`

    

Do not throw an error if the database does not exist. A notice is issued in
this case.

`-?`  
`--help`

    

Show help about dropdb command line arguments, and exit.

dropdb also accepts the following command-line arguments for connection
parameters:

`-h _`host`_`  
`--host=_`host`_`

    

Specifies the host name of the machine on which the server is running. If the
value begins with a slash, it is used as the directory for the Unix domain
socket.

`-p _`port`_`  
`--port=_`port`_`

    

Specifies the TCP port or local Unix domain socket file extension on which the
server is listening for connections.

`-U _`username`_`  
`--username=_`username`_`

    

User name to connect as.

`-w`  
`--no-password`

    

Never issue a password prompt. If the server requires password authentication
and a password is not available by other means such as a `.pgpass` file, the
connection attempt will fail. This option can be useful in batch jobs and
scripts where no user is present to enter a password.

`-W`  
`--password`

    

Force dropdb to prompt for a password before connecting to a database.

This option is never essential, since dropdb will automatically prompt for a
password if the server demands password authentication. However, dropdb will
waste a connection attempt finding out that the server wants a password. In
some cases it is worth typing `-W` to avoid the extra connection attempt.

`--maintenance-db=_`dbname`_`

    

Specifies the name of the database to connect to in order to drop the target
database. If not specified, the `postgres` database will be used; if that does
not exist (or is the database being dropped), `template1` will be used. This
can be a [connection string](libpq-connect.html#LIBPQ-CONNSTRING
"34.1.1. Connection Strings"). If so, connection string parameters will
override any conflicting command line options.

## Environment

`PGHOST`  
`PGPORT`  
`PGUSER`

    

Default connection parameters

`PG_COLOR`

    

Specifies whether to use color in diagnostic messages. Possible values are
`always`, `auto` and `never`.

This utility, like most other PostgreSQL utilities, also uses the environment
variables supported by libpq (see [Section 34.15](libpq-envars.html
"34.15. Environment Variables")).

## Diagnostics

In case of difficulty, see [DROP DATABASE](sql-dropdatabase.html "DROP
DATABASE") and [psql](app-psql.html "psql") for discussions of potential
problems and error messages. The database server must be running at the
targeted host. Also, any default connection settings and environment variables
used by the libpq front-end library will apply.

## Examples

To destroy the database `demo` on the default database server:

    
    
    $ **dropdb demo**
    

To destroy the database `demo` using the server on host `eden`, port 5000,
with verification and a peek at the underlying command:

    
    
    $ **dropdb -p 5000 -h eden -i -e demo**
    Database "demo" will be permanently deleted.
    Are you sure? (y/n) **y**
    DROP DATABASE demo;
    

## See Also

[createdb](app-createdb.html "createdb"), [DROP DATABASE](sql-
dropdatabase.html "DROP DATABASE")

* * *

[Prev](app-createuser.html "createuser")  | [Up](reference-client.html "PostgreSQL Client Applications") |  [Next](app-dropuser.html "dropuser")  
---|---|---  
createuser  | [Home](index.html "PostgreSQL 16.9 Documentation") |  dropuser  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/app-dropdb.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

