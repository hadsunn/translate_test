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

Supported Versions: [Current](/docs/current/libpq-fastpath.html "PostgreSQL 17
- 34.8. The Fast-Path Interface") ([17](/docs/17/libpq-fastpath.html
"PostgreSQL 17 - 34.8. The Fast-Path Interface")) / [16](/docs/16/libpq-
fastpath.html "PostgreSQL 16 - 34.8. The Fast-Path Interface") /
[15](/docs/15/libpq-fastpath.html "PostgreSQL 15 - 34.8. The Fast-Path
Interface") / [14](/docs/14/libpq-fastpath.html "PostgreSQL 14 - 34.8. The
Fast-Path Interface") / [13](/docs/13/libpq-fastpath.html "PostgreSQL 13 -
34.8. The Fast-Path Interface")

Development Versions: [18](/docs/18/libpq-fastpath.html "PostgreSQL 18 -
34.8. The Fast-Path Interface") / [devel](/docs/devel/libpq-fastpath.html
"PostgreSQL devel - 34.8. The Fast-Path Interface")

Unsupported versions: [12](/docs/12/libpq-fastpath.html "PostgreSQL 12 -
34.8. The Fast-Path Interface") / [11](/docs/11/libpq-fastpath.html
"PostgreSQL 11 - 34.8. The Fast-Path Interface") / [10](/docs/10/libpq-
fastpath.html "PostgreSQL 10 - 34.8. The Fast-Path Interface") /
[9.6](/docs/9.6/libpq-fastpath.html "PostgreSQL 9.6 - 34.8. The Fast-Path
Interface") / [9.5](/docs/9.5/libpq-fastpath.html "PostgreSQL 9.5 - 34.8. The
Fast-Path Interface") / [9.4](/docs/9.4/libpq-fastpath.html "PostgreSQL 9.4 -
34.8. The Fast-Path Interface") / [9.3](/docs/9.3/libpq-fastpath.html
"PostgreSQL 9.3 - 34.8. The Fast-Path Interface") / [9.2](/docs/9.2/libpq-
fastpath.html "PostgreSQL 9.2 - 34.8. The Fast-Path Interface") /
[9.1](/docs/9.1/libpq-fastpath.html "PostgreSQL 9.1 - 34.8. The Fast-Path
Interface") / [9.0](/docs/9.0/libpq-fastpath.html "PostgreSQL 9.0 - 34.8. The
Fast-Path Interface") / [8.4](/docs/8.4/libpq-fastpath.html "PostgreSQL 8.4 -
34.8. The Fast-Path Interface") / [8.3](/docs/8.3/libpq-fastpath.html
"PostgreSQL 8.3 - 34.8. The Fast-Path Interface") / [8.2](/docs/8.2/libpq-
fastpath.html "PostgreSQL 8.2 - 34.8. The Fast-Path Interface") /
[8.1](/docs/8.1/libpq-fastpath.html "PostgreSQL 8.1 - 34.8. The Fast-Path
Interface") / [8.0](/docs/8.0/libpq-fastpath.html "PostgreSQL 8.0 - 34.8. The
Fast-Path Interface") / [7.4](/docs/7.4/libpq-fastpath.html "PostgreSQL 7.4 -
34.8. The Fast-Path Interface") / [7.3](/docs/7.3/libpq-fastpath.html
"PostgreSQL 7.3 - 34.8. The Fast-Path Interface") / [7.2](/docs/7.2/libpq-
fastpath.html "PostgreSQL 7.2 - 34.8. The Fast-Path Interface") /
[7.1](/docs/7.1/libpq-fastpath.html "PostgreSQL 7.1 - 34.8. The Fast-Path
Interface")

__

34.8. The Fast-Path Interface  
---  
[Prev](libpq-cancel.html "34.7. Canceling Queries in Progress")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-notify.html "34.9. Asynchronous Notification")  
  
* * *

## 34.8. The Fast-Path Interface #

PostgreSQL provides a fast-path interface to send simple function calls to the
server.

### Tip

This interface is somewhat obsolete, as one can achieve similar performance
and greater functionality by setting up a prepared statement to define the
function call. Then, executing the statement with binary transmission of
parameters and results substitutes for a fast-path function call.

The function `PQfn` requests execution of a server function via the fast-path
interface:

    
    
    PGresult *PQfn(PGconn *conn,
                   int fnid,
                   int *result_buf,
                   int *result_len,
                   int result_is_int,
                   const PQArgBlock *args,
                   int nargs);
    
    typedef struct
    {
        int len;
        int isint;
        union
        {
            int *ptr;
            int integer;
        } u;
    } PQArgBlock;
    

The _`fnid`_ argument is the OID of the function to be executed. _`args`_ and
_`nargs`_ define the parameters to be passed to the function; they must match
the declared function argument list. When the _`isint`_ field of a parameter
structure is true, the _`u.integer`_ value is sent to the server as an integer
of the indicated length (this must be 2 or 4 bytes); proper byte-swapping
occurs. When _`isint`_ is false, the indicated number of bytes at _`*u.ptr`_
are sent with no processing; the data must be in the format expected by the
server for binary transmission of the function's argument data type. (The
declaration of _`u.ptr`_ as being of type `int *` is historical; it would be
better to consider it `void *`.) _`result_buf`_ points to the buffer in which
to place the function's return value. The caller must have allocated
sufficient space to store the return value. (There is no check!) The actual
result length in bytes will be returned in the integer pointed to by
_`result_len`_. If a 2- or 4-byte integer result is expected, set
_`result_is_int`_ to 1, otherwise set it to 0. Setting _`result_is_int`_ to 1
causes libpq to byte-swap the value if necessary, so that it is delivered as a
proper `int` value for the client machine; note that a 4-byte integer is
delivered into _`*result_buf`_ for either allowed result size. When
_`result_is_int`_ is 0, the binary-format byte string sent by the server is
returned unmodified. (In this case it's better to consider _`result_buf`_ as
being of type `void *`.)

`PQfn` always returns a valid `PGresult` pointer, with status
`PGRES_COMMAND_OK` for success or `PGRES_FATAL_ERROR` if some problem was
encountered. The result status should be checked before the result is used.
The caller is responsible for freeing the `PGresult` with [`PQclear`](libpq-
exec.html#LIBPQ-PQCLEAR) when it is no longer needed.

To pass a NULL argument to the function, set the _`len`_ field of that
parameter structure to `-1`; the _`isint`_ and _`u`_ fields are then
irrelevant.

If the function returns NULL, _`*result_len`_ is set to `-1`, and
_`*result_buf`_ is not modified.

Note that it is not possible to handle set-valued results when using this
interface. Also, the function must be a plain function, not an aggregate,
window function, or procedure.

* * *

[Prev](libpq-cancel.html "34.7. Canceling Queries in Progress")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](libpq-notify.html "34.9. Asynchronous Notification")  
---|---|---  
34.7. Canceling Queries in Progress  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.9. Asynchronous Notification  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-fastpath.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

