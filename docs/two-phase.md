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

Supported Versions: [Current](/docs/current/two-phase.html "PostgreSQL 17 -
74.4. Two-Phase Transactions") ([17](/docs/17/two-phase.html "PostgreSQL 17 -
74.4. Two-Phase Transactions")) / [16](/docs/16/two-phase.html "PostgreSQL 16
- 74.4. Two-Phase Transactions")

Development Versions: [18](/docs/18/two-phase.html "PostgreSQL 18 - 74.4. Two-
Phase Transactions") / [devel](/docs/devel/two-phase.html "PostgreSQL devel -
74.4. Two-Phase Transactions")

__

74.4. Two-Phase Transactions  
---  
[Prev](subxacts.html "74.3. Subtransactions")  | [Up](transactions.html "Chapter 74. Transaction Processing") | Chapter 74. Transaction Processing | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](bki.html "Chapter 75. System Catalog Declarations and Initial Contents")  
  
* * *

## 74.4. Two-Phase Transactions #

PostgreSQL supports a two-phase commit (2PC) protocol that allows multiple
distributed systems to work together in a transactional manner. The commands
are `PREPARE TRANSACTION`, `COMMIT PREPARED` and `ROLLBACK PREPARED`. Two-
phase transactions are intended for use by external transaction management
systems. PostgreSQL follows the features and model proposed by the X/Open XA
standard, but does not implement some less often used aspects.

When the user executes `PREPARE TRANSACTION`, the only possible next commands
are `COMMIT PREPARED` or `ROLLBACK PREPARED`. In general, this prepared state
is intended to be of very short duration, but external availability issues
might mean transactions stay in this state for an extended interval. Short-
lived prepared transactions are stored only in shared memory and WAL.
Transactions that span checkpoints are recorded in the `pg_twophase`
directory. Transactions that are currently prepared can be inspected using
[`pg_prepared_xacts`](view-pg-prepared-xacts.html "54.16. pg_prepared_xacts").

* * *

[Prev](subxacts.html "74.3. Subtransactions")  | [Up](transactions.html "Chapter 74. Transaction Processing") |  [Next](bki.html "Chapter 75. System Catalog Declarations and Initial Contents")  
---|---|---  
74.3. Subtransactions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 75. System Catalog Declarations and Initial Contents  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/two-phase.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

