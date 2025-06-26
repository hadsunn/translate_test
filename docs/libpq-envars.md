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

Supported Versions: [Current](/docs/current/libpq-envars.html "PostgreSQL 17 -
34.15. Environment Variables") ([17](/docs/17/libpq-envars.html "PostgreSQL 17
- 34.15. Environment Variables")) / [16](/docs/16/libpq-envars.html
"PostgreSQL 16 - 34.15. Environment Variables") / [15](/docs/15/libpq-
envars.html "PostgreSQL 15 - 34.15. Environment Variables") /
[14](/docs/14/libpq-envars.html "PostgreSQL 14 - 34.15. Environment
Variables") / [13](/docs/13/libpq-envars.html "PostgreSQL 13 -
34.15. Environment Variables")

Development Versions: [18](/docs/18/libpq-envars.html "PostgreSQL 18 -
34.15. Environment Variables") / [devel](/docs/devel/libpq-envars.html
"PostgreSQL devel - 34.15. Environment Variables")

Unsupported versions: [12](/docs/12/libpq-envars.html "PostgreSQL 12 -
34.15. Environment Variables") / [11](/docs/11/libpq-envars.html "PostgreSQL
11 - 34.15. Environment Variables") / [10](/docs/10/libpq-envars.html
"PostgreSQL 10 - 34.15. Environment Variables") / [9.6](/docs/9.6/libpq-
envars.html "PostgreSQL 9.6 - 34.15. Environment Variables") /
[9.5](/docs/9.5/libpq-envars.html "PostgreSQL 9.5 - 34.15. Environment
Variables") / [9.4](/docs/9.4/libpq-envars.html "PostgreSQL 9.4 -
34.15. Environment Variables") / [9.3](/docs/9.3/libpq-envars.html "PostgreSQL
9.3 - 34.15. Environment Variables") / [9.2](/docs/9.2/libpq-envars.html
"PostgreSQL 9.2 - 34.15. Environment Variables") / [9.1](/docs/9.1/libpq-
envars.html "PostgreSQL 9.1 - 34.15. Environment Variables") /
[9.0](/docs/9.0/libpq-envars.html "PostgreSQL 9.0 - 34.15. Environment
Variables") / [8.4](/docs/8.4/libpq-envars.html "PostgreSQL 8.4 -
34.15. Environment Variables") / [8.3](/docs/8.3/libpq-envars.html "PostgreSQL
8.3 - 34.15. Environment Variables") / [8.2](/docs/8.2/libpq-envars.html
"PostgreSQL 8.2 - 34.15. Environment Variables") / [8.1](/docs/8.1/libpq-
envars.html "PostgreSQL 8.1 - 34.15. Environment Variables") /
[8.0](/docs/8.0/libpq-envars.html "PostgreSQL 8.0 - 34.15. Environment
Variables") / [7.4](/docs/7.4/libpq-envars.html "PostgreSQL 7.4 -
34.15. Environment Variables") / [7.3](/docs/7.3/libpq-envars.html "PostgreSQL
7.3 - 34.15. Environment Variables") / [7.2](/docs/7.2/libpq-envars.html
"PostgreSQL 7.2 - 34.15. Environment Variables") / [7.1](/docs/7.1/libpq-
envars.html "PostgreSQL 7.1 - 34.15. Environment Variables")

__

34.15. Environment Variables  
---  
[Prev](libpq-events.html "34.14. Event System")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-pgpass.html "34.16. The Password File")  
  
* * *

## 34.15. Environment Variables #

