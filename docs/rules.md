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

Supported Versions: [Current](/docs/current/rules.html "PostgreSQL 17 -
Chapter 41. The Rule System") ([17](/docs/17/rules.html "PostgreSQL 17 -
Chapter 41. The Rule System")) / [16](/docs/16/rules.html "PostgreSQL 16 -
Chapter 41. The Rule System") / [15](/docs/15/rules.html "PostgreSQL 15 -
Chapter 41. The Rule System") / [14](/docs/14/rules.html "PostgreSQL 14 -
Chapter 41. The Rule System") / [13](/docs/13/rules.html "PostgreSQL 13 -
Chapter 41. The Rule System")

Development Versions: [18](/docs/18/rules.html "PostgreSQL 18 -
Chapter 41. The Rule System") / [devel](/docs/devel/rules.html "PostgreSQL
devel - Chapter 41. The Rule System")

Unsupported versions: [12](/docs/12/rules.html "PostgreSQL 12 -
Chapter 41. The Rule System") / [11](/docs/11/rules.html "PostgreSQL 11 -
Chapter 41. The Rule System") / [10](/docs/10/rules.html "PostgreSQL 10 -
Chapter 41. The Rule System") / [9.6](/docs/9.6/rules.html "PostgreSQL 9.6 -
Chapter 41. The Rule System") / [9.5](/docs/9.5/rules.html "PostgreSQL 9.5 -
Chapter 41. The Rule System") / [9.4](/docs/9.4/rules.html "PostgreSQL 9.4 -
Chapter 41. The Rule System") / [9.3](/docs/9.3/rules.html "PostgreSQL 9.3 -
Chapter 41. The Rule System") / [9.2](/docs/9.2/rules.html "PostgreSQL 9.2 -
Chapter 41. The Rule System") / [9.1](/docs/9.1/rules.html "PostgreSQL 9.1 -
Chapter 41. The Rule System") / [9.0](/docs/9.0/rules.html "PostgreSQL 9.0 -
Chapter 41. The Rule System") / [8.4](/docs/8.4/rules.html "PostgreSQL 8.4 -
Chapter 41. The Rule System") / [8.3](/docs/8.3/rules.html "PostgreSQL 8.3 -
Chapter 41. The Rule System") / [8.2](/docs/8.2/rules.html "PostgreSQL 8.2 -
Chapter 41. The Rule System") / [8.1](/docs/8.1/rules.html "PostgreSQL 8.1 -
Chapter 41. The Rule System") / [8.0](/docs/8.0/rules.html "PostgreSQL 8.0 -
Chapter 41. The Rule System") / [7.4](/docs/7.4/rules.html "PostgreSQL 7.4 -
Chapter 41. The Rule System") / [7.3](/docs/7.3/rules.html "PostgreSQL 7.3 -
Chapter 41. The Rule System") / [7.2](/docs/7.2/rules.html "PostgreSQL 7.2 -
Chapter 41. The Rule System") / [7.1](/docs/7.1/rules.html "PostgreSQL 7.1 -
Chapter 41. The Rule System")

__

Chapter 41. The Rule System  
---  
[Prev](event-trigger-table-rewrite-example.html "40.5. A Table Rewrite Event Trigger Example")  | [Up](server-programming.html "Part V. Server Programming") | Part V. Server Programming | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](querytree.html "41.1. The Query Tree")  
  
* * *

## Chapter 41. The Rule System

**Table of Contents**

[41.1. The Query Tree](querytree.html)

[41.2. Views and the Rule System](rules-views.html)

    

[41.2.1. How `SELECT` Rules Work](rules-views.html#RULES-SELECT)

[41.2.2. View Rules in Non-`SELECT` Statements](rules-views.html#RULES-VIEWS-
NON-SELECT)

[41.2.3. The Power of Views in PostgreSQL](rules-views.html#RULES-VIEWS-POWER)

[41.2.4. Updating a View](rules-views.html#RULES-VIEWS-UPDATE)

[41.3. Materialized Views](rules-materializedviews.html)

[41.4. Rules on `INSERT`, `UPDATE`, and `DELETE`](rules-update.html)

    

[41.4.1. How Update Rules Work](rules-update.html#RULES-UPDATE-HOW)

[41.4.2. Cooperation with Views](rules-update.html#RULES-UPDATE-VIEWS)

[41.5. Rules and Privileges](rules-privileges.html)

[41.6. Rules and Command Status](rules-status.html)

[41.7. Rules Versus Triggers](rules-triggers.html)

This chapter discusses the rule system in PostgreSQL. Production rule systems
are conceptually simple, but there are many subtle points involved in actually
using them.

Some other database systems define active database rules, which are usually
stored procedures and triggers. In PostgreSQL, these can be implemented using
functions and triggers as well.

The rule system (more precisely speaking, the query rewrite rule system) is
totally different from stored procedures and triggers. It modifies queries to
take rules into consideration, and then passes the modified query to the query
planner for planning and execution. It is very powerful, and can be used for
many things such as query language procedures, views, and versions. The
theoretical foundations and the power of this rule system are also discussed
in [[ston90b]](biblio.html#STON90B) and [[ong90]](biblio.html#ONG90).

* * *

[Prev](event-trigger-table-rewrite-example.html "40.5. A Table Rewrite Event Trigger Example")  | [Up](server-programming.html "Part V. Server Programming") |  [Next](querytree.html "41.1. The Query Tree")  
---|---|---  
40.5. A Table Rewrite Event Trigger Example  | [Home](index.html "PostgreSQL 16.9 Documentation") |  41.1. The Query Tree  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/rules.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

