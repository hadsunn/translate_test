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

Supported Versions: [Current](/docs/current/server-shutdown.html "PostgreSQL
17 - 19.5. Shutting Down the Server") ([17](/docs/17/server-shutdown.html
"PostgreSQL 17 - 19.5. Shutting Down the Server")) / [16](/docs/16/server-
shutdown.html "PostgreSQL 16 - 19.5. Shutting Down the Server") /
[15](/docs/15/server-shutdown.html "PostgreSQL 15 - 19.5. Shutting Down the
Server") / [14](/docs/14/server-shutdown.html "PostgreSQL 14 - 19.5. Shutting
Down the Server") / [13](/docs/13/server-shutdown.html "PostgreSQL 13 -
19.5. Shutting Down the Server")

Development Versions: [18](/docs/18/server-shutdown.html "PostgreSQL 18 -
19.5. Shutting Down the Server") / [devel](/docs/devel/server-shutdown.html
"PostgreSQL devel - 19.5. Shutting Down the Server")

Unsupported versions: [12](/docs/12/server-shutdown.html "PostgreSQL 12 -
19.5. Shutting Down the Server") / [11](/docs/11/server-shutdown.html
"PostgreSQL 11 - 19.5. Shutting Down the Server") / [10](/docs/10/server-
shutdown.html "PostgreSQL 10 - 19.5. Shutting Down the Server") /
[9.6](/docs/9.6/server-shutdown.html "PostgreSQL 9.6 - 19.5. Shutting Down the
Server") / [9.5](/docs/9.5/server-shutdown.html "PostgreSQL 9.5 -
19.5. Shutting Down the Server") / [9.4](/docs/9.4/server-shutdown.html
"PostgreSQL 9.4 - 19.5. Shutting Down the Server") / [9.3](/docs/9.3/server-
shutdown.html "PostgreSQL 9.3 - 19.5. Shutting Down the Server") /
[9.2](/docs/9.2/server-shutdown.html "PostgreSQL 9.2 - 19.5. Shutting Down the
Server") / [9.1](/docs/9.1/server-shutdown.html "PostgreSQL 9.1 -
19.5. Shutting Down the Server") / [9.0](/docs/9.0/server-shutdown.html
"PostgreSQL 9.0 - 19.5. Shutting Down the Server") / [8.4](/docs/8.4/server-
shutdown.html "PostgreSQL 8.4 - 19.5. Shutting Down the Server") /
[8.3](/docs/8.3/server-shutdown.html "PostgreSQL 8.3 - 19.5. Shutting Down the
Server") / [8.2](/docs/8.2/server-shutdown.html "PostgreSQL 8.2 -
19.5. Shutting Down the Server")

__

19.5. Shutting Down the Server  
---  
[Prev](kernel-resources.html "19.4. Managing Kernel Resources")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") | Chapter 19. Server Setup and Operation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](upgrading.html "19.6. Upgrading a PostgreSQL Cluster")  
  
* * *

## 19.5. Shutting Down the Server #

There are several ways to shut down the database server. Under the hood, they
all reduce to sending a signal to the supervisor `postgres` process.

If you are using a pre-packaged version of PostgreSQL, and you used its
provisions for starting the server, then you should also use its provisions
for stopping the server. Consult the package-level documentation for details.

When managing the server directly, you can control the type of shutdown by
sending different signals to the `postgres` process:

SIGTERM

    

This is the _Smart Shutdown_ mode. After receiving SIGTERM, the server
disallows new connections, but lets existing sessions end their work normally.
It shuts down only after all of the sessions terminate. If the server is in
recovery when a smart shutdown is requested, recovery and streaming
replication will be stopped only after all regular sessions have terminated.

SIGINT

    

This is the _Fast Shutdown_ mode. The server disallows new connections and
sends all existing server processes SIGTERM, which will cause them to abort
their current transactions and exit promptly. It then waits for all server
processes to exit and finally shuts down.

SIGQUIT

    

This is the _Immediate Shutdown_ mode. The server will send SIGQUIT to all
child processes and wait for them to terminate. If any do not terminate within
5 seconds, they will be sent SIGKILL. The supervisor server process exits as
soon as all child processes have exited, without doing normal database
shutdown processing. This will lead to recovery (by replaying the WAL log)
upon next start-up. This is recommended only in emergencies.

The [pg_ctl](app-pg-ctl.html "pg_ctl") program provides a convenient interface
for sending these signals to shut down the server. Alternatively, you can send
the signal directly using `kill` on non-Windows systems. The PID of the
`postgres` process can be found using the `ps` program, or from the file
`postmaster.pid` in the data directory. For example, to do a fast shutdown:

    
    
    $ **kill -INT `head -1 /usr/local/pgsql/data/postmaster.pid`**
    

### Important

It is best not to use SIGKILL to shut down the server. Doing so will prevent
the server from releasing shared memory and semaphores. Furthermore, SIGKILL
kills the `postgres` process without letting it relay the signal to its
subprocesses, so it might be necessary to kill the individual subprocesses by
hand as well.

To terminate an individual session while allowing other sessions to continue,
use `pg_terminate_backend()` (see [Table 9.90](functions-admin.html#FUNCTIONS-
ADMIN-SIGNAL-TABLE "Table 9.90. Server Signaling Functions")) or send a
SIGTERM signal to the child process associated with the session.

* * *

[Prev](kernel-resources.html "19.4. Managing Kernel Resources")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") |  [Next](upgrading.html "19.6. Upgrading a PostgreSQL Cluster")  
---|---|---  
19.4. Managing Kernel Resources  | [Home](index.html "PostgreSQL 16.9 Documentation") |  19.6. Upgrading a PostgreSQL Cluster  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/server-shutdown.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

