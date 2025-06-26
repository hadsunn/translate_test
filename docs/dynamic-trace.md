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

Supported Versions: [Current](/docs/current/dynamic-trace.html "PostgreSQL 17
- 28.5. Dynamic Tracing") ([17](/docs/17/dynamic-trace.html "PostgreSQL 17 -
28.5. Dynamic Tracing")) / [16](/docs/16/dynamic-trace.html "PostgreSQL 16 -
28.5. Dynamic Tracing") / [15](/docs/15/dynamic-trace.html "PostgreSQL 15 -
28.5. Dynamic Tracing") / [14](/docs/14/dynamic-trace.html "PostgreSQL 14 -
28.5. Dynamic Tracing") / [13](/docs/13/dynamic-trace.html "PostgreSQL 13 -
28.5. Dynamic Tracing")

Development Versions: [18](/docs/18/dynamic-trace.html "PostgreSQL 18 -
28.5. Dynamic Tracing") / [devel](/docs/devel/dynamic-trace.html "PostgreSQL
devel - 28.5. Dynamic Tracing")

Unsupported versions: [12](/docs/12/dynamic-trace.html "PostgreSQL 12 -
28.5. Dynamic Tracing") / [11](/docs/11/dynamic-trace.html "PostgreSQL 11 -
28.5. Dynamic Tracing") / [10](/docs/10/dynamic-trace.html "PostgreSQL 10 -
28.5. Dynamic Tracing") / [9.6](/docs/9.6/dynamic-trace.html "PostgreSQL 9.6 -
28.5. Dynamic Tracing") / [9.5](/docs/9.5/dynamic-trace.html "PostgreSQL 9.5 -
28.5. Dynamic Tracing") / [9.4](/docs/9.4/dynamic-trace.html "PostgreSQL 9.4 -
28.5. Dynamic Tracing") / [9.3](/docs/9.3/dynamic-trace.html "PostgreSQL 9.3 -
28.5. Dynamic Tracing") / [9.2](/docs/9.2/dynamic-trace.html "PostgreSQL 9.2 -
28.5. Dynamic Tracing") / [9.1](/docs/9.1/dynamic-trace.html "PostgreSQL 9.1 -
28.5. Dynamic Tracing") / [9.0](/docs/9.0/dynamic-trace.html "PostgreSQL 9.0 -
28.5. Dynamic Tracing") / [8.4](/docs/8.4/dynamic-trace.html "PostgreSQL 8.4 -
28.5. Dynamic Tracing") / [8.3](/docs/8.3/dynamic-trace.html "PostgreSQL 8.3 -
28.5. Dynamic Tracing") / [8.2](/docs/8.2/dynamic-trace.html "PostgreSQL 8.2 -
28.5. Dynamic Tracing")

__

28.5. Dynamic Tracing  
---  
[Prev](progress-reporting.html "28.4. Progress Reporting")  | [Up](monitoring.html "Chapter 28. Monitoring Database Activity") | Chapter 28. Monitoring Database Activity | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](diskusage.html "Chapter 29. Monitoring Disk Usage")  
  
* * *

## 28.5. Dynamic Tracing #

[28.5.1. Compiling for Dynamic Tracing](dynamic-trace.html#COMPILING-FOR-
TRACE)

[28.5.2. Built-in Probes](dynamic-trace.html#TRACE-POINTS)

[28.5.3. Using Probes](dynamic-trace.html#USING-TRACE-POINTS)

[28.5.4. Defining New Probes](dynamic-trace.html#DEFINING-TRACE-POINTS)

PostgreSQL provides facilities to support dynamic tracing of the database
server. This allows an external utility to be called at specific points in the
code and thereby trace execution.

A number of probes or trace points are already inserted into the source code.
These probes are intended to be used by database developers and
administrators. By default the probes are not compiled into PostgreSQL; the
user needs to explicitly tell the configure script to make the probes
available.

Currently, the [DTrace](https://en.wikipedia.org/wiki/DTrace) utility is
supported, which, at the time of this writing, is available on Solaris, macOS,
FreeBSD, NetBSD, and Oracle Linux. The
[SystemTap](https://sourceware.org/systemtap/) project for Linux provides a
DTrace equivalent and can also be used. Supporting other dynamic tracing
utilities is theoretically possible by changing the definitions for the macros
in `src/include/utils/probes.h`.

### 28.5.1. Compiling for Dynamic Tracing #

By default, probes are not available, so you will need to explicitly tell the
configure script to make the probes available in PostgreSQL. To include DTrace
support specify `--enable-dtrace` to configure. See [Section
17.3.3.6](install-make.html#CONFIGURE-OPTIONS-DEVEL "17.3.3.6. Developer
Options") for further information.

### 28.5.2. Built-in Probes #

A number of standard probes are provided in the source code, as shown in
[Table 28.48](dynamic-trace.html#DTRACE-PROBE-POINT-TABLE "Table 28.48. Built-
in DTrace Probes"); [Table 28.49](dynamic-trace.html#TYPEDEFS-TABLE
"Table 28.49. Defined Types Used in Probe Parameters") shows the types used in
the probes. More probes can certainly be added to enhance PostgreSQL's
observability.

**Table  28.48. Built-in DTrace Probes**

Name | Parameters | Description  
---|---|---  
`transaction-start` | `(LocalTransactionId)` | Probe that fires at the start of a new transaction. arg0 is the transaction ID.  
`transaction-commit` | `(LocalTransactionId)` | Probe that fires when a transaction completes successfully. arg0 is the transaction ID.  
`transaction-abort` | `(LocalTransactionId)` | Probe that fires when a transaction completes unsuccessfully. arg0 is the transaction ID.  
`query-start` | `(const char *)` | Probe that fires when the processing of a query is started. arg0 is the query string.  
`query-done` | `(const char *)` | Probe that fires when the processing of a query is complete. arg0 is the query string.  
`query-parse-start` | `(const char *)` | Probe that fires when the parsing of a query is started. arg0 is the query string.  
`query-parse-done` | `(const char *)` | Probe that fires when the parsing of a query is complete. arg0 is the query string.  
`query-rewrite-start` | `(const char *)` | Probe that fires when the rewriting of a query is started. arg0 is the query string.  
`query-rewrite-done` | `(const char *)` | Probe that fires when the rewriting of a query is complete. arg0 is the query string.  
`query-plan-start` | `()` | Probe that fires when the planning of a query is started.  
`query-plan-done` | `()` | Probe that fires when the planning of a query is complete.  
`query-execute-start` | `()` | Probe that fires when the execution of a query is started.  
`query-execute-done` | `()` | Probe that fires when the execution of a query is complete.  
`statement-status` | `(const char *)` | Probe that fires anytime the server process updates its `pg_stat_activity`.`status`. arg0 is the new status string.  
`checkpoint-start` | `(int)` | Probe that fires when a checkpoint is started. arg0 holds the bitwise flags used to distinguish different checkpoint types, such as shutdown, immediate or force.  
`checkpoint-done` | `(int, int, int, int, int)` | Probe that fires when a checkpoint is complete. (The probes listed next fire in sequence during checkpoint processing.) arg0 is the number of buffers written. arg1 is the total number of buffers. arg2, arg3 and arg4 contain the number of WAL files added, removed and recycled respectively.  
`clog-checkpoint-start` | `(bool)` | Probe that fires when the CLOG portion of a checkpoint is started. arg0 is true for normal checkpoint, false for shutdown checkpoint.  
`clog-checkpoint-done` | `(bool)` | Probe that fires when the CLOG portion of a checkpoint is complete. arg0 has the same meaning as for `clog-checkpoint-start`.  
`subtrans-checkpoint-start` | `(bool)` | Probe that fires when the SUBTRANS portion of a checkpoint is started. arg0 is true for normal checkpoint, false for shutdown checkpoint.  
`subtrans-checkpoint-done` | `(bool)` | Probe that fires when the SUBTRANS portion of a checkpoint is complete. arg0 has the same meaning as for `subtrans-checkpoint-start`.  
`multixact-checkpoint-start` | `(bool)` | Probe that fires when the MultiXact portion of a checkpoint is started. arg0 is true for normal checkpoint, false for shutdown checkpoint.  
`multixact-checkpoint-done` | `(bool)` | Probe that fires when the MultiXact portion of a checkpoint is complete. arg0 has the same meaning as for `multixact-checkpoint-start`.  
`buffer-checkpoint-start` | `(int)` | Probe that fires when the buffer-writing portion of a checkpoint is started. arg0 holds the bitwise flags used to distinguish different checkpoint types, such as shutdown, immediate or force.  
`buffer-sync-start` | `(int, int)` | Probe that fires when we begin to write dirty buffers during checkpoint (after identifying which buffers must be written). arg0 is the total number of buffers. arg1 is the number that are currently dirty and need to be written.  
`buffer-sync-written` | `(int)` | Probe that fires after each buffer is written during checkpoint. arg0 is the ID number of the buffer.  
`buffer-sync-done` | `(int, int, int)` | Probe that fires when all dirty buffers have been written. arg0 is the total number of buffers. arg1 is the number of buffers actually written by the checkpoint process. arg2 is the number that were expected to be written (arg1 of `buffer-sync-start`); any difference reflects other processes flushing buffers during the checkpoint.  
`buffer-checkpoint-sync-start` | `()` | Probe that fires after dirty buffers have been written to the kernel, and before starting to issue fsync requests.  
`buffer-checkpoint-done` | `()` | Probe that fires when syncing of buffers to disk is complete.  
`twophase-checkpoint-start` | `()` | Probe that fires when the two-phase portion of a checkpoint is started.  
`twophase-checkpoint-done` | `()` | Probe that fires when the two-phase portion of a checkpoint is complete.  
`buffer-extend-start` | `(ForkNumber, BlockNumber, Oid, Oid, Oid, int, unsigned int)` | Probe that fires when a relation extension starts. arg0 contains the fork to be extended. arg1, arg2, and arg3 contain the tablespace, database, and relation OIDs identifying the relation. arg4 is the ID of the backend which created the temporary relation for a local buffer, or `InvalidBackendId` (-1) for a shared buffer. arg5 is the number of blocks the caller would like to extend by.  
`buffer-extend-done` | `(ForkNumber, BlockNumber, Oid, Oid, Oid, int, unsigned int, BlockNumber)` | Probe that fires when a relation extension is complete. arg0 contains the fork to be extended. arg1, arg2, and arg3 contain the tablespace, database, and relation OIDs identifying the relation. arg4 is the ID of the backend which created the temporary relation for a local buffer, or `InvalidBackendId` (-1) for a shared buffer. arg5 is the number of blocks the relation was extended by, this can be less than the number in the `buffer-extend-start` due to resource constraints. arg6 contains the BlockNumber of the first new block.  
`buffer-read-start` | `(ForkNumber, BlockNumber, Oid, Oid, Oid, int)` | Probe that fires when a buffer read is started. arg0 and arg1 contain the fork and block numbers of the page. arg2, arg3, and arg4 contain the tablespace, database, and relation OIDs identifying the relation. arg5 is the ID of the backend which created the temporary relation for a local buffer, or `InvalidBackendId` (-1) for a shared buffer.  
`buffer-read-done` | `(ForkNumber, BlockNumber, Oid, Oid, Oid, int, bool)` | Probe that fires when a buffer read is complete. arg0 and arg1 contain the fork and block numbers of the page. arg2, arg3, and arg4 contain the tablespace, database, and relation OIDs identifying the relation. arg5 is the ID of the backend which created the temporary relation for a local buffer, or `InvalidBackendId` (-1) for a shared buffer. arg6 is true if the buffer was found in the pool, false if not.  
`buffer-flush-start` | `(ForkNumber, BlockNumber, Oid, Oid, Oid)` | Probe that fires before issuing any write request for a shared buffer. arg0 and arg1 contain the fork and block numbers of the page. arg2, arg3, and arg4 contain the tablespace, database, and relation OIDs identifying the relation.  
`buffer-flush-done` | `(ForkNumber, BlockNumber, Oid, Oid, Oid)` | Probe that fires when a write request is complete. (Note that this just reflects the time to pass the data to the kernel; it's typically not actually been written to disk yet.) The arguments are the same as for `buffer-flush-start`.  
`wal-buffer-write-dirty-start` | `()` | Probe that fires when a server process begins to write a dirty WAL buffer because no more WAL buffer space is available. (If this happens often, it implies that [wal_buffers](runtime-config-wal.html#GUC-WAL-BUFFERS) is too small.)  
`wal-buffer-write-dirty-done` | `()` | Probe that fires when a dirty WAL buffer write is complete.  
`wal-insert` | `(unsigned char, unsigned char)` | Probe that fires when a WAL record is inserted. arg0 is the resource manager (rmid) for the record. arg1 contains the info flags.  
`wal-switch` | `()` | Probe that fires when a WAL segment switch is requested.  
`smgr-md-read-start` | `(ForkNumber, BlockNumber, Oid, Oid, Oid, int)` | Probe that fires when beginning to read a block from a relation. arg0 and arg1 contain the fork and block numbers of the page. arg2, arg3, and arg4 contain the tablespace, database, and relation OIDs identifying the relation. arg5 is the ID of the backend which created the temporary relation for a local buffer, or `InvalidBackendId` (-1) for a shared buffer.  
`smgr-md-read-done` | `(ForkNumber, BlockNumber, Oid, Oid, Oid, int, int, int)` | Probe that fires when a block read is complete. arg0 and arg1 contain the fork and block numbers of the page. arg2, arg3, and arg4 contain the tablespace, database, and relation OIDs identifying the relation. arg5 is the ID of the backend which created the temporary relation for a local buffer, or `InvalidBackendId` (-1) for a shared buffer. arg6 is the number of bytes actually read, while arg7 is the number requested (if these are different it indicates trouble).  
`smgr-md-write-start` | `(ForkNumber, BlockNumber, Oid, Oid, Oid, int)` | Probe that fires when beginning to write a block to a relation. arg0 and arg1 contain the fork and block numbers of the page. arg2, arg3, and arg4 contain the tablespace, database, and relation OIDs identifying the relation. arg5 is the ID of the backend which created the temporary relation for a local buffer, or `InvalidBackendId` (-1) for a shared buffer.  
`smgr-md-write-done` | `(ForkNumber, BlockNumber, Oid, Oid, Oid, int, int, int)` | Probe that fires when a block write is complete. arg0 and arg1 contain the fork and block numbers of the page. arg2, arg3, and arg4 contain the tablespace, database, and relation OIDs identifying the relation. arg5 is the ID of the backend which created the temporary relation for a local buffer, or `InvalidBackendId` (-1) for a shared buffer. arg6 is the number of bytes actually written, while arg7 is the number requested (if these are different it indicates trouble).  
`sort-start` | `(int, bool, int, int, bool, int)` | Probe that fires when a sort operation is started. arg0 indicates heap, index or datum sort. arg1 is true for unique-value enforcement. arg2 is the number of key columns. arg3 is the number of kilobytes of work memory allowed. arg4 is true if random access to the sort result is required. arg5 indicates serial when `0`, parallel worker when `1`, or parallel leader when `2`.  
`sort-done` | `(bool, long)` | Probe that fires when a sort is complete. arg0 is true for external sort, false for internal sort. arg1 is the number of disk blocks used for an external sort, or kilobytes of memory used for an internal sort.  
`lwlock-acquire` | `(char *, LWLockMode)` | Probe that fires when an LWLock has been acquired. arg0 is the LWLock's tranche. arg1 is the requested lock mode, either exclusive or shared.  
`lwlock-release` | `(char *)` | Probe that fires when an LWLock has been released (but note that any released waiters have not yet been awakened). arg0 is the LWLock's tranche.  
`lwlock-wait-start` | `(char *, LWLockMode)` | Probe that fires when an LWLock was not immediately available and a server process has begun to wait for the lock to become available. arg0 is the LWLock's tranche. arg1 is the requested lock mode, either exclusive or shared.  
`lwlock-wait-done` | `(char *, LWLockMode)` | Probe that fires when a server process has been released from its wait for an LWLock (it does not actually have the lock yet). arg0 is the LWLock's tranche. arg1 is the requested lock mode, either exclusive or shared.  
`lwlock-condacquire` | `(char *, LWLockMode)` | Probe that fires when an LWLock was successfully acquired when the caller specified no waiting. arg0 is the LWLock's tranche. arg1 is the requested lock mode, either exclusive or shared.  
`lwlock-condacquire-fail` | `(char *, LWLockMode)` | Probe that fires when an LWLock was not successfully acquired when the caller specified no waiting. arg0 is the LWLock's tranche. arg1 is the requested lock mode, either exclusive or shared.  
`lock-wait-start` | `(unsigned int, unsigned int, unsigned int, unsigned int, unsigned int, LOCKMODE)` | Probe that fires when a request for a heavyweight lock (lmgr lock) has begun to wait because the lock is not available. arg0 through arg3 are the tag fields identifying the object being locked. arg4 indicates the type of object being locked. arg5 indicates the lock type being requested.  
`lock-wait-done` | `(unsigned int, unsigned int, unsigned int, unsigned int, unsigned int, LOCKMODE)` | Probe that fires when a request for a heavyweight lock (lmgr lock) has finished waiting (i.e., has acquired the lock). The arguments are the same as for `lock-wait-start`.  
`deadlock-found` | `()` | Probe that fires when a deadlock is found by the deadlock detector.  
  
  

**Table  28.49. Defined Types Used in Probe Parameters**

Type | Definition  
---|---  
`LocalTransactionId` | `unsigned int`  
`LWLockMode` | `int`  
`LOCKMODE` | `int`  
`BlockNumber` | `unsigned int`  
`Oid` | `unsigned int`  
`ForkNumber` | `int`  
`bool` | `unsigned char`  
  
  

### 28.5.3. Using Probes #

The example below shows a DTrace script for analyzing transaction counts in
the system, as an alternative to snapshotting `pg_stat_database` before and
after a performance test:

    
    
    #!/usr/sbin/dtrace -qs
    
    postgresql$1:::transaction-start
    {
          @start["Start"] = count();
          self->ts  = timestamp;
    }
    
    postgresql$1:::transaction-abort
    {
          @abort["Abort"] = count();
    }
    
    postgresql$1:::transaction-commit
    /self->ts/
    {
          @commit["Commit"] = count();
          @time["Total time (ns)"] = sum(timestamp - self->ts);
          self->ts=0;
    }
    

When executed, the example D script gives output such as:

    
    
    # ./txn_count.d `pgrep -n postgres` or ./txn_count.d <PID>
    ^C
    
    Start                                          71
    Commit                                         70
    Total time (ns)                        2312105013
    

### Note

SystemTap uses a different notation for trace scripts than DTrace does, even
though the underlying trace points are compatible. One point worth noting is
that at this writing, SystemTap scripts must reference probe names using
double underscores in place of hyphens. This is expected to be fixed in future
SystemTap releases.

You should remember that DTrace scripts need to be carefully written and
debugged, otherwise the trace information collected might be meaningless. In
most cases where problems are found it is the instrumentation that is at
fault, not the underlying system. When discussing information found using
dynamic tracing, be sure to enclose the script used to allow that too to be
checked and discussed.

### 28.5.4. Defining New Probes #

New probes can be defined within the code wherever the developer desires,
though this will require a recompilation. Below are the steps for inserting
new probes:

  1. Decide on probe names and data to be made available through the probes

  2. Add the probe definitions to `src/backend/utils/probes.d`

  3. Include `pg_trace.h` if it is not already present in the module(s) containing the probe points, and insert `TRACE_POSTGRESQL` probe macros at the desired locations in the source code

  4. Recompile and verify that the new probes are available

**Example:  ** Here is an example of how you would add a probe to trace all
new transactions by transaction ID.

  1. Decide that the probe will be named `transaction-start` and requires a parameter of type `LocalTransactionId`

  2. Add the probe definition to `src/backend/utils/probes.d`:
         
         probe transaction__start(LocalTransactionId);
         

Note the use of the double underline in the probe name. In a DTrace script
using the probe, the double underline needs to be replaced with a hyphen, so
`transaction-start` is the name to document for users.

  3. At compile time, `transaction__start` is converted to a macro called `TRACE_POSTGRESQL_TRANSACTION_START` (notice the underscores are single here), which is available by including `pg_trace.h`. Add the macro call to the appropriate location in the source code. In this case, it looks like the following:
         
         TRACE_POSTGRESQL_TRANSACTION_START(vxid.localTransactionId);
         

  4. After recompiling and running the new binary, check that your newly added probe is available by executing the following DTrace command. You should see similar output:
         
         # dtrace -ln transaction-start
            ID    PROVIDER          MODULE           FUNCTION NAME
         18705 postgresql49878     postgres     StartTransactionCommand transaction-start
         18755 postgresql49877     postgres     StartTransactionCommand transaction-start
         18805 postgresql49876     postgres     StartTransactionCommand transaction-start
         18855 postgresql49875     postgres     StartTransactionCommand transaction-start
         18986 postgresql49873     postgres     StartTransactionCommand transaction-start
         

There are a few things to be careful about when adding trace macros to the C
code:

  * You should take care that the data types specified for a probe's parameters match the data types of the variables used in the macro. Otherwise, you will get compilation errors.

  * On most platforms, if PostgreSQL is built with `--enable-dtrace`, the arguments to a trace macro will be evaluated whenever control passes through the macro, _even if no tracing is being done_. This is usually not worth worrying about if you are just reporting the values of a few local variables. But beware of putting expensive function calls into the arguments. If you need to do that, consider protecting the macro with a check to see if the trace is actually enabled:
        
        if (TRACE_POSTGRESQL_TRANSACTION_START_ENABLED())
            TRACE_POSTGRESQL_TRANSACTION_START(some_function(...));
        

Each trace macro has a corresponding `ENABLED` macro.

* * *

[Prev](progress-reporting.html "28.4. Progress Reporting")  | [Up](monitoring.html "Chapter 28. Monitoring Database Activity") |  [Next](diskusage.html "Chapter 29. Monitoring Disk Usage")  
---|---|---  
28.4. Progress Reporting  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 29. Monitoring Disk Usage  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/dynamic-trace.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

