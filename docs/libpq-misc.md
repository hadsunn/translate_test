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

Supported Versions: [Current](/docs/current/libpq-misc.html "PostgreSQL 17 -
34.12. Miscellaneous Functions") ([17](/docs/17/libpq-misc.html "PostgreSQL 17
- 34.12. Miscellaneous Functions")) / [16](/docs/16/libpq-misc.html
"PostgreSQL 16 - 34.12. Miscellaneous Functions") / [15](/docs/15/libpq-
misc.html "PostgreSQL 15 - 34.12. Miscellaneous Functions") /
[14](/docs/14/libpq-misc.html "PostgreSQL 14 - 34.12. Miscellaneous
Functions") / [13](/docs/13/libpq-misc.html "PostgreSQL 13 -
34.12. Miscellaneous Functions")

Development Versions: [18](/docs/18/libpq-misc.html "PostgreSQL 18 -
34.12. Miscellaneous Functions") / [devel](/docs/devel/libpq-misc.html
"PostgreSQL devel - 34.12. Miscellaneous Functions")

Unsupported versions: [12](/docs/12/libpq-misc.html "PostgreSQL 12 -
34.12. Miscellaneous Functions") / [11](/docs/11/libpq-misc.html "PostgreSQL
11 - 34.12. Miscellaneous Functions") / [10](/docs/10/libpq-misc.html
"PostgreSQL 10 - 34.12. Miscellaneous Functions") / [9.6](/docs/9.6/libpq-
misc.html "PostgreSQL 9.6 - 34.12. Miscellaneous Functions") /
[9.5](/docs/9.5/libpq-misc.html "PostgreSQL 9.5 - 34.12. Miscellaneous
Functions") / [9.4](/docs/9.4/libpq-misc.html "PostgreSQL 9.4 -
34.12. Miscellaneous Functions") / [9.3](/docs/9.3/libpq-misc.html "PostgreSQL
9.3 - 34.12. Miscellaneous Functions") / [9.2](/docs/9.2/libpq-misc.html
"PostgreSQL 9.2 - 34.12. Miscellaneous Functions") / [9.1](/docs/9.1/libpq-
misc.html "PostgreSQL 9.1 - 34.12. Miscellaneous Functions") /
[9.0](/docs/9.0/libpq-misc.html "PostgreSQL 9.0 - 34.12. Miscellaneous
Functions") / [8.4](/docs/8.4/libpq-misc.html "PostgreSQL 8.4 -
34.12. Miscellaneous Functions") / [8.3](/docs/8.3/libpq-misc.html "PostgreSQL
8.3 - 34.12. Miscellaneous Functions") / [8.2](/docs/8.2/libpq-misc.html
"PostgreSQL 8.2 - 34.12. Miscellaneous Functions")

__

34.12. Miscellaneous Functions  
---  
[Prev](libpq-control.html "34.11. Control Functions")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-notice-processing.html "34.13. Notice Processing")  
  
* * *

## 34.12. Miscellaneous Functions #

As always, there are some functions that just don't fit anywhere.

`PQfreemem` #

    

Frees memory allocated by libpq.

    
    
    void PQfreemem(void *ptr);
    

