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

Supported Versions: [Current](/docs/current/transactions.html "PostgreSQL 17 -
Chapter 74. Transaction Processing") ([17](/docs/17/transactions.html
"PostgreSQL 17 - Chapter 74. Transaction Processing")) /
[16](/docs/16/transactions.html "PostgreSQL 16 - Chapter 74. Transaction
Processing")

Development Versions: [18](/docs/18/transactions.html "PostgreSQL 18 -
Chapter 74. Transaction Processing") / [devel](/docs/devel/transactions.html
"PostgreSQL devel - Chapter 74. Transaction Processing")

__

Chapter 74. Transaction Processing  
---  
[Prev](storage-hot.html "73.7. Heap-Only Tuples \(HOT\)")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](transaction-id.html "74.1. Transactions and Identifiers")  
  
* * *

## Chapter 74. Transaction Processing

**Table of Contents**

[74.1. Transactions and Identifiers](transaction-id.html)

[74.2. Transactions and Locking](xact-locking.html)

[74.3. Subtransactions](subxacts.html)

[74.4. Two-Phase Transactions](two-phase.html)

This chapter provides an overview of the internals of PostgreSQL's transaction
management system. The word transaction is often abbreviated as _xact_.

* * *

[Prev](storage-hot.html "73.7. Heap-Only Tuples \(HOT\)")  | [Up](internals.html "Part VII. Internals") |  [Next](transaction-id.html "74.1. Transactions and Identifiers")  
---|---|---  
73.7. Heap-Only Tuples (HOT)  | [Home](index.html "PostgreSQL 16.9 Documentation") |  74.1. Transactions and Identifiers  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/transactions.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

