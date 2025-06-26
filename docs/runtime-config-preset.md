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

Supported Versions: [Current](/docs/current/runtime-config-preset.html
"PostgreSQL 17 - 20.15. Preset Options") ([17](/docs/17/runtime-config-
preset.html "PostgreSQL 17 - 20.15. Preset Options")) / [16](/docs/16/runtime-
config-preset.html "PostgreSQL 16 - 20.15. Preset Options") /
[15](/docs/15/runtime-config-preset.html "PostgreSQL 15 - 20.15. Preset
Options") / [14](/docs/14/runtime-config-preset.html "PostgreSQL 14 -
20.15. Preset Options") / [13](/docs/13/runtime-config-preset.html "PostgreSQL
13 - 20.15. Preset Options")

Development Versions: [18](/docs/18/runtime-config-preset.html "PostgreSQL 18
- 20.15. Preset Options") / [devel](/docs/devel/runtime-config-preset.html
"PostgreSQL devel - 20.15. Preset Options")

Unsupported versions: [12](/docs/12/runtime-config-preset.html "PostgreSQL 12
- 20.15. Preset Options") / [11](/docs/11/runtime-config-preset.html
"PostgreSQL 11 - 20.15. Preset Options") / [10](/docs/10/runtime-config-
preset.html "PostgreSQL 10 - 20.15. Preset Options") /
[9.6](/docs/9.6/runtime-config-preset.html "PostgreSQL 9.6 - 20.15. Preset
Options") / [9.5](/docs/9.5/runtime-config-preset.html "PostgreSQL 9.5 -
20.15. Preset Options") / [9.4](/docs/9.4/runtime-config-preset.html
"PostgreSQL 9.4 - 20.15. Preset Options") / [9.3](/docs/9.3/runtime-config-
preset.html "PostgreSQL 9.3 - 20.15. Preset Options") /
[9.2](/docs/9.2/runtime-config-preset.html "PostgreSQL 9.2 - 20.15. Preset
Options") / [9.1](/docs/9.1/runtime-config-preset.html "PostgreSQL 9.1 -
20.15. Preset Options") / [9.0](/docs/9.0/runtime-config-preset.html
"PostgreSQL 9.0 - 20.15. Preset Options") / [8.4](/docs/8.4/runtime-config-
preset.html "PostgreSQL 8.4 - 20.15. Preset Options") /
[8.3](/docs/8.3/runtime-config-preset.html "PostgreSQL 8.3 - 20.15. Preset
Options") / [8.2](/docs/8.2/runtime-config-preset.html "PostgreSQL 8.2 -
20.15. Preset Options") / [8.1](/docs/8.1/runtime-config-preset.html
"PostgreSQL 8.1 - 20.15. Preset Options")

__

20.15. Preset Options  
---  
[Prev](runtime-config-error-handling.html "20.14. Error Handling")  | [Up](runtime-config.html "Chapter 20. Server Configuration") | Chapter 20. Server Configuration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](runtime-config-custom.html "20.16. Customized Options")  
  
* * *

## 20.15. Preset Options #

The following “parameters” are read-only. As such, they have been excluded
from the sample `postgresql.conf` file. These options report various aspects
of PostgreSQL behavior that might be of interest to certain applications,
particularly administrative front-ends. Most of them are determined when
PostgreSQL is compiled or when it is installed.

`block_size` (`integer`)  #

    

