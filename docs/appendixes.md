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

Supported Versions: [Current](/docs/current/appendixes.html "PostgreSQL 17 -
Part VIII. Appendixes") ([17](/docs/17/appendixes.html "PostgreSQL 17 -
Part VIII. Appendixes")) / [16](/docs/16/appendixes.html "PostgreSQL 16 -
Part VIII. Appendixes") / [15](/docs/15/appendixes.html "PostgreSQL 15 -
Part VIII. Appendixes") / [14](/docs/14/appendixes.html "PostgreSQL 14 -
Part VIII. Appendixes") / [13](/docs/13/appendixes.html "PostgreSQL 13 -
Part VIII. Appendixes")

Development Versions: [18](/docs/18/appendixes.html "PostgreSQL 18 -
Part VIII. Appendixes") / [devel](/docs/devel/appendixes.html "PostgreSQL
devel - Part VIII. Appendixes")

Unsupported versions: [12](/docs/12/appendixes.html "PostgreSQL 12 -
Part VIII. Appendixes") / [11](/docs/11/appendixes.html "PostgreSQL 11 -
Part VIII. Appendixes") / [10](/docs/10/appendixes.html "PostgreSQL 10 -
Part VIII. Appendixes") / [9.6](/docs/9.6/appendixes.html "PostgreSQL 9.6 -
Part VIII. Appendixes") / [9.5](/docs/9.5/appendixes.html "PostgreSQL 9.5 -
Part VIII. Appendixes") / [9.4](/docs/9.4/appendixes.html "PostgreSQL 9.4 -
Part VIII. Appendixes") / [9.3](/docs/9.3/appendixes.html "PostgreSQL 9.3 -
Part VIII. Appendixes") / [9.2](/docs/9.2/appendixes.html "PostgreSQL 9.2 -
Part VIII. Appendixes") / [9.1](/docs/9.1/appendixes.html "PostgreSQL 9.1 -
Part VIII. Appendixes") / [9.0](/docs/9.0/appendixes.html "PostgreSQL 9.0 -
Part VIII. Appendixes") / [8.4](/docs/8.4/appendixes.html "PostgreSQL 8.4 -
Part VIII. Appendixes") / [8.3](/docs/8.3/appendixes.html "PostgreSQL 8.3 -
Part VIII. Appendixes") / [8.2](/docs/8.2/appendixes.html "PostgreSQL 8.2 -
Part VIII. Appendixes") / [8.1](/docs/8.1/appendixes.html "PostgreSQL 8.1 -
Part VIII. Appendixes") / [8.0](/docs/8.0/appendixes.html "PostgreSQL 8.0 -
Part VIII. Appendixes") / [7.4](/docs/7.4/appendixes.html "PostgreSQL 7.4 -
Part VIII. Appendixes")

__

Part VIII. Appendixes  
---  
[Prev](backup-manifest-wal-ranges.html "77.3. Backup Manifest WAL Range Object")  | [Up](index.html "PostgreSQL 16.9 Documentation") | PostgreSQL 16.9 Documentation | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](errcodes-appendix.html "Appendix A. PostgreSQL Error Codes")  
  
* * *

# Part VIII. Appendixes

**Table of Contents**

[A. PostgreSQL Error Codes](errcodes-appendix.html)

[B. Date/Time Support](datetime-appendix.html)

    

[B.1. Date/Time Input Interpretation](datetime-input-rules.html)

[B.2. Handling of Invalid or Ambiguous Timestamps](datetime-invalid-
input.html)

[B.3. Date/Time Key Words](datetime-keywords.html)

[B.4. Date/Time Configuration Files](datetime-config-files.html)

[B.5. POSIX Time Zone Specifications](datetime-posix-timezone-specs.html)

[B.6. History of Units](datetime-units-history.html)

[B.7. Julian Dates](datetime-julian-dates.html)

[C. SQL Key Words](sql-keywords-appendix.html)

[D. SQL Conformance](features.html)

    

[D.1. Supported Features](features-sql-standard.html)

[D.2. Unsupported Features](unsupported-features-sql-standard.html)

[D.3. XML Limits and Conformance to SQL/XML](xml-limits-conformance.html)

[E. Release Notes](release.html)

    

[E.1. Release 16.9](release-16-9.html)

[E.2. Release 16.8](release-16-8.html)

[E.3. Release 16.7](release-16-7.html)

[E.4. Release 16.6](release-16-6.html)

[E.5. Release 16.5](release-16-5.html)

[E.6. Release 16.4](release-16-4.html)

[E.7. Release 16.3](release-16-3.html)

[E.8. Release 16.2](release-16-2.html)

[E.9. Release 16.1](release-16-1.html)

[E.10. Release 16](release-16.html)

[E.11. Prior Releases](release-prior.html)

[F. Additional Supplied Modules and Extensions](contrib.html)

    

[F.1. adminpack — pgAdmin support toolpack](adminpack.html)

[F.2. amcheck — tools to verify table and index consistency](amcheck.html)

[F.3. auth_delay — pause on authentication failure](auth-delay.html)

[F.4. auto_explain — log execution plans of slow queries](auto-explain.html)

[F.5. basebackup_to_shell — example "shell" pg_basebackup module](basebackup-
to-shell.html)

[F.6. basic_archive — an example WAL archive module](basic-archive.html)

[F.7. bloom — bloom filter index access method](bloom.html)

[F.8. btree_gin — GIN operator classes with B-tree behavior](btree-gin.html)

[F.9. btree_gist — GiST operator classes with B-tree behavior](btree-
gist.html)

[F.10. citext — a case-insensitive character string type](citext.html)

[F.11. cube — a multi-dimensional cube data type](cube.html)

[F.12. dblink — connect to other PostgreSQL databases](dblink.html)

[F.13. dict_int — example full-text search dictionary for integers](dict-
int.html)

[F.14. dict_xsyn — example synonym full-text search dictionary](dict-
xsyn.html)

[F.15. earthdistance — calculate great-circle distances](earthdistance.html)

[F.16. file_fdw — access data files in the server's file system](file-
fdw.html)

[F.17. fuzzystrmatch — determine string similarities and
distance](fuzzystrmatch.html)

[F.18. hstore — hstore key/value datatype](hstore.html)

[F.19. intagg — integer aggregator and enumerator](intagg.html)

[F.20. intarray — manipulate arrays of integers](intarray.html)

[F.21. isn — data types for international standard numbers (ISBN, EAN, UPC,
etc.)](isn.html)

[F.22. lo — manage large objects](lo.html)

[F.23. ltree — hierarchical tree-like data type](ltree.html)

[F.24. old_snapshot — inspect `old_snapshot_threshold`
state](oldsnapshot.html)

[F.25. pageinspect — low-level inspection of database pages](pageinspect.html)

[F.26. passwordcheck — verify password strength](passwordcheck.html)

[F.27. pg_buffercache — inspect PostgreSQL buffer cache
state](pgbuffercache.html)

[F.28. pgcrypto — cryptographic functions](pgcrypto.html)

[F.29. pg_freespacemap — examine the free space map](pgfreespacemap.html)

[F.30. pg_prewarm — preload relation data into buffer caches](pgprewarm.html)

[F.31. pgrowlocks — show a table's row locking information](pgrowlocks.html)

[F.32. pg_stat_statements — track statistics of SQL planning and
execution](pgstatstatements.html)

[F.33. pgstattuple — obtain tuple-level statistics](pgstattuple.html)

[F.34. pg_surgery — perform low-level surgery on relation
data](pgsurgery.html)

[F.35. pg_trgm — support for similarity of text using trigram
matching](pgtrgm.html)

[F.36. pg_visibility — visibility map information and
utilities](pgvisibility.html)

[F.37. pg_walinspect — low-level WAL inspection](pgwalinspect.html)

[F.38. postgres_fdw — access data stored in external PostgreSQL
servers](postgres-fdw.html)

[F.39. seg — a datatype for line segments or floating point
intervals](seg.html)

[F.40. sepgsql — SELinux-, label-based mandatory access control (MAC) security
module](sepgsql.html)

[F.41. spi — Server Programming Interface features/examples](contrib-spi.html)

[F.42. sslinfo — obtain client SSL information](sslinfo.html)

[F.43. tablefunc — functions that return tables (`crosstab` and
others)](tablefunc.html)

[F.44. tcn — a trigger function to notify listeners of changes to table
content](tcn.html)

[F.45. test_decoding — SQL-based test/example module for WAL logical
decoding](test-decoding.html)

[F.46. tsm_system_rows — the `SYSTEM_ROWS` sampling method for
`TABLESAMPLE`](tsm-system-rows.html)

[F.47. tsm_system_time — the `SYSTEM_TIME` sampling method for
`TABLESAMPLE`](tsm-system-time.html)

[F.48. unaccent — a text search dictionary which removes
diacritics](unaccent.html)

[F.49. uuid-ossp — a UUID generator](uuid-ossp.html)

[F.50. xml2 — XPath querying and XSLT functionality](xml2.html)

[G. Additional Supplied Programs](contrib-prog.html)

    

[G.1. Client Applications](contrib-prog-client.html)

[G.2. Server Applications](contrib-prog-server.html)

[H. External Projects](external-projects.html)

    

[H.1. Client Interfaces](external-interfaces.html)

[H.2. Administration Tools](external-admin-tools.html)

[H.3. Procedural Languages](external-pl.html)

[H.4. Extensions](external-extensions.html)

[I. The Source Code Repository](sourcerepo.html)

    

[I.1. Getting the Source via Git](git.html)

[J. Documentation](docguide.html)

    

[J.1. DocBook](docguide-docbook.html)

[J.2. Tool Sets](docguide-toolsets.html)

[J.3. Building the Documentation with Make](docguide-build.html)

[J.4. Building the Documentation with Meson](docguide-build-meson.html)

[J.5. Documentation Authoring](docguide-authoring.html)

[J.6. Style Guide](docguide-style.html)

[K. PostgreSQL Limits](limits.html)

[L. Acronyms](acronyms.html)

[M. Glossary](glossary.html)

[N. Color Support](color.html)

    

[N.1. When Color is Used](color-when.html)

[N.2. Configuring the Colors](color-which.html)

[O. Obsolete or Renamed Features](appendix-obsolete.html)

    

[O.1. `recovery.conf` file merged into `postgresql.conf`](recovery-
config.html)

[O.2. Default Roles Renamed to Predefined Roles](default-roles.html)

[O.3. `pg_xlogdump` renamed to `pg_waldump`](pgxlogdump.html)

[O.4. `pg_resetxlog` renamed to `pg_resetwal`](app-pgresetxlog.html)

[O.5. `pg_receivexlog` renamed to `pg_receivewal`](app-pgreceivexlog.html)

* * *

[Prev](backup-manifest-wal-ranges.html "77.3. Backup Manifest WAL Range Object")  | [Up](index.html "PostgreSQL 16.9 Documentation") |  [Next](errcodes-appendix.html "Appendix A. PostgreSQL Error Codes")  
---|---|---  
77.3. Backup Manifest WAL Range Object  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Appendix A. PostgreSQL Error Codes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/appendixes.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

