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

Supported Versions: [Current](/docs/current/event-triggers.html "PostgreSQL 17
- Chapter 40. Event Triggers") ([17](/docs/17/event-triggers.html "PostgreSQL
17 - Chapter 40. Event Triggers")) / [16](/docs/16/event-triggers.html
"PostgreSQL 16 - Chapter 40. Event Triggers") / [15](/docs/15/event-
triggers.html "PostgreSQL 15 - Chapter 40. Event Triggers") /
[14](/docs/14/event-triggers.html "PostgreSQL 14 - Chapter 40. Event
Triggers") / [13](/docs/13/event-triggers.html "PostgreSQL 13 -
Chapter 40. Event Triggers")

Development Versions: [18](/docs/18/event-triggers.html "PostgreSQL 18 -
Chapter 40. Event Triggers") / [devel](/docs/devel/event-triggers.html
"PostgreSQL devel - Chapter 40. Event Triggers")

Unsupported versions: [12](/docs/12/event-triggers.html "PostgreSQL 12 -
Chapter 40. Event Triggers") / [11](/docs/11/event-triggers.html "PostgreSQL
11 - Chapter 40. Event Triggers") / [10](/docs/10/event-triggers.html
"PostgreSQL 10 - Chapter 40. Event Triggers") / [9.6](/docs/9.6/event-
triggers.html "PostgreSQL 9.6 - Chapter 40. Event Triggers") /
[9.5](/docs/9.5/event-triggers.html "PostgreSQL 9.5 - Chapter 40. Event
Triggers") / [9.4](/docs/9.4/event-triggers.html "PostgreSQL 9.4 -
Chapter 40. Event Triggers") / [9.3](/docs/9.3/event-triggers.html "PostgreSQL
9.3 - Chapter 40. Event Triggers")

__

Chapter 40. Event Triggers  
---  
[Prev](trigger-example.html "39.4. A Complete Trigger Example")  | [Up](server-programming.html "Part V. Server Programming") | Part V. Server Programming | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](event-trigger-definition.html "40.1. Overview of Event Trigger Behavior")  
  
* * *

## Chapter 40. Event Triggers

**Table of Contents**

[40.1. Overview of Event Trigger Behavior](event-trigger-definition.html)

[40.2. Event Trigger Firing Matrix](event-trigger-matrix.html)

[40.3. Writing Event Trigger Functions in C](event-trigger-interface.html)

[40.4. A Complete Event Trigger Example](event-trigger-example.html)

[40.5. A Table Rewrite Event Trigger Example](event-trigger-table-rewrite-
example.html)

To supplement the trigger mechanism discussed in [Chapter 39](triggers.html
"Chapter 39. Triggers"), PostgreSQL also provides event triggers. Unlike
regular triggers, which are attached to a single table and capture only DML
events, event triggers are global to a particular database and are capable of
capturing DDL events.

Like regular triggers, event triggers can be written in any procedural
language that includes event trigger support, or in C, but not in plain SQL.

* * *

[Prev](trigger-example.html "39.4. A Complete Trigger Example")  | [Up](server-programming.html "Part V. Server Programming") |  [Next](event-trigger-definition.html "40.1. Overview of Event Trigger Behavior")  
---|---|---  
39.4. A Complete Trigger Example  | [Home](index.html "PostgreSQL 16.9 Documentation") |  40.1. Overview of Event Trigger Behavior  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/event-triggers.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