The following environment variables can be used to select default connection
parameter values, which will be used by [`PQconnectdb`](libpq-
connect.html#LIBPQ-PQCONNECTDB), [`PQsetdbLogin`](libpq-connect.html#LIBPQ-
PQSETDBLOGIN) and [`PQsetdb`](libpq-connect.html#LIBPQ-PQSETDB) if no value is
directly specified by the calling code. These are useful to avoid hard-coding
database connection information into simple client applications, for example.

  * `PGHOST` behaves the same as the [host](libpq-connect.html#LIBPQ-CONNECT-HOST) connection parameter.

  * `PGHOSTADDR` behaves the same as the [hostaddr](libpq-connect.html#LIBPQ-CONNECT-HOSTADDR) connection parameter. This can be set instead of or in addition to `PGHOST` to avoid DNS lookup overhead.

  * `PGPORT` behaves the same as the [port](libpq-connect.html#LIBPQ-CONNECT-PORT) connection parameter.

  * `PGDATABASE` behaves the same as the [dbname](libpq-connect.html#LIBPQ-CONNECT-DBNAME) connection parameter.

  * `PGUSER` behaves the same as the [user](libpq-connect.html#LIBPQ-CONNECT-USER) connection parameter.

  * `PGPASSWORD` behaves the same as the [password](libpq-connect.html#LIBPQ-CONNECT-PASSWORD) connection parameter. Use of this environment variable is not recommended for security reasons, as some operating systems allow non-root users to see process environment variables via ps; instead consider using a password file (see [Section 34.16](libpq-pgpass.html "34.16. The Password File")).

  * `PGPASSFILE` behaves the same as the [passfile](libpq-connect.html#LIBPQ-CONNECT-PASSFILE) connection parameter.

  * `PGREQUIREAUTH` behaves the same as the [require_auth](libpq-connect.html#LIBPQ-CONNECT-REQUIRE-AUTH) connection parameter.

  * `PGCHANNELBINDING` behaves the same as the [channel_binding](libpq-connect.html#LIBPQ-CONNECT-CHANNEL-BINDING) connection parameter.

  * `PGSERVICE` behaves the same as the [service](libpq-connect.html#LIBPQ-CONNECT-SERVICE) connection parameter.

  * `PGSERVICEFILE` specifies the name of the per-user connection service file (see [Section 34.17](libpq-pgservice.html "34.17. The Connection Service File")). Defaults to `~/.pg_service.conf`, or `%APPDATA%\postgresql\.pg_service.conf` on Microsoft Windows.

  * `PGOPTIONS` behaves the same as the [options](libpq-connect.html#LIBPQ-CONNECT-OPTIONS) connection parameter.

  * `PGAPPNAME` behaves the same as the [application_name](libpq-connect.html#LIBPQ-CONNECT-APPLICATION-NAME) connection parameter.

  * `PGSSLMODE` behaves the same as the [sslmode](libpq-connect.html#LIBPQ-CONNECT-SSLMODE) connection parameter.

  * `PGREQUIRESSL` behaves the same as the [requiressl](libpq-connect.html#LIBPQ-CONNECT-REQUIRESSL) connection parameter. This environment variable is deprecated in favor of the `PGSSLMODE` variable; setting both variables suppresses the effect of this one.

  * `PGSSLCOMPRESSION` behaves the same as the [sslcompression](libpq-connect.html#LIBPQ-CONNECT-SSLCOMPRESSION) connection parameter.

  * `PGSSLCERT` behaves the same as the [sslcert](libpq-connect.html#LIBPQ-CONNECT-SSLCERT) connection parameter.

  * `PGSSLKEY` behaves the same as the [sslkey](libpq-connect.html#LIBPQ-CONNECT-SSLKEY) connection parameter.

  * `PGSSLCERTMODE` behaves the same as the [sslcertmode](libpq-connect.html#LIBPQ-CONNECT-SSLCERTMODE) connection parameter.

  * `PGSSLROOTCERT` behaves the same as the [sslrootcert](libpq-connect.html#LIBPQ-CONNECT-SSLROOTCERT) connection parameter.

  * `PGSSLCRL` behaves the same as the [sslcrl](libpq-connect.html#LIBPQ-CONNECT-SSLCRL) connection parameter.

  * `PGSSLCRLDIR` behaves the same as the [sslcrldir](libpq-connect.html#LIBPQ-CONNECT-SSLCRLDIR) connection parameter.

  * `PGSSLSNI` behaves the same as the [sslsni](libpq-connect.html#LIBPQ-CONNECT-SSLSNI) connection parameter.

  * `PGREQUIREPEER` behaves the same as the [requirepeer](libpq-connect.html#LIBPQ-CONNECT-REQUIREPEER) connection parameter.

  * `PGSSLMINPROTOCOLVERSION` behaves the same as the [ssl_min_protocol_version](libpq-connect.html#LIBPQ-CONNECT-SSL-MIN-PROTOCOL-VERSION) connection parameter.

  * `PGSSLMAXPROTOCOLVERSION` behaves the same as the [ssl_max_protocol_version](libpq-connect.html#LIBPQ-CONNECT-SSL-MAX-PROTOCOL-VERSION) connection parameter.

  * `PGGSSENCMODE` behaves the same as the [gssencmode](libpq-connect.html#LIBPQ-CONNECT-GSSENCMODE) connection parameter.

  * `PGKRBSRVNAME` behaves the same as the [krbsrvname](libpq-connect.html#LIBPQ-CONNECT-KRBSRVNAME) connection parameter.

  * `PGGSSLIB` behaves the same as the [gsslib](libpq-connect.html#LIBPQ-CONNECT-GSSLIB) connection parameter.

  * `PGGSSDELEGATION` behaves the same as the [gssdelegation](libpq-connect.html#LIBPQ-CONNECT-GSSDELEGATION) connection parameter.

  * `PGCONNECT_TIMEOUT` behaves the same as the [connect_timeout](libpq-connect.html#LIBPQ-CONNECT-CONNECT-TIMEOUT) connection parameter.

  * `PGCLIENTENCODING` behaves the same as the [client_encoding](libpq-connect.html#LIBPQ-CONNECT-CLIENT-ENCODING) connection parameter.

  * `PGTARGETSESSIONATTRS` behaves the same as the [target_session_attrs](libpq-connect.html#LIBPQ-CONNECT-TARGET-SESSION-ATTRS) connection parameter.

  * `PGLOADBALANCEHOSTS` behaves the same as the [load_balance_hosts](libpq-connect.html#LIBPQ-CONNECT-LOAD-BALANCE-HOSTS) connection parameter.

The following environment variables can be used to specify default behavior
for each PostgreSQL session. (See also the [ALTER ROLE](sql-alterrole.html
"ALTER ROLE") and [ALTER DATABASE](sql-alterdatabase.html "ALTER DATABASE")
commands for ways to set default behavior on a per-user or per-database
basis.)

  * `PGDATESTYLE` sets the default style of date/time representation. (Equivalent to `SET datestyle TO ...`.)

  * `PGTZ` sets the default time zone. (Equivalent to `SET timezone TO ...`.)

  * `PGGEQO` sets the default mode for the genetic query optimizer. (Equivalent to `SET geqo TO ...`.)

Refer to the SQL command [SET](sql-set.html "SET") for information on correct
values for these environment variables.

The following environment variables determine internal behavior of libpq; they
override compiled-in defaults.

  * `PGSYSCONFDIR` sets the directory containing the `pg_service.conf` file and in a future version possibly other system-wide configuration files.

  * `PGLOCALEDIR` sets the directory containing the `locale` files for message localization.

* * *

[Prev](libpq-events.html "34.14. Event System")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](libpq-pgpass.html "34.16. The Password File")  
---|---|---  
34.14. Event System  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.16. The Password File  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-envars.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

