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

Supported Versions: [Current](/docs/current/jit-configuration.html "PostgreSQL
17 - 32.3. Configuration") ([17](/docs/17/jit-configuration.html "PostgreSQL
17 - 32.3. Configuration")) / [16](/docs/16/jit-configuration.html "PostgreSQL
16 - 32.3. Configuration") / [15](/docs/15/jit-configuration.html "PostgreSQL
15 - 32.3. Configuration") / [14](/docs/14/jit-configuration.html "PostgreSQL
14 - 32.3. Configuration") / [13](/docs/13/jit-configuration.html "PostgreSQL
13 - 32.3. Configuration")

Development Versions: [18](/docs/18/jit-configuration.html "PostgreSQL 18 -
32.3. Configuration") / [devel](/docs/devel/jit-configuration.html "PostgreSQL
devel - 32.3. Configuration")

Unsupported versions: [12](/docs/12/jit-configuration.html "PostgreSQL 12 -
32.3. Configuration") / [11](/docs/11/jit-configuration.html "PostgreSQL 11 -
32.3. Configuration")

__

32.3. Configuration  
---  
[Prev](jit-decision.html "32.2. When to JIT?")  | [Up](jit.html "Chapter 32. Just-in-Time Compilation \(JIT\)") | Chapter 32. Just-in-Time Compilation (JIT) | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](jit-extensibility.html "32.4. Extensibility")  
  
* * *

## 32.3. Configuration #

The configuration variable [jit](runtime-config-query.html#GUC-JIT) determines
whether JIT compilation is enabled or disabled. If it is enabled, the
configuration variables [jit_above_cost](runtime-config-query.html#GUC-JIT-
ABOVE-COST), [jit_inline_above_cost](runtime-config-query.html#GUC-JIT-INLINE-
ABOVE-COST), and [jit_optimize_above_cost](runtime-config-query.html#GUC-JIT-
OPTIMIZE-ABOVE-COST) determine whether JIT compilation is performed for a
query, and how much effort is spent doing so.

[jit_provider](runtime-config-client.html#GUC-JIT-PROVIDER) determines which
JIT implementation is used. It is rarely required to be changed. See [Section
32.4.2](jit-extensibility.html#JIT-PLUGGABLE "32.4.2. Pluggable JIT
Providers").

For development and debugging purposes a few additional configuration
parameters exist, as described in [Section 20.17](runtime-config-
developer.html "20.17. Developer Options").

* * *

[Prev](jit-decision.html "32.2. When to JIT?")  | [Up](jit.html "Chapter 32. Just-in-Time Compilation \(JIT\)") |  [Next](jit-extensibility.html "32.4. Extensibility")  
---|---|---  
32.2. When to JIT?  | [Home](index.html "PostgreSQL 16.9 Documentation") |  32.4. Extensibility  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/jit-configuration.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

