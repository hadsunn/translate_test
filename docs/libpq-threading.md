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

Supported Versions: [Current](/docs/current/libpq-threading.html "PostgreSQL
17 - 34.20. Behavior in Threaded Programs") ([17](/docs/17/libpq-
threading.html "PostgreSQL 17 - 34.20. Behavior in Threaded Programs")) /
[16](/docs/16/libpq-threading.html "PostgreSQL 16 - 34.20. Behavior in
Threaded Programs") / [15](/docs/15/libpq-threading.html "PostgreSQL 15 -
34.20. Behavior in Threaded Programs") / [14](/docs/14/libpq-threading.html
"PostgreSQL 14 - 34.20. Behavior in Threaded Programs") / [13](/docs/13/libpq-
threading.html "PostgreSQL 13 - 34.20. Behavior in Threaded Programs")

Development Versions: [18](/docs/18/libpq-threading.html "PostgreSQL 18 -
34.20. Behavior in Threaded Programs") / [devel](/docs/devel/libpq-
threading.html "PostgreSQL devel - 34.20. Behavior in Threaded Programs")

Unsupported versions: [12](/docs/12/libpq-threading.html "PostgreSQL 12 -
34.20. Behavior in Threaded Programs") / [11](/docs/11/libpq-threading.html
"PostgreSQL 11 - 34.20. Behavior in Threaded Programs") / [10](/docs/10/libpq-
threading.html "PostgreSQL 10 - 34.20. Behavior in Threaded Programs") /
[9.6](/docs/9.6/libpq-threading.html "PostgreSQL 9.6 - 34.20. Behavior in
Threaded Programs") / [9.5](/docs/9.5/libpq-threading.html "PostgreSQL 9.5 -
34.20. Behavior in Threaded Programs") / [9.4](/docs/9.4/libpq-threading.html
"PostgreSQL 9.4 - 34.20. Behavior in Threaded Programs") /
[9.3](/docs/9.3/libpq-threading.html "PostgreSQL 9.3 - 34.20. Behavior in
Threaded Programs") / [9.2](/docs/9.2/libpq-threading.html "PostgreSQL 9.2 -
34.20. Behavior in Threaded Programs") / [9.1](/docs/9.1/libpq-threading.html
"PostgreSQL 9.1 - 34.20. Behavior in Threaded Programs") /
[9.0](/docs/9.0/libpq-threading.html "PostgreSQL 9.0 - 34.20. Behavior in
Threaded Programs") / [8.4](/docs/8.4/libpq-threading.html "PostgreSQL 8.4 -
34.20. Behavior in Threaded Programs") / [8.3](/docs/8.3/libpq-threading.html
"PostgreSQL 8.3 - 34.20. Behavior in Threaded Programs") /
[8.2](/docs/8.2/libpq-threading.html "PostgreSQL 8.2 - 34.20. Behavior in
Threaded Programs") / [8.1](/docs/8.1/libpq-threading.html "PostgreSQL 8.1 -
34.20. Behavior in Threaded Programs") / [8.0](/docs/8.0/libpq-threading.html
"PostgreSQL 8.0 - 34.20. Behavior in Threaded Programs") /
[7.4](/docs/7.4/libpq-threading.html "PostgreSQL 7.4 - 34.20. Behavior in
Threaded Programs") / [7.3](/docs/7.3/libpq-threading.html "PostgreSQL 7.3 -
34.20. Behavior in Threaded Programs") / [7.2](/docs/7.2/libpq-threading.html
"PostgreSQL 7.2 - 34.20. Behavior in Threaded Programs") /
[7.1](/docs/7.1/libpq-threading.html "PostgreSQL 7.1 - 34.20. Behavior in
Threaded Programs")

__

34.20. Behavior in Threaded Programs  
---  
[Prev](libpq-ssl.html "34.19. SSL Support")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-build.html "34.21. Building libpq Programs")  
  
* * *

## 34.20. Behavior in Threaded Programs #

libpq is reentrant and thread-safe by default. You might need to use special
compiler command-line options when you compile your application code. Refer to
your system's documentation for information about how to build thread-enabled
applications, or look in `src/Makefile.global` for `PTHREAD_CFLAGS` and
`PTHREAD_LIBS`. This function allows the querying of libpq's thread-safe
status:

`PQisthreadsafe` #

    

Returns the thread safety status of the libpq library.

    
    
    int PQisthreadsafe();
    

Returns 1 if the libpq is thread-safe and 0 if it is not.

One thread restriction is that no two threads attempt to manipulate the same
`PGconn` object at the same time. In particular, you cannot issue concurrent
commands from different threads through the same connection object. (If you
need to run concurrent commands, use multiple connections.)

`PGresult` objects are normally read-only after creation, and so can be passed
around freely between threads. However, if you use any of the
`PGresult`-modifying functions described in [Section 34.12](libpq-misc.html
"34.12. Miscellaneous Functions") or [Section 34.14](libpq-events.html
"34.14. Event System"), it's up to you to avoid concurrent operations on the
same `PGresult`, too.

The deprecated functions [`PQrequestCancel`](libpq-cancel.html#LIBPQ-
PQREQUESTCANCEL) and [`PQoidStatus`](libpq-exec.html#LIBPQ-PQOIDSTATUS) are
not thread-safe and should not be used in multithread programs.
[`PQrequestCancel`](libpq-cancel.html#LIBPQ-PQREQUESTCANCEL) can be replaced
by [`PQcancel`](libpq-cancel.html#LIBPQ-PQCANCEL). [`PQoidStatus`](libpq-
exec.html#LIBPQ-PQOIDSTATUS) can be replaced by [`PQoidValue`](libpq-
exec.html#LIBPQ-PQOIDVALUE).

If you are using Kerberos inside your application (in addition to inside
libpq), you will need to do locking around Kerberos calls because Kerberos
functions are not thread-safe. See function `PQregisterThreadLock` in the
libpq source code for a way to do cooperative locking between libpq and your
application.

* * *

[Prev](libpq-ssl.html "34.19. SSL Support")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](libpq-build.html "34.21. Building libpq Programs")  
---|---|---  
34.19. SSL Support  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.21. Building libpq Programs  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-threading.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

