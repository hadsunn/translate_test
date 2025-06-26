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

Supported Versions: [Current](/docs/current/jit.html "PostgreSQL 17 -
Chapter 32. Just-in-Time Compilation \(JIT\)") ([17](/docs/17/jit.html
"PostgreSQL 17 - Chapter 32. Just-in-Time Compilation \(JIT\)")) /
[16](/docs/16/jit.html "PostgreSQL 16 - Chapter 32. Just-in-Time Compilation
\(JIT\)") / [15](/docs/15/jit.html "PostgreSQL 15 - Chapter 32. Just-in-Time
Compilation \(JIT\)") / [14](/docs/14/jit.html "PostgreSQL 14 -
Chapter 32. Just-in-Time Compilation \(JIT\)") / [13](/docs/13/jit.html
"PostgreSQL 13 - Chapter 32. Just-in-Time Compilation \(JIT\)")

Development Versions: [18](/docs/18/jit.html "PostgreSQL 18 -
Chapter 32. Just-in-Time Compilation \(JIT\)") / [devel](/docs/devel/jit.html
"PostgreSQL devel - Chapter 32. Just-in-Time Compilation \(JIT\)")

Unsupported versions: [12](/docs/12/jit.html "PostgreSQL 12 -
Chapter 32. Just-in-Time Compilation \(JIT\)") / [11](/docs/11/jit.html
"PostgreSQL 11 - Chapter 32. Just-in-Time Compilation \(JIT\)")

__

Chapter 32. Just-in-Time Compilation (JIT)  
---  
[Prev](logical-replication-quick-setup.html "31.11. Quick Setup")  | [Up](admin.html "Part III. Server Administration") | Part III. Server Administration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](jit-reason.html "32.1. What Is JIT compilation?")  
  
* * *

## Chapter 32. Just-in-Time Compilation (JIT)

**Table of Contents**

[32.1. What Is JIT compilation?](jit-reason.html)

    

[32.1.1. JIT Accelerated Operations](jit-reason.html#JIT-ACCELERATED-
OPERATIONS)

[32.1.2. Inlining](jit-reason.html#JIT-INLINING)

[32.1.3. Optimization](jit-reason.html#JIT-OPTIMIZATION)

[32.2. When to JIT?](jit-decision.html)

[32.3. Configuration](jit-configuration.html)

[32.4. Extensibility](jit-extensibility.html)

    

[32.4.1. Inlining Support for Extensions](jit-extensibility.html#JIT-
EXTENSIBILITY-BITCODE)

[32.4.2. Pluggable JIT Providers](jit-extensibility.html#JIT-PLUGGABLE)

This chapter explains what just-in-time compilation is, and how it can be
configured in PostgreSQL.

* * *

[Prev](logical-replication-quick-setup.html "31.11. Quick Setup")  | [Up](admin.html "Part III. Server Administration") |  [Next](jit-reason.html "32.1. What Is JIT compilation?")  
---|---|---  
31.11. Quick Setup  | [Home](index.html "PostgreSQL 16.9 Documentation") |  32.1. What Is JIT compilation?  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/jit.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

