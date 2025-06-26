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

Supported Versions: [Current](/docs/current/regress-tap.html "PostgreSQL 17 -
33.4. TAP Tests") ([17](/docs/17/regress-tap.html "PostgreSQL 17 - 33.4. TAP
Tests")) / [16](/docs/16/regress-tap.html "PostgreSQL 16 - 33.4. TAP Tests") /
[15](/docs/15/regress-tap.html "PostgreSQL 15 - 33.4. TAP Tests") /
[14](/docs/14/regress-tap.html "PostgreSQL 14 - 33.4. TAP Tests") /
[13](/docs/13/regress-tap.html "PostgreSQL 13 - 33.4. TAP Tests")

Development Versions: [18](/docs/18/regress-tap.html "PostgreSQL 18 -
33.4. TAP Tests") / [devel](/docs/devel/regress-tap.html "PostgreSQL devel -
33.4. TAP Tests")

Unsupported versions: [12](/docs/12/regress-tap.html "PostgreSQL 12 -
33.4. TAP Tests") / [11](/docs/11/regress-tap.html "PostgreSQL 11 - 33.4. TAP
Tests") / [10](/docs/10/regress-tap.html "PostgreSQL 10 - 33.4. TAP Tests") /
[9.6](/docs/9.6/regress-tap.html "PostgreSQL 9.6 - 33.4. TAP Tests") /
[9.5](/docs/9.5/regress-tap.html "PostgreSQL 9.5 - 33.4. TAP Tests") /
[9.4](/docs/9.4/regress-tap.html "PostgreSQL 9.4 - 33.4. TAP Tests")

__

33.4. TAP Tests  
---  
[Prev](regress-variant.html "33.3. Variant Comparison Files")  | [Up](regress.html "Chapter 33. Regression Tests") | Chapter 33. Regression Tests | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](regress-coverage.html "33.5. Test Coverage Examination")  
  
* * *

## 33.4. TAP Tests #

[33.4.1. Environment Variables](regress-tap.html#REGRESS-TAP-VARS)

Various tests, particularly the client program tests under `src/bin`, use the
Perl TAP tools and are run using the Perl testing program `prove`. You can
pass command-line options to `prove` by setting the `make` variable
`PROVE_FLAGS`, for example:

    
    
    make -C src/bin check PROVE_FLAGS='--timer'
    

See the manual page of `prove` for more information.

The `make` variable `PROVE_TESTS` can be used to define a whitespace-separated
list of paths relative to the `Makefile` invoking `prove` to run the specified
subset of tests instead of the default `t/*.pl`. For example:

    
    
    make check PROVE_TESTS='t/001_test1.pl t/003_test3.pl'
    

The TAP tests require the Perl module `IPC::Run`. This module is available
from [CPAN](https://metacpan.org/dist/IPC-Run) or an operating system package.
They also require PostgreSQL to be configured with the option `--enable-tap-
tests`.

Generically speaking, the TAP tests will test the executables in a previously-
installed installation tree if you say `make installcheck`, or will build a
new local installation tree from current sources if you say `make check`. In
either case they will initialize a local instance (data directory) and
transiently run a server in it. Some of these tests run more than one server.
Thus, these tests can be fairly resource-intensive.

It's important to realize that the TAP tests will start test server(s) even
when you say `make installcheck`; this is unlike the traditional non-TAP
testing infrastructure, which expects to use an already-running test server in
that case. Some PostgreSQL subdirectories contain both traditional-style and
TAP-style tests, meaning that `make installcheck` will produce a mix of
results from temporary servers and the already-running test server.

### 33.4.1. Environment Variables #

Data directories are named according to the test filename, and will be
retained if a test fails. If the environment variable `PG_TEST_NOCLEAN` is
set, data directories will be retained regardless of test status. For example,
retaining the data directory regardless of test results when running the
pg_dump tests:

    
    
    PG_TEST_NOCLEAN=1 make -C src/bin/pg_dump check
    

This environment variable also prevents the test's temporary directories from
being removed.

Many operations in the test suites use a 180-second timeout, which on slow
hosts may lead to load-induced timeouts. Setting the environment variable
`PG_TEST_TIMEOUT_DEFAULT` to a higher number will change the default to avoid
this.

* * *

[Prev](regress-variant.html "33.3. Variant Comparison Files")  | [Up](regress.html "Chapter 33. Regression Tests") |  [Next](regress-coverage.html "33.5. Test Coverage Examination")  
---|---|---  
33.3. Variant Comparison Files  | [Home](index.html "PostgreSQL 16.9 Documentation") |  33.5. Test Coverage Examination  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/regress-tap.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