Frees memory allocated by libpq, particularly [`PQescapeByteaConn`](libpq-
exec.html#LIBPQ-PQESCAPEBYTEACONN), [`PQescapeBytea`](libpq-exec.html#LIBPQ-
PQESCAPEBYTEA), [`PQunescapeBytea`](libpq-exec.html#LIBPQ-PQUNESCAPEBYTEA),
and `PQnotifies`. It is particularly important that this function, rather than
`free()`, be used on Microsoft Windows. This is because allocating memory in a
DLL and releasing it in the application works only if multithreaded/single-
threaded, release/debug, and static/dynamic flags are the same for the DLL and
the application. On non-Microsoft Windows platforms, this function is the same
as the standard library function `free()`.

`PQconninfoFree` #

    

Frees the data structures allocated by [`PQconndefaults`](libpq-
connect.html#LIBPQ-PQCONNDEFAULTS) or [`PQconninfoParse`](libpq-
connect.html#LIBPQ-PQCONNINFOPARSE).

    
    
    void PQconninfoFree(PQconninfoOption *connOptions);
    

If the argument is a `NULL` pointer, no operation is performed.

A simple [`PQfreemem`](libpq-misc.html#LIBPQ-PQFREEMEM) will not do for this,
since the array contains references to subsidiary strings.

`PQencryptPasswordConn` #

    

Prepares the encrypted form of a PostgreSQL password.

    
    
    char *PQencryptPasswordConn(PGconn *conn, const char *passwd, const char *user, const char *algorithm);
    

This function is intended to be used by client applications that wish to send
commands like `ALTER USER joe PASSWORD 'pwd'`. It is good practice not to send
the original cleartext password in such a command, because it might be exposed
in command logs, activity displays, and so on. Instead, use this function to
convert the password to encrypted form before it is sent.

The _`passwd`_ and _`user`_ arguments are the cleartext password, and the SQL
name of the user it is for. _`algorithm`_ specifies the encryption algorithm
to use to encrypt the password. Currently supported algorithms are `md5` and
`scram-sha-256` (`on` and `off` are also accepted as aliases for `md5`, for
compatibility with older server versions). Note that support for `scram-
sha-256` was introduced in PostgreSQL version 10, and will not work correctly
with older server versions. If _`algorithm`_ is `NULL`, this function will
query the server for the current value of the [password_encryption](runtime-
config-connection.html#GUC-PASSWORD-ENCRYPTION) setting. That can block, and
will fail if the current transaction is aborted, or if the connection is busy
executing another query. If you wish to use the default algorithm for the
server but want to avoid blocking, query `password_encryption` yourself before
calling [`PQencryptPasswordConn`](libpq-misc.html#LIBPQ-
PQENCRYPTPASSWORDCONN), and pass that value as the _`algorithm`_.

The return value is a string allocated by `malloc`. The caller can assume the
string doesn't contain any special characters that would require escaping. Use
[`PQfreemem`](libpq-misc.html#LIBPQ-PQFREEMEM) to free the result when done
with it. On error, returns `NULL`, and a suitable message is stored in the
connection object.

`PQencryptPassword` #

    

Prepares the md5-encrypted form of a PostgreSQL password.

    
    
    char *PQencryptPassword(const char *passwd, const char *user);
    

[`PQencryptPassword`](libpq-misc.html#LIBPQ-PQENCRYPTPASSWORD) is an older,
deprecated version of [`PQencryptPasswordConn`](libpq-misc.html#LIBPQ-
PQENCRYPTPASSWORDCONN). The difference is that [`PQencryptPassword`](libpq-
misc.html#LIBPQ-PQENCRYPTPASSWORD) does not require a connection object, and
`md5` is always used as the encryption algorithm.

`PQmakeEmptyPGresult` #

    

Constructs an empty `PGresult` object with the given status.

    
    
    PGresult *PQmakeEmptyPGresult(PGconn *conn, ExecStatusType status);
    

This is libpq's internal function to allocate and initialize an empty
`PGresult` object. This function returns `NULL` if memory could not be
allocated. It is exported because some applications find it useful to generate
result objects (particularly objects with error status) themselves. If
_`conn`_ is not null and _`status`_ indicates an error, the current error
message of the specified connection is copied into the `PGresult`. Also, if
_`conn`_ is not null, any event procedures registered in the connection are
copied into the `PGresult`. (They do not get `PGEVT_RESULTCREATE` calls, but
see [`PQfireResultCreateEvents`](libpq-misc.html#LIBPQ-
PQFIRERESULTCREATEEVENTS).) Note that [`PQclear`](libpq-exec.html#LIBPQ-
PQCLEAR) should eventually be called on the object, just as with a `PGresult`
returned by libpq itself.

`PQfireResultCreateEvents` #

    

Fires a `PGEVT_RESULTCREATE` event (see [Section 34.14](libpq-events.html
"34.14. Event System")) for each event procedure registered in the `PGresult`
object. Returns non-zero for success, zero if any event procedure fails.

    
    
    int PQfireResultCreateEvents(PGconn *conn, PGresult *res);
    

The `conn` argument is passed through to event procedures but not used
directly. It can be `NULL` if the event procedures won't use it.

Event procedures that have already received a `PGEVT_RESULTCREATE` or
`PGEVT_RESULTCOPY` event for this object are not fired again.

The main reason that this function is separate from
[`PQmakeEmptyPGresult`](libpq-misc.html#LIBPQ-PQMAKEEMPTYPGRESULT) is that it
is often appropriate to create a `PGresult` and fill it with data before
invoking the event procedures.

`PQcopyResult` #

    

Makes a copy of a `PGresult` object. The copy is not linked to the source
result in any way and [`PQclear`](libpq-exec.html#LIBPQ-PQCLEAR) must be
called when the copy is no longer needed. If the function fails, `NULL` is
returned.

    
    
    PGresult *PQcopyResult(const PGresult *src, int flags);
    

This is not intended to make an exact copy. The returned result is always put
into `PGRES_TUPLES_OK` status, and does not copy any error message in the
source. (It does copy the command status string, however.) The _`flags`_
argument determines what else is copied. It is a bitwise OR of several flags.
`PG_COPYRES_ATTRS` specifies copying the source result's attributes (column
definitions). `PG_COPYRES_TUPLES` specifies copying the source result's
tuples. (This implies copying the attributes, too.) `PG_COPYRES_NOTICEHOOKS`
specifies copying the source result's notify hooks. `PG_COPYRES_EVENTS`
specifies copying the source result's events. (But any instance data
associated with the source is not copied.) The event procedures receive
`PGEVT_RESULTCOPY` events.

`PQsetResultAttrs` #

    

Sets the attributes of a `PGresult` object.

    
    
    int PQsetResultAttrs(PGresult *res, int numAttributes, PGresAttDesc *attDescs);
    

The provided _`attDescs`_ are copied into the result. If the _`attDescs`_
pointer is `NULL` or _`numAttributes`_ is less than one, the request is
ignored and the function succeeds. If _`res`_ already contains attributes, the
function will fail. If the function fails, the return value is zero. If the
function succeeds, the return value is non-zero.

`PQsetvalue` #

    

Sets a tuple field value of a `PGresult` object.

    
    
    int PQsetvalue(PGresult *res, int tup_num, int field_num, char *value, int len);
    

The function will automatically grow the result's internal tuples array as
needed. However, the _`tup_num`_ argument must be less than or equal to
[`PQntuples`](libpq-exec.html#LIBPQ-PQNTUPLES), meaning this function can only
grow the tuples array one tuple at a time. But any field of any existing tuple
can be modified in any order. If a value at _`field_num`_ already exists, it
will be overwritten. If _`len`_ is -1 or _`value`_ is `NULL`, the field value
will be set to an SQL null value. The _`value`_ is copied into the result's
private storage, thus is no longer needed after the function returns. If the
function fails, the return value is zero. If the function succeeds, the return
value is non-zero.

`PQresultAlloc` #

    

Allocate subsidiary storage for a `PGresult` object.

    
    
    void *PQresultAlloc(PGresult *res, size_t nBytes);
    

Any memory allocated with this function will be freed when _`res`_ is cleared.
If the function fails, the return value is `NULL`. The result is guaranteed to
be adequately aligned for any type of data, just as for `malloc`.

`PQresultMemorySize` #

    

Retrieves the number of bytes allocated for a `PGresult` object.

    
    
    size_t PQresultMemorySize(const PGresult *res);
    

This value is the sum of all `malloc` requests associated with the `PGresult`
object, that is, all the space that will be freed by [`PQclear`](libpq-
exec.html#LIBPQ-PQCLEAR). This information can be useful for managing memory
consumption.

`PQlibVersion` #

    

Return the version of libpq that is being used.

    
    
    int PQlibVersion(void);
    

The result of this function can be used to determine, at run time, whether
specific functionality is available in the currently loaded version of libpq.
The function can be used, for example, to determine which connection options
are available in [`PQconnectdb`](libpq-connect.html#LIBPQ-PQCONNECTDB).

The result is formed by multiplying the library's major version number by
10000 and adding the minor version number. For example, version 10.1 will be
returned as 100001, and version 11.0 will be returned as 110000.

Prior to major version 10, PostgreSQL used three-part version numbers in which
the first two parts together represented the major version. For those
versions, [`PQlibVersion`](libpq-misc.html#LIBPQ-PQLIBVERSION) uses two digits
for each part; for example version 9.1.5 will be returned as 90105, and
version 9.2.0 will be returned as 90200.

Therefore, for purposes of determining feature compatibility, applications
should divide the result of [`PQlibVersion`](libpq-misc.html#LIBPQ-
PQLIBVERSION) by 100 not 10000 to determine a logical major version number. In
all release series, only the last two digits differ between minor releases
(bug-fix releases).

### Note

This function appeared in PostgreSQL version 9.1, so it cannot be used to
detect required functionality in earlier versions, since calling it will
create a link dependency on version 9.1 or later.

* * *

[Prev](libpq-control.html "34.11. Control Functions")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](libpq-notice-processing.html "34.13. Notice Processing")  
---|---|---  
34.11. Control Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.13. Notice Processing  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-misc.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

