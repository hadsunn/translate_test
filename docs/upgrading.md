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

Supported Versions: [Current](/docs/current/upgrading.html "PostgreSQL 17 -
19.6. Upgrading a PostgreSQL Cluster") ([17](/docs/17/upgrading.html
"PostgreSQL 17 - 19.6. Upgrading a PostgreSQL Cluster")) /
[16](/docs/16/upgrading.html "PostgreSQL 16 - 19.6. Upgrading a PostgreSQL
Cluster") / [15](/docs/15/upgrading.html "PostgreSQL 15 - 19.6. Upgrading a
PostgreSQL Cluster") / [14](/docs/14/upgrading.html "PostgreSQL 14 -
19.6. Upgrading a PostgreSQL Cluster") / [13](/docs/13/upgrading.html
"PostgreSQL 13 - 19.6. Upgrading a PostgreSQL Cluster")

Development Versions: [18](/docs/18/upgrading.html "PostgreSQL 18 -
19.6. Upgrading a PostgreSQL Cluster") / [devel](/docs/devel/upgrading.html
"PostgreSQL devel - 19.6. Upgrading a PostgreSQL Cluster")

Unsupported versions: [12](/docs/12/upgrading.html "PostgreSQL 12 -
19.6. Upgrading a PostgreSQL Cluster") / [11](/docs/11/upgrading.html
"PostgreSQL 11 - 19.6. Upgrading a PostgreSQL Cluster") /
[10](/docs/10/upgrading.html "PostgreSQL 10 - 19.6. Upgrading a PostgreSQL
Cluster") / [9.6](/docs/9.6/upgrading.html "PostgreSQL 9.6 - 19.6. Upgrading a
PostgreSQL Cluster") / [9.5](/docs/9.5/upgrading.html "PostgreSQL 9.5 -
19.6. Upgrading a PostgreSQL Cluster") / [9.4](/docs/9.4/upgrading.html
"PostgreSQL 9.4 - 19.6. Upgrading a PostgreSQL Cluster") /
[9.3](/docs/9.3/upgrading.html "PostgreSQL 9.3 - 19.6. Upgrading a PostgreSQL
Cluster") / [9.2](/docs/9.2/upgrading.html "PostgreSQL 9.2 - 19.6. Upgrading a
PostgreSQL Cluster") / [9.1](/docs/9.1/upgrading.html "PostgreSQL 9.1 -
19.6. Upgrading a PostgreSQL Cluster")

__

19.6. Upgrading a PostgreSQL Cluster  
---  
[Prev](server-shutdown.html "19.5. Shutting Down the Server")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") | Chapter 19. Server Setup and Operation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](preventing-server-spoofing.html "19.7. Preventing Server Spoofing")  
  
* * *

## 19.6. Upgrading a PostgreSQL Cluster #

[19.6.1. Upgrading Data via pg_dumpall](upgrading.html#UPGRADING-VIA-
PGDUMPALL)

[19.6.2. Upgrading Data via pg_upgrade](upgrading.html#UPGRADING-VIA-PG-
UPGRADE)

[19.6.3. Upgrading Data via Replication](upgrading.html#UPGRADING-VIA-
REPLICATION)

This section discusses how to upgrade your database data from one PostgreSQL
release to a newer one.

Current PostgreSQL version numbers consist of a major and a minor version
number. For example, in the version number 10.1, the 10 is the major version
number and the 1 is the minor version number, meaning this would be the first
minor release of the major release 10. For releases before PostgreSQL version
10.0, version numbers consist of three numbers, for example, 9.5.3. In those
cases, the major version consists of the first two digit groups of the version
number, e.g., 9.5, and the minor version is the third number, e.g., 3, meaning
this would be the third minor release of the major release 9.5.

Minor releases never change the internal storage format and are always
compatible with earlier and later minor releases of the same major version
number. For example, version 10.1 is compatible with version 10.0 and version
10.6. Similarly, for example, 9.5.3 is compatible with 9.5.0, 9.5.1, and
9.5.6. To update between compatible versions, you simply replace the
executables while the server is down and restart the server. The data
directory remains unchanged — minor upgrades are that simple.

For _major_ releases of PostgreSQL, the internal data storage format is
subject to change, thus complicating upgrades. The traditional method for
moving data to a new major version is to dump and restore the database, though
this can be slow. A faster method is [pg_upgrade](pgupgrade.html
"pg_upgrade"). Replication methods are also available, as discussed below. (If
you are using a pre-packaged version of PostgreSQL, it may provide scripts to
assist with major version upgrades. Consult the package-level documentation
for details.)

New major versions also typically introduce some user-visible
incompatibilities, so application programming changes might be required. All
user-visible changes are listed in the release notes ([Appendix
E](release.html "Appendix E. Release Notes")); pay particular attention to the
section labeled "Migration". Though you can upgrade from one major version to
another without upgrading to intervening versions, you should read the major
release notes of all intervening versions.

Cautious users will want to test their client applications on the new version
before switching over fully; therefore, it's often a good idea to set up
concurrent installations of old and new versions. When testing a PostgreSQL
major upgrade, consider the following categories of possible changes:

Administration

    

The capabilities available for administrators to monitor and control the
server often change and improve in each major release.

SQL

    

Typically this includes new SQL command capabilities and not changes in
behavior, unless specifically mentioned in the release notes.

Library API

    

Typically libraries like libpq only add new functionality, again unless
mentioned in the release notes.

System Catalogs

    

System catalog changes usually only affect database management tools.

Server C-language API

    

This involves changes in the backend function API, which is written in the C
programming language. Such changes affect code that references backend
functions deep inside the server.

### 19.6.1. Upgrading Data via pg_dumpall #

One upgrade method is to dump data from one major version of PostgreSQL and
restore it in another — to do this, you must use a _logical_ backup tool like
pg_dumpall; file system level backup methods will not work. (There are checks
in place that prevent you from using a data directory with an incompatible
version of PostgreSQL, so no great harm can be done by trying to start the
wrong server version on a data directory.)

It is recommended that you use the pg_dump and pg_dumpall programs from the
_newer_ version of PostgreSQL, to take advantage of enhancements that might
have been made in these programs. Current releases of the dump programs can
read data from any server version back to 9.2.

These instructions assume that your existing installation is under the
`/usr/local/pgsql` directory, and that the data area is in
`/usr/local/pgsql/data`. Substitute your paths appropriately.

  1. If making a backup, make sure that your database is not being updated. This does not affect the integrity of the backup, but the changed data would of course not be included. If necessary, edit the permissions in the file `/usr/local/pgsql/data/pg_hba.conf` (or equivalent) to disallow access from everyone except you. See [Chapter 21](client-authentication.html "Chapter 21. Client Authentication") for additional information on access control.

To back up your database installation, type:

         
         **pg_dumpall> _outputfile_**
         

To make the backup, you can use the pg_dumpall command from the version you
are currently running; see [Section 26.1.2](backup-dump.html#BACKUP-DUMP-ALL
"26.1.2. Using pg_dumpall") for more details. For best results, however, try
to use the pg_dumpall command from PostgreSQL 16.9, since this version
contains bug fixes and improvements over older versions. While this advice
might seem idiosyncratic since you haven't installed the new version yet, it
is advisable to follow it if you plan to install the new version in parallel
with the old version. In that case you can complete the installation normally
and transfer the data later. This will also decrease the downtime.

  2. Shut down the old server:
         
         **pg_ctl stop**
         

On systems that have PostgreSQL started at boot time, there is probably a
start-up file that will accomplish the same thing. For example, on a Red Hat
Linux system one might find that this works:

         
         **/etc/rc.d/init.d/postgresql stop**
         

See [Chapter 19](runtime.html "Chapter 19. Server Setup and Operation") for
details about starting and stopping the server.

  3. If restoring from backup, rename or delete the old installation directory if it is not version-specific. It is a good idea to rename the directory, rather than delete it, in case you have trouble and need to revert to it. Keep in mind the directory might consume significant disk space. To rename the directory, use a command like this:
         
         **mv /usr/local/pgsql /usr/local/pgsql.old**
         

(Be sure to move the directory as a single unit so relative paths remain
unchanged.)

  4. Install the new version of PostgreSQL as outlined in [Chapter 17](installation.html "Chapter 17. Installation from Source Code").

  5. Create a new database cluster if needed. Remember that you must execute these commands while logged in to the special database user account (which you already have if you are upgrading).
         
         **/usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data**
         

  6. Restore your previous `pg_hba.conf` and any `postgresql.conf` modifications.

  7. Start the database server, again using the special database user account:
         
         **/usr/local/pgsql/bin/postgres -D /usr/local/pgsql/data**
         

  8. Finally, restore your data from backup with:
         
         **/usr/local/pgsql/bin/psql -d postgres -f _outputfile_**
         

using the _new_ psql.

The least downtime can be achieved by installing the new server in a different
directory and running both the old and the new servers in parallel, on
different ports. Then you can use something like:

    
    
    pg_dumpall -p 5432 | psql -d postgres -p 5433
    

to transfer your data.

### 19.6.2. Upgrading Data via pg_upgrade #

The [pg_upgrade](pgupgrade.html "pg_upgrade") module allows an installation to
be migrated in-place from one major PostgreSQL version to another. Upgrades
can be performed in minutes, particularly with `--link` mode. It requires
steps similar to pg_dumpall above, e.g., starting/stopping the server, running
initdb. The pg_upgrade [documentation](pgupgrade.html "pg_upgrade") outlines
the necessary steps.

### 19.6.3. Upgrading Data via Replication #

It is also possible to use logical replication methods to create a standby
server with the updated version of PostgreSQL. This is possible because
logical replication supports replication between different major versions of
PostgreSQL. The standby can be on the same computer or a different computer.
Once it has synced up with the primary server (running the older version of
PostgreSQL), you can switch primaries and make the standby the primary and
shut down the older database instance. Such a switch-over results in only
several seconds of downtime for an upgrade.

This method of upgrading can be performed using the built-in logical
replication facilities as well as using external logical replication systems
such as pglogical, Slony, Londiste, and Bucardo.

* * *

[Prev](server-shutdown.html "19.5. Shutting Down the Server")  | [Up](runtime.html "Chapter 19. Server Setup and Operation") |  [Next](preventing-server-spoofing.html "19.7. Preventing Server Spoofing")  
---|---|---  
19.5. Shutting Down the Server  | [Home](index.html "PostgreSQL 16.9 Documentation") |  19.7. Preventing Server Spoofing  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/upgrading.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

