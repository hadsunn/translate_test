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

Supported Versions: [Current](/docs/current/regress-variant.html "PostgreSQL
17 - 33.3. Variant Comparison Files") ([17](/docs/17/regress-variant.html
"PostgreSQL 17 - 33.3. Variant Comparison Files")) / [16](/docs/16/regress-
variant.html "PostgreSQL 16 - 33.3. Variant Comparison Files") /
[15](/docs/15/regress-variant.html "PostgreSQL 15 - 33.3. Variant Comparison
Files") / [14](/docs/14/regress-variant.html "PostgreSQL 14 - 33.3. Variant
Comparison Files") / [13](/docs/13/regress-variant.html "PostgreSQL 13 -
33.3. Variant Comparison Files")

Development Versions: [18](/docs/18/regress-variant.html "PostgreSQL 18 -
33.3. Variant Comparison Files") / [devel](/docs/devel/regress-variant.html
"PostgreSQL devel - 33.3. Variant Comparison Files")

Unsupported versions: [12](/docs/12/regress-variant.html "PostgreSQL 12 -
33.3. Variant Comparison Files") / [11](/docs/11/regress-variant.html
"PostgreSQL 11 - 33.3. Variant Comparison Files") / [10](/docs/10/regress-
variant.html "PostgreSQL 10 - 33.3. Variant Comparison Files") /
[9.6](/docs/9.6/regress-variant.html "PostgreSQL 9.6 - 33.3. Variant
Comparison Files") / [9.5](/docs/9.5/regress-variant.html "PostgreSQL 9.5 -
33.3. Variant Comparison Files") / [9.4](/docs/9.4/regress-variant.html
"PostgreSQL 9.4 - 33.3. Variant Comparison Files") / [9.3](/docs/9.3/regress-
variant.html "PostgreSQL 9.3 - 33.3. Variant Comparison Files") /
[9.2](/docs/9.2/regress-variant.html "PostgreSQL 9.2 - 33.3. Variant
Comparison Files") / [9.1](/docs/9.1/regress-variant.html "PostgreSQL 9.1 -
33.3. Variant Comparison Files") / [9.0](/docs/9.0/regress-variant.html
"PostgreSQL 9.0 - 33.3. Variant Comparison Files") / [8.4](/docs/8.4/regress-
variant.html "PostgreSQL 8.4 - 33.3. Variant Comparison Files") /
[8.3](/docs/8.3/regress-variant.html "PostgreSQL 8.3 - 33.3. Variant
Comparison Files") / [8.2](/docs/8.2/regress-variant.html "PostgreSQL 8.2 -
33.3. Variant Comparison Files") / [8.1](/docs/8.1/regress-variant.html
"PostgreSQL 8.1 - 33.3. Variant Comparison Files")

__

33.3. Variant Comparison Files  
---  
[Prev](regress-evaluation.html "33.2. Test Evaluation")  | [Up](regress.html "Chapter 33. Regression Tests") | Chapter 33. Regression Tests | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](regress-tap.html "33.4. TAP Tests")  
  
* * *

## 33.3. Variant Comparison Files #

Since some of the tests inherently produce environment-dependent results, we
have provided ways to specify alternate “expected” result files. Each
regression test can have several comparison files showing possible results on
different platforms. There are two independent mechanisms for determining
which comparison file is used for each test.

The first mechanism allows comparison files to be selected for specific
platforms. There is a mapping file, `src/test/regress/resultmap`, that defines
which comparison file to use for each platform. To eliminate bogus test
“failures” for a particular platform, you first choose or make a variant
result file, and then add a line to the `resultmap` file.

Each line in the mapping file is of the form

    
    
    testname:output:platformpattern=comparisonfilename
    

The test name is just the name of the particular regression test module. The
output value indicates which output file to check. For the standard regression
tests, this is always `out`. The value corresponds to the file extension of
the output file. The platform pattern is a pattern in the style of the Unix
tool `expr` (that is, a regular expression with an implicit `^` anchor at the
start). It is matched against the platform name as printed by `config.guess`.
The comparison file name is the base name of the substitute result comparison
file.

For example: some systems lack a working `strtof` function, for which our
workaround causes rounding errors in the `float4` regression test. Therefore,
we provide a variant comparison file, `float4-misrounded-input.out`, which
includes the results to be expected on these systems. To silence the bogus
“failure” message on Cygwin platforms, `resultmap` includes:

    
    
    float4:out:.*-.*-cygwin.*=float4-misrounded-input.out
    

which will trigger on any machine where the output of `config.guess` matches
`.*-.*-cygwin.*`. Other lines in `resultmap` select the variant comparison
file for other platforms where it's appropriate.

The second selection mechanism for variant comparison files is much more
automatic: it simply uses the “best match” among several supplied comparison
files. The regression test driver script considers both the standard
comparison file for a test, `_`testname`_.out`, and variant files named
`_`testname`_ __`digit`_.out` (where the _`digit`_ is any single digit
`0`-`9`). If any such file is an exact match, the test is considered to pass;
otherwise, the one that generates the shortest diff is used to create the
failure report. (If `resultmap` includes an entry for the particular test,
then the base _`testname`_ is the substitute name given in `resultmap`.)

For example, for the `char` test, the comparison file `char.out` contains
results that are expected in the `C` and `POSIX` locales, while the file
`char_1.out` contains results sorted as they appear in many other locales.

The best-match mechanism was devised to cope with locale-dependent results,
but it can be used in any situation where the test results cannot be predicted
easily from the platform name alone. A limitation of this mechanism is that
the test driver cannot tell which variant is actually “correct” for the
current environment; it will just pick the variant that seems to work best.
Therefore it is safest to use this mechanism only for variant results that you
are willing to consider equally valid in all contexts.

* * *

[Prev](regress-evaluation.html "33.2. Test Evaluation")  | [Up](regress.html "Chapter 33. Regression Tests") |  [Next](regress-tap.html "33.4. TAP Tests")  
---|---|---  
33.2. Test Evaluation  | [Home](index.html "PostgreSQL 16.9 Documentation") |  33.4. TAP Tests  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/regress-variant.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

