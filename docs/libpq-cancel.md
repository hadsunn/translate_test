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

Supported Versions: [Current](/docs/current/libpq-cancel.html "PostgreSQL 17 -
34.7. Canceling Queries in Progress") ([17](/docs/17/libpq-cancel.html
"PostgreSQL 17 - 34.7. Canceling Queries in Progress")) / [16](/docs/16/libpq-
cancel.html "PostgreSQL 16 - 34.7. Canceling Queries in Progress") /
[15](/docs/15/libpq-cancel.html "PostgreSQL 15 - 34.7. Canceling Queries in
Progress") / [14](/docs/14/libpq-cancel.html "PostgreSQL 14 - 34.7. Canceling
Queries in Progress") / [13](/docs/13/libpq-cancel.html "PostgreSQL 13 -
34.7. Canceling Queries in Progress")

Development Versions: [18](/docs/18/libpq-cancel.html "PostgreSQL 18 -
34.7. Canceling Queries in Progress") / [devel](/docs/devel/libpq-cancel.html
"PostgreSQL devel - 34.7. Canceling Queries in Progress")

Unsupported versions: [12](/docs/12/libpq-cancel.html "PostgreSQL 12 -
34.7. Canceling Queries in Progress") / [11](/docs/11/libpq-cancel.html
"PostgreSQL 11 - 34.7. Canceling Queries in Progress") / [10](/docs/10/libpq-
cancel.html "PostgreSQL 10 - 34.7. Canceling Queries in Progress") /
[9.6](/docs/9.6/libpq-cancel.html "PostgreSQL 9.6 - 34.7. Canceling Queries in
Progress") / [9.5](/docs/9.5/libpq-cancel.html "PostgreSQL 9.5 -
34.7. Canceling Queries in Progress") / [9.4](/docs/9.4/libpq-cancel.html
"PostgreSQL 9.4 - 34.7. Canceling Queries in Progress") /
[9.3](/docs/9.3/libpq-cancel.html "PostgreSQL 9.3 - 34.7. Canceling Queries in
Progress") / [9.2](/docs/9.2/libpq-cancel.html "PostgreSQL 9.2 -
34.7. Canceling Queries in Progress") / [9.1](/docs/9.1/libpq-cancel.html
"PostgreSQL 9.1 - 34.7. Canceling Queries in Progress") /
[9.0](/docs/9.0/libpq-cancel.html "PostgreSQL 9.0 - 34.7. Canceling Queries in
Progress") / [8.4](/docs/8.4/libpq-cancel.html "PostgreSQL 8.4 -
34.7. Canceling Queries in Progress") / [8.3](/docs/8.3/libpq-cancel.html
"PostgreSQL 8.3 - 34.7. Canceling Queries in Progress") /
[8.2](/docs/8.2/libpq-cancel.html "PostgreSQL 8.2 - 34.7. Canceling Queries in
Progress") / [8.1](/docs/8.1/libpq-cancel.html "PostgreSQL 8.1 -
34.7. Canceling Queries in Progress") / [8.0](/docs/8.0/libpq-cancel.html
"PostgreSQL 8.0 - 34.7. Canceling Queries in Progress")

__

34.7. Canceling Queries in Progress  
---  
[Prev](libpq-single-row-mode.html "34.6. Retrieving Query Results Row-by-Row")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-fastpath.html "34.8. The Fast-Path Interface")  
  
* * *

## 34.7. Canceling Queries in Progress #

A client application can request cancellation of a command that is still being
processed by the server, using the functions described in this section.

`PQgetCancel` #

    

Creates a data structure containing the information needed to cancel a command
issued through a particular database connection.

    
    
    PGcancel *PQgetCancel(PGconn *conn);
    

[`PQgetCancel`](libpq-cancel.html#LIBPQ-PQGETCANCEL) creates a `PGcancel`
object given a `PGconn` connection object. It will return `NULL` if the given
_`conn`_ is `NULL` or an invalid connection. The `PGcancel` object is an
opaque structure that is not meant to be accessed directly by the application;
it can only be passed to [`PQcancel`](libpq-cancel.html#LIBPQ-PQCANCEL) or
[`PQfreeCancel`](libpq-cancel.html#LIBPQ-PQFREECANCEL).

`PQfreeCancel` #

    

Frees a data structure created by [`PQgetCancel`](libpq-cancel.html#LIBPQ-
PQGETCANCEL).

    
    
    void PQfreeCancel(PGcancel *cancel);
    

[`PQfreeCancel`](libpq-cancel.html#LIBPQ-PQFREECANCEL) frees a data object
previously created by [`PQgetCancel`](libpq-cancel.html#LIBPQ-PQGETCANCEL).

`PQcancel` #

    

Requests that the server abandon processing of the current command.

    
    
    int PQcancel(PGcancel *cancel, char *errbuf, int errbufsize);
    

The return value is 1 if the cancel request was successfully dispatched and 0
if not. If not, _`errbuf`_ is filled with an explanatory error message.
_`errbuf`_ must be a char array of size _`errbufsize`_ (the recommended size
is 256 bytes).

Successful dispatch is no guarantee that the request will have any effect,
however. If the cancellation is effective, the current command will terminate
early and return an error result. If the cancellation fails (say, because the
server was already done processing the command), then there will be no visible
result at all.

[`PQcancel`](libpq-cancel.html#LIBPQ-PQCANCEL) can safely be invoked from a
signal handler, if the _`errbuf`_ is a local variable in the signal handler.
The `PGcancel` object is read-only as far as [`PQcancel`](libpq-
cancel.html#LIBPQ-PQCANCEL) is concerned, so it can also be invoked from a
thread that is separate from the one manipulating the `PGconn` object.

`PQrequestCancel` #

    

[`PQrequestCancel`](libpq-cancel.html#LIBPQ-PQREQUESTCANCEL) is a deprecated
variant of [`PQcancel`](libpq-cancel.html#LIBPQ-PQCANCEL).

    
    
    int PQrequestCancel(PGconn *conn);
    

Requests that the server abandon processing of the current command. It
operates directly on the `PGconn` object, and in case of failure stores the
error message in the `PGconn` object (whence it can be retrieved by
[`PQerrorMessage`](libpq-status.html#LIBPQ-PQERRORMESSAGE)). Although the
functionality is the same, this approach is not safe within multiple-thread
programs or signal handlers, since it is possible that overwriting the
`PGconn`'s error message will mess up the operation currently in progress on
the connection.

* * *

[Prev](libpq-single-row-mode.html "34.6. Retrieving Query Results Row-by-Row")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](libpq-fastpath.html "34.8. The Fast-Path Interface")  
---|---|---  
34.6. Retrieving Query Results Row-by-Row  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.8. The Fast-Path Interface  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-cancel.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

