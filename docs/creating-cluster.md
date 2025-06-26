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

Supported Versions: [Current](/docs/current/creating-cluster.html "PostgreSQL
17 - 19.2. Creating a Database Cluster") ([17](/docs/17/creating-cluster.html
"PostgreSQL 17 - 19.2. Creating a Database Cluster")) /
[16](/docs/16/creating-cluster.html "PostgreSQL 16 - 19.2. Creating a Database
Cluster") / [15](/docs/15/creating-cluster.html "PostgreSQL 15 -
19.2. Creating a Database Cluster") / [14](/docs/14/creating-cluster.html
"PostgreSQL 14 - 19.2. Creating a Database Cluster") / [13](/docs/13/creating-
cluster.html "PostgreSQL 13 - 19.2. Creating a Database Cluster")

Development Versions: [18](/docs/18/creating-cluster.html "PostgreSQL 18 -
19.2. Creating a Database Cluster") / [devel](/docs/devel/creating-
cluster.html "PostgreSQL devel - 19.2. Creating a Database Cluster")

Unsupported versions: [12](/docs/12/creating-cluster.html "PostgreSQL 12 -
19.2. Creating a Database Cluster") / [11](/docs/11/creating-cluster.html
"PostgreSQL 11 - 19.2. Creating a Database Cluster") / [10](/docs/10/creating-
cluster.html "PostgreSQL 10 - 19.2. Creating a Database Cluster") /
[9.6](/docs/9.6/creating-cluster.html "PostgreSQL 9.6 - 19.2. Creating a
Database Cluster") / [9.5](/docs/9.5/creating-cluster.html "PostgreSQL 9.5 -
19.2. Creating a Database Cluster") / [9.4](/docs/9.4/creating-cluster.html
"PostgreSQL 9.4 - 19.2. Creating a Database Cluster") /
[9.3](/docs/9.3/creating-cluster.html "PostgreSQL 9.3 - 19.2. Creating a
Database Cluster") / [9.2](/docs/9.2/creating-cluster.html "PostgreSQL 9.2 -
19.2. Creating a Database Cluster") / [9.1](/docs/9.1/creating-cluster.html
"PostgreSQL 9.1 - 19.2. Creating a Database Cluster") /
[9.0](/docs/9.0/creating-cluster.html "PostgreSQL 9.0 - 19.2. Creating a
Database Cluster") / [8.4](/docs/8.4/creating-cluster.html "PostgreSQL 8.4 -
19.2. Creating a Database Cluster") / [8.3](/docs/8.3/creating-cluster.html
"PostgreSQL 8.3 - 19.2. Creating a Database Cluster") /
[8.2](/docs/8.2/creating-cluster.html "PostgreSQL 8.2 - 19.2. Creating a
Database Cluster") / [8.1](/docs/8.1/creating-cluster.html "PostgreSQL 8.1 -
19.2. Creating a Database Cluster") / [8.0](/docs/8.0/creating-cluster.html
"PostgreSQL 8.0 - 19.2. Creating a Database Cluster") /
[7.4](/docs/7.4/creating-cluster.html "PostgreSQL 7.4 - 19.2. Creating a
Database Cluster") / [7.3](/docs/7.3/creating-cluster.html "PostgreSQL 7.3 -
19.2. Creating a Database Cluster") / [7.2](/docs/7.2/creating-cluster.html
"PostgreSQL 7.2 - 19.2. Creating a Database Cluster") /
[7.1](/docs/7.1/creating-cluster.html "PostgreSQL 7.1 - 19.2. Creating a
Database Cluster")

__

19.2. Creating a Database Cluster  
---  
[Prev](postgres-user.html "19.1. The PostgreSQL User Account")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") | Chapter 19. Server Setup and Operation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](server-start.html "19.3. Starting the Database Server")  
  
* * *

## 19.2. Creating a Database Cluster #

[19.2.1. Use of Secondary File Systems](creating-cluster.html#CREATING-
CLUSTER-MOUNT-POINTS)

[19.2.2. File Systems](creating-cluster.html#CREATING-CLUSTER-FILESYSTEM)

Before you can do anything, you must initialize a database storage area on
disk. We call this a _database cluster_. (The SQL standard uses the term
catalog cluster.) A database cluster is a collection of databases that is
managed by a single instance of a running database server. After
initialization, a database cluster will contain a database named `postgres`,
which is meant as a default database for use by utilities, users and third
party applications. The database server itself does not require the `postgres`
database to exist, but many external utility programs assume it exists. There
are two more databases created within each cluster during initialization,
named `template1` and `template0`. As the names suggest, these will be used as
templates for subsequently-created databases; they should not be used for
actual work. (See [Chapter 23](managing-databases.html "Chapter 23. Managing
Databases") for information about creating new databases within a cluster.)

In file system terms, a database cluster is a single directory under which all
data will be stored. We call this the _data directory_ or _data area_. It is
completely up to you where you choose to store your data. There is no default,
although locations such as `/usr/local/pgsql/data` or `/var/lib/pgsql/data`
are popular. The data directory must be initialized before being used, using
the program [initdb](app-initdb.html "initdb") which is installed with
PostgreSQL.

If you are using a pre-packaged version of PostgreSQL, it may well have a
specific convention for where to place the data directory, and it may also
provide a script for creating the data directory. In that case you should use
that script in preference to running `initdb` directly. Consult the package-
level documentation for details.

To initialize a database cluster manually, run `initdb` and specify the
desired file system location of the database cluster with the `-D` option, for
example:

    
    
    $ **initdb -D /usr/local/pgsql/data**
    

Note that you must execute this command while logged into the PostgreSQL user
account, which is described in the previous section.

### Tip

As an alternative to the `-D` option, you can set the environment variable
`PGDATA`.

Alternatively, you can run `initdb` via the [pg_ctl](app-pg-ctl.html "pg_ctl")
program like so:

    
    
    $ **pg_ctl -D /usr/local/pgsql/data initdb**
    

This may be more intuitive if you are using `pg_ctl` for starting and stopping
the server (see [Section 19.3](server-start.html "19.3. Starting the Database
Server")), so that `pg_ctl` would be the sole command you use for managing the
database server instance.

`initdb` will attempt to create the directory you specify if it does not
already exist. Of course, this will fail if `initdb` does not have permissions
to write in the parent directory. It's generally recommendable that the
PostgreSQL user own not just the data directory but its parent directory as
well, so that this should not be a problem. If the desired parent directory
doesn't exist either, you will need to create it first, using root privileges
if the grandparent directory isn't writable. So the process might look like
this:

    
    
    root# **mkdir /usr/local/pgsql**
    root# **chown postgres /usr/local/pgsql**
    root# **su postgres**
    postgres$ **initdb -D /usr/local/pgsql/data**
    

`initdb` will refuse to run if the data directory exists and already contains
files; this is to prevent accidentally overwriting an existing installation.

Because the data directory contains all the data stored in the database, it is
essential that it be secured from unauthorized access. `initdb` therefore
revokes access permissions from everyone but the PostgreSQL user, and
optionally, group. Group access, when enabled, is read-only. This allows an
unprivileged user in the same group as the cluster owner to take a backup of
the cluster data or perform other operations that only require read access.

Note that enabling or disabling group access on an existing cluster requires
the cluster to be shut down and the appropriate mode to be set on all
directories and files before restarting PostgreSQL. Otherwise, a mix of modes
might exist in the data directory. For clusters that allow access only by the
owner, the appropriate modes are `0700` for directories and `0600` for files.
For clusters that also allow reads by the group, the appropriate modes are
`0750` for directories and `0640` for files.

However, while the directory contents are secure, the default client
authentication setup allows any local user to connect to the database and even
become the database superuser. If you do not trust other local users, we
recommend you use one of `initdb`'s `-W`, `--pwprompt` or `--pwfile` options
to assign a password to the database superuser. Also, specify `-A scram-
sha-256` so that the default `trust` authentication mode is not used; or
modify the generated `pg_hba.conf` file after running `initdb`, but _before_
you start the server for the first time. (Other reasonable approaches include
using `peer` authentication or file system permissions to restrict
connections. See [Chapter 21](client-authentication.html "Chapter 21. Client
Authentication") for more information.)

`initdb` also initializes the default locale for the database cluster.
Normally, it will just take the locale settings in the environment and apply
them to the initialized database. It is possible to specify a different locale
for the database; more information about that can be found in [Section
24.1](locale.html "24.1. Locale Support"). The default sort order used within
the particular database cluster is set by `initdb`, and while you can create
new databases using different sort order, the order used in the template
databases that initdb creates cannot be changed without dropping and
recreating them. There is also a performance impact for using locales other
than `C` or `POSIX`. Therefore, it is important to make this choice correctly
the first time.

`initdb` also sets the default character set encoding for the database
cluster. Normally this should be chosen to match the locale setting. For
details see [Section 24.3](multibyte.html "24.3. Character Set Support").

Non-`C` and non-`POSIX` locales rely on the operating system's collation
library for character set ordering. This controls the ordering of keys stored
in indexes. For this reason, a cluster cannot switch to an incompatible
collation library version, either through snapshot restore, binary streaming
replication, a different operating system, or an operating system upgrade.

### 19.2.1. Use of Secondary File Systems #

Many installations create their database clusters on file systems (volumes)
other than the machine's “root” volume. If you choose to do this, it is not
advisable to try to use the secondary volume's topmost directory (mount point)
as the data directory. Best practice is to create a directory within the
mount-point directory that is owned by the PostgreSQL user, and then create
the data directory within that. This avoids permissions problems, particularly
for operations such as pg_upgrade, and it also ensures clean failures if the
secondary volume is taken offline.

### 19.2.2. File Systems #

Generally, any file system with POSIX semantics can be used for PostgreSQL.
Users prefer different file systems for a variety of reasons, including vendor
support, performance, and familiarity. Experience suggests that, all other
things being equal, one should not expect major performance or behavior
changes merely from switching file systems or making minor file system
configuration changes.

#### 19.2.2.1. NFS #

It is possible to use an NFS file system for storing the PostgreSQL data
directory. PostgreSQL does nothing special for NFS file systems, meaning it
assumes NFS behaves exactly like locally-connected drives. PostgreSQL does not
use any functionality that is known to have nonstandard behavior on NFS, such
as file locking.

The only firm requirement for using NFS with PostgreSQL is that the file
system is mounted using the `hard` option. With the `hard` option, processes
can “hang” indefinitely if there are network problems, so this configuration
will require a careful monitoring setup. The `soft` option will interrupt
system calls in case of network problems, but PostgreSQL will not repeat
system calls interrupted in this way, so any such interruption will result in
an I/O error being reported.

It is not necessary to use the `sync` mount option. The behavior of the
`async` option is sufficient, since PostgreSQL issues `fsync` calls at
appropriate times to flush the write caches. (This is analogous to how it
works on a local file system.) However, it is strongly recommended to use the
`sync` export option on the NFS _server_ on systems where it exists (mainly
Linux). Otherwise, an `fsync` or equivalent on the NFS client is not actually
guaranteed to reach permanent storage on the server, which could cause
corruption similar to running with the parameter [fsync](runtime-config-
wal.html#GUC-FSYNC) off. The defaults of these mount and export options differ
between vendors and versions, so it is recommended to check and perhaps
specify them explicitly in any case to avoid any ambiguity.

In some cases, an external storage product can be accessed either via NFS or a
lower-level protocol such as iSCSI. In the latter case, the storage appears as
a block device and any available file system can be created on it. That
approach might relieve the DBA from having to deal with some of the
idiosyncrasies of NFS, but of course the complexity of managing remote storage
then happens at other levels.

* * *

[Prev](postgres-user.html "19.1. The PostgreSQL User Account")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") |  [Next](server-start.html "19.3. Starting the Database Server")  
---|---|---  
19.1. The PostgreSQL User Account  | [Home](index.html "PostgreSQL 16.9 Documentation") |  19.3. Starting the Database Server  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/creating-cluster.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

