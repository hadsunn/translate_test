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

Supported Versions: [Current](/docs/current/custom-scan.html "PostgreSQL 17 -
Chapter 61. Writing a Custom Scan Provider") ([17](/docs/17/custom-scan.html
"PostgreSQL 17 - Chapter 61. Writing a Custom Scan Provider")) /
[16](/docs/16/custom-scan.html "PostgreSQL 16 - Chapter 61. Writing a Custom
Scan Provider") / [15](/docs/15/custom-scan.html "PostgreSQL 15 -
Chapter 61. Writing a Custom Scan Provider") / [14](/docs/14/custom-scan.html
"PostgreSQL 14 - Chapter 61. Writing a Custom Scan Provider") /
[13](/docs/13/custom-scan.html "PostgreSQL 13 - Chapter 61. Writing a Custom
Scan Provider")

Development Versions: [18](/docs/18/custom-scan.html "PostgreSQL 18 -
Chapter 61. Writing a Custom Scan Provider") / [devel](/docs/devel/custom-
scan.html "PostgreSQL devel - Chapter 61. Writing a Custom Scan Provider")

Unsupported versions: [12](/docs/12/custom-scan.html "PostgreSQL 12 -
Chapter 61. Writing a Custom Scan Provider") / [11](/docs/11/custom-scan.html
"PostgreSQL 11 - Chapter 61. Writing a Custom Scan Provider") /
[10](/docs/10/custom-scan.html "PostgreSQL 10 - Chapter 61. Writing a Custom
Scan Provider") / [9.6](/docs/9.6/custom-scan.html "PostgreSQL 9.6 -
Chapter 61. Writing a Custom Scan Provider") / [9.5](/docs/9.5/custom-
scan.html "PostgreSQL 9.5 - Chapter 61. Writing a Custom Scan Provider")

__

Chapter 61. Writing a Custom Scan Provider  
---  
[Prev](tablesample-support-functions.html "60.1. Sampling Method Support Functions")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](custom-scan-path.html "61.1. Creating Custom Scan Paths")  
  
* * *

## Chapter 61. Writing a Custom Scan Provider

**Table of Contents**

[61.1. Creating Custom Scan Paths](custom-scan-path.html)

    

[61.1.1. Custom Scan Path Callbacks](custom-scan-path.html#CUSTOM-SCAN-PATH-
CALLBACKS)

[61.2. Creating Custom Scan Plans](custom-scan-plan.html)

    

[61.2.1. Custom Scan Plan Callbacks](custom-scan-plan.html#CUSTOM-SCAN-PLAN-
CALLBACKS)

[61.3. Executing Custom Scans](custom-scan-execution.html)

    

[61.3.1. Custom Scan Execution Callbacks](custom-scan-execution.html#CUSTOM-
SCAN-EXECUTION-CALLBACKS)

PostgreSQL supports a set of experimental facilities which are intended to
allow extension modules to add new scan types to the system. Unlike a [foreign
data wrapper](fdwhandler.html "Chapter 59. Writing a Foreign Data Wrapper"),
which is only responsible for knowing how to scan its own foreign tables, a
custom scan provider can provide an alternative method of scanning any
relation in the system. Typically, the motivation for writing a custom scan
provider will be to allow the use of some optimization not supported by the
core system, such as caching or some form of hardware acceleration. This
chapter outlines how to write a new custom scan provider.

Implementing a new type of custom scan is a three-step process. First, during
planning, it is necessary to generate access paths representing a scan using
the proposed strategy. Second, if one of those access paths is selected by the
planner as the optimal strategy for scanning a particular relation, the access
path must be converted to a plan. Finally, it must be possible to execute the
plan and generate the same results that would have been generated for any
other access path targeting the same relation.

* * *

[Prev](tablesample-support-functions.html "60.1. Sampling Method Support Functions")  | [Up](internals.html "Part VII. Internals") |  [Next](custom-scan-path.html "61.1. Creating Custom Scan Paths")  
---|---|---  
60.1. Sampling Method Support Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  61.1. Creating Custom Scan Paths  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/custom-scan.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

