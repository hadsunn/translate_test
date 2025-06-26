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

Supported Versions: [Current](/docs/current/views.html "PostgreSQL 17 -
Chapter 54. System Views") ([17](/docs/17/views.html "PostgreSQL 17 -
Chapter 54. System Views")) / [16](/docs/16/views.html "PostgreSQL 16 -
Chapter 54. System Views") / [15](/docs/15/views.html "PostgreSQL 15 -
Chapter 54. System Views")

Development Versions: [18](/docs/18/views.html "PostgreSQL 18 -
Chapter 54. System Views") / [devel](/docs/devel/views.html "PostgreSQL devel
- Chapter 54. System Views")

__

Chapter 54. System Views  
---  
[Prev](catalog-pg-user-mapping.html "53.65. pg_user_mapping")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](views-overview.html "54.1. Overview")  
  
* * *

## Chapter 54. System Views

**Table of Contents**

[54.1. Overview](views-overview.html)

[54.2. `pg_available_extensions`](view-pg-available-extensions.html)

[54.3. `pg_available_extension_versions`](view-pg-available-extension-
versions.html)

[54.4. `pg_backend_memory_contexts`](view-pg-backend-memory-contexts.html)

[54.5. `pg_config`](view-pg-config.html)

[54.6. `pg_cursors`](view-pg-cursors.html)

[54.7. `pg_file_settings`](view-pg-file-settings.html)

[54.8. `pg_group`](view-pg-group.html)

[54.9. `pg_hba_file_rules`](view-pg-hba-file-rules.html)

[54.10. `pg_ident_file_mappings`](view-pg-ident-file-mappings.html)

[54.11. `pg_indexes`](view-pg-indexes.html)

[54.12. `pg_locks`](view-pg-locks.html)

[54.13. `pg_matviews`](view-pg-matviews.html)

[54.14. `pg_policies`](view-pg-policies.html)

[54.15. `pg_prepared_statements`](view-pg-prepared-statements.html)

[54.16. `pg_prepared_xacts`](view-pg-prepared-xacts.html)

[54.17. `pg_publication_tables`](view-pg-publication-tables.html)

[54.18. `pg_replication_origin_status`](view-pg-replication-origin-
status.html)

[54.19. `pg_replication_slots`](view-pg-replication-slots.html)

[54.20. `pg_roles`](view-pg-roles.html)

[54.21. `pg_rules`](view-pg-rules.html)

[54.22. `pg_seclabels`](view-pg-seclabels.html)

[54.23. `pg_sequences`](view-pg-sequences.html)

[54.24. `pg_settings`](view-pg-settings.html)

[54.25. `pg_shadow`](view-pg-shadow.html)

[54.26. `pg_shmem_allocations`](view-pg-shmem-allocations.html)

[54.27. `pg_stats`](view-pg-stats.html)

[54.28. `pg_stats_ext`](view-pg-stats-ext.html)

[54.29. `pg_stats_ext_exprs`](view-pg-stats-ext-exprs.html)

[54.30. `pg_tables`](view-pg-tables.html)

[54.31. `pg_timezone_abbrevs`](view-pg-timezone-abbrevs.html)

[54.32. `pg_timezone_names`](view-pg-timezone-names.html)

[54.33. `pg_user`](view-pg-user.html)

[54.34. `pg_user_mappings`](view-pg-user-mappings.html)

[54.35. `pg_views`](view-pg-views.html)

In addition to the system catalogs, PostgreSQL provides a number of built-in
views. Some system views provide convenient access to some commonly used
queries on the system catalogs. Other views provide access to internal server
state.

The information schema ([Chapter 37](information-schema.html "Chapter 37. The
Information Schema")) provides an alternative set of views which overlap the
functionality of the system views. Since the information schema is SQL-
standard whereas the views described here are PostgreSQL-specific, it's
usually better to use the information schema if it provides all the
information you need.

[Table 54.1](views-overview.html#VIEW-TABLE "Table 54.1. System Views") lists
the system views described here. More detailed documentation of each view
follows below. There are some additional views that provide access to
accumulated statistics; they are described in [Table 28.2](monitoring-
stats.html#MONITORING-STATS-VIEWS-TABLE "Table 28.2. Collected Statistics
Views").

* * *

[Prev](catalog-pg-user-mapping.html "53.65. pg_user_mapping")  | [Up](internals.html "Part VII. Internals") |  [Next](views-overview.html "54.1. Overview")  
---|---|---  
53.65. `pg_user_mapping`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  54.1. Overview  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/views.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

