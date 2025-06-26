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

Supported Versions: [Current](/docs/current/datetime-appendix.html "PostgreSQL
17 - Appendix B. Date/Time Support") ([17](/docs/17/datetime-appendix.html
"PostgreSQL 17 - Appendix B. Date/Time Support")) / [16](/docs/16/datetime-
appendix.html "PostgreSQL 16 - Appendix B. Date/Time Support") /
[15](/docs/15/datetime-appendix.html "PostgreSQL 15 - Appendix B. Date/Time
Support") / [14](/docs/14/datetime-appendix.html "PostgreSQL 14 -
Appendix B. Date/Time Support") / [13](/docs/13/datetime-appendix.html
"PostgreSQL 13 - Appendix B. Date/Time Support")

Development Versions: [18](/docs/18/datetime-appendix.html "PostgreSQL 18 -
Appendix B. Date/Time Support") / [devel](/docs/devel/datetime-appendix.html
"PostgreSQL devel - Appendix B. Date/Time Support")

Unsupported versions: [12](/docs/12/datetime-appendix.html "PostgreSQL 12 -
Appendix B. Date/Time Support") / [11](/docs/11/datetime-appendix.html
"PostgreSQL 11 - Appendix B. Date/Time Support") / [10](/docs/10/datetime-
appendix.html "PostgreSQL 10 - Appendix B. Date/Time Support") /
[9.6](/docs/9.6/datetime-appendix.html "PostgreSQL 9.6 - Appendix B. Date/Time
Support") / [9.5](/docs/9.5/datetime-appendix.html "PostgreSQL 9.5 -
Appendix B. Date/Time Support") / [9.4](/docs/9.4/datetime-appendix.html
"PostgreSQL 9.4 - Appendix B. Date/Time Support") / [9.3](/docs/9.3/datetime-
appendix.html "PostgreSQL 9.3 - Appendix B. Date/Time Support") /
[9.2](/docs/9.2/datetime-appendix.html "PostgreSQL 9.2 - Appendix B. Date/Time
Support") / [9.1](/docs/9.1/datetime-appendix.html "PostgreSQL 9.1 -
Appendix B. Date/Time Support") / [9.0](/docs/9.0/datetime-appendix.html
"PostgreSQL 9.0 - Appendix B. Date/Time Support") / [8.4](/docs/8.4/datetime-
appendix.html "PostgreSQL 8.4 - Appendix B. Date/Time Support") /
[8.3](/docs/8.3/datetime-appendix.html "PostgreSQL 8.3 - Appendix B. Date/Time
Support") / [8.2](/docs/8.2/datetime-appendix.html "PostgreSQL 8.2 -
Appendix B. Date/Time Support") / [8.1](/docs/8.1/datetime-appendix.html
"PostgreSQL 8.1 - Appendix B. Date/Time Support") / [8.0](/docs/8.0/datetime-
appendix.html "PostgreSQL 8.0 - Appendix B. Date/Time Support") /
[7.4](/docs/7.4/datetime-appendix.html "PostgreSQL 7.4 - Appendix B. Date/Time
Support") / [7.3](/docs/7.3/datetime-appendix.html "PostgreSQL 7.3 -
Appendix B. Date/Time Support") / [7.2](/docs/7.2/datetime-appendix.html
"PostgreSQL 7.2 - Appendix B. Date/Time Support") / [7.1](/docs/7.1/datetime-
appendix.html "PostgreSQL 7.1 - Appendix B. Date/Time Support")

__

Appendix B. Date/Time Support  
---  
[Prev](errcodes-appendix.html "Appendix A. PostgreSQL Error Codes")  | [Up](appendixes.html "Part VIII. Appendixes") | Part VIII. Appendixes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datetime-input-rules.html "B.1. Date/Time Input Interpretation")  
  
* * *

## Appendix B. Date/Time Support

**Table of Contents**

[B.1. Date/Time Input Interpretation](datetime-input-rules.html)

[B.2. Handling of Invalid or Ambiguous Timestamps](datetime-invalid-
input.html)

[B.3. Date/Time Key Words](datetime-keywords.html)

[B.4. Date/Time Configuration Files](datetime-config-files.html)

[B.5. POSIX Time Zone Specifications](datetime-posix-timezone-specs.html)

[B.6. History of Units](datetime-units-history.html)

[B.7. Julian Dates](datetime-julian-dates.html)

PostgreSQL uses an internal heuristic parser for all date/time input support.
Dates and times are input as strings, and are broken up into distinct fields
with a preliminary determination of what kind of information can be in the
field. Each field is interpreted and either assigned a numeric value, ignored,
or rejected. The parser contains internal lookup tables for all textual
fields, including months, days of the week, and time zones.

This appendix includes information on the content of these lookup tables and
describes the steps used by the parser to decode dates and times.

* * *

[Prev](errcodes-appendix.html "Appendix A. PostgreSQL Error Codes")  | [Up](appendixes.html "Part VIII. Appendixes") |  [Next](datetime-input-rules.html "B.1. Date/Time Input Interpretation")  
---|---|---  
Appendix A. PostgreSQL Error Codes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  B.1. Date/Time Input Interpretation  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datetime-appendix.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

