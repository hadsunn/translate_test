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

Supported Versions: [Current](/docs/current/rules-status.html "PostgreSQL 17 -
41.6. Rules and Command Status") ([17](/docs/17/rules-status.html "PostgreSQL
17 - 41.6. Rules and Command Status")) / [16](/docs/16/rules-status.html
"PostgreSQL 16 - 41.6. Rules and Command Status") / [15](/docs/15/rules-
status.html "PostgreSQL 15 - 41.6. Rules and Command Status") /
[14](/docs/14/rules-status.html "PostgreSQL 14 - 41.6. Rules and Command
Status") / [13](/docs/13/rules-status.html "PostgreSQL 13 - 41.6. Rules and
Command Status")

Development Versions: [18](/docs/18/rules-status.html "PostgreSQL 18 -
41.6. Rules and Command Status") / [devel](/docs/devel/rules-status.html
"PostgreSQL devel - 41.6. Rules and Command Status")

Unsupported versions: [12](/docs/12/rules-status.html "PostgreSQL 12 -
41.6. Rules and Command Status") / [11](/docs/11/rules-status.html "PostgreSQL
11 - 41.6. Rules and Command Status") / [10](/docs/10/rules-status.html
"PostgreSQL 10 - 41.6. Rules and Command Status") / [9.6](/docs/9.6/rules-
status.html "PostgreSQL 9.6 - 41.6. Rules and Command Status") /
[9.5](/docs/9.5/rules-status.html "PostgreSQL 9.5 - 41.6. Rules and Command
Status") / [9.4](/docs/9.4/rules-status.html "PostgreSQL 9.4 - 41.6. Rules and
Command Status") / [9.3](/docs/9.3/rules-status.html "PostgreSQL 9.3 -
41.6. Rules and Command Status") / [9.2](/docs/9.2/rules-status.html
"PostgreSQL 9.2 - 41.6. Rules and Command Status") / [9.1](/docs/9.1/rules-
status.html "PostgreSQL 9.1 - 41.6. Rules and Command Status") /
[9.0](/docs/9.0/rules-status.html "PostgreSQL 9.0 - 41.6. Rules and Command
Status") / [8.4](/docs/8.4/rules-status.html "PostgreSQL 8.4 - 41.6. Rules and
Command Status") / [8.3](/docs/8.3/rules-status.html "PostgreSQL 8.3 -
41.6. Rules and Command Status") / [8.2](/docs/8.2/rules-status.html
"PostgreSQL 8.2 - 41.6. Rules and Command Status") / [8.1](/docs/8.1/rules-
status.html "PostgreSQL 8.1 - 41.6. Rules and Command Status") /
[8.0](/docs/8.0/rules-status.html "PostgreSQL 8.0 - 41.6. Rules and Command
Status") / [7.4](/docs/7.4/rules-status.html "PostgreSQL 7.4 - 41.6. Rules and
Command Status") / [7.3](/docs/7.3/rules-status.html "PostgreSQL 7.3 -
41.6. Rules and Command Status")

__

41.6. Rules and Command Status  
---  
[Prev](rules-privileges.html "41.5. Rules and Privileges")  | [Up](rules.html "Chapter 41. The Rule System") | Chapter 41. The Rule System | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](rules-triggers.html "41.7. Rules Versus Triggers")  
  
* * *

## 41.6. Rules and Command Status #

The PostgreSQL server returns a command status string, such as `INSERT 149592
1`, for each command it receives. This is simple enough when there are no
rules involved, but what happens when the query is rewritten by rules?

Rules affect the command status as follows:

  * If there is no unconditional `INSTEAD` rule for the query, then the originally given query will be executed, and its command status will be returned as usual. (But note that if there were any conditional `INSTEAD` rules, the negation of their qualifications will have been added to the original query. This might reduce the number of rows it processes, and if so the reported status will be affected.)

  * If there is any unconditional `INSTEAD` rule for the query, then the original query will not be executed at all. In this case, the server will return the command status for the last query that was inserted by an `INSTEAD` rule (conditional or unconditional) and is of the same command type (`INSERT`, `UPDATE`, or `DELETE`) as the original query. If no query meeting those requirements is added by any rule, then the returned command status shows the original query type and zeroes for the row-count and OID fields.

The programmer can ensure that any desired `INSTEAD` rule is the one that sets
the command status in the second case, by giving it the alphabetically last
rule name among the active rules, so that it gets applied last.

* * *

[Prev](rules-privileges.html "41.5. Rules and Privileges")  | [Up](rules.html "Chapter 41. The Rule System") |  [Next](rules-triggers.html "41.7. Rules Versus Triggers")  
---|---|---  
41.5. Rules and Privileges  | [Home](index.html "PostgreSQL 16.9 Documentation") |  41.7. Rules Versus Triggers  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/rules-status.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

