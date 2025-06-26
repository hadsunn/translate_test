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

Supported Versions: [Current](/docs/current/libpq.html "PostgreSQL 17 -
Chapter 34. libpq — C Library") ([17](/docs/17/libpq.html "PostgreSQL 17 -
Chapter 34. libpq — C Library")) / [16](/docs/16/libpq.html "PostgreSQL 16 -
Chapter 34. libpq — C Library") / [15](/docs/15/libpq.html "PostgreSQL 15 -
Chapter 34. libpq — C Library") / [14](/docs/14/libpq.html "PostgreSQL 14 -
Chapter 34. libpq — C Library") / [13](/docs/13/libpq.html "PostgreSQL 13 -
Chapter 34. libpq — C Library")

Development Versions: [18](/docs/18/libpq.html "PostgreSQL 18 -
Chapter 34. libpq — C Library") / [devel](/docs/devel/libpq.html "PostgreSQL
devel - Chapter 34. libpq — C Library")

Unsupported versions: [12](/docs/12/libpq.html "PostgreSQL 12 -
Chapter 34. libpq — C Library") / [11](/docs/11/libpq.html "PostgreSQL 11 -
Chapter 34. libpq — C Library") / [10](/docs/10/libpq.html "PostgreSQL 10 -
Chapter 34. libpq — C Library") / [9.6](/docs/9.6/libpq.html "PostgreSQL 9.6 -
Chapter 34. libpq — C Library") / [9.5](/docs/9.5/libpq.html "PostgreSQL 9.5 -
Chapter 34. libpq — C Library") / [9.4](/docs/9.4/libpq.html "PostgreSQL 9.4 -
Chapter 34. libpq — C Library") / [9.3](/docs/9.3/libpq.html "PostgreSQL 9.3 -
Chapter 34. libpq — C Library") / [9.2](/docs/9.2/libpq.html "PostgreSQL 9.2 -
Chapter 34. libpq — C Library") / [9.1](/docs/9.1/libpq.html "PostgreSQL 9.1 -
Chapter 34. libpq — C Library") / [9.0](/docs/9.0/libpq.html "PostgreSQL 9.0 -
Chapter 34. libpq — C Library") / [8.4](/docs/8.4/libpq.html "PostgreSQL 8.4 -
Chapter 34. libpq — C Library") / [8.3](/docs/8.3/libpq.html "PostgreSQL 8.3 -
Chapter 34. libpq — C Library") / [8.2](/docs/8.2/libpq.html "PostgreSQL 8.2 -
Chapter 34. libpq — C Library") / [8.1](/docs/8.1/libpq.html "PostgreSQL 8.1 -
Chapter 34. libpq — C Library") / [8.0](/docs/8.0/libpq.html "PostgreSQL 8.0 -
Chapter 34. libpq — C Library") / [7.4](/docs/7.4/libpq.html "PostgreSQL 7.4 -
Chapter 34. libpq — C Library") / [7.3](/docs/7.3/libpq.html "PostgreSQL 7.3 -
Chapter 34. libpq — C Library") / [7.2](/docs/7.2/libpq.html "PostgreSQL 7.2 -
Chapter 34. libpq — C Library") / [7.1](/docs/7.1/libpq.html "PostgreSQL 7.1 -
Chapter 34. libpq — C Library")

__

Chapter 34. libpq — C Library  
---  
[Prev](client-interfaces.html "Part IV. Client Interfaces")  | [Up](client-interfaces.html "Part IV. Client Interfaces") | Part IV. Client Interfaces | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-connect.html "34.1. Database Connection Control Functions")  
  
* * *

## Chapter 34. libpq — C Library

**Table of Contents**

[34.1. Database Connection Control Functions](libpq-connect.html)

    

[34.1.1. Connection Strings](libpq-connect.html#LIBPQ-CONNSTRING)

[34.1.2. Parameter Key Words](libpq-connect.html#LIBPQ-PARAMKEYWORDS)

[34.2. Connection Status Functions](libpq-status.html)

[34.3. Command Execution Functions](libpq-exec.html)

    

[34.3.1. Main Functions](libpq-exec.html#LIBPQ-EXEC-MAIN)

[34.3.2. Retrieving Query Result Information](libpq-exec.html#LIBPQ-EXEC-
SELECT-INFO)

[34.3.3. Retrieving Other Result Information](libpq-exec.html#LIBPQ-EXEC-
NONSELECT)

[34.3.4. Escaping Strings for Inclusion in SQL Commands](libpq-
exec.html#LIBPQ-EXEC-ESCAPE-STRING)

[34.4. Asynchronous Command Processing](libpq-async.html)

[34.5. Pipeline Mode](libpq-pipeline-mode.html)

    

[34.5.1. Using Pipeline Mode](libpq-pipeline-mode.html#LIBPQ-PIPELINE-USING)

[34.5.2. Functions Associated with Pipeline Mode](libpq-pipeline-
mode.html#LIBPQ-PIPELINE-FUNCTIONS)

[34.5.3. When to Use Pipeline Mode](libpq-pipeline-mode.html#LIBPQ-PIPELINE-
TIPS)

[34.6. Retrieving Query Results Row-by-Row](libpq-single-row-mode.html)

[34.7. Canceling Queries in Progress](libpq-cancel.html)

[34.8. The Fast-Path Interface](libpq-fastpath.html)

[34.9. Asynchronous Notification](libpq-notify.html)

[34.10. Functions Associated with the `COPY` Command](libpq-copy.html)

    

[34.10.1. Functions for Sending `COPY` Data](libpq-copy.html#LIBPQ-COPY-SEND)

[34.10.2. Functions for Receiving `COPY` Data](libpq-copy.html#LIBPQ-COPY-
RECEIVE)

[34.10.3. Obsolete Functions for `COPY`](libpq-copy.html#LIBPQ-COPY-
DEPRECATED)

[34.11. Control Functions](libpq-control.html)

[34.12. Miscellaneous Functions](libpq-misc.html)

[34.13. Notice Processing](libpq-notice-processing.html)

[34.14. Event System](libpq-events.html)

    

[34.14.1. Event Types](libpq-events.html#LIBPQ-EVENTS-TYPES)

[34.14.2. Event Callback Procedure](libpq-events.html#LIBPQ-EVENTS-PROC)

[34.14.3. Event Support Functions](libpq-events.html#LIBPQ-EVENTS-FUNCS)

[34.14.4. Event Example](libpq-events.html#LIBPQ-EVENTS-EXAMPLE)

[34.15. Environment Variables](libpq-envars.html)

[34.16. The Password File](libpq-pgpass.html)

[34.17. The Connection Service File](libpq-pgservice.html)

[34.18. LDAP Lookup of Connection Parameters](libpq-ldap.html)

[34.19. SSL Support](libpq-ssl.html)

    

[34.19.1. Client Verification of Server Certificates](libpq-ssl.html#LIBQ-SSL-
CERTIFICATES)

[34.19.2. Client Certificates](libpq-ssl.html#LIBPQ-SSL-CLIENTCERT)

[34.19.3. Protection Provided in Different Modes](libpq-ssl.html#LIBPQ-SSL-
PROTECTION)

[34.19.4. SSL Client File Usage](libpq-ssl.html#LIBPQ-SSL-FILEUSAGE)

[34.19.5. SSL Library Initialization](libpq-ssl.html#LIBPQ-SSL-INITIALIZE)

[34.20. Behavior in Threaded Programs](libpq-threading.html)

[34.21. Building libpq Programs](libpq-build.html)

[34.22. Example Programs](libpq-example.html)

libpq is the C application programmer's interface to PostgreSQL. libpq is a
set of library functions that allow client programs to pass queries to the
PostgreSQL backend server and to receive the results of these queries.

libpq is also the underlying engine for several other PostgreSQL application
interfaces, including those written for C++, Perl, Python, Tcl and ECPG. So
some aspects of libpq's behavior will be important to you if you use one of
those packages. In particular, [Section 34.15](libpq-envars.html
"34.15. Environment Variables"), [Section 34.16](libpq-pgpass.html "34.16. The
Password File") and [Section 34.19](libpq-ssl.html "34.19. SSL Support")
describe behavior that is visible to the user of any application that uses
libpq.

Some short programs are included at the end of this chapter ([Section
34.22](libpq-example.html "34.22. Example Programs")) to show how to write
programs that use libpq. There are also several complete examples of libpq
applications in the directory `src/test/examples` in the source code
distribution.

Client programs that use libpq must include the header file `libpq-fe.h` and
must link with the libpq library.

* * *

[Prev](client-interfaces.html "Part IV. Client Interfaces")  | [Up](client-interfaces.html "Part IV. Client Interfaces") |  [Next](libpq-connect.html "34.1. Database Connection Control Functions")  
---|---|---  
Part IV. Client Interfaces  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.1. Database Connection Control Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

