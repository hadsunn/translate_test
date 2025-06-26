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

Supported Versions: [Current](/docs/current/planner-stats-details.html
"PostgreSQL 17 - Chapter 76. How the Planner Uses Statistics")
([17](/docs/17/planner-stats-details.html "PostgreSQL 17 - Chapter 76. How the
Planner Uses Statistics")) / [16](/docs/16/planner-stats-details.html
"PostgreSQL 16 - Chapter 76. How the Planner Uses Statistics") /
[15](/docs/15/planner-stats-details.html "PostgreSQL 15 - Chapter 76. How the
Planner Uses Statistics") / [14](/docs/14/planner-stats-details.html
"PostgreSQL 14 - Chapter 76. How the Planner Uses Statistics") /
[13](/docs/13/planner-stats-details.html "PostgreSQL 13 - Chapter 76. How the
Planner Uses Statistics")

Development Versions: [18](/docs/18/planner-stats-details.html "PostgreSQL 18
- Chapter 76. How the Planner Uses Statistics") / [devel](/docs/devel/planner-
stats-details.html "PostgreSQL devel - Chapter 76. How the Planner Uses
Statistics")

Unsupported versions: [12](/docs/12/planner-stats-details.html "PostgreSQL 12
- Chapter 76. How the Planner Uses Statistics") / [11](/docs/11/planner-stats-
details.html "PostgreSQL 11 - Chapter 76. How the Planner Uses Statistics") /
[10](/docs/10/planner-stats-details.html "PostgreSQL 10 - Chapter 76. How the
Planner Uses Statistics") / [9.6](/docs/9.6/planner-stats-details.html
"PostgreSQL 9.6 - Chapter 76. How the Planner Uses Statistics") /
[9.5](/docs/9.5/planner-stats-details.html "PostgreSQL 9.5 - Chapter 76. How
the Planner Uses Statistics") / [9.4](/docs/9.4/planner-stats-details.html
"PostgreSQL 9.4 - Chapter 76. How the Planner Uses Statistics") /
[9.3](/docs/9.3/planner-stats-details.html "PostgreSQL 9.3 - Chapter 76. How
the Planner Uses Statistics") / [9.2](/docs/9.2/planner-stats-details.html
"PostgreSQL 9.2 - Chapter 76. How the Planner Uses Statistics") /
[9.1](/docs/9.1/planner-stats-details.html "PostgreSQL 9.1 - Chapter 76. How
the Planner Uses Statistics") / [9.0](/docs/9.0/planner-stats-details.html
"PostgreSQL 9.0 - Chapter 76. How the Planner Uses Statistics") /
[8.4](/docs/8.4/planner-stats-details.html "PostgreSQL 8.4 - Chapter 76. How
the Planner Uses Statistics") / [8.3](/docs/8.3/planner-stats-details.html
"PostgreSQL 8.3 - Chapter 76. How the Planner Uses Statistics") /
[8.2](/docs/8.2/planner-stats-details.html "PostgreSQL 8.2 - Chapter 76. How
the Planner Uses Statistics") / [8.1](/docs/8.1/planner-stats-details.html
"PostgreSQL 8.1 - Chapter 76. How the Planner Uses Statistics")

__

Chapter 76. How the Planner Uses Statistics  
---  
[Prev](bki-example.html "75.6. BKI Example")  | [Up](internals.html "Part VII. Internals") | Part VII. Internals | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](row-estimation-examples.html "76.1. Row Estimation Examples")  
  
* * *

## Chapter 76. How the Planner Uses Statistics

**Table of Contents**

[76.1. Row Estimation Examples](row-estimation-examples.html)

[76.2. Multivariate Statistics Examples](multivariate-statistics-
examples.html)

    

[76.2.1. Functional Dependencies](multivariate-statistics-
examples.html#FUNCTIONAL-DEPENDENCIES)

[76.2.2. Multivariate N-Distinct Counts](multivariate-statistics-
examples.html#MULTIVARIATE-NDISTINCT-COUNTS)

[76.2.3. MCV Lists](multivariate-statistics-examples.html#MCV-LISTS)

[76.3. Planner Statistics and Security](planner-stats-security.html)

This chapter builds on the material covered in [Section 14.1](using-
explain.html "14.1. Using EXPLAIN") and [Section 14.2](planner-stats.html
"14.2. Statistics Used by the Planner") to show some additional details about
how the planner uses the system statistics to estimate the number of rows each
part of a query might return. This is a significant part of the planning
process, providing much of the raw material for cost calculation.

The intent of this chapter is not to document the code in detail, but to
present an overview of how it works. This will perhaps ease the learning curve
for someone who subsequently wishes to read the code.

* * *

[Prev](bki-example.html "75.6. BKI Example")  | [Up](internals.html "Part VII. Internals") |  [Next](row-estimation-examples.html "76.1. Row Estimation Examples")  
---|---|---  
75.6. BKI Example  | [Home](index.html "PostgreSQL 16.9 Documentation") |  76.1. Row Estimation Examples  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/planner-stats-details.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

