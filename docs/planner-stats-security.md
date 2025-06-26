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

Supported Versions: [Current](/docs/current/planner-stats-security.html
"PostgreSQL 17 - 76.3. Planner Statistics and Security")
([17](/docs/17/planner-stats-security.html "PostgreSQL 17 - 76.3. Planner
Statistics and Security")) / [16](/docs/16/planner-stats-security.html
"PostgreSQL 16 - 76.3. Planner Statistics and Security") /
[15](/docs/15/planner-stats-security.html "PostgreSQL 15 - 76.3. Planner
Statistics and Security") / [14](/docs/14/planner-stats-security.html
"PostgreSQL 14 - 76.3. Planner Statistics and Security") /
[13](/docs/13/planner-stats-security.html "PostgreSQL 13 - 76.3. Planner
Statistics and Security")

Development Versions: [18](/docs/18/planner-stats-security.html "PostgreSQL 18
- 76.3. Planner Statistics and Security") / [devel](/docs/devel/planner-stats-
security.html "PostgreSQL devel - 76.3. Planner Statistics and Security")

Unsupported versions: [12](/docs/12/planner-stats-security.html "PostgreSQL 12
- 76.3. Planner Statistics and Security") / [11](/docs/11/planner-stats-
security.html "PostgreSQL 11 - 76.3. Planner Statistics and Security") /
[10](/docs/10/planner-stats-security.html "PostgreSQL 10 - 76.3. Planner
Statistics and Security") / [9.6](/docs/9.6/planner-stats-security.html
"PostgreSQL 9.6 - 76.3. Planner Statistics and Security") /
[9.5](/docs/9.5/planner-stats-security.html "PostgreSQL 9.5 - 76.3. Planner
Statistics and Security") / [9.4](/docs/9.4/planner-stats-security.html
"PostgreSQL 9.4 - 76.3. Planner Statistics and Security") /
[9.3](/docs/9.3/planner-stats-security.html "PostgreSQL 9.3 - 76.3. Planner
Statistics and Security") / [9.2](/docs/9.2/planner-stats-security.html
"PostgreSQL 9.2 - 76.3. Planner Statistics and Security")

__

76.3. Planner Statistics and Security  
---  
[Prev](multivariate-statistics-examples.html "76.2. Multivariate Statistics Examples")  | [Up](planner-stats-details.html "Chapter 76. How the Planner Uses Statistics") | Chapter 76. How the Planner Uses Statistics | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](backup-manifest-format.html "Chapter 77. Backup Manifest Format")  
  
* * *

## 76.3. Planner Statistics and Security #

Access to the table `pg_statistic` is restricted to superusers, so that
ordinary users cannot learn about the contents of the tables of other users
from it. Some selectivity estimation functions will use a user-provided
operator (either the operator appearing in the query or a related operator) to
analyze the stored statistics. For example, in order to determine whether a
stored most common value is applicable, the selectivity estimator will have to
run the appropriate `=` operator to compare the constant in the query to the
stored value. Thus the data in `pg_statistic` is potentially passed to user-
defined operators. An appropriately crafted operator can intentionally leak
the passed operands (for example, by logging them or writing them to a
different table), or accidentally leak them by showing their values in error
messages, in either case possibly exposing data from `pg_statistic` to a user
who should not be able to see it.

In order to prevent this, the following applies to all built-in selectivity
estimation functions. When planning a query, in order to be able to use stored
statistics, the current user must either have `SELECT` privilege on the table
or the involved columns, or the operator used must be `LEAKPROOF` (more
accurately, the function that the operator is based on). If not, then the
selectivity estimator will behave as if no statistics are available, and the
planner will proceed with default or fall-back assumptions.

If a user does not have the required privilege on the table or columns, then
in many cases the query will ultimately receive a permission-denied error, in
which case this mechanism is invisible in practice. But if the user is reading
from a security-barrier view, then the planner might wish to check the
statistics of an underlying table that is otherwise inaccessible to the user.
In that case, the operator should be leak-proof or the statistics will not be
used. There is no direct feedback about that, except that the plan might be
suboptimal. If one suspects that this is the case, one could try running the
query as a more privileged user, to see if a different plan results.

This restriction applies only to cases where the planner would need to execute
a user-defined operator on one or more values from `pg_statistic`. Thus the
planner is permitted to use generic statistical information, such as the
fraction of null values or the number of distinct values in a column,
regardless of access privileges.

Selectivity estimation functions contained in third-party extensions that
potentially operate on statistics with user-defined operators should follow
the same security rules. Consult the PostgreSQL source code for guidance.

* * *

[Prev](multivariate-statistics-examples.html "76.2. Multivariate Statistics Examples")  | [Up](planner-stats-details.html "Chapter 76. How the Planner Uses Statistics") |  [Next](backup-manifest-format.html "Chapter 77. Backup Manifest Format")  
---|---|---  
76.2. Multivariate Statistics Examples  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 77. Backup Manifest Format  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/planner-stats-security.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

