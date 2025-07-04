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

Supported Versions: [Current](/docs/current/server-start.html "PostgreSQL 17 -
19.3. Starting the Database Server") ([17](/docs/17/server-start.html
"PostgreSQL 17 - 19.3. Starting the Database Server")) / [16](/docs/16/server-
start.html "PostgreSQL 16 - 19.3. Starting the Database Server") /
[15](/docs/15/server-start.html "PostgreSQL 15 - 19.3. Starting the Database
Server") / [14](/docs/14/server-start.html "PostgreSQL 14 - 19.3. Starting the
Database Server") / [13](/docs/13/server-start.html "PostgreSQL 13 -
19.3. Starting the Database Server")

Development Versions: [18](/docs/18/server-start.html "PostgreSQL 18 -
19.3. Starting the Database Server") / [devel](/docs/devel/server-start.html
"PostgreSQL devel - 19.3. Starting the Database Server")

Unsupported versions: [12](/docs/12/server-start.html "PostgreSQL 12 -
19.3. Starting the Database Server") / [11](/docs/11/server-start.html
"PostgreSQL 11 - 19.3. Starting the Database Server") / [10](/docs/10/server-
start.html "PostgreSQL 10 - 19.3. Starting the Database Server") /
[9.6](/docs/9.6/server-start.html "PostgreSQL 9.6 - 19.3. Starting the
Database Server") / [9.5](/docs/9.5/server-start.html "PostgreSQL 9.5 -
19.3. Starting the Database Server") / [9.4](/docs/9.4/server-start.html
"PostgreSQL 9.4 - 19.3. Starting the Database Server") /
[9.3](/docs/9.3/server-start.html "PostgreSQL 9.3 - 19.3. Starting the
Database Server") / [9.2](/docs/9.2/server-start.html "PostgreSQL 9.2 -
19.3. Starting the Database Server") / [9.1](/docs/9.1/server-start.html
"PostgreSQL 9.1 - 19.3. Starting the Database Server") /
[9.0](/docs/9.0/server-start.html "PostgreSQL 9.0 - 19.3. Starting the
Database Server") / [8.4](/docs/8.4/server-start.html "PostgreSQL 8.4 -
19.3. Starting the Database Server") / [8.3](/docs/8.3/server-start.html
"PostgreSQL 8.3 - 19.3. Starting the Database Server") /
[8.2](/docs/8.2/server-start.html "PostgreSQL 8.2 - 19.3. Starting the
Database Server")

__

19.3. Starting the Database Server  
---  
[Prev](creating-cluster.html "19.2. Creating a Database Cluster")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") | Chapter 19. Server Setup and Operation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](kernel-resources.html "19.4. Managing Kernel Resources")  
  
* * *

## 19.3. Starting the Database Server #

[19.3.1. Server Start-up Failures](server-start.html#SERVER-START-FAILURES)

[19.3.2. Client Connection Problems](server-start.html#CLIENT-CONNECTION-
PROBLEMS)

Before anyone can access the database, you must start the database server. The
database server program is called `postgres`.

If you are using a pre-packaged version of PostgreSQL, it almost certainly
includes provisions for running the server as a background task according to
the conventions of your operating system. Using the package's infrastructure
to start the server will be much less work than figuring out how to do this
yourself. Consult the package-level documentation for details.

The bare-bones way to start the server manually is just to invoke `postgres`
directly, specifying the location of the data directory with the `-D` option,
for example:

    
    
    $ **postgres -D /usr/local/pgsql/data**
    

which will leave the server running in the foreground. This must be done while
logged into the PostgreSQL user account. Without `-D`, the server will try to
use the data directory named by the environment variable `PGDATA`. If that
variable is not provided either, it will fail.

Normally it is better to start `postgres` in the background. For this, use the
usual Unix shell syntax:

    
    
    $ **postgres -D /usr/local/pgsql/data>logfile 2>&1 &**
    

It is important to store the server's stdout and stderr output somewhere, as
shown above. It will help for auditing purposes and to diagnose problems. (See
[Section 25.3](logfile-maintenance.html "25.3. Log File Maintenance") for a
more thorough discussion of log file handling.)

The `postgres` program also takes a number of other command-line options. For
more information, see the [postgres](app-postgres.html "postgres") reference
page and [Chapter 20](runtime-config.html "Chapter 20. Server Configuration")
below.

This shell syntax can get tedious quickly. Therefore the wrapper program
[pg_ctl](app-pg-ctl.html "pg_ctl") is provided to simplify some tasks. For
example:

    
    
    pg_ctl start -l logfile
    

will start the server in the background and put the output into the named log
file. The `-D` option has the same meaning here as for `postgres`. `pg_ctl` is
also capable of stopping the server.

Normally, you will want to start the database server when the computer boots.
Autostart scripts are operating-system-specific. There are a few example
scripts distributed with PostgreSQL in the `contrib/start-scripts` directory.
Installing one will require root privileges.

Different systems have different conventions for starting up daemons at boot
time. Many systems have a file `/etc/rc.local` or `/etc/rc.d/rc.local`. Others
use `init.d` or `rc.d` directories. Whatever you do, the server must be run by
the PostgreSQL user account _and not by root_ or any other user. Therefore you
probably should form your commands using `su postgres -c '...'`. For example:

    
    
    su postgres -c 'pg_ctl start -D /usr/local/pgsql/data -l serverlog'
    

Here are a few more operating-system-specific suggestions. (In each case be
sure to use the proper installation directory and user name where we show
generic values.)

  * For FreeBSD, look at the file `contrib/start-scripts/freebsd` in the PostgreSQL source distribution. 

  * On OpenBSD, add the following lines to the file `/etc/rc.local`: 
        
        if [ -x /usr/local/pgsql/bin/pg_ctl -a -x /usr/local/pgsql/bin/postgres ]; then
            su -l postgres -c '/usr/local/pgsql/bin/pg_ctl start -s -l /var/postgresql/log -D /usr/local/pgsql/data'
            echo -n ' postgresql'
        fi
        

  * On Linux systems either add 
        
        /usr/local/pgsql/bin/pg_ctl start -l logfile -D /usr/local/pgsql/data
        

to `/etc/rc.d/rc.local` or `/etc/rc.local` or look at the file `contrib/start-
scripts/linux` in the PostgreSQL source distribution.

When using systemd, you can use the following service unit file (e.g., at
`/etc/systemd/system/postgresql.service`):

        
        [Unit]
        Description=PostgreSQL database server
        Documentation=man:postgres(1)
        After=network-online.target
        Wants=network-online.target
        
        [Service]
        Type=notify
        User=postgres
        ExecStart=/usr/local/pgsql/bin/postgres -D /usr/local/pgsql/data
        ExecReload=/bin/kill -HUP $MAINPID
        KillMode=mixed
        KillSignal=SIGINT
        TimeoutSec=infinity
        
        [Install]
        WantedBy=multi-user.target
        

Using `Type=notify` requires that the server binary was built with `configure
--with-systemd`.

Consider carefully the timeout setting. systemd has a default timeout of 90
seconds as of this writing and will kill a process that does not report
readiness within that time. But a PostgreSQL server that might have to perform
crash recovery at startup could take much longer to become ready. The
suggested value of `infinity` disables the timeout logic.

  * On NetBSD, use either the FreeBSD or Linux start scripts, depending on preference. 

  * On Solaris, create a file called `/etc/init.d/postgresql` that contains the following line: 
        
        su - postgres -c "/usr/local/pgsql/bin/pg_ctl start -l logfile -D /usr/local/pgsql/data"
        

Then, create a symbolic link to it in `/etc/rc3.d` as `S99postgresql`.

While the server is running, its PID is stored in the file `postmaster.pid` in
the data directory. This is used to prevent multiple server instances from
running in the same data directory and can also be used for shutting down the
server.

### 19.3.1. Server Start-up Failures #

There are several common reasons the server might fail to start. Check the
server's log file, or start it by hand (without redirecting standard output or
standard error) and see what error messages appear. Below we explain some of
the most common error messages in more detail.

    
    
    LOG:  could not bind IPv4 address "127.0.0.1": Address already in use
    HINT:  Is another postmaster already running on port 5432? If not, wait a few seconds and retry.
    FATAL:  could not create any TCP/IP sockets
    

This usually means just what it suggests: you tried to start another server on
the same port where one is already running. However, if the kernel error
message is not `Address already in use` or some variant of that, there might
be a different problem. For example, trying to start a server on a reserved
port number might draw something like:

    
    
    $ **postgres -p 666**
    LOG:  could not bind IPv4 address "127.0.0.1": Permission denied
    HINT:  Is another postmaster already running on port 666? If not, wait a few seconds and retry.
    FATAL:  could not create any TCP/IP sockets
    

A message like:

    
    
    FATAL:  could not create shared memory segment: Invalid argument
    DETAIL:  Failed system call was shmget(key=5440001, size=4011376640, 03600).
    

probably means your kernel's limit on the size of shared memory is smaller
than the work area PostgreSQL is trying to create (4011376640 bytes in this
example). This is only likely to happen if you have set `shared_memory_type`
to `sysv`. In that case, you can try starting the server with a smaller-than-
normal number of buffers ([shared_buffers](runtime-config-resource.html#GUC-
SHARED-BUFFERS)), or reconfigure your kernel to increase the allowed shared
memory size. You might also see this message when trying to start multiple
servers on the same machine, if their total space requested exceeds the kernel
limit.

An error like:

    
    
    FATAL:  could not create semaphores: No space left on device
    DETAIL:  Failed system call was semget(5440126, 17, 03600).
    

does _not_ mean you've run out of disk space. It means your kernel's limit on
the number of System V semaphores is smaller than the number PostgreSQL wants
to create. As above, you might be able to work around the problem by starting
the server with a reduced number of allowed connections
([max_connections](runtime-config-connection.html#GUC-MAX-CONNECTIONS)), but
you'll eventually want to increase the kernel limit.

Details about configuring System V IPC facilities are given in [Section
19.4.1](kernel-resources.html#SYSVIPC "19.4.1. Shared Memory and Semaphores").

### 19.3.2. Client Connection Problems #

Although the error conditions possible on the client side are quite varied and
application-dependent, a few of them might be directly related to how the
server was started. Conditions other than those shown below should be
documented with the respective client application.

    
    
    psql: error: connection to server at "server.joe.com" (123.123.123.123), port 5432 failed: Connection refused
            Is the server running on that host and accepting TCP/IP connections?
    

This is the generic “I couldn't find a server to talk to” failure. It looks
like the above when TCP/IP communication is attempted. A common mistake is to
forget to configure the server to allow TCP/IP connections.

Alternatively, you might get this when attempting Unix-domain socket
communication to a local server:

    
    
    psql: error: connection to server on socket "/tmp/.s.PGSQL.5432" failed: No such file or directory
            Is the server running locally and accepting connections on that socket?
    

If the server is indeed running, check that the client's idea of the socket
path (here `/tmp`) agrees with the server's [unix_socket_directories](runtime-
config-connection.html#GUC-UNIX-SOCKET-DIRECTORIES) setting.

A connection failure message always shows the server address or socket path
name, which is useful in verifying that the client is trying to connect to the
right place. If there is in fact no server listening there, the kernel error
message will typically be either `Connection refused` or `No such file or
directory`, as illustrated. (It is important to realize that `Connection
refused` in this context does _not_ mean that the server got your connection
request and rejected it. That case will produce a different message, as shown
in [Section 21.15](client-authentication-problems.html "21.15. Authentication
Problems").) Other error messages such as `Connection timed out` might
indicate more fundamental problems, like lack of network connectivity, or a
firewall blocking the connection.

* * *

[Prev](creating-cluster.html "19.2. Creating a Database Cluster")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") |  [Next](kernel-resources.html "19.4. Managing Kernel Resources")  
---|---|---  
19.2. Creating a Database Cluster  | [Home](index.html "PostgreSQL 16.9 Documentation") |  19.4. Managing Kernel Resources  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/server-start.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

