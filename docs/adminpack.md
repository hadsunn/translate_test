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

Supported Versions: [16](/docs/16/adminpack.html "PostgreSQL 16 -
F.1. adminpack — pgAdmin support toolpack") / [15](/docs/15/adminpack.html
"PostgreSQL 15 - F.1. adminpack — pgAdmin support toolpack") /
[14](/docs/14/adminpack.html "PostgreSQL 14 - F.1. adminpack — pgAdmin support
toolpack") / [13](/docs/13/adminpack.html "PostgreSQL 13 - F.1. adminpack —
pgAdmin support toolpack")

Unsupported versions: [12](/docs/12/adminpack.html "PostgreSQL 12 -
F.1. adminpack — pgAdmin support toolpack") / [11](/docs/11/adminpack.html
"PostgreSQL 11 - F.1. adminpack — pgAdmin support toolpack") /
[10](/docs/10/adminpack.html "PostgreSQL 10 - F.1. adminpack — pgAdmin support
toolpack") / [9.6](/docs/9.6/adminpack.html "PostgreSQL 9.6 - F.1. adminpack —
pgAdmin support toolpack") / [9.5](/docs/9.5/adminpack.html "PostgreSQL 9.5 -
F.1. adminpack — pgAdmin support toolpack") / [9.4](/docs/9.4/adminpack.html
"PostgreSQL 9.4 - F.1. adminpack — pgAdmin support toolpack") /
[9.3](/docs/9.3/adminpack.html "PostgreSQL 9.3 - F.1. adminpack — pgAdmin
support toolpack") / [9.2](/docs/9.2/adminpack.html "PostgreSQL 9.2 -
F.1. adminpack — pgAdmin support toolpack") / [9.1](/docs/9.1/adminpack.html
"PostgreSQL 9.1 - F.1. adminpack — pgAdmin support toolpack") /
[9.0](/docs/9.0/adminpack.html "PostgreSQL 9.0 - F.1. adminpack — pgAdmin
support toolpack") / [8.4](/docs/8.4/adminpack.html "PostgreSQL 8.4 -
F.1. adminpack — pgAdmin support toolpack") / [8.3](/docs/8.3/adminpack.html
"PostgreSQL 8.3 - F.1. adminpack — pgAdmin support toolpack")

__

F.1. adminpack — pgAdmin support toolpack  
---  
[Prev](contrib.html "Appendix F. Additional Supplied Modules and Extensions")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](amcheck.html "F.2. amcheck — tools to verify table and index consistency")  
  
* * *

## F.1. adminpack — pgAdmin support toolpack #

`adminpack` provides a number of support functions which pgAdmin and other
administration and management tools can use to provide additional
functionality, such as remote management of server log files. Use of all these
functions is only allowed to database superusers by default, but may be
allowed to other users by using the `GRANT` command.

The functions shown in [Table F.1](adminpack.html#FUNCTIONS-ADMINPACK-TABLE
"Table F.1. adminpack Functions") provide write access to files on the machine
hosting the server. (See also the functions in [Table 9.101](functions-
admin.html#FUNCTIONS-ADMIN-GENFILE-TABLE "Table 9.101. Generic File Access
Functions"), which provide read-only access.) Only files within the database
cluster directory can be accessed, unless the user is a superuser or given
privileges of one of the `pg_read_server_files` or `pg_write_server_files`
roles, as appropriate for the function, but either a relative or absolute path
is allowable.

**Table  F.1. `adminpack` Functions**

Function Description  
---  
`pg_catalog.pg_file_write` ( _`filename`_ `text`, _`data`_ `text`, _`append`_
`boolean` ) → `bigint` Writes, or appends to, a text file.  
`pg_catalog.pg_file_sync` ( _`filename`_ `text` ) → `void` Flushes a file or
directory to disk.  
`pg_catalog.pg_file_rename` ( _`oldname`_ `text`, _`newname`_ `text` [,
_`archivename`_ `text` ] ) → `boolean` Renames a file.  
`pg_catalog.pg_file_unlink` ( _`filename`_ `text` ) → `boolean` Removes a
file.  
`pg_catalog.pg_logdir_ls` () → `setof record` Lists the log files in the
`log_directory` directory.  
  
  

`pg_file_write` writes the specified _`data`_ into the file named by
_`filename`_. If _`append`_ is false, the file must not already exist. If
_`append`_ is true, the file can already exist, and will be appended to if so.
Returns the number of bytes written.

`pg_file_sync` fsyncs the specified file or directory named by _`filename`_.
An error is thrown on failure (e.g., the specified file is not present). Note
that [data_sync_retry](runtime-config-error-handling.html#GUC-DATA-SYNC-RETRY)
has no effect on this function, and therefore a PANIC-level error will not be
raised even on failure to flush database files.

`pg_file_rename` renames a file. If _`archivename`_ is omitted or NULL, it
simply renames _`oldname`_ to _`newname`_ (which must not already exist). If
_`archivename`_ is provided, it first renames _`newname`_ to _`archivename`_
(which must not already exist), and then renames _`oldname`_ to _`newname`_.
In event of failure of the second rename step, it will try to rename
_`archivename`_ back to _`newname`_ before reporting the error. Returns true
on success, false if the source file(s) are not present or not writable; other
cases throw errors.

`pg_file_unlink` removes the specified file. Returns true on success, false if
the specified file is not present or the `unlink()` call fails; other cases
throw errors.

`pg_logdir_ls` returns the start timestamps and path names of all the log
files in the [log_directory](runtime-config-logging.html#GUC-LOG-DIRECTORY)
directory. The [log_filename](runtime-config-logging.html#GUC-LOG-FILENAME)
parameter must have its default setting (`postgresql-%Y-%m-%d_%H%M%S.log`) to
use this function.

* * *

[Prev](contrib.html "Appendix F. Additional Supplied Modules and Extensions")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](amcheck.html "F.2. amcheck — tools to verify table and index consistency")  
---|---|---  
Appendix F. Additional Supplied Modules and Extensions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.2. amcheck — tools to verify table and index consistency  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/adminpack.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

