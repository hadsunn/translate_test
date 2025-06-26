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

Supported Versions: [Current](/docs/current/admin.html "PostgreSQL 17 -
Part III. Server Administration") ([17](/docs/17/admin.html "PostgreSQL 17 -
Part III. Server Administration")) / [16](/docs/16/admin.html "PostgreSQL 16 -
Part III. Server Administration") / [15](/docs/15/admin.html "PostgreSQL 15 -
Part III. Server Administration") / [14](/docs/14/admin.html "PostgreSQL 14 -
Part III. Server Administration") / [13](/docs/13/admin.html "PostgreSQL 13 -
Part III. Server Administration")

Development Versions: [18](/docs/18/admin.html "PostgreSQL 18 -
Part III. Server Administration") / [devel](/docs/devel/admin.html "PostgreSQL
devel - Part III. Server Administration")

Unsupported versions: [12](/docs/12/admin.html "PostgreSQL 12 -
Part III. Server Administration") / [11](/docs/11/admin.html "PostgreSQL 11 -
Part III. Server Administration") / [10](/docs/10/admin.html "PostgreSQL 10 -
Part III. Server Administration") / [9.6](/docs/9.6/admin.html "PostgreSQL 9.6
- Part III. Server Administration") / [9.5](/docs/9.5/admin.html "PostgreSQL
9.5 - Part III. Server Administration") / [9.4](/docs/9.4/admin.html
"PostgreSQL 9.4 - Part III. Server Administration") /
[9.3](/docs/9.3/admin.html "PostgreSQL 9.3 - Part III. Server Administration")
/ [9.2](/docs/9.2/admin.html "PostgreSQL 9.2 - Part III. Server
Administration") / [9.1](/docs/9.1/admin.html "PostgreSQL 9.1 -
Part III. Server Administration") / [9.0](/docs/9.0/admin.html "PostgreSQL 9.0
- Part III. Server Administration") / [8.4](/docs/8.4/admin.html "PostgreSQL
8.4 - Part III. Server Administration") / [8.3](/docs/8.3/admin.html
"PostgreSQL 8.3 - Part III. Server Administration") /
[8.2](/docs/8.2/admin.html "PostgreSQL 8.2 - Part III. Server Administration")
/ [8.1](/docs/8.1/admin.html "PostgreSQL 8.1 - Part III. Server
Administration") / [8.0](/docs/8.0/admin.html "PostgreSQL 8.0 -
Part III. Server Administration") / [7.4](/docs/7.4/admin.html "PostgreSQL 7.4
- Part III. Server Administration") / [7.3](/docs/7.3/admin.html "PostgreSQL
7.3 - Part III. Server Administration") / [7.2](/docs/7.2/admin.html
"PostgreSQL 7.2 - Part III. Server Administration") /
[7.1](/docs/7.1/admin.html "PostgreSQL 7.1 - Part III. Server Administration")

__

Part III. Server Administration  
---  
[Prev](parallel-safety.html "15.4. Parallel Safety")  | [Up](index.html "PostgreSQL 16.9 Documentation") | PostgreSQL 16.9 Documentation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](install-binaries.html "Chapter 16. Installation from Binaries")  
  
* * *

# Part III. Server Administration

This part covers topics that are of interest to a PostgreSQL database
administrator. This includes installation of the software, set up and
configuration of the server, management of users and databases, and
maintenance tasks. Anyone who runs a PostgreSQL server, even for personal use,
but especially in production, should be familiar with the topics covered in
this part.

The information in this part is arranged approximately in the order in which a
new user should read it. But the chapters are self-contained and can be read
individually as desired. The information in this part is presented in a
narrative fashion in topical units. Readers looking for a complete description
of a particular command should see [Part VI](reference.html
"Part VI. Reference").

The first few chapters are written so they can be understood without
prerequisite knowledge, so new users who need to set up their own server can
begin their exploration with this part. The rest of this part is about tuning
and management; that material assumes that the reader is familiar with the
general use of the PostgreSQL database system. Readers are encouraged to look
at [Part I](tutorial.html "Part I. Tutorial") and [Part II](sql.html
"Part II. The SQL Language") for additional information.

**Table of Contents**

[16\. Installation from Binaries](install-binaries.html)

[17\. Installation from Source Code](installation.html)

    

[17.1. Requirements](install-requirements.html)

[17.2. Getting the Source](install-getsource.html)

[17.3. Building and Installation with Autoconf and Make](install-make.html)

[17.4. Building and Installation with Meson](install-meson.html)

[17.5. Post-Installation Setup](install-post.html)

[17.6. Supported Platforms](supported-platforms.html)

[17.7. Platform-Specific Notes](installation-platform-notes.html)

[18\. Installation from Source Code on Windows](install-windows.html)

    

[18.1. Building with Visual C++ or the Microsoft Windows SDK](install-windows-
full.html)

[19\. Server Setup and Operation](runtime.html)

    

[19.1. The PostgreSQL User Account](postgres-user.html)

[19.2. Creating a Database Cluster](creating-cluster.html)

[19.3. Starting the Database Server](server-start.html)

[19.4. Managing Kernel Resources](kernel-resources.html)

[19.5. Shutting Down the Server](server-shutdown.html)

[19.6. Upgrading a PostgreSQL Cluster](upgrading.html)

[19.7. Preventing Server Spoofing](preventing-server-spoofing.html)

[19.8. Encryption Options](encryption-options.html)

[19.9. Secure TCP/IP Connections with SSL](ssl-tcp.html)

[19.10. Secure TCP/IP Connections with GSSAPI Encryption](gssapi-enc.html)

[19.11. Secure TCP/IP Connections with SSH Tunnels](ssh-tunnels.html)

[19.12. Registering Event Log on Windows](event-log-registration.html)

[20\. Server Configuration](runtime-config.html)

    

[20.1. Setting Parameters](config-setting.html)

[20.2. File Locations](runtime-config-file-locations.html)

[20.3. Connections and Authentication](runtime-config-connection.html)

[20.4. Resource Consumption](runtime-config-resource.html)

[20.5. Write Ahead Log](runtime-config-wal.html)

[20.6. Replication](runtime-config-replication.html)

[20.7. Query Planning](runtime-config-query.html)

[20.8. Error Reporting and Logging](runtime-config-logging.html)

[20.9. Run-time Statistics](runtime-config-statistics.html)

[20.10. Automatic Vacuuming](runtime-config-autovacuum.html)

[20.11. Client Connection Defaults](runtime-config-client.html)

[20.12. Lock Management](runtime-config-locks.html)

[20.13. Version and Platform Compatibility](runtime-config-compatible.html)

[20.14. Error Handling](runtime-config-error-handling.html)

[20.15. Preset Options](runtime-config-preset.html)

[20.16. Customized Options](runtime-config-custom.html)

[20.17. Developer Options](runtime-config-developer.html)

[20.18. Short Options](runtime-config-short.html)

[21\. Client Authentication](client-authentication.html)

    

[21.1. The `pg_hba.conf` File](auth-pg-hba-conf.html)

[21.2. User Name Maps](auth-username-maps.html)

[21.3. Authentication Methods](auth-methods.html)

[21.4. Trust Authentication](auth-trust.html)

[21.5. Password Authentication](auth-password.html)

[21.6. GSSAPI Authentication](gssapi-auth.html)

[21.7. SSPI Authentication](sspi-auth.html)

[21.8. Ident Authentication](auth-ident.html)

[21.9. Peer Authentication](auth-peer.html)

[21.10. LDAP Authentication](auth-ldap.html)

[21.11. RADIUS Authentication](auth-radius.html)

[21.12. Certificate Authentication](auth-cert.html)

[21.13. PAM Authentication](auth-pam.html)

[21.14. BSD Authentication](auth-bsd.html)

[21.15. Authentication Problems](client-authentication-problems.html)

[22\. Database Roles](user-manag.html)

    

[22.1. Database Roles](database-roles.html)

[22.2. Role Attributes](role-attributes.html)

[22.3. Role Membership](role-membership.html)

[22.4. Dropping Roles](role-removal.html)

[22.5. Predefined Roles](predefined-roles.html)

[22.6. Function Security](perm-functions.html)

[23\. Managing Databases](managing-databases.html)

    

[23.1. Overview](manage-ag-overview.html)

[23.2. Creating a Database](manage-ag-createdb.html)

[23.3. Template Databases](manage-ag-templatedbs.html)

[23.4. Database Configuration](manage-ag-config.html)

[23.5. Destroying a Database](manage-ag-dropdb.html)

[23.6. Tablespaces](manage-ag-tablespaces.html)

[24\. Localization](charset.html)

    

[24.1. Locale Support](locale.html)

[24.2. Collation Support](collation.html)

[24.3. Character Set Support](multibyte.html)

[25\. Routine Database Maintenance Tasks](maintenance.html)

    

[25.1. Routine Vacuuming](routine-vacuuming.html)

[25.2. Routine Reindexing](routine-reindex.html)

[25.3. Log File Maintenance](logfile-maintenance.html)

[26\. Backup and Restore](backup.html)

    

[26.1. SQL Dump](backup-dump.html)

[26.2. File System Level Backup](backup-file.html)

[26.3. Continuous Archiving and Point-in-Time Recovery (PITR)](continuous-
archiving.html)

[27\. High Availability, Load Balancing, and Replication](high-
availability.html)

    

[27.1. Comparison of Different Solutions](different-replication-
solutions.html)

[27.2. Log-Shipping Standby Servers](warm-standby.html)

[27.3. Failover](warm-standby-failover.html)

[27.4. Hot Standby](hot-standby.html)

[28\. Monitoring Database Activity](monitoring.html)

    

[28.1. Standard Unix Tools](monitoring-ps.html)

[28.2. The Cumulative Statistics System](monitoring-stats.html)

[28.3. Viewing Locks](monitoring-locks.html)

[28.4. Progress Reporting](progress-reporting.html)

[28.5. Dynamic Tracing](dynamic-trace.html)

[29\. Monitoring Disk Usage](diskusage.html)

    

[29.1. Determining Disk Usage](disk-usage.html)

[29.2. Disk Full Failure](disk-full.html)

[30\. Reliability and the Write-Ahead Log](wal.html)

    

[30.1. Reliability](wal-reliability.html)

[30.2. Data Checksums](checksums.html)

[30.3. Write-Ahead Logging (WAL)](wal-intro.html)

[30.4. Asynchronous Commit](wal-async-commit.html)

[30.5. WAL Configuration](wal-configuration.html)

[30.6. WAL Internals](wal-internals.html)

[31\. Logical Replication](logical-replication.html)

    

[31.1. Publication](logical-replication-publication.html)

[31.2. Subscription](logical-replication-subscription.html)

[31.3. Row Filters](logical-replication-row-filter.html)

[31.4. Column Lists](logical-replication-col-lists.html)

[31.5. Conflicts](logical-replication-conflicts.html)

[31.6. Restrictions](logical-replication-restrictions.html)

[31.7. Architecture](logical-replication-architecture.html)

[31.8. Monitoring](logical-replication-monitoring.html)

[31.9. Security](logical-replication-security.html)

[31.10. Configuration Settings](logical-replication-config.html)

[31.11. Quick Setup](logical-replication-quick-setup.html)

[32\. Just-in-Time Compilation (JIT)](jit.html)

    

[32.1. What Is JIT compilation?](jit-reason.html)

[32.2. When to JIT?](jit-decision.html)

[32.3. Configuration](jit-configuration.html)

[32.4. Extensibility](jit-extensibility.html)

[33\. Regression Tests](regress.html)

    

[33.1. Running the Tests](regress-run.html)

[33.2. Test Evaluation](regress-evaluation.html)

[33.3. Variant Comparison Files](regress-variant.html)

[33.4. TAP Tests](regress-tap.html)

[33.5. Test Coverage Examination](regress-coverage.html)

* * *

[Prev](parallel-safety.html "15.4. Parallel Safety")  | [Up](index.html "PostgreSQL 16.9 Documentation") |  [Next](install-binaries.html "Chapter 16. Installation from Binaries")  
---|---|---  
15.4. Parallel Safety  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 16. Installation from Binaries  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/admin.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

