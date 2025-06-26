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

Supported Versions: [Current](/docs/current/app-clusterdb.html "PostgreSQL 17
- clusterdb") ([17](/docs/17/app-clusterdb.html "PostgreSQL 17 - clusterdb"))
/ [16](/docs/16/app-clusterdb.html "PostgreSQL 16 - clusterdb") /
[15](/docs/15/app-clusterdb.html "PostgreSQL 15 - clusterdb") /
[14](/docs/14/app-clusterdb.html "PostgreSQL 14 - clusterdb") /
[13](/docs/13/app-clusterdb.html "PostgreSQL 13 - clusterdb")

Development Versions: [18](/docs/18/app-clusterdb.html "PostgreSQL 18 -
clusterdb") / [devel](/docs/devel/app-clusterdb.html "PostgreSQL devel -
clusterdb")

Unsupported versions: [12](/docs/12/app-clusterdb.html "PostgreSQL 12 -
clusterdb") / [11](/docs/11/app-clusterdb.html "PostgreSQL 11 - clusterdb") /
[10](/docs/10/app-clusterdb.html "PostgreSQL 10 - clusterdb") /
[9.6](/docs/9.6/app-clusterdb.html "PostgreSQL 9.6 - clusterdb") /
[9.5](/docs/9.5/app-clusterdb.html "PostgreSQL 9.5 - clusterdb") /
[9.4](/docs/9.4/app-clusterdb.html "PostgreSQL 9.4 - clusterdb") /
[9.3](/docs/9.3/app-clusterdb.html "PostgreSQL 9.3 - clusterdb") /
[9.2](/docs/9.2/app-clusterdb.html "PostgreSQL 9.2 - clusterdb") /
[9.1](/docs/9.1/app-clusterdb.html "PostgreSQL 9.1 - clusterdb") /
[9.0](/docs/9.0/app-clusterdb.html "PostgreSQL 9.0 - clusterdb") /
[8.4](/docs/8.4/app-clusterdb.html "PostgreSQL 8.4 - clusterdb") /
[8.3](/docs/8.3/app-clusterdb.html "PostgreSQL 8.3 - clusterdb") /
[8.2](/docs/8.2/app-clusterdb.html "PostgreSQL 8.2 - clusterdb") /
[8.1](/docs/8.1/app-clusterdb.html "PostgreSQL 8.1 - clusterdb") /
[8.0](/docs/8.0/app-clusterdb.html "PostgreSQL 8.0 - clusterdb") /
[7.4](/docs/7.4/app-clusterdb.html "PostgreSQL 7.4 - clusterdb") /
[7.3](/docs/7.3/app-clusterdb.html "PostgreSQL 7.3 - clusterdb")

__

clusterdb  
---  
[Prev](reference-client.html "PostgreSQL Client Applications")  | [Up](reference-client.html "PostgreSQL Client Applications") | PostgreSQL Client Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](app-createdb.html "createdb")  
  
* * *

## clusterdb

clusterdb — cluster a PostgreSQL database

## Synopsis

`clusterdb` [_`connection-option`_...] [ `--verbose` | `-v` ] [ `--table` | `-t` _`table`_ ] ... [_`dbname`_]

`clusterdb` [_`connection-option`_...] [ `--verbose` | `-v` ] `--all` | `-a`

## Description

clusterdb is a utility for reclustering tables in a PostgreSQL database. It
finds tables that have previously been clustered, and clusters them again on
the same index that was last used. Tables that have never been clustered are
not affected.

clusterdb is a wrapper around the SQL command [CLUSTER](sql-cluster.html
"CLUSTER"). There is no effective difference between clustering databases via
this utility and via other methods for accessing the server.

## Options

clusterdb accepts the following command-line arguments:

`-a`  
`--all`

    

Cluster all databases.

`[-d] _`dbname`_`  
`[--dbname=]_`dbname`_`

    

Specifies the name of the database to be clustered, when `-a`/`--all` is not
used. If this is not specified, the database name is read from the environment
variable `PGDATABASE`. If that is not set, the user name specified for the
connection is used. The _`dbname`_ can be a [connection string](libpq-
connect.html#LIBPQ-CONNSTRING "34.1.1. Connection Strings"). If so, connection
string parameters will override any conflicting command line options.

`-e`  
`--echo`

    

Echo the commands that clusterdb generates and sends to the server.

`-q`  
`--quiet`

    

Do not display progress messages.

`-t _`table`_`  
`--table=_`table`_`

    

Cluster _`table`_ only. Multiple tables can be clustered by writing multiple
`-t` switches.

`-v`  
`--verbose`

    

Print detailed information during processing.

`-V`  
`--version`

    

Print the clusterdb version and exit.

`-?`  
`--help`

    

Show help about clusterdb command line arguments, and exit.

clusterdb also accepts the following command-line arguments for connection
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

    

Force clusterdb to prompt for a password before connecting to a database.

This option is never essential, since clusterdb will automatically prompt for
a password if the server demands password authentication. However, clusterdb
will waste a connection attempt finding out that the server wants a password.
In some cases it is worth typing `-W` to avoid the extra connection attempt.

`--maintenance-db=_`dbname`_`

    

When the `-a`/`--all` is used, connect to this database to gather the list of
databases to cluster. If not specified, the `postgres` database will be used,
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

In case of difficulty, see [CLUSTER](sql-cluster.html "CLUSTER") and
[psql](app-psql.html "psql") for discussions of potential problems and error
messages. The database server must be running at the targeted host. Also, any
default connection settings and environment variables used by the libpq front-
end library will apply.

## Examples

To cluster the database `test`:

    
    
    $ **clusterdb test**
    

To cluster a single table `foo` in a database named `xyzzy`:

    
    
    $ **clusterdb --table=foo xyzzy**
    

## See Also

[CLUSTER](sql-cluster.html "CLUSTER")

* * *

[Prev](reference-client.html "PostgreSQL Client Applications")  | [Up](reference-client.html "PostgreSQL Client Applications") |  [Next](app-createdb.html "createdb")  
---|---|---  
PostgreSQL Client Applications  | [Home](index.html "PostgreSQL 16.9 Documentation") |  createdb  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/app-clusterdb.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

