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

Supported Versions: [Current](/docs/current/libpq-pgservice.html "PostgreSQL
17 - 34.17. The Connection Service File") ([17](/docs/17/libpq-pgservice.html
"PostgreSQL 17 - 34.17. The Connection Service File")) / [16](/docs/16/libpq-
pgservice.html "PostgreSQL 16 - 34.17. The Connection Service File") /
[15](/docs/15/libpq-pgservice.html "PostgreSQL 15 - 34.17. The Connection
Service File") / [14](/docs/14/libpq-pgservice.html "PostgreSQL 14 -
34.17. The Connection Service File") / [13](/docs/13/libpq-pgservice.html
"PostgreSQL 13 - 34.17. The Connection Service File")

Development Versions: [18](/docs/18/libpq-pgservice.html "PostgreSQL 18 -
34.17. The Connection Service File") / [devel](/docs/devel/libpq-
pgservice.html "PostgreSQL devel - 34.17. The Connection Service File")

Unsupported versions: [12](/docs/12/libpq-pgservice.html "PostgreSQL 12 -
34.17. The Connection Service File") / [11](/docs/11/libpq-pgservice.html
"PostgreSQL 11 - 34.17. The Connection Service File") / [10](/docs/10/libpq-
pgservice.html "PostgreSQL 10 - 34.17. The Connection Service File") /
[9.6](/docs/9.6/libpq-pgservice.html "PostgreSQL 9.6 - 34.17. The Connection
Service File") / [9.5](/docs/9.5/libpq-pgservice.html "PostgreSQL 9.5 -
34.17. The Connection Service File") / [9.4](/docs/9.4/libpq-pgservice.html
"PostgreSQL 9.4 - 34.17. The Connection Service File") /
[9.3](/docs/9.3/libpq-pgservice.html "PostgreSQL 9.3 - 34.17. The Connection
Service File") / [9.2](/docs/9.2/libpq-pgservice.html "PostgreSQL 9.2 -
34.17. The Connection Service File") / [9.1](/docs/9.1/libpq-pgservice.html
"PostgreSQL 9.1 - 34.17. The Connection Service File") /
[9.0](/docs/9.0/libpq-pgservice.html "PostgreSQL 9.0 - 34.17. The Connection
Service File") / [8.4](/docs/8.4/libpq-pgservice.html "PostgreSQL 8.4 -
34.17. The Connection Service File") / [8.3](/docs/8.3/libpq-pgservice.html
"PostgreSQL 8.3 - 34.17. The Connection Service File") /
[8.2](/docs/8.2/libpq-pgservice.html "PostgreSQL 8.2 - 34.17. The Connection
Service File") / [8.1](/docs/8.1/libpq-pgservice.html "PostgreSQL 8.1 -
34.17. The Connection Service File")

__

34.17. The Connection Service File  
---  
[Prev](libpq-pgpass.html "34.16. The Password File")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-ldap.html "34.18. LDAP Lookup of Connection Parameters")  
  
* * *

## 34.17. The Connection Service File #

The connection service file allows libpq connection parameters to be
associated with a single service name. That service name can then be specified
in a libpq connection string, and the associated settings will be used. This
allows connection parameters to be modified without requiring a recompile of
the libpq-using application. The service name can also be specified using the
`PGSERVICE` environment variable.

Service names can be defined in either a per-user service file or a system-
wide file. If the same service name exists in both the user and the system
file, the user file takes precedence. By default, the per-user service file is
named `~/.pg_service.conf`. On Microsoft Windows, it is named
`%APPDATA%\postgresql\.pg_service.conf` (where `%APPDATA%` refers to the
Application Data subdirectory in the user's profile). A different file name
can be specified by setting the environment variable `PGSERVICEFILE`. The
system-wide file is named `pg_service.conf`. By default it is sought in the
`etc` directory of the PostgreSQL installation (use `pg_config --sysconfdir`
to identify this directory precisely). Another directory, but not a different
file name, can be specified by setting the environment variable
`PGSYSCONFDIR`.

Either service file uses an “INI file” format where the section name is the
service name and the parameters are connection parameters; see [Section
34.1.2](libpq-connect.html#LIBPQ-PARAMKEYWORDS "34.1.2. Parameter Key Words")
for a list. For example:

    
    
    # comment
    [mydb]
    host=somehost
    port=5433
    user=admin
    

An example file is provided in the PostgreSQL installation at
`share/pg_service.conf.sample`.

Connection parameters obtained from a service file are combined with
parameters obtained from other sources. A service file setting overrides the
corresponding environment variable, and in turn can be overridden by a value
given directly in the connection string. For example, using the above service
file, a connection string `service=mydb port=5434` will use host `somehost`,
port `5434`, user `admin`, and other parameters as set by environment
variables or built-in defaults.

* * *

[Prev](libpq-pgpass.html "34.16. The Password File")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](libpq-ldap.html "34.18. LDAP Lookup of Connection Parameters")  
---|---|---  
34.16. The Password File  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.18. LDAP Lookup of Connection Parameters  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-pgservice.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

