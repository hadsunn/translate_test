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

Supported Versions: [Current](/docs/current/pgprewarm.html "PostgreSQL 17 -
F.30. pg_prewarm — preload relation data into buffer caches")
([17](/docs/17/pgprewarm.html "PostgreSQL 17 - F.30. pg_prewarm — preload
relation data into buffer caches")) / [16](/docs/16/pgprewarm.html "PostgreSQL
16 - F.30. pg_prewarm — preload relation data into buffer caches") /
[15](/docs/15/pgprewarm.html "PostgreSQL 15 - F.30. pg_prewarm — preload
relation data into buffer caches") / [14](/docs/14/pgprewarm.html "PostgreSQL
14 - F.30. pg_prewarm — preload relation data into buffer caches") /
[13](/docs/13/pgprewarm.html "PostgreSQL 13 - F.30. pg_prewarm — preload
relation data into buffer caches")

Development Versions: [18](/docs/18/pgprewarm.html "PostgreSQL 18 -
F.30. pg_prewarm — preload relation data into buffer caches") /
[devel](/docs/devel/pgprewarm.html "PostgreSQL devel - F.30. pg_prewarm —
preload relation data into buffer caches")

Unsupported versions: [12](/docs/12/pgprewarm.html "PostgreSQL 12 -
F.30. pg_prewarm — preload relation data into buffer caches") /
[11](/docs/11/pgprewarm.html "PostgreSQL 11 - F.30. pg_prewarm — preload
relation data into buffer caches") / [10](/docs/10/pgprewarm.html "PostgreSQL
10 - F.30. pg_prewarm — preload relation data into buffer caches") /
[9.6](/docs/9.6/pgprewarm.html "PostgreSQL 9.6 - F.30. pg_prewarm — preload
relation data into buffer caches") / [9.5](/docs/9.5/pgprewarm.html
"PostgreSQL 9.5 - F.30. pg_prewarm — preload relation data into buffer
caches") / [9.4](/docs/9.4/pgprewarm.html "PostgreSQL 9.4 - F.30. pg_prewarm —
preload relation data into buffer caches")

__

F.30. pg_prewarm — preload relation data into buffer caches  
---  
[Prev](pgfreespacemap.html "F.29. pg_freespacemap — examine the free space map")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pgrowlocks.html "F.31. pgrowlocks — show a table's row locking information")  
  
* * *

## F.30. pg_prewarm — preload relation data into buffer caches #

[F.30.1. Functions](pgprewarm.html#PGPREWARM-FUNCS)

[F.30.2. Configuration Parameters](pgprewarm.html#PGPREWARM-CONFIG-PARAMS)

[F.30.3. Author](pgprewarm.html#PGPREWARM-AUTHOR)

The `pg_prewarm` module provides a convenient way to load relation data into
either the operating system buffer cache or the PostgreSQL buffer cache.
Prewarming can be performed manually using the `pg_prewarm` function, or can
be performed automatically by including `pg_prewarm` in
[shared_preload_libraries](runtime-config-client.html#GUC-SHARED-PRELOAD-
LIBRARIES). In the latter case, the system will run a background worker which
periodically records the contents of shared buffers in a file called
`autoprewarm.blocks` and will, using 2 background workers, reload those same
blocks after a restart.

### F.30.1. Functions #

    
    
    pg_prewarm(regclass, mode text default 'buffer', fork text default 'main',
               first_block int8 default null,
               last_block int8 default null) RETURNS int8
    

The first argument is the relation to be prewarmed. The second argument is the
prewarming method to be used, as further discussed below; the third is the
relation fork to be prewarmed, usually `main`. The fourth argument is the
first block number to prewarm (`NULL` is accepted as a synonym for zero). The
fifth argument is the last block number to prewarm (`NULL` means prewarm
through the last block in the relation). The return value is the number of
blocks prewarmed.

There are three available prewarming methods. `prefetch` issues asynchronous
prefetch requests to the operating system, if this is supported, or throws an
error otherwise. `read` reads the requested range of blocks; unlike
`prefetch`, this is synchronous and supported on all platforms and builds, but
may be slower. `buffer` reads the requested range of blocks into the database
buffer cache.

Note that with any of these methods, attempting to prewarm more blocks than
can be cached — by the OS when using `prefetch` or `read`, or by PostgreSQL
when using `buffer` — will likely result in lower-numbered blocks being
evicted as higher numbered blocks are read in. Prewarmed data also enjoys no
special protection from cache evictions, so it is possible that other system
activity may evict the newly prewarmed blocks shortly after they are read;
conversely, prewarming may also evict other data from cache. For these
reasons, prewarming is typically most useful at startup, when caches are
largely empty.

    
    
    autoprewarm_start_worker() RETURNS void
    

Launch the main autoprewarm worker. This will normally happen automatically,
but is useful if automatic prewarm was not configured at server startup time
and you wish to start up the worker at a later time.

    
    
    autoprewarm_dump_now() RETURNS int8
    

Update `autoprewarm.blocks` immediately. This may be useful if the autoprewarm
worker is not running but you anticipate running it after the next restart.
The return value is the number of records written to `autoprewarm.blocks`.

### F.30.2. Configuration Parameters #

`pg_prewarm.autoprewarm` (`boolean`)

    

Controls whether the server should run the autoprewarm worker. This is on by
default. This parameter can only be set at server start.

`pg_prewarm.autoprewarm_interval` (`integer`)

    

This is the interval between updates to `autoprewarm.blocks`. The default is
300 seconds. If set to 0, the file will not be dumped at regular intervals,
but only when the server is shut down.

These parameters must be set in `postgresql.conf`. Typical usage might be:

    
    
    # postgresql.conf
    shared_preload_libraries = 'pg_prewarm'
    
    pg_prewarm.autoprewarm = true
    pg_prewarm.autoprewarm_interval = 300s
    
    

### F.30.3. Author #

Robert Haas `<[rhaas@postgresql.org](mailto:rhaas@postgresql.org)>`

* * *

[Prev](pgfreespacemap.html "F.29. pg_freespacemap — examine the free space map")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](pgrowlocks.html "F.31. pgrowlocks — show a table's row locking information")  
---|---|---  
F.29. pg_freespacemap — examine the free space map  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.31. pgrowlocks — show a table's row locking information  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pgprewarm.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

