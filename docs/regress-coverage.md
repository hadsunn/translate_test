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

Supported Versions: [Current](/docs/current/regress-coverage.html "PostgreSQL
17 - 33.5. Test Coverage Examination") ([17](/docs/17/regress-coverage.html
"PostgreSQL 17 - 33.5. Test Coverage Examination")) / [16](/docs/16/regress-
coverage.html "PostgreSQL 16 - 33.5. Test Coverage Examination") /
[15](/docs/15/regress-coverage.html "PostgreSQL 15 - 33.5. Test Coverage
Examination") / [14](/docs/14/regress-coverage.html "PostgreSQL 14 -
33.5. Test Coverage Examination") / [13](/docs/13/regress-coverage.html
"PostgreSQL 13 - 33.5. Test Coverage Examination")

Development Versions: [18](/docs/18/regress-coverage.html "PostgreSQL 18 -
33.5. Test Coverage Examination") / [devel](/docs/devel/regress-coverage.html
"PostgreSQL devel - 33.5. Test Coverage Examination")

Unsupported versions: [12](/docs/12/regress-coverage.html "PostgreSQL 12 -
33.5. Test Coverage Examination") / [11](/docs/11/regress-coverage.html
"PostgreSQL 11 - 33.5. Test Coverage Examination") / [10](/docs/10/regress-
coverage.html "PostgreSQL 10 - 33.5. Test Coverage Examination") /
[9.6](/docs/9.6/regress-coverage.html "PostgreSQL 9.6 - 33.5. Test Coverage
Examination") / [9.5](/docs/9.5/regress-coverage.html "PostgreSQL 9.5 -
33.5. Test Coverage Examination") / [9.4](/docs/9.4/regress-coverage.html
"PostgreSQL 9.4 - 33.5. Test Coverage Examination") / [9.3](/docs/9.3/regress-
coverage.html "PostgreSQL 9.3 - 33.5. Test Coverage Examination") /
[9.2](/docs/9.2/regress-coverage.html "PostgreSQL 9.2 - 33.5. Test Coverage
Examination") / [9.1](/docs/9.1/regress-coverage.html "PostgreSQL 9.1 -
33.5. Test Coverage Examination") / [9.0](/docs/9.0/regress-coverage.html
"PostgreSQL 9.0 - 33.5. Test Coverage Examination") / [8.4](/docs/8.4/regress-
coverage.html "PostgreSQL 8.4 - 33.5. Test Coverage Examination")

__

33.5. Test Coverage Examination  
---  
[Prev](regress-tap.html "33.4. TAP Tests")  | [Up](regress.html "Chapter 33. Regression Tests") | Chapter 33. Regression Tests | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](client-interfaces.html "Part IV. Client Interfaces")  
  
* * *

## 33.5. Test Coverage Examination #

[33.5.1. Coverage with Autoconf and Make](regress-coverage.html#REGRESS-
COVERAGE-CONFIGURE)

[33.5.2. Coverage with Meson](regress-coverage.html#REGRESS-COVERAGE-MESON)

The PostgreSQL source code can be compiled with coverage testing
instrumentation, so that it becomes possible to examine which parts of the
code are covered by the regression tests or any other test suite that is run
with the code. This is currently supported when compiling with GCC, and it
requires the `gcov` and `lcov` packages.

### 33.5.1. Coverage with Autoconf and Make #

A typical workflow looks like this:

    
    
    ./configure --enable-coverage ... OTHER OPTIONS ...
    make
    make check # or other test suite
    make coverage-html
    

Then point your HTML browser to `coverage/index.html`.

If you don't have `lcov` or prefer text output over an HTML report, you can
run

    
    
    make coverage
    

instead of `make coverage-html`, which will produce `.gcov` output files for
each source file relevant to the test. (`make coverage` and `make coverage-
html` will overwrite each other's files, so mixing them might be confusing.)

You can run several different tests before making the coverage report; the
execution counts will accumulate. If you want to reset the execution counts
between test runs, run:

    
    
    make coverage-clean
    

You can run the `make coverage-html` or `make coverage` command in a
subdirectory if you want a coverage report for only a portion of the code
tree.

Use `make distclean` to clean up when done.

### 33.5.2. Coverage with Meson #

A typical workflow looks like this:

    
    
    meson setup -Db_coverage=true ... OTHER OPTIONS ... builddir/
    meson compile -C builddir/
    meson test -C builddir/
    cd builddir/
    ninja coverage-html
    

Then point your HTML browser to `./meson-logs/coveragereport/index.html`.

You can run several different tests before making the coverage report; the
execution counts will accumulate.

* * *

[Prev](regress-tap.html "33.4. TAP Tests")  | [Up](regress.html "Chapter 33. Regression Tests") |  [Next](client-interfaces.html "Part IV. Client Interfaces")  
---|---|---  
33.4. TAP Tests  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Part IV. Client Interfaces  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/regress-coverage.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

