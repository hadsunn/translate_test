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

Supported Versions: [Current](/docs/current/app-dropuser.html "PostgreSQL 17 -
dropuser") ([17](/docs/17/app-dropuser.html "PostgreSQL 17 - dropuser")) /
[16](/docs/16/app-dropuser.html "PostgreSQL 16 - dropuser") /
[15](/docs/15/app-dropuser.html "PostgreSQL 15 - dropuser") /
[14](/docs/14/app-dropuser.html "PostgreSQL 14 - dropuser") /
[13](/docs/13/app-dropuser.html "PostgreSQL 13 - dropuser")

Development Versions: [18](/docs/18/app-dropuser.html "PostgreSQL 18 -
dropuser") / [devel](/docs/devel/app-dropuser.html "PostgreSQL devel -
dropuser")

Unsupported versions: [12](/docs/12/app-dropuser.html "PostgreSQL 12 -
dropuser") / [11](/docs/11/app-dropuser.html "PostgreSQL 11 - dropuser") /
[10](/docs/10/app-dropuser.html "PostgreSQL 10 - dropuser") /
[9.6](/docs/9.6/app-dropuser.html "PostgreSQL 9.6 - dropuser") /
[9.5](/docs/9.5/app-dropuser.html "PostgreSQL 9.5 - dropuser") /
[9.4](/docs/9.4/app-dropuser.html "PostgreSQL 9.4 - dropuser") /
[9.3](/docs/9.3/app-dropuser.html "PostgreSQL 9.3 - dropuser") /
[9.2](/docs/9.2/app-dropuser.html "PostgreSQL 9.2 - dropuser") /
[9.1](/docs/9.1/app-dropuser.html "PostgreSQL 9.1 - dropuser") /
[9.0](/docs/9.0/app-dropuser.html "PostgreSQL 9.0 - dropuser") /
[8.4](/docs/8.4/app-dropuser.html "PostgreSQL 8.4 - dropuser") /
[8.3](/docs/8.3/app-dropuser.html "PostgreSQL 8.3 - dropuser") /
[8.2](/docs/8.2/app-dropuser.html "PostgreSQL 8.2 - dropuser") /
[8.1](/docs/8.1/app-dropuser.html "PostgreSQL 8.1 - dropuser") /
[8.0](/docs/8.0/app-dropuser.html "PostgreSQL 8.0 - dropuser") /
[7.4](/docs/7.4/app-dropuser.html "PostgreSQL 7.4 - dropuser") /
[7.3](/docs/7.3/app-dropuser.html "PostgreSQL 7.3 - dropuser") /
[7.2](/docs/7.2/app-dropuser.html "PostgreSQL 7.2 - dropuser") /
[7.1](/docs/7.1/app-dropuser.html "PostgreSQL 7.1 - dropuser")

__

dropuser  
---  
[Prev](app-dropdb.html "dropdb")  | [Up](reference-client.html "PostgreSQL Client Applications") | PostgreSQL Client Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](app-ecpg.html "ecpg")  
  
* * *

## dropuser

dropuser — remove a PostgreSQL user account

## Synopsis

`dropuser` [_`connection-option`_...] [_`option`_...] [_`username`_]

## Description

dropuser removes an existing PostgreSQL user. Superusers can use this command
to remove any role; otherwise, only non-superuser roles can be removed, and
only by a user who possesses the `CREATEROLE` privilege and has been granted
`ADMIN OPTION` on the target role.

dropuser is a wrapper around the SQL command [`DROP ROLE`](sql-droprole.html
"DROP ROLE"). There is no effective difference between dropping users via this
utility and via other methods for accessing the server.

## Options

dropuser accepts the following command-line arguments:

_`username`_

    

Specifies the name of the PostgreSQL user to be removed. You will be prompted
for a name if none is specified on the command line and the
`-i`/`--interactive` option is used.

`-e`  
`--echo`

    

Echo the commands that dropuser generates and sends to the server.

`-i`  
`--interactive`

    

Prompt for confirmation before actually removing the user, and prompt for the
user name if none is specified on the command line.

`-V`  
`--version`

    

Print the dropuser version and exit.

`--if-exists`

    

Do not throw an error if the user does not exist. A notice is issued in this
case.

`-?`  
`--help`

    

Show help about dropuser command line arguments, and exit.

dropuser also accepts the following command-line arguments for connection
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

    

User name to connect as (not the user name to drop).

`-w`  
`--no-password`

    

Never issue a password prompt. If the server requires password authentication
and a password is not available by other means such as a `.pgpass` file, the
connection attempt will fail. This option can be useful in batch jobs and
scripts where no user is present to enter a password.

`-W`  
`--password`

    

Force dropuser to prompt for a password before connecting to a database.

This option is never essential, since dropuser will automatically prompt for a
password if the server demands password authentication. However, dropuser will
waste a connection attempt finding out that the server wants a password. In
some cases it is worth typing `-W` to avoid the extra connection attempt.

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

In case of difficulty, see [DROP ROLE](sql-droprole.html "DROP ROLE") and
[psql](app-psql.html "psql") for discussions of potential problems and error
messages. The database server must be running at the targeted host. Also, any
default connection settings and environment variables used by the libpq front-
end library will apply.

## Examples

To remove user `joe` from the default database server:

    
    
    $ **dropuser joe**
    

To remove user `joe` using the server on host `eden`, port 5000, with
verification and a peek at the underlying command:

    
    
    $ **dropuser -p 5000 -h eden -i -e joe**
    Role "joe" will be permanently removed.
    Are you sure? (y/n) **y**
    DROP ROLE joe;
    

## See Also

[createuser](app-createuser.html "createuser"), [DROP ROLE](sql-droprole.html
"DROP ROLE")

* * *

[Prev](app-dropdb.html "dropdb")  | [Up](reference-client.html "PostgreSQL Client Applications") |  [Next](app-ecpg.html "ecpg")  
---|---|---  
dropdb  | [Home](index.html "PostgreSQL 16.9 Documentation") |  ecpg  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/app-dropuser.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

