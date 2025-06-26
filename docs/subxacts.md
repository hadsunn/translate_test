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

Supported Versions: [Current](/docs/current/subxacts.html "PostgreSQL 17 -
74.3. Subtransactions") ([17](/docs/17/subxacts.html "PostgreSQL 17 -
74.3. Subtransactions")) / [16](/docs/16/subxacts.html "PostgreSQL 16 -
74.3. Subtransactions")

Development Versions: [18](/docs/18/subxacts.html "PostgreSQL 18 -
74.3. Subtransactions") / [devel](/docs/devel/subxacts.html "PostgreSQL devel
- 74.3. Subtransactions")

__

74.3. Subtransactions  
---  
[Prev](xact-locking.html "74.2. Transactions and Locking")  | [Up](transactions.html "Chapter 74. Transaction Processing") | Chapter 74. Transaction Processing | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](two-phase.html "74.4. Two-Phase Transactions")  
  
* * *

## 74.3. Subtransactions #

Subtransactions are started inside transactions, allowing large transactions
to be broken into smaller units. Subtransactions can commit or abort without
affecting their parent transactions, allowing parent transactions to continue.
This allows errors to be handled more easily, which is a common application
development pattern. The word subtransaction is often abbreviated as
_subxact_.

Subtransactions can be started explicitly using the `SAVEPOINT` command, but
can also be started in other ways, such as PL/pgSQL's `EXCEPTION` clause.
PL/Python and PL/Tcl also support explicit subtransactions. Subtransactions
can also be started from other subtransactions. The top-level transaction and
its child subtransactions form a hierarchy or tree, which is why we refer to
the main transaction as the top-level transaction.

If a subtransaction is assigned a non-virtual transaction ID, its transaction
ID is referred to as a “subxid”. Read-only subtransactions are not assigned
subxids, but once they attempt to write, they will be assigned one. This also
causes all of a subxid's parents, up to and including the top-level
transaction, to be assigned non-virtual transaction ids. We ensure that a
parent xid is always lower than any of its child subxids.

The immediate parent xid of each subxid is recorded in the `pg_subtrans`
directory. No entry is made for top-level xids since they do not have a
parent, nor is an entry made for read-only subtransactions.

When a subtransaction commits, all of its committed child subtransactions with
subxids will also be considered subcommitted in that transaction. When a
subtransaction aborts, all of its child subtransactions will also be
considered aborted.

When a top-level transaction with an xid commits, all of its subcommitted
child subtransactions are also persistently recorded as committed in the
`pg_xact` subdirectory. If the top-level transaction aborts, all its
subtransactions are also aborted, even if they were subcommitted.

The more subtransactions each transaction keeps open (not rolled back or
released), the greater the transaction management overhead. Up to 64 open
subxids are cached in shared memory for each backend; after that point, the
storage I/O overhead increases significantly due to additional lookups of
subxid entries in `pg_subtrans`.

* * *

[Prev](xact-locking.html "74.2. Transactions and Locking")  | [Up](transactions.html "Chapter 74. Transaction Processing") |  [Next](two-phase.html "74.4. Two-Phase Transactions")  
---|---|---  
74.2. Transactions and Locking  | [Home](index.html "PostgreSQL 16.9 Documentation") |  74.4. Two-Phase Transactions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/subxacts.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

