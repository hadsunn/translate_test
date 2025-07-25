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

Supported Versions: [Current](/docs/current/libpq-events.html "PostgreSQL 17 -
34.14. Event System") ([17](/docs/17/libpq-events.html "PostgreSQL 17 -
34.14. Event System")) / [16](/docs/16/libpq-events.html "PostgreSQL 16 -
34.14. Event System") / [15](/docs/15/libpq-events.html "PostgreSQL 15 -
34.14. Event System") / [14](/docs/14/libpq-events.html "PostgreSQL 14 -
34.14. Event System") / [13](/docs/13/libpq-events.html "PostgreSQL 13 -
34.14. Event System")

Development Versions: [18](/docs/18/libpq-events.html "PostgreSQL 18 -
34.14. Event System") / [devel](/docs/devel/libpq-events.html "PostgreSQL
devel - 34.14. Event System")

Unsupported versions: [12](/docs/12/libpq-events.html "PostgreSQL 12 -
34.14. Event System") / [11](/docs/11/libpq-events.html "PostgreSQL 11 -
34.14. Event System") / [10](/docs/10/libpq-events.html "PostgreSQL 10 -
34.14. Event System") / [9.6](/docs/9.6/libpq-events.html "PostgreSQL 9.6 -
34.14. Event System") / [9.5](/docs/9.5/libpq-events.html "PostgreSQL 9.5 -
34.14. Event System") / [9.4](/docs/9.4/libpq-events.html "PostgreSQL 9.4 -
34.14. Event System") / [9.3](/docs/9.3/libpq-events.html "PostgreSQL 9.3 -
34.14. Event System") / [9.2](/docs/9.2/libpq-events.html "PostgreSQL 9.2 -
34.14. Event System") / [9.1](/docs/9.1/libpq-events.html "PostgreSQL 9.1 -
34.14. Event System") / [9.0](/docs/9.0/libpq-events.html "PostgreSQL 9.0 -
34.14. Event System") / [8.4](/docs/8.4/libpq-events.html "PostgreSQL 8.4 -
34.14. Event System")

__

34.14. Event System  
---  
[Prev](libpq-notice-processing.html "34.13. Notice Processing")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](libpq-envars.html "34.15. Environment Variables")  
  
* * *

## 34.14. Event System #

[34.14.1. Event Types](libpq-events.html#LIBPQ-EVENTS-TYPES)

[34.14.2. Event Callback Procedure](libpq-events.html#LIBPQ-EVENTS-PROC)

[34.14.3. Event Support Functions](libpq-events.html#LIBPQ-EVENTS-FUNCS)

[34.14.4. Event Example](libpq-events.html#LIBPQ-EVENTS-EXAMPLE)

libpq's event system is designed to notify registered event handlers about
interesting libpq events, such as the creation or destruction of `PGconn` and
`PGresult` objects. A principal use case is that this allows applications to
associate their own data with a `PGconn` or `PGresult` and ensure that that
data is freed at an appropriate time.

Each registered event handler is associated with two pieces of data, known to
libpq only as opaque `void *` pointers. There is a _pass-through_ pointer that
is provided by the application when the event handler is registered with a
`PGconn`. The pass-through pointer never changes for the life of the `PGconn`
and all `PGresult`s generated from it; so if used, it must point to long-lived
data. In addition there is an _instance data_ pointer, which starts out `NULL`
in every `PGconn` and `PGresult`. This pointer can be manipulated using the
[`PQinstanceData`](libpq-events.html#LIBPQ-PQINSTANCEDATA),
[`PQsetInstanceData`](libpq-events.html#LIBPQ-PQSETINSTANCEDATA),
[`PQresultInstanceData`](libpq-events.html#LIBPQ-PQRESULTINSTANCEDATA) and
[`PQresultSetInstanceData`](libpq-events.html#LIBPQ-PQRESULTSETINSTANCEDATA)
functions. Note that unlike the pass-through pointer, instance data of a
`PGconn` is not automatically inherited by `PGresult`s created from it. libpq
does not know what pass-through and instance data pointers point to (if
anything) and will never attempt to free them — that is the responsibility of
the event handler.

### 34.14.1. Event Types #

The enum `PGEventId` names the types of events handled by the event system.
All its values have names beginning with `PGEVT`. For each event type, there
is a corresponding event info structure that carries the parameters passed to
the event handlers. The event types are:

`PGEVT_REGISTER` #

    

The register event occurs when [`PQregisterEventProc`](libpq-
events.html#LIBPQ-PQREGISTEREVENTPROC) is called. It is the ideal time to
initialize any `instanceData` an event procedure may need. Only one register
event will be fired per event handler per connection. If the event procedure
fails (returns zero), the registration is cancelled.

    
    
    typedef struct
    {
        PGconn *conn;
    } PGEventRegister;
    

When a `PGEVT_REGISTER` event is received, the _`evtInfo`_ pointer should be
cast to a `PGEventRegister *`. This structure contains a `PGconn` that should
be in the `CONNECTION_OK` status; guaranteed if one calls
[`PQregisterEventProc`](libpq-events.html#LIBPQ-PQREGISTEREVENTPROC) right
after obtaining a good `PGconn`. When returning a failure code, all cleanup
must be performed as no `PGEVT_CONNDESTROY` event will be sent.

`PGEVT_CONNRESET` #

    

The connection reset event is fired on completion of [`PQreset`](libpq-
connect.html#LIBPQ-PQRESET) or `PQresetPoll`. In both cases, the event is only
fired if the reset was successful. The return value of the event procedure is
ignored in PostgreSQL v15 and later. With earlier versions, however, it's
important to return success (nonzero) or the connection will be aborted.

    
    
    typedef struct
    {
        PGconn *conn;
    } PGEventConnReset;
    

When a `PGEVT_CONNRESET` event is received, the _`evtInfo`_ pointer should be
cast to a `PGEventConnReset *`. Although the contained `PGconn` was just
reset, all event data remains unchanged. This event should be used to
reset/reload/requery any associated `instanceData`. Note that even if the
event procedure fails to process `PGEVT_CONNRESET`, it will still receive a
`PGEVT_CONNDESTROY` event when the connection is closed.

`PGEVT_CONNDESTROY` #

    

The connection destroy event is fired in response to [`PQfinish`](libpq-
connect.html#LIBPQ-PQFINISH). It is the event procedure's responsibility to
properly clean up its event data as libpq has no ability to manage this
memory. Failure to clean up will lead to memory leaks.

    
    
    typedef struct
    {
        PGconn *conn;
    } PGEventConnDestroy;
    

When a `PGEVT_CONNDESTROY` event is received, the _`evtInfo`_ pointer should
be cast to a `PGEventConnDestroy *`. This event is fired prior to
[`PQfinish`](libpq-connect.html#LIBPQ-PQFINISH) performing any other cleanup.
The return value of the event procedure is ignored since there is no way of
indicating a failure from [`PQfinish`](libpq-connect.html#LIBPQ-PQFINISH).
Also, an event procedure failure should not abort the process of cleaning up
unwanted memory.

`PGEVT_RESULTCREATE` #

    

The result creation event is fired in response to any query execution function
that generates a result, including [`PQgetResult`](libpq-async.html#LIBPQ-
PQGETRESULT). This event will only be fired after the result has been created
successfully.

    
    
    typedef struct
    {
        PGconn *conn;
        PGresult *result;
    } PGEventResultCreate;
    

When a `PGEVT_RESULTCREATE` event is received, the _`evtInfo`_ pointer should
be cast to a `PGEventResultCreate *`. The _`conn`_ is the connection used to
generate the result. This is the ideal place to initialize any `instanceData`
that needs to be associated with the result. If an event procedure fails
(returns zero), that event procedure will be ignored for the remaining
lifetime of the result; that is, it will not receive `PGEVT_RESULTCOPY` or
`PGEVT_RESULTDESTROY` events for this result or results copied from it.

`PGEVT_RESULTCOPY` #

    

The result copy event is fired in response to [`PQcopyResult`](libpq-
misc.html#LIBPQ-PQCOPYRESULT). This event will only be fired after the copy is
complete. Only event procedures that have successfully handled the
`PGEVT_RESULTCREATE` or `PGEVT_RESULTCOPY` event for the source result will
receive `PGEVT_RESULTCOPY` events.

    
    
    typedef struct
    {
        const PGresult *src;
        PGresult *dest;
    } PGEventResultCopy;
    

When a `PGEVT_RESULTCOPY` event is received, the _`evtInfo`_ pointer should be
cast to a `PGEventResultCopy *`. The _`src`_ result is what was copied while
the _`dest`_ result is the copy destination. This event can be used to provide
a deep copy of `instanceData`, since `PQcopyResult` cannot do that. If an
event procedure fails (returns zero), that event procedure will be ignored for
the remaining lifetime of the new result; that is, it will not receive
`PGEVT_RESULTCOPY` or `PGEVT_RESULTDESTROY` events for that result or results
copied from it.

`PGEVT_RESULTDESTROY` #

    

The result destroy event is fired in response to a [`PQclear`](libpq-
exec.html#LIBPQ-PQCLEAR). It is the event procedure's responsibility to
properly clean up its event data as libpq has no ability to manage this
memory. Failure to clean up will lead to memory leaks.

    
    
    typedef struct
    {
        PGresult *result;
    } PGEventResultDestroy;
    

When a `PGEVT_RESULTDESTROY` event is received, the _`evtInfo`_ pointer should
be cast to a `PGEventResultDestroy *`. This event is fired prior to
[`PQclear`](libpq-exec.html#LIBPQ-PQCLEAR) performing any other cleanup. The
return value of the event procedure is ignored since there is no way of
indicating a failure from [`PQclear`](libpq-exec.html#LIBPQ-PQCLEAR). Also, an
event procedure failure should not abort the process of cleaning up unwanted
memory.

### 34.14.2. Event Callback Procedure #

`PGEventProc` #

    

`PGEventProc` is a typedef for a pointer to an event procedure, that is, the
user callback function that receives events from libpq. The signature of an
event procedure must be

    
    
    int eventproc(PGEventId evtId, void *evtInfo, void *passThrough)
    

The _`evtId`_ parameter indicates which `PGEVT` event occurred. The
_`evtInfo`_ pointer must be cast to the appropriate structure type to obtain
further information about the event. The _`passThrough`_ parameter is the
pointer provided to [`PQregisterEventProc`](libpq-events.html#LIBPQ-
PQREGISTEREVENTPROC) when the event procedure was registered. The function
should return a non-zero value if it succeeds and zero if it fails.

A particular event procedure can be registered only once in any `PGconn`. This
is because the address of the procedure is used as a lookup key to identify
the associated instance data.

### Caution

On Windows, functions can have two different addresses: one visible from
outside a DLL and another visible from inside the DLL. One should be careful
that only one of these addresses is used with libpq's event-procedure
functions, else confusion will result. The simplest rule for writing code that
will work is to ensure that event procedures are declared `static`. If the
procedure's address must be available outside its own source file, expose a
separate function to return the address.

### 34.14.3. Event Support Functions #

`PQregisterEventProc` #

    

Registers an event callback procedure with libpq.

    
    
    int PQregisterEventProc(PGconn *conn, PGEventProc proc,
                            const char *name, void *passThrough);
    

An event procedure must be registered once on each `PGconn` you want to
receive events about. There is no limit, other than memory, on the number of
event procedures that can be registered with a connection. The function
returns a non-zero value if it succeeds and zero if it fails.

The _`proc`_ argument will be called when a libpq event is fired. Its memory
address is also used to lookup `instanceData`. The _`name`_ argument is used
to refer to the event procedure in error messages. This value cannot be `NULL`
or a zero-length string. The name string is copied into the `PGconn`, so what
is passed need not be long-lived. The _`passThrough`_ pointer is passed to the
_`proc`_ whenever an event occurs. This argument can be `NULL`.

`PQsetInstanceData` #

    

Sets the connection _`conn`_ 's `instanceData` for procedure _`proc`_ to
_`data`_. This returns non-zero for success and zero for failure. (Failure is
only possible if _`proc`_ has not been properly registered in _`conn`_.)

    
    
    int PQsetInstanceData(PGconn *conn, PGEventProc proc, void *data);
    

`PQinstanceData` #

    

Returns the connection _`conn`_ 's `instanceData` associated with procedure
_`proc`_ , or `NULL` if there is none.

    
    
    void *PQinstanceData(const PGconn *conn, PGEventProc proc);
    

`PQresultSetInstanceData` #

    

Sets the result's `instanceData` for _`proc`_ to _`data`_. This returns non-
zero for success and zero for failure. (Failure is only possible if _`proc`_
has not been properly registered in the result.)

    
    
    int PQresultSetInstanceData(PGresult *res, PGEventProc proc, void *data);
    

Beware that any storage represented by _`data`_ will not be accounted for by
[`PQresultMemorySize`](libpq-misc.html#LIBPQ-PQRESULTMEMORYSIZE), unless it is
allocated using [`PQresultAlloc`](libpq-misc.html#LIBPQ-PQRESULTALLOC). (Doing
so is recommendable because it eliminates the need to free such storage
explicitly when the result is destroyed.)

`PQresultInstanceData` #

    

Returns the result's `instanceData` associated with _`proc`_ , or `NULL` if
there is none.

    
    
    void *PQresultInstanceData(const PGresult *res, PGEventProc proc);
    

### 34.14.4. Event Example #

Here is a skeleton example of managing private data associated with libpq
connections and results.

    
    
    
    /* required header for libpq events (note: includes libpq-fe.h) */
    #include <libpq-events.h>
    
    /* The instanceData */
    typedef struct
    {
        int n;
        char *str;
    } mydata;
    
    /* PGEventProc */
    static int myEventProc(PGEventId evtId, void *evtInfo, void *passThrough);
    
    int
    main(void)
    {
        mydata *data;
        PGresult *res;
        PGconn *conn =
            PQconnectdb("dbname=postgres options=-csearch_path=");
    
        if (PQstatus(conn) != CONNECTION_OK)
        {
            /* PQerrorMessage's result includes a trailing newline */
            fprintf(stderr, "%s", PQerrorMessage(conn));
            PQfinish(conn);
            return 1;
        }
    
        /* called once on any connection that should receive events.
         * Sends a PGEVT_REGISTER to myEventProc.
         */
        if (!PQregisterEventProc(conn, myEventProc, "mydata_proc", NULL))
        {
            fprintf(stderr, "Cannot register PGEventProc\n");
            PQfinish(conn);
            return 1;
        }
    
        /* conn instanceData is available */
        data = PQinstanceData(conn, myEventProc);
    
        /* Sends a PGEVT_RESULTCREATE to myEventProc */
        res = PQexec(conn, "SELECT 1 + 1");
    
        /* result instanceData is available */
        data = PQresultInstanceData(res, myEventProc);
    
        /* If PG_COPYRES_EVENTS is used, sends a PGEVT_RESULTCOPY to myEventProc */
        res_copy = PQcopyResult(res, PG_COPYRES_TUPLES | PG_COPYRES_EVENTS);
    
        /* result instanceData is available if PG_COPYRES_EVENTS was
         * used during the PQcopyResult call.
         */
        data = PQresultInstanceData(res_copy, myEventProc);
    
        /* Both clears send a PGEVT_RESULTDESTROY to myEventProc */
        PQclear(res);
        PQclear(res_copy);
    
        /* Sends a PGEVT_CONNDESTROY to myEventProc */
        PQfinish(conn);
    
        return 0;
    }
    
    static int
    myEventProc(PGEventId evtId, void *evtInfo, void *passThrough)
    {
        switch (evtId)
        {
            case PGEVT_REGISTER:
            {
                PGEventRegister *e = (PGEventRegister *)evtInfo;
                mydata *data = get_mydata(e->conn);
    
                /* associate app specific data with connection */
                PQsetInstanceData(e->conn, myEventProc, data);
                break;
            }
    
            case PGEVT_CONNRESET:
            {
                PGEventConnReset *e = (PGEventConnReset *)evtInfo;
                mydata *data = PQinstanceData(e->conn, myEventProc);
    
                if (data)
                  memset(data, 0, sizeof(mydata));
                break;
            }
    
            case PGEVT_CONNDESTROY:
            {
                PGEventConnDestroy *e = (PGEventConnDestroy *)evtInfo;
                mydata *data = PQinstanceData(e->conn, myEventProc);
    
                /* free instance data because the conn is being destroyed */
                if (data)
                  free_mydata(data);
                break;
            }
    
            case PGEVT_RESULTCREATE:
            {
                PGEventResultCreate *e = (PGEventResultCreate *)evtInfo;
                mydata *conn_data = PQinstanceData(e->conn, myEventProc);
                mydata *res_data = dup_mydata(conn_data);
    
                /* associate app specific data with result (copy it from conn) */
                PQresultSetInstanceData(e->result, myEventProc, res_data);
                break;
            }
    
            case PGEVT_RESULTCOPY:
            {
                PGEventResultCopy *e = (PGEventResultCopy *)evtInfo;
                mydata *src_data = PQresultInstanceData(e->src, myEventProc);
                mydata *dest_data = dup_mydata(src_data);
    
                /* associate app specific data with result (copy it from a result) */
                PQresultSetInstanceData(e->dest, myEventProc, dest_data);
                break;
            }
    
            case PGEVT_RESULTDESTROY:
            {
                PGEventResultDestroy *e = (PGEventResultDestroy *)evtInfo;
                mydata *data = PQresultInstanceData(e->result, myEventProc);
    
                /* free instance data because the result is being destroyed */
                if (data)
                  free_mydata(data);
                break;
            }
    
            /* unknown event ID, just return true. */
            default:
                break;
        }
    
        return true; /* event processing succeeded */
    }
    
    

* * *

[Prev](libpq-notice-processing.html "34.13. Notice Processing")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](libpq-envars.html "34.15. Environment Variables")  
---|---|---  
34.13. Notice Processing  | [Home](index.html "PostgreSQL 16.9 Documentation") |  34.15. Environment Variables  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-events.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

