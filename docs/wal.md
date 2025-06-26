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

Supported Versions: [Current](/docs/current/wal.html "PostgreSQL 17 -
Chapter 30. Reliability and the Write-Ahead Log") ([17](/docs/17/wal.html
"PostgreSQL 17 - Chapter 30. Reliability and the Write-Ahead Log")) /
[16](/docs/16/wal.html "PostgreSQL 16 - Chapter 30. Reliability and the Write-
Ahead Log") / [15](/docs/15/wal.html "PostgreSQL 15 - Chapter 30. Reliability
and the Write-Ahead Log") / [14](/docs/14/wal.html "PostgreSQL 14 -
Chapter 30. Reliability and the Write-Ahead Log") / [13](/docs/13/wal.html
"PostgreSQL 13 - Chapter 30. Reliability and the Write-Ahead Log")

Development Versions: [18](/docs/18/wal.html "PostgreSQL 18 -
Chapter 30. Reliability and the Write-Ahead Log") /
[devel](/docs/devel/wal.html "PostgreSQL devel - Chapter 30. Reliability and
the Write-Ahead Log")

Unsupported versions: [12](/docs/12/wal.html "PostgreSQL 12 -
Chapter 30. Reliability and the Write-Ahead Log") / [11](/docs/11/wal.html
"PostgreSQL 11 - Chapter 30. Reliability and the Write-Ahead Log") /
[10](/docs/10/wal.html "PostgreSQL 10 - Chapter 30. Reliability and the Write-
Ahead Log") / [9.6](/docs/9.6/wal.html "PostgreSQL 9.6 -
Chapter 30. Reliability and the Write-Ahead Log") / [9.5](/docs/9.5/wal.html
"PostgreSQL 9.5 - Chapter 30. Reliability and the Write-Ahead Log") /
[9.4](/docs/9.4/wal.html "PostgreSQL 9.4 - Chapter 30. Reliability and the
Write-Ahead Log") / [9.3](/docs/9.3/wal.html "PostgreSQL 9.3 -
Chapter 30. Reliability and the Write-Ahead Log") / [9.2](/docs/9.2/wal.html
"PostgreSQL 9.2 - Chapter 30. Reliability and the Write-Ahead Log") /
[9.1](/docs/9.1/wal.html "PostgreSQL 9.1 - Chapter 30. Reliability and the
Write-Ahead Log") / [9.0](/docs/9.0/wal.html "PostgreSQL 9.0 -
Chapter 30. Reliability and the Write-Ahead Log") / [8.4](/docs/8.4/wal.html
"PostgreSQL 8.4 - Chapter 30. Reliability and the Write-Ahead Log") /
[8.3](/docs/8.3/wal.html "PostgreSQL 8.3 - Chapter 30. Reliability and the
Write-Ahead Log") / [8.2](/docs/8.2/wal.html "PostgreSQL 8.2 -
Chapter 30. Reliability and the Write-Ahead Log") / [8.1](/docs/8.1/wal.html
"PostgreSQL 8.1 - Chapter 30. Reliability and the Write-Ahead Log") /
[8.0](/docs/8.0/wal.html "PostgreSQL 8.0 - Chapter 30. Reliability and the
Write-Ahead Log") / [7.4](/docs/7.4/wal.html "PostgreSQL 7.4 -
Chapter 30. Reliability and the Write-Ahead Log") / [7.3](/docs/7.3/wal.html
"PostgreSQL 7.3 - Chapter 30. Reliability and the Write-Ahead Log") /
[7.2](/docs/7.2/wal.html "PostgreSQL 7.2 - Chapter 30. Reliability and the
Write-Ahead Log") / [7.1](/docs/7.1/wal.html "PostgreSQL 7.1 -
Chapter 30. Reliability and the Write-Ahead Log")

__

Chapter 30. Reliability and the Write-Ahead Log  
---  
[Prev](disk-full.html "29.2. Disk Full Failure")  | [Up](admin.html "Part III. Server Administration") | Part III. Server Administration | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](wal-reliability.html "30.1. Reliability")  
  
* * *

## Chapter 30. Reliability and the Write-Ahead Log

**Table of Contents**

[30.1. Reliability](wal-reliability.html)

[30.2. Data Checksums](checksums.html)

    

[30.2.1. Off-line Enabling of Checksums](checksums.html#CHECKSUMS-OFFLINE-
ENABLE-DISABLE)

[30.3. Write-Ahead Logging (WAL)](wal-intro.html)

[30.4. Asynchronous Commit](wal-async-commit.html)

[30.5. WAL Configuration](wal-configuration.html)

[30.6. WAL Internals](wal-internals.html)

This chapter explains how to control the reliability of PostgreSQL, including
details about the Write-Ahead Log.

* * *

[Prev](disk-full.html "29.2. Disk Full Failure")  | [Up](admin.html "Part III. Server Administration") |  [Next](wal-reliability.html "30.1. Reliability")  
---|---|---  
29.2. Disk Full Failure  | [Home](index.html "PostgreSQL 16.9 Documentation") |  30.1. Reliability  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/wal.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