Reports the size of a disk block. It is determined by the value of `BLCKSZ`
when building the server. The default value is 8192 bytes. The meaning of some
configuration variables (such as [shared_buffers](runtime-config-
resource.html#GUC-SHARED-BUFFERS)) is influenced by `block_size`. See [Section
20.4](runtime-config-resource.html "20.4. Resource Consumption") for
information.

`data_checksums` (`boolean`)  #

    

Reports whether data checksums are enabled for this cluster. See [data
checksums](app-initdb.html#APP-INITDB-DATA-CHECKSUMS) for more information.

`data_directory_mode` (`integer`)  #

    

On Unix systems this parameter reports the permissions the data directory
(defined by [data_directory](runtime-config-file-locations.html#GUC-DATA-
DIRECTORY)) had at server startup. (On Microsoft Windows this parameter will
always display `0700`.) See [group access](app-initdb.html#APP-INITDB-ALLOW-
GROUP-ACCESS) for more information.

`debug_assertions` (`boolean`)  #

    

Reports whether PostgreSQL has been built with assertions enabled. That is the
case if the macro `USE_ASSERT_CHECKING` is defined when PostgreSQL is built
(accomplished e.g., by the `configure` option `--enable-cassert`). By default
PostgreSQL is built without assertions.

`integer_datetimes` (`boolean`)  #

    

Reports whether PostgreSQL was built with support for 64-bit-integer dates and
times. As of PostgreSQL 10, this is always `on`.

`in_hot_standby` (`boolean`)  #

    

Reports whether the server is currently in hot standby mode. When this is
`on`, all transactions are forced to be read-only. Within a session, this can
change only if the server is promoted to be primary. See [Section 27.4](hot-
standby.html "27.4. Hot Standby") for more information.

`max_function_args` (`integer`)  #

    

Reports the maximum number of function arguments. It is determined by the
value of `FUNC_MAX_ARGS` when building the server. The default value is 100
arguments.

`max_identifier_length` (`integer`)  #

    

Reports the maximum identifier length. It is determined as one less than the
value of `NAMEDATALEN` when building the server. The default value of
`NAMEDATALEN` is 64; therefore the default `max_identifier_length` is 63
bytes, which can be less than 63 characters when using multibyte encodings.

`max_index_keys` (`integer`)  #

    

Reports the maximum number of index keys. It is determined by the value of
`INDEX_MAX_KEYS` when building the server. The default value is 32 keys.

`segment_size` (`integer`)  #

    

Reports the number of blocks (pages) that can be stored within a file segment.
It is determined by the value of `RELSEG_SIZE` when building the server. The
maximum size of a segment file in bytes is equal to `segment_size` multiplied
by `block_size`; by default this is 1GB.

`server_encoding` (`string`)  #

    

Reports the database encoding (character set). It is determined when the
database is created. Ordinarily, clients need only be concerned with the value
of [client_encoding](runtime-config-client.html#GUC-CLIENT-ENCODING).

`server_version` (`string`)  #

    

Reports the version number of the server. It is determined by the value of
`PG_VERSION` when building the server.

`server_version_num` (`integer`)  #

    

Reports the version number of the server as an integer. It is determined by
the value of `PG_VERSION_NUM` when building the server.

`shared_memory_size` (`integer`)  #

    

Reports the size of the main shared memory area, rounded up to the nearest
megabyte.

`shared_memory_size_in_huge_pages` (`integer`)  #

    

Reports the number of huge pages that are needed for the main shared memory
area based on the specified [huge_page_size](runtime-config-resource.html#GUC-
HUGE-PAGE-SIZE). If huge pages are not supported, this will be `-1`.

This setting is supported only on Linux. It is always set to `-1` on other
platforms. For more details about using huge pages on Linux, see [Section
19.4.5](kernel-resources.html#LINUX-HUGE-PAGES "19.4.5. Linux Huge Pages").

`ssl_library` (`string`)  #

    

Reports the name of the SSL library that this PostgreSQL server was built with
(even if SSL is not currently configured or in use on this instance), for
example `OpenSSL`, or an empty string if none.

`wal_block_size` (`integer`)  #

    

Reports the size of a WAL disk block. It is determined by the value of
`XLOG_BLCKSZ` when building the server. The default value is 8192 bytes.

`wal_segment_size` (`integer`)  #

    

Reports the size of write ahead log segments. The default value is 16MB. See
[Section 30.5](wal-configuration.html "30.5. WAL Configuration") for more
information.

* * *

[Prev](runtime-config-error-handling.html "20.14. Error Handling")  | [Up](runtime-config.html "Chapter 20. Server Configuration") |  [Next](runtime-config-custom.html "20.16. Customized Options")  
---|---|---  
20.14. Error Handling  | [Home](index.html "PostgreSQL 16.9 Documentation") |  20.16. Customized Options  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/runtime-config-preset.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

