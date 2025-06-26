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

Supported Versions: [Current](/docs/current/features.html "PostgreSQL 17 -
Appendix D. SQL Conformance") ([17](/docs/17/features.html "PostgreSQL 17 -
Appendix D. SQL Conformance")) / [16](/docs/16/features.html "PostgreSQL 16 -
Appendix D. SQL Conformance") / [15](/docs/15/features.html "PostgreSQL 15 -
Appendix D. SQL Conformance") / [14](/docs/14/features.html "PostgreSQL 14 -
Appendix D. SQL Conformance") / [13](/docs/13/features.html "PostgreSQL 13 -
Appendix D. SQL Conformance")

Development Versions: [18](/docs/18/features.html "PostgreSQL 18 -
Appendix D. SQL Conformance") / [devel](/docs/devel/features.html "PostgreSQL
devel - Appendix D. SQL Conformance")

Unsupported versions: [12](/docs/12/features.html "PostgreSQL 12 -
Appendix D. SQL Conformance") / [11](/docs/11/features.html "PostgreSQL 11 -
Appendix D. SQL Conformance") / [10](/docs/10/features.html "PostgreSQL 10 -
Appendix D. SQL Conformance") / [9.6](/docs/9.6/features.html "PostgreSQL 9.6
- Appendix D. SQL Conformance") / [9.5](/docs/9.5/features.html "PostgreSQL
9.5 - Appendix D. SQL Conformance") / [9.4](/docs/9.4/features.html
"PostgreSQL 9.4 - Appendix D. SQL Conformance") /
[9.3](/docs/9.3/features.html "PostgreSQL 9.3 - Appendix D. SQL Conformance")
/ [9.2](/docs/9.2/features.html "PostgreSQL 9.2 - Appendix D. SQL
Conformance") / [9.1](/docs/9.1/features.html "PostgreSQL 9.1 -
Appendix D. SQL Conformance") / [9.0](/docs/9.0/features.html "PostgreSQL 9.0
- Appendix D. SQL Conformance") / [8.4](/docs/8.4/features.html "PostgreSQL
8.4 - Appendix D. SQL Conformance") / [8.3](/docs/8.3/features.html
"PostgreSQL 8.3 - Appendix D. SQL Conformance") /
[8.2](/docs/8.2/features.html "PostgreSQL 8.2 - Appendix D. SQL Conformance")
/ [8.1](/docs/8.1/features.html "PostgreSQL 8.1 - Appendix D. SQL
Conformance") / [8.0](/docs/8.0/features.html "PostgreSQL 8.0 -
Appendix D. SQL Conformance") / [7.4](/docs/7.4/features.html "PostgreSQL 7.4
- Appendix D. SQL Conformance") / [7.3](/docs/7.3/features.html "PostgreSQL
7.3 - Appendix D. SQL Conformance")

__

Appendix D. SQL Conformance  
---  
[Prev](sql-keywords-appendix.html "Appendix C. SQL Key Words")  | [Up](appendixes.html "Part VIII. Appendixes") | Part VIII. Appendixes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](features-sql-standard.html "D.1. Supported Features")  
  
* * *

## Appendix D. SQL Conformance

**Table of Contents**

[D.1. Supported Features](features-sql-standard.html)

[D.2. Unsupported Features](unsupported-features-sql-standard.html)

[D.3. XML Limits and Conformance to SQL/XML](xml-limits-conformance.html)

    

[D.3.1. Queries Are Restricted to XPath 1.0](xml-limits-
conformance.html#FUNCTIONS-XML-LIMITS-XPATH1)

[D.3.2. Incidental Limits of the Implementation](xml-limits-
conformance.html#FUNCTIONS-XML-LIMITS-POSTGRESQL)

This section attempts to outline to what extent PostgreSQL conforms to the
current SQL standard. The following information is not a full statement of
conformance, but it presents the main topics in as much detail as is both
reasonable and useful for users.

The formal name of the SQL standard is ISO/IEC 9075 “Database Language SQL”. A
revised version of the standard is released from time to time; the most recent
update appearing in 2023. The 2023 version is referred to as ISO/IEC
9075:2023, or simply as SQL:2023. The versions prior to that were SQL:2016,
SQL:2011, SQL:2008, SQL:2006, SQL:2003, SQL:1999, and SQL-92. Each version
replaces the previous one, so claims of conformance to earlier versions have
no official merit. PostgreSQL development aims for conformance with the latest
official version of the standard where such conformance does not contradict
traditional features or common sense. Many of the features required by the SQL
standard are supported, though sometimes with slightly differing syntax or
function. Further moves towards conformance can be expected over time.

SQL-92 defined three feature sets for conformance: Entry, Intermediate, and
Full. Most database management systems claiming SQL standard conformance were
conforming at only the Entry level, since the entire set of features in the
Intermediate and Full levels was either too voluminous or in conflict with
legacy behaviors.

Starting with SQL:1999, the SQL standard defines a large set of individual
features rather than the ineffectively broad three levels found in SQL-92. A
large subset of these features represents the “Core” features, which every
conforming SQL implementation must supply. The rest of the features are purely
optional.

The standard is split into a number of parts, each also known by a shorthand
name:

  * ISO/IEC 9075-1 Framework (SQL/Framework)

  * ISO/IEC 9075-2 Foundation (SQL/Foundation)

  * ISO/IEC 9075-3 Call Level Interface (SQL/CLI)

  * ISO/IEC 9075-4 Persistent Stored Modules (SQL/PSM)

  * ISO/IEC 9075-9 Management of External Data (SQL/MED)

  * ISO/IEC 9075-10 Object Language Bindings (SQL/OLB)

  * ISO/IEC 9075-11 Information and Definition Schemas (SQL/Schemata)

  * ISO/IEC 9075-13 Routines and Types using the Java Language (SQL/JRT)

  * ISO/IEC 9075-14 XML-related specifications (SQL/XML)

  * ISO/IEC 9075-15 Multi-dimensional arrays (SQL/MDA)

  * ISO/IEC 9075-16 Property Graph Queries (SQL/PGQ)

Note that some part numbers are not (or no longer) used.

The PostgreSQL core covers parts 1, 2, 9, 11, and 14. Part 3 is covered by the
ODBC driver, and part 13 is covered by the PL/Java plug-in, but exact
conformance is currently not being verified for these components. There are
currently no implementations of parts 4, 10, 15, and 16 for PostgreSQL.

PostgreSQL supports most of the major features of SQL:2023. Out of 177
mandatory features required for full Core conformance, PostgreSQL conforms to
at least 170. In addition, there is a long list of supported optional
features. It might be worth noting that at the time of writing, no current
version of any database management system claims full conformance to Core
SQL:2023.

In the following two sections, we provide a list of those features that
PostgreSQL supports, followed by a list of the features defined in SQL:2023
which are not yet supported in PostgreSQL. Both of these lists are
approximate: There might be minor details that are nonconforming for a feature
that is listed as supported, and large parts of an unsupported feature might
in fact be implemented. The main body of the documentation always contains the
most accurate information about what does and does not work.

### Note

Feature codes containing a hyphen are subfeatures. Therefore, if a particular
subfeature is not supported, the main feature is listed as unsupported even if
some other subfeatures are supported.

* * *

[Prev](sql-keywords-appendix.html "Appendix C. SQL Key Words")  | [Up](appendixes.html "Part VIII. Appendixes") |  [Next](features-sql-standard.html "D.1. Supported Features")  
---|---|---  
Appendix C. SQL Key Words  | [Home](index.html "PostgreSQL 16.9 Documentation") |  D.1. Supported Features  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/features.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

