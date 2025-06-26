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

Supported Versions: [Current](/docs/current/rule-system.html "PostgreSQL 17 -
52.4. The PostgreSQL Rule System") ([17](/docs/17/rule-system.html "PostgreSQL
17 - 52.4. The PostgreSQL Rule System")) / [16](/docs/16/rule-system.html
"PostgreSQL 16 - 52.4. The PostgreSQL Rule System") / [15](/docs/15/rule-
system.html "PostgreSQL 15 - 52.4. The PostgreSQL Rule System") /
[14](/docs/14/rule-system.html "PostgreSQL 14 - 52.4. The PostgreSQL Rule
System") / [13](/docs/13/rule-system.html "PostgreSQL 13 - 52.4. The
PostgreSQL Rule System")

Development Versions: [18](/docs/18/rule-system.html "PostgreSQL 18 -
52.4. The PostgreSQL Rule System") / [devel](/docs/devel/rule-system.html
"PostgreSQL devel - 52.4. The PostgreSQL Rule System")

Unsupported versions: [12](/docs/12/rule-system.html "PostgreSQL 12 -
52.4. The PostgreSQL Rule System") / [11](/docs/11/rule-system.html
"PostgreSQL 11 - 52.4. The PostgreSQL Rule System") / [10](/docs/10/rule-
system.html "PostgreSQL 10 - 52.4. The PostgreSQL Rule System") /
[9.6](/docs/9.6/rule-system.html "PostgreSQL 9.6 - 52.4. The PostgreSQL Rule
System") / [9.5](/docs/9.5/rule-system.html "PostgreSQL 9.5 - 52.4. The
PostgreSQL Rule System") / [9.4](/docs/9.4/rule-system.html "PostgreSQL 9.4 -
52.4. The PostgreSQL Rule System") / [9.3](/docs/9.3/rule-system.html
"PostgreSQL 9.3 - 52.4. The PostgreSQL Rule System") / [9.2](/docs/9.2/rule-
system.html "PostgreSQL 9.2 - 52.4. The PostgreSQL Rule System") /
[9.1](/docs/9.1/rule-system.html "PostgreSQL 9.1 - 52.4. The PostgreSQL Rule
System") / [9.0](/docs/9.0/rule-system.html "PostgreSQL 9.0 - 52.4. The
PostgreSQL Rule System") / [8.4](/docs/8.4/rule-system.html "PostgreSQL 8.4 -
52.4. The PostgreSQL Rule System") / [8.3](/docs/8.3/rule-system.html
"PostgreSQL 8.3 - 52.4. The PostgreSQL Rule System") / [8.2](/docs/8.2/rule-
system.html "PostgreSQL 8.2 - 52.4. The PostgreSQL Rule System") /
[8.1](/docs/8.1/rule-system.html "PostgreSQL 8.1 - 52.4. The PostgreSQL Rule
System") / [8.0](/docs/8.0/rule-system.html "PostgreSQL 8.0 - 52.4. The
PostgreSQL Rule System") / [7.4](/docs/7.4/rule-system.html "PostgreSQL 7.4 -
52.4. The PostgreSQL Rule System") / [7.3](/docs/7.3/rule-system.html
"PostgreSQL 7.3 - 52.4. The PostgreSQL Rule System") / [7.2](/docs/7.2/rule-
system.html "PostgreSQL 7.2 - 52.4. The PostgreSQL Rule System") /
[7.1](/docs/7.1/rule-system.html "PostgreSQL 7.1 - 52.4. The PostgreSQL Rule
System")

__

52.4. The PostgreSQL Rule System  
---  
[Prev](parser-stage.html "52.3. The Parser Stage")  | [Up](overview.html "Chapter 52. Overview of PostgreSQL Internals") | Chapter 52. Overview of PostgreSQL Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](planner-optimizer.html "52.5. Planner/Optimizer")  
  
* * *

## 52.4. The PostgreSQL Rule System #

PostgreSQL supports a powerful _rule system_ for the specification of _views_
and ambiguous _view updates_. Originally the PostgreSQL rule system consisted
of two implementations:

  * The first one worked using _row level_ processing and was implemented deep in the _executor_. The rule system was called whenever an individual row had been accessed. This implementation was removed in 1995 when the last official release of the Berkeley Postgres project was transformed into Postgres95.

  * The second implementation of the rule system is a technique called _query rewriting_. The _rewrite system_ is a module that exists between the _parser stage_ and the _planner/optimizer_. This technique is still implemented.

The query rewriter is discussed in some detail in [Chapter 41](rules.html
"Chapter 41. The Rule System"), so there is no need to cover it here. We will
only point out that both the input and the output of the rewriter are query
trees, that is, there is no change in the representation or level of semantic
detail in the trees. Rewriting can be thought of as a form of macro expansion.

* * *

[Prev](parser-stage.html "52.3. The Parser Stage")  | [Up](overview.html "Chapter 52. Overview of PostgreSQL Internals") |  [Next](planner-optimizer.html "52.5. Planner/Optimizer")  
---|---|---  
52.3. The Parser Stage  | [Home](index.html "PostgreSQL 16.9 Documentation") |  52.5. Planner/Optimizer  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/rule-system.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

