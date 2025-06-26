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

Supported Versions: [Current](/docs/current/file-fdw.html "PostgreSQL 17 -
F.16. file_fdw — access data files in the server's file system")
([17](/docs/17/file-fdw.html "PostgreSQL 17 - F.16. file_fdw — access data
files in the server's file system")) / [16](/docs/16/file-fdw.html "PostgreSQL
16 - F.16. file_fdw — access data files in the server's file system") /
[15](/docs/15/file-fdw.html "PostgreSQL 15 - F.16. file_fdw — access data
files in the server's file system") / [14](/docs/14/file-fdw.html "PostgreSQL
14 - F.16. file_fdw — access data files in the server's file system") /
[13](/docs/13/file-fdw.html "PostgreSQL 13 - F.16. file_fdw — access data
files in the server's file system")

Development Versions: [18](/docs/18/file-fdw.html "PostgreSQL 18 -
F.16. file_fdw — access data files in the server's file system") /
[devel](/docs/devel/file-fdw.html "PostgreSQL devel - F.16. file_fdw — access
data files in the server's file system")

Unsupported versions: [12](/docs/12/file-fdw.html "PostgreSQL 12 -
F.16. file_fdw — access data files in the server's file system") /
[11](/docs/11/file-fdw.html "PostgreSQL 11 - F.16. file_fdw — access data
files in the server's file system") / [10](/docs/10/file-fdw.html "PostgreSQL
10 - F.16. file_fdw — access data files in the server's file system") /
[9.6](/docs/9.6/file-fdw.html "PostgreSQL 9.6 - F.16. file_fdw — access data
files in the server's file system") / [9.5](/docs/9.5/file-fdw.html
"PostgreSQL 9.5 - F.16. file_fdw — access data files in the server's file
system") / [9.4](/docs/9.4/file-fdw.html "PostgreSQL 9.4 - F.16. file_fdw —
access data files in the server's file system") / [9.3](/docs/9.3/file-
fdw.html "PostgreSQL 9.3 - F.16. file_fdw — access data files in the server's
file system") / [9.2](/docs/9.2/file-fdw.html "PostgreSQL 9.2 - F.16. file_fdw
— access data files in the server's file system") / [9.1](/docs/9.1/file-
fdw.html "PostgreSQL 9.1 - F.16. file_fdw — access data files in the server's
file system")

__

F.16. file_fdw — access data files in the server's file system  
---  
[Prev](earthdistance.html "F.15. earthdistance — calculate great-circle distances")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](fuzzystrmatch.html "F.17. fuzzystrmatch — determine string similarities and distance")  
  
* * *

## F.16. file_fdw — access data files in the server's file system #

The `file_fdw` module provides the foreign-data wrapper `file_fdw`, which can
be used to access data files in the server's file system, or to execute
programs on the server and read their output. The data file or program output
must be in a format that can be read by `COPY FROM`; see [COPY](sql-copy.html
"COPY") for details. Access to data files is currently read-only.

A foreign table created using this wrapper can have the following options:

`filename`

    

Specifies the file to be read. Relative paths are relative to the data
directory. Either `filename` or `program` must be specified, but not both.

`program`

    

Specifies the command to be executed. The standard output of this command will
be read as though `COPY FROM PROGRAM` were used. Either `program` or
`filename` must be specified, but not both.

`format`

    

Specifies the data format, the same as `COPY`'s `FORMAT` option.

`header`

    

Specifies whether the data has a header line, the same as `COPY`'s `HEADER`
option.

`delimiter`

    

Specifies the data delimiter character, the same as `COPY`'s `DELIMITER`
option.

`quote`

    

Specifies the data quote character, the same as `COPY`'s `QUOTE` option.

`escape`

    

Specifies the data escape character, the same as `COPY`'s `ESCAPE` option.

`null`

    

Specifies the data null string, the same as `COPY`'s `NULL` option.

`encoding`

    

Specifies the data encoding, the same as `COPY`'s `ENCODING` option.

Note that while `COPY` allows options such as `HEADER` to be specified without
a corresponding value, the foreign table option syntax requires a value to be
present in all cases. To activate `COPY` options typically written without a
value, you can pass the value TRUE, since all such options are Booleans.

A column of a foreign table created using this wrapper can have the following
options:

`force_not_null`

    

This is a Boolean option. If true, it specifies that values of the column
should not be matched against the null string (that is, the table-level `null`
option). This has the same effect as listing the column in `COPY`'s
`FORCE_NOT_NULL` option.

`force_null`

    

This is a Boolean option. If true, it specifies that values of the column
which match the null string are returned as `NULL` even if the value is
quoted. Without this option, only unquoted values matching the null string are
returned as `NULL`. This has the same effect as listing the column in `COPY`'s
`FORCE_NULL` option.

`COPY`'s `FORCE_QUOTE` option is currently not supported by `file_fdw`.

These options can only be specified for a foreign table or its columns, not in
the options of the `file_fdw` foreign-data wrapper, nor in the options of a
server or user mapping using the wrapper.

Changing table-level options requires being a superuser or having the
privileges of the role `pg_read_server_files` (to use a filename) or the role
`pg_execute_server_program` (to use a program), for security reasons: only
certain users should be able to control which file is read or which program is
run. In principle regular users could be allowed to change the other options,
but that's not supported at present.

When specifying the `program` option, keep in mind that the option string is
executed by the shell. If you need to pass any arguments to the command that
come from an untrusted source, you must be careful to strip or escape any
characters that might have special meaning to the shell. For security reasons,
it is best to use a fixed command string, or at least avoid passing any user
input in it.

For a foreign table using `file_fdw`, `EXPLAIN` shows the name of the file to
be read or program to be run. For a file, unless `COSTS OFF` is specified, the
file size (in bytes) is shown as well.

**Example  F.1. Create a Foreign Table for PostgreSQL CSV Logs**

One of the obvious uses for `file_fdw` is to make the PostgreSQL activity log
available as a table for querying. To do this, first you must be [logging to a
CSV file,](runtime-config-logging.html#RUNTIME-CONFIG-LOGGING-CSVLOG
"20.8.4. Using CSV-Format Log Output") which here we will call `pglog.csv`.
First, install `file_fdw` as an extension:

    
    
    CREATE EXTENSION file_fdw;
    

Then create a foreign server:

    
    
    CREATE SERVER pglog FOREIGN DATA WRAPPER file_fdw;
    

Now you are ready to create the foreign data table. Using the `CREATE FOREIGN
TABLE` command, you will need to define the columns for the table, the CSV
file name, and its format:

    
    
    CREATE FOREIGN TABLE pglog (
      log_time timestamp(3) with time zone,
      user_name text,
      database_name text,
      process_id integer,
      connection_from text,
      session_id text,
      session_line_num bigint,
      command_tag text,
      session_start_time timestamp with time zone,
      virtual_transaction_id text,
      transaction_id bigint,
      error_severity text,
      sql_state_code text,
      message text,
      detail text,
      hint text,
      internal_query text,
      internal_query_pos integer,
      context text,
      query text,
      query_pos integer,
      location text,
      application_name text,
      backend_type text,
      leader_pid integer,
      query_id bigint
    ) SERVER pglog
    OPTIONS ( filename 'log/pglog.csv', format 'csv' );
    

That's it — now you can query your log directly. In production, of course, you
would need to define some way to deal with log rotation.

  

* * *

[Prev](earthdistance.html "F.15. earthdistance — calculate great-circle distances")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](fuzzystrmatch.html "F.17. fuzzystrmatch — determine string similarities and distance")  
---|---|---  
F.15. earthdistance — calculate great-circle distances  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.17. fuzzystrmatch — determine string similarities and distance  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/file-fdw.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

