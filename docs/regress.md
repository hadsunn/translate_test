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

Supported Versions: [Current](/docs/current/regress.html "PostgreSQL 17 -
Chapter 33. Regression Tests") ([17](/docs/17/regress.html "PostgreSQL 17 -
Chapter 33. Regression Tests")) / [16](/docs/16/regress.html "PostgreSQL 16 -
Chapter 33. Regression Tests") / [15](/docs/15/regress.html "PostgreSQL 15 -
Chapter 33. Regression Tests") / [14](/docs/14/regress.html "PostgreSQL 14 -
Chapter 33. Regression Tests") / [13](/docs/13/regress.html "PostgreSQL 13 -
Chapter 33. Regression Tests")

Development Versions: [18](/docs/18/regress.html "PostgreSQL 18 -
Chapter 33. Regression Tests") / [devel](/docs/devel/regress.html "PostgreSQL
devel - Chapter 33. Regression Tests")

Unsupported versions: [12](/docs/12/regress.html "PostgreSQL 12 -
Chapter 33. Regression Tests") / [11](/docs/11/regress.html "PostgreSQL 11 -
Chapter 33. Regression Tests") / [10](/docs/10/regress.html "PostgreSQL 10 -
Chapter 33. Regression Tests") / [9.6](/docs/9.6/regress.html "PostgreSQL 9.6
- Chapter 33. Regression Tests") / [9.5](/docs/9.5/regress.html "PostgreSQL
9.5 - Chapter 33. Regression Tests") / [9.4](/docs/9.4/regress.html
"PostgreSQL 9.4 - Chapter 33. Regression Tests") /
[9.3](/docs/9.3/regress.html "PostgreSQL 9.3 - Chapter 33. Regression Tests")
/ [9.2](/docs/9.2/regress.html "PostgreSQL 9.2 - Chapter 33. Regression
Tests") / [9.1](/docs/9.1/regress.html "PostgreSQL 9.1 -
Chapter 33. Regression Tests") / [9.0](/docs/9.0/regress.html "PostgreSQL 9.0
- Chapter 33. Regression Tests") / [8.4](/docs/8.4/regress.html "PostgreSQL
8.4 - Chapter 33. Regression Tests") / [8.3](/docs/8.3/regress.html
"PostgreSQL 8.3 - Chapter 33. Regression Tests") /
[8.2](/docs/8.2/regress.html "PostgreSQL 8.2 - Chapter 33. Regression Tests")
/ [8.1](/docs/8.1/regress.html "PostgreSQL 8.1 - Chapter 33. Regression
Tests") / [8.0](/docs/8.0/regress.html "PostgreSQL 8.0 -
Chapter 33. Regression Tests") / [7.4](/docs/7.4/regress.html "PostgreSQL 7.4
- Chapter 33. Regression Tests") / [7.3](/docs/7.3/regress.html "PostgreSQL
7.3 - Chapter 33. Regression Tests") / [7.2](/docs/7.2/regress.html
"PostgreSQL 7.2 - Chapter 33. Regression Tests") /
[7.1](/docs/7.1/regress.html "PostgreSQL 7.1 - Chapter 33. Regression Tests")

__

Chapter 33. Regression Tests  
---  
[Prev](jit-extensibility.html "32.4. Extensibility")  | [Up](admin.html "Part III. Server Administration") | Part III. Server Administration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](regress-run.html "33.1. Running the Tests")  
  
* * *

## Chapter 33. Regression Tests

**Table of Contents**

[33.1. Running the Tests](regress-run.html)

    

[33.1.1. Running the Tests Against a Temporary Installation](regress-
run.html#REGRESS-RUN-TEMP-INST)

[33.1.2. Running the Tests Against an Existing Installation](regress-
run.html#REGRESS-RUN-EXISTING-INST)

[33.1.3. Additional Test Suites](regress-run.html#REGRESS-ADDITIONAL)

[33.1.4. Locale and Encoding](regress-run.html#REGRESS-RUN-LOCALE)

[33.1.5. Custom Server Settings](regress-run.html#REGRESS-RUN-CUSTOM-SETTINGS)

[33.1.6. Extra Tests](regress-run.html#REGRESS-RUN-EXTRA-TESTS)

[33.2. Test Evaluation](regress-evaluation.html)

    

[33.2.1. Error Message Differences](regress-evaluation.html#REGRESS-
EVALUATION-MESSAGE-DIFFERENCES)

[33.2.2. Locale Differences](regress-evaluation.html#REGRESS-EVALUATION-
LOCALE-DIFFERENCES)

[33.2.3. Date and Time Differences](regress-evaluation.html#REGRESS-
EVALUATION-DATE-TIME-DIFFERENCES)

[33.2.4. Floating-Point Differences](regress-evaluation.html#REGRESS-
EVALUATION-FLOAT-DIFFERENCES)

[33.2.5. Row Ordering Differences](regress-evaluation.html#REGRESS-EVALUATION-
ORDERING-DIFFERENCES)

[33.2.6. Insufficient Stack Depth](regress-evaluation.html#REGRESS-EVALUATION-
STACK-DEPTH)

[33.2.7. The “random” Test](regress-evaluation.html#REGRESS-EVALUATION-RANDOM-
TEST)

[33.2.8. Configuration Parameters](regress-evaluation.html#REGRESS-EVALUATION-
CONFIG-PARAMS)

[33.3. Variant Comparison Files](regress-variant.html)

[33.4. TAP Tests](regress-tap.html)

    

[33.4.1. Environment Variables](regress-tap.html#REGRESS-TAP-VARS)

[33.5. Test Coverage Examination](regress-coverage.html)

    

[33.5.1. Coverage with Autoconf and Make](regress-coverage.html#REGRESS-
COVERAGE-CONFIGURE)

[33.5.2. Coverage with Meson](regress-coverage.html#REGRESS-COVERAGE-MESON)

The regression tests are a comprehensive set of tests for the SQL
implementation in PostgreSQL. They test standard SQL operations as well as the
extended capabilities of PostgreSQL.

* * *

[Prev](jit-extensibility.html "32.4. Extensibility")  | [Up](admin.html "Part III. Server Administration") |  [Next](regress-run.html "33.1. Running the Tests")  
---|---|---  
32.4. Extensibility  | [Home](index.html "PostgreSQL 16.9 Documentation") |  33.1. Running the Tests  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/regress.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

