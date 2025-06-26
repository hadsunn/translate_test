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

Supported Versions: [Current](/docs/current/app-reindexdb.html "PostgreSQL 17
- reindexdb") ([17](/docs/17/app-reindexdb.html "PostgreSQL 17 - reindexdb"))
/ [16](/docs/16/app-reindexdb.html "PostgreSQL 16 - reindexdb") /
[15](/docs/15/app-reindexdb.html "PostgreSQL 15 - reindexdb") /
[14](/docs/14/app-reindexdb.html "PostgreSQL 14 - reindexdb") /
[13](/docs/13/app-reindexdb.html "PostgreSQL 13 - reindexdb")

Development Versions: [18](/docs/18/app-reindexdb.html "PostgreSQL 18 -
reindexdb") / [devel](/docs/devel/app-reindexdb.html "PostgreSQL devel -
reindexdb")

Unsupported versions: [12](/docs/12/app-reindexdb.html "PostgreSQL 12 -
reindexdb") / [11](/docs/11/app-reindexdb.html "PostgreSQL 11 - reindexdb") /
[10](/docs/10/app-reindexdb.html "PostgreSQL 10 - reindexdb") /
[9.6](/docs/9.6/app-reindexdb.html "PostgreSQL 9.6 - reindexdb") /
[9.5](/docs/9.5/app-reindexdb.html "PostgreSQL 9.5 - reindexdb") /
[9.4](/docs/9.4/app-reindexdb.html "PostgreSQL 9.4 - reindexdb") /
[9.3](/docs/9.3/app-reindexdb.html "PostgreSQL 9.3 - reindexdb") /
[9.2](/docs/9.2/app-reindexdb.html "PostgreSQL 9.2 - reindexdb") /
[9.1](/docs/9.1/app-reindexdb.html "PostgreSQL 9.1 - reindexdb") /
[9.0](/docs/9.0/app-reindexdb.html "PostgreSQL 9.0 - reindexdb") /
[8.4](/docs/8.4/app-reindexdb.html "PostgreSQL 8.4 - reindexdb") /
[8.3](/docs/8.3/app-reindexdb.html "PostgreSQL 8.3 - reindexdb") /
[8.2](/docs/8.2/app-reindexdb.html "PostgreSQL 8.2 - reindexdb") /
[8.1](/docs/8.1/app-reindexdb.html "PostgreSQL 8.1 - reindexdb")

__

reindexdb  
---  
[Prev](app-psql.html "psql")  | [Up](reference-client.html "PostgreSQL Client Applications") | PostgreSQL Client Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](app-vacuumdb.html "vacuumdb")  
  
* * *

## reindexdb

reindexdb — reindex a PostgreSQL database

## Synopsis

`reindexdb` [_`connection-option`_...] [_`option`_...] [ `-S` | `--schema` _`schema`_ ] ... [ `-t` | `--table` _`table`_ ] ... [ `-i` | `--index` _`index`_ ] ... [_`dbname`_]

`reindexdb` [_`connection-option`_...] [_`option`_...] `-a` | `--all`

`reindexdb` [_`connection-option`_...] [_`option`_...] `-s` | `--system` [_`dbname`_]

## Description

reindexdb is a utility for rebuilding indexes in a PostgreSQL database.

reindexdb is a wrapper around the SQL command [`REINDEX`](sql-reindex.html
"REINDEX"). There is no effective difference between reindexing databases via
this utility and via other methods for accessing the server.

## Options

reindexdb accepts the following command-line arguments:

`-a`  
`--all`

    

Reindex all databases.

`--concurrently`

    

Use the `CONCURRENTLY` option. See [REINDEX](sql-reindex.html "REINDEX"),
where all the caveats of this option are explained in detail.

`[-d] _`dbname`_`  
`[--dbname=]_`dbname`_`

    

Specifies the name of the database to be reindexed, when `-a`/`--all` is not
used. If this is not specified, the database name is read from the environment
variable `PGDATABASE`. If that is not set, the user name specified for the
connection is used. The _`dbname`_ can be a [connection string](libpq-
connect.html#LIBPQ-CONNSTRING "34.1.1. Connection Strings"). If so, connection
string parameters will override any conflicting command line options.

`-e`  
`--echo`

    

Echo the commands that reindexdb generates and sends to the server.

`-i _`index`_`  
`--index=_`index`_`

    

Recreate _`index`_ only. Multiple indexes can be recreated by writing multiple
`-i` switches.

`-j _`njobs`_`  
`--jobs=_`njobs`_`

    

Execute the reindex commands in parallel by running _`njobs`_ commands
simultaneously. This option may reduce the processing time but it also
increases the load on the database server.

reindexdb will open _`njobs`_ connections to the database, so make sure your
[max_connections](runtime-config-connection.html#GUC-MAX-CONNECTIONS) setting
is high enough to accommodate all connections.

Note that this option is incompatible with the `--index` and `--system`
options.

`-q`  
`--quiet`

    

Do not display progress messages.

`-s`  
`--system`

    

Reindex database's system catalogs only.

`-S _`schema`_`  
`--schema=_`schema`_`

    

Reindex _`schema`_ only. Multiple schemas can be reindexed by writing multiple
`-S` switches.

`-t _`table`_`  
`--table=_`table`_`

    

Reindex _`table`_ only. Multiple tables can be reindexed by writing multiple
`-t` switches.

`--tablespace=_`tablespace`_`

    

Specifies the tablespace where indexes are rebuilt. (This name is processed as
a double-quoted identifier.)

`-v`  
`--verbose`

    

Print detailed information during processing.

`-V`  
`--version`

    

Print the reindexdb version and exit.

`-?`  
`--help`

    

Show help about reindexdb command line arguments, and exit.

reindexdb also accepts the following command-line arguments for connection
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

    

Force reindexdb to prompt for a password before connecting to a database.

This option is never essential, since reindexdb will automatically prompt for
a password if the server demands password authentication. However, reindexdb
will waste a connection attempt finding out that the server wants a password.
In some cases it is worth typing `-W` to avoid the extra connection attempt.

`--maintenance-db=_`dbname`_`

    

When the `-a`/`--all` is used, connect to this database to gather the list of
databases to reindex. If not specified, the `postgres` database will be used,
or if that does not exist, `template1` will be used. This can be a [connection
string](libpq-connect.html#LIBPQ-CONNSTRING "34.1.1. Connection Strings"). If
so, connection string parameters will override any conflicting command line
options. Also, connection string parameters other than the database name
itself will be re-used when connecting to other databases.

## Environment

`PGDATABASE`  
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

In case of difficulty, see [REINDEX](sql-reindex.html "REINDEX") and
[psql](app-psql.html "psql") for discussions of potential problems and error
messages. The database server must be running at the targeted host. Also, any
default connection settings and environment variables used by the libpq front-
end library will apply.

## Notes

reindexdb might need to connect several times to the PostgreSQL server, asking
for a password each time. It is convenient to have a `~/.pgpass` file in such
cases. See [Section 34.16](libpq-pgpass.html "34.16. The Password File") for
more information.

## Examples

To reindex the database `test`:

    
    
    $ **reindexdb test**
    

To reindex the table `foo` and the index `bar` in a database named `abcd`:

    
    
    $ **reindexdb --table=foo --index=bar abcd**
    

## See Also

[REINDEX](sql-reindex.html "REINDEX")

* * *

[Prev](app-psql.html "psql")  | [Up](reference-client.html "PostgreSQL Client Applications") |  [Next](app-vacuumdb.html "vacuumdb")  
---|---|---  
psql  | [Home](index.html "PostgreSQL 16.9 Documentation") |  vacuumdb  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/app-reindexdb.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

