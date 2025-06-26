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

Supported Versions: [Current](/docs/current/app-vacuumdb.html "PostgreSQL 17 -
vacuumdb") ([17](/docs/17/app-vacuumdb.html "PostgreSQL 17 - vacuumdb")) /
[16](/docs/16/app-vacuumdb.html "PostgreSQL 16 - vacuumdb") /
[15](/docs/15/app-vacuumdb.html "PostgreSQL 15 - vacuumdb") /
[14](/docs/14/app-vacuumdb.html "PostgreSQL 14 - vacuumdb") /
[13](/docs/13/app-vacuumdb.html "PostgreSQL 13 - vacuumdb")

Development Versions: [18](/docs/18/app-vacuumdb.html "PostgreSQL 18 -
vacuumdb") / [devel](/docs/devel/app-vacuumdb.html "PostgreSQL devel -
vacuumdb")

Unsupported versions: [12](/docs/12/app-vacuumdb.html "PostgreSQL 12 -
vacuumdb") / [11](/docs/11/app-vacuumdb.html "PostgreSQL 11 - vacuumdb") /
[10](/docs/10/app-vacuumdb.html "PostgreSQL 10 - vacuumdb") /
[9.6](/docs/9.6/app-vacuumdb.html "PostgreSQL 9.6 - vacuumdb") /
[9.5](/docs/9.5/app-vacuumdb.html "PostgreSQL 9.5 - vacuumdb") /
[9.4](/docs/9.4/app-vacuumdb.html "PostgreSQL 9.4 - vacuumdb") /
[9.3](/docs/9.3/app-vacuumdb.html "PostgreSQL 9.3 - vacuumdb") /
[9.2](/docs/9.2/app-vacuumdb.html "PostgreSQL 9.2 - vacuumdb") /
[9.1](/docs/9.1/app-vacuumdb.html "PostgreSQL 9.1 - vacuumdb") /
[9.0](/docs/9.0/app-vacuumdb.html "PostgreSQL 9.0 - vacuumdb") /
[8.4](/docs/8.4/app-vacuumdb.html "PostgreSQL 8.4 - vacuumdb") /
[8.3](/docs/8.3/app-vacuumdb.html "PostgreSQL 8.3 - vacuumdb") /
[8.2](/docs/8.2/app-vacuumdb.html "PostgreSQL 8.2 - vacuumdb") /
[8.1](/docs/8.1/app-vacuumdb.html "PostgreSQL 8.1 - vacuumdb") /
[8.0](/docs/8.0/app-vacuumdb.html "PostgreSQL 8.0 - vacuumdb") /
[7.4](/docs/7.4/app-vacuumdb.html "PostgreSQL 7.4 - vacuumdb") /
[7.3](/docs/7.3/app-vacuumdb.html "PostgreSQL 7.3 - vacuumdb") /
[7.2](/docs/7.2/app-vacuumdb.html "PostgreSQL 7.2 - vacuumdb") /
[7.1](/docs/7.1/app-vacuumdb.html "PostgreSQL 7.1 - vacuumdb")

__

vacuumdb  
---  
[Prev](app-reindexdb.html "reindexdb")  | [Up](reference-client.html "PostgreSQL Client Applications") | PostgreSQL Client Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](reference-server.html "PostgreSQL Server Applications")  
  
* * *

## vacuumdb

vacuumdb — garbage-collect and analyze a PostgreSQL database

## Synopsis

`vacuumdb` [_`connection-option`_...] [_`option`_...] [ `-t` | `--table` _`table`_ [( _`column`_ [,...] )] ] ... [_`dbname`_]

`vacuumdb` [_`connection-option`_...] [_`option`_...] [ [ `-n` | `--schema` _`schema`_ ] | [ `-N` | `--exclude-schema` _`schema`_ ] ] ... [_`dbname`_]

`vacuumdb` [_`connection-option`_...] [_`option`_...] `-a` | `--all`

## Description

vacuumdb is a utility for cleaning a PostgreSQL database. vacuumdb will also
generate internal statistics used by the PostgreSQL query optimizer.

vacuumdb is a wrapper around the SQL command [`VACUUM`](sql-vacuum.html
"VACUUM"). There is no effective difference between vacuuming and analyzing
databases via this utility and via other methods for accessing the server.

## Options

vacuumdb accepts the following command-line arguments:

`-a`  
`--all`

    

Vacuum all databases.

`--buffer-usage-limit _`size`_`

    

Specifies the [](glossary.html#GLOSSARY-BUFFER-ACCESS-STRATEGY)[Buffer Access
Strategy](glossary.html#GLOSSARY-BUFFER-ACCESS-STRATEGY "Buffer Access
Strategy") ring buffer size for a given invocation of vacuumdb. This size is
used to calculate the number of shared buffers which will be reused as part of
this strategy. See [VACUUM](sql-vacuum.html "VACUUM").

`[-d] _`dbname`_`  
`[--dbname=]_`dbname`_`

    

Specifies the name of the database to be cleaned or analyzed, when
`-a`/`--all` is not used. If this is not specified, the database name is read
from the environment variable `PGDATABASE`. If that is not set, the user name
specified for the connection is used. The _`dbname`_ can be a [connection
string](libpq-connect.html#LIBPQ-CONNSTRING "34.1.1. Connection Strings"). If
so, connection string parameters will override any conflicting command line
options.

`--disable-page-skipping`

    

Disable skipping pages based on the contents of the visibility map.

`-e`  
`--echo`

    

Echo the commands that vacuumdb generates and sends to the server.

`-f`  
`--full`

    

Perform “full” vacuuming.

`-F`  
`--freeze`

    

Aggressively “freeze” tuples.

`--force-index-cleanup`

    

Always remove index entries pointing to dead tuples.

`-j _`njobs`_`  
`--jobs=_`njobs`_`

    

Execute the vacuum or analyze commands in parallel by running _`njobs`_
commands simultaneously. This option may reduce the processing time but it
also increases the load on the database server.

vacuumdb will open _`njobs`_ connections to the database, so make sure your
[max_connections](runtime-config-connection.html#GUC-MAX-CONNECTIONS) setting
is high enough to accommodate all connections.

Note that using this mode together with the `-f` (`FULL`) option might cause
deadlock failures if certain system catalogs are processed in parallel.

`--min-mxid-age _`mxid_age`_`

    

Only execute the vacuum or analyze commands on tables with a multixact ID age
of at least _`mxid_age`_. This setting is useful for prioritizing tables to
process to prevent multixact ID wraparound (see [Section 25.1.5.1](routine-
vacuuming.html#VACUUM-FOR-MULTIXACT-WRAPAROUND "25.1.5.1. Multixacts and
Wraparound")).

For the purposes of this option, the multixact ID age of a relation is the
greatest of the ages of the main relation and its associated TOAST table, if
one exists. Since the commands issued by vacuumdb will also process the TOAST
table for the relation if necessary, it does not need to be considered
separately.

`--min-xid-age _`xid_age`_`

    

Only execute the vacuum or analyze commands on tables with a transaction ID
age of at least _`xid_age`_. This setting is useful for prioritizing tables to
process to prevent transaction ID wraparound (see [Section 25.1.5](routine-
vacuuming.html#VACUUM-FOR-WRAPAROUND "25.1.5. Preventing Transaction ID
Wraparound Failures")).

For the purposes of this option, the transaction ID age of a relation is the
greatest of the ages of the main relation and its associated TOAST table, if
one exists. Since the commands issued by vacuumdb will also process the TOAST
table for the relation if necessary, it does not need to be considered
separately.

`-n _`schema`_`  
`--schema=_`schema`_`

    

Clean or analyze all tables in _`schema`_ only. Multiple schemas can be
vacuumed by writing multiple `-n` switches.

`-N _`schema`_`  
`--exclude-schema=_`schema`_`

    

Do not clean or analyze any tables in _`schema`_. Multiple schemas can be
excluded by writing multiple `-N` switches.

`--no-index-cleanup`

    

Do not remove index entries pointing to dead tuples.

`--no-process-main`

    

Skip the main relation.

`--no-process-toast`

    

Skip the TOAST table associated with the table to vacuum, if any.

`--no-truncate`

    

Do not truncate empty pages at the end of the table.

`-P _`parallel_workers`_`  
`--parallel=_`parallel_workers`_`

    

Specify the number of parallel workers for _parallel vacuum_. This allows the
vacuum to leverage multiple CPUs to process indexes. See [VACUUM](sql-
vacuum.html "VACUUM").

`-q`  
`--quiet`

    

Do not display progress messages.

`--skip-locked`

    

Skip relations that cannot be immediately locked for processing.

`-t _`table`_ [ (_`column`_ [,...]) ]`  
`--table=_`table`_ [ (_`column`_ [,...]) ]`

    

Clean or analyze _`table`_ only. Column names can be specified only in
conjunction with the `--analyze` or `--analyze-only` options. Multiple tables
can be vacuumed by writing multiple `-t` switches.

### Tip

If you specify columns, you probably have to escape the parentheses from the
shell. (See examples below.)

`-v`  
`--verbose`

    

Print detailed information during processing.

`-V`  
`--version`

    

Print the vacuumdb version and exit.

`-z`  
`--analyze`

    

Also calculate statistics for use by the optimizer.

`-Z`  
`--analyze-only`

    

Only calculate statistics for use by the optimizer (no vacuum).

`--analyze-in-stages`

    

Only calculate statistics for use by the optimizer (no vacuum), like
`--analyze-only`. Run three stages of analyze; the first stage uses the lowest
possible statistics target (see [default_statistics_target](runtime-config-
query.html#GUC-DEFAULT-STATISTICS-TARGET)) to produce usable statistics
faster, and subsequent stages build the full statistics.

This option is only useful to analyze a database that currently has no
statistics or has wholly incorrect ones, such as if it is newly populated from
a restored dump or by `pg_upgrade`. Be aware that running with this option in
a database with existing statistics may cause the query optimizer choices to
become transiently worse due to the low statistics targets of the early
stages.

`-?`  
`--help`

    

Show help about vacuumdb command line arguments, and exit.

vacuumdb also accepts the following command-line arguments for connection
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

    

Force vacuumdb to prompt for a password before connecting to a database.

This option is never essential, since vacuumdb will automatically prompt for a
password if the server demands password authentication. However, vacuumdb will
waste a connection attempt finding out that the server wants a password. In
some cases it is worth typing `-W` to avoid the extra connection attempt.

`--maintenance-db=_`dbname`_`

    

When the `-a`/`--all` is used, connect to this database to gather the list of
databases to vacuum. If not specified, the `postgres` database will be used,
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

In case of difficulty, see [VACUUM](sql-vacuum.html "VACUUM") and [psql](app-
psql.html "psql") for discussions of potential problems and error messages.
The database server must be running at the targeted host. Also, any default
connection settings and environment variables used by the libpq front-end
library will apply.

## Notes

vacuumdb might need to connect several times to the PostgreSQL server, asking
for a password each time. It is convenient to have a `~/.pgpass` file in such
cases. See [Section 34.16](libpq-pgpass.html "34.16. The Password File") for
more information.

## Examples

To clean the database `test`:

    
    
    $ **vacuumdb test**
    

To clean and analyze for the optimizer a database named `bigdb`:

    
    
    $ **vacuumdb --analyze bigdb**
    

To clean a single table `foo` in a database named `xyzzy`, and analyze a
single column `bar` of the table for the optimizer:

    
    
    $ **vacuumdb --analyze --verbose --table='foo(bar)' xyzzy**
    

To clean all tables in the `foo` and `bar` schemas in a database named
`xyzzy`:

    
    
    $ **vacuumdb --schema='foo' --schema='bar' xyzzy**
    

## See Also

[VACUUM](sql-vacuum.html "VACUUM")

* * *

[Prev](app-reindexdb.html "reindexdb")  | [Up](reference-client.html "PostgreSQL Client Applications") |  [Next](reference-server.html "PostgreSQL Server Applications")  
---|---|---  
reindexdb  | [Home](index.html "PostgreSQL 16.9 Documentation") |  PostgreSQL Server Applications  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/app-vacuumdb.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

