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

Supported Versions: [Current](/docs/current/mvcc-serialization-failure-
handling.html "PostgreSQL 17 - 13.5. Serialization Failure Handling")
([17](/docs/17/mvcc-serialization-failure-handling.html "PostgreSQL 17 -
13.5. Serialization Failure Handling")) / [16](/docs/16/mvcc-serialization-
failure-handling.html "PostgreSQL 16 - 13.5. Serialization Failure Handling")
/ [15](/docs/15/mvcc-serialization-failure-handling.html "PostgreSQL 15 -
13.5. Serialization Failure Handling")

Development Versions: [18](/docs/18/mvcc-serialization-failure-handling.html
"PostgreSQL 18 - 13.5. Serialization Failure Handling") /
[devel](/docs/devel/mvcc-serialization-failure-handling.html "PostgreSQL devel
- 13.5. Serialization Failure Handling")

__

13.5. Serialization Failure Handling  
---  
[Prev](applevel-consistency.html "13.4. Data Consistency Checks at the Application Level")  | [Up](mvcc.html "Chapter 13. Concurrency Control") | Chapter 13. Concurrency Control | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](mvcc-caveats.html "13.6. Caveats")  
  
* * *

## 13.5. Serialization Failure Handling #

Both Repeatable Read and Serializable isolation levels can produce errors that
are designed to prevent serialization anomalies. As previously stated,
applications using these levels must be prepared to retry transactions that
fail due to serialization errors. Such an error's message text will vary
according to the precise circumstances, but it will always have the SQLSTATE
code `40001` (`serialization_failure`).

It may also be advisable to retry deadlock failures. These have the SQLSTATE
code `40P01` (`deadlock_detected`).

In some cases it is also appropriate to retry unique-key failures, which have
SQLSTATE code `23505` (`unique_violation`), and exclusion constraint failures,
which have SQLSTATE code `23P01` (`exclusion_violation`). For example, if the
application selects a new value for a primary key column after inspecting the
currently stored keys, it could get a unique-key failure because another
application instance selected the same new key concurrently. This is
effectively a serialization failure, but the server will not detect it as such
because it cannot “see” the connection between the inserted value and the
previous reads. There are also some corner cases in which the server will
issue a unique-key or exclusion constraint error even though in principle it
has enough information to determine that a serialization problem is the
underlying cause. While it's recommendable to just retry
`serialization_failure` errors unconditionally, more care is needed when
retrying these other error codes, since they might represent persistent error
conditions rather than transient failures.

It is important to retry the complete transaction, including all logic that
decides which SQL to issue and/or which values to use. Therefore, PostgreSQL
does not offer an automatic retry facility, since it cannot do so with any
guarantee of correctness.

Transaction retry does not guarantee that the retried transaction will
complete; multiple retries may be needed. In cases with very high contention,
it is possible that completion of a transaction may take many attempts. In
cases involving a conflicting prepared transaction, it may not be possible to
make progress until the prepared transaction commits or rolls back.

* * *

[Prev](applevel-consistency.html "13.4. Data Consistency Checks at the Application Level")  | [Up](mvcc.html "Chapter 13. Concurrency Control") |  [Next](mvcc-caveats.html "13.6. Caveats")  
---|---|---  
13.4. Data Consistency Checks at the Application Level  | [Home](index.html "PostgreSQL 16.9 Documentation") |  13.6. Caveats  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/mvcc-serialization-failure-
handling.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

