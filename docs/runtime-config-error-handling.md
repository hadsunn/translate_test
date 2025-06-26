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

Supported Versions: [Current](/docs/current/runtime-config-error-handling.html
"PostgreSQL 17 - 20.14. Error Handling") ([17](/docs/17/runtime-config-error-
handling.html "PostgreSQL 17 - 20.14. Error Handling")) /
[16](/docs/16/runtime-config-error-handling.html "PostgreSQL 16 - 20.14. Error
Handling") / [15](/docs/15/runtime-config-error-handling.html "PostgreSQL 15 -
20.14. Error Handling") / [14](/docs/14/runtime-config-error-handling.html
"PostgreSQL 14 - 20.14. Error Handling") / [13](/docs/13/runtime-config-error-
handling.html "PostgreSQL 13 - 20.14. Error Handling")

Development Versions: [18](/docs/18/runtime-config-error-handling.html
"PostgreSQL 18 - 20.14. Error Handling") / [devel](/docs/devel/runtime-config-
error-handling.html "PostgreSQL devel - 20.14. Error Handling")

Unsupported versions: [12](/docs/12/runtime-config-error-handling.html
"PostgreSQL 12 - 20.14. Error Handling") / [11](/docs/11/runtime-config-error-
handling.html "PostgreSQL 11 - 20.14. Error Handling") /
[10](/docs/10/runtime-config-error-handling.html "PostgreSQL 10 - 20.14. Error
Handling") / [9.6](/docs/9.6/runtime-config-error-handling.html "PostgreSQL
9.6 - 20.14. Error Handling") / [9.5](/docs/9.5/runtime-config-error-
handling.html "PostgreSQL 9.5 - 20.14. Error Handling") /
[9.4](/docs/9.4/runtime-config-error-handling.html "PostgreSQL 9.4 -
20.14. Error Handling") / [9.3](/docs/9.3/runtime-config-error-handling.html
"PostgreSQL 9.3 - 20.14. Error Handling") / [9.2](/docs/9.2/runtime-config-
error-handling.html "PostgreSQL 9.2 - 20.14. Error Handling") /
[9.1](/docs/9.1/runtime-config-error-handling.html "PostgreSQL 9.1 -
20.14. Error Handling")

__

20.14. Error Handling  
---  
[Prev](runtime-config-compatible.html "20.13. Version and Platform Compatibility")  | [Up](runtime-config.html "Chapter 20. Server Configuration") | Chapter 20. Server Configuration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](runtime-config-preset.html "20.15. Preset Options")  
  
* * *

## 20.14. Error Handling #

`exit_on_error` (`boolean`)  #

    

If on, any error will terminate the current session. By default, this is set
to off, so that only FATAL errors will terminate the session.

`restart_after_crash` (`boolean`)  #

    

When set to on, which is the default, PostgreSQL will automatically
reinitialize after a backend crash. Leaving this value set to on is normally
the best way to maximize the availability of the database. However, in some
circumstances, such as when PostgreSQL is being invoked by clusterware, it may
be useful to disable the restart so that the clusterware can gain control and
take any actions it deems appropriate.

This parameter can only be set in the `postgresql.conf` file or on the server
command line.

`data_sync_retry` (`boolean`)  #

    

When set to off, which is the default, PostgreSQL will raise a PANIC-level
error on failure to flush modified data files to the file system. This causes
the database server to crash. This parameter can only be set at server start.

On some operating systems, the status of data in the kernel's page cache is
unknown after a write-back failure. In some cases it might have been entirely
forgotten, making it unsafe to retry; the second attempt may be reported as
successful, when in fact the data has been lost. In these circumstances, the
only way to avoid data loss is to recover from the WAL after any failure is
reported, preferably after investigating the root cause of the failure and
replacing any faulty hardware.

If set to on, PostgreSQL will instead report an error but continue to run so
that the data flushing operation can be retried in a later checkpoint. Only
set it to on after investigating the operating system's treatment of buffered
data in case of write-back failure.

`recovery_init_sync_method` (`enum`)  #

    

When set to `fsync`, which is the default, PostgreSQL will recursively open
and synchronize all files in the data directory before crash recovery begins.
The search for files will follow symbolic links for the WAL directory and each
configured tablespace (but not any other symbolic links). This is intended to
make sure that all WAL and data files are durably stored on disk before
replaying changes. This applies whenever starting a database cluster that did
not shut down cleanly, including copies created with pg_basebackup.

On Linux, `syncfs` may be used instead, to ask the operating system to
synchronize the whole file systems that contain the data directory, the WAL
files and each tablespace (but not any other file systems that may be
reachable through symbolic links). This may be a lot faster than the `fsync`
setting, because it doesn't need to open each file one by one. On the other
hand, it may be slower if a file system is shared by other applications that
modify a lot of files, since those files will also be written to disk.
Furthermore, on versions of Linux before 5.8, I/O errors encountered while
writing data to disk may not be reported to PostgreSQL, and relevant error
messages may appear only in kernel logs.

This parameter can only be set in the `postgresql.conf` file or on the server
command line.

* * *

[Prev](runtime-config-compatible.html "20.13. Version and Platform Compatibility")  | [Up](runtime-config.html "Chapter 20. Server Configuration") |  [Next](runtime-config-preset.html "20.15. Preset Options")  
---|---|---  
20.13. Version and Platform Compatibility  | [Home](index.html "PostgreSQL 16.9 Documentation") |  20.15. Preset Options  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/runtime-config-error-
handling.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

