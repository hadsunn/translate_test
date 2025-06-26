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

Supported Versions: [Current](/docs/current/logicaldecoding-explanation.html
"PostgreSQL 17 - 49.2. Logical Decoding Concepts")
([17](/docs/17/logicaldecoding-explanation.html "PostgreSQL 17 - 49.2. Logical
Decoding Concepts")) / [16](/docs/16/logicaldecoding-explanation.html
"PostgreSQL 16 - 49.2. Logical Decoding Concepts") /
[15](/docs/15/logicaldecoding-explanation.html "PostgreSQL 15 - 49.2. Logical
Decoding Concepts") / [14](/docs/14/logicaldecoding-explanation.html
"PostgreSQL 14 - 49.2. Logical Decoding Concepts") /
[13](/docs/13/logicaldecoding-explanation.html "PostgreSQL 13 - 49.2. Logical
Decoding Concepts")

Development Versions: [18](/docs/18/logicaldecoding-explanation.html
"PostgreSQL 18 - 49.2. Logical Decoding Concepts") /
[devel](/docs/devel/logicaldecoding-explanation.html "PostgreSQL devel -
49.2. Logical Decoding Concepts")

Unsupported versions: [12](/docs/12/logicaldecoding-explanation.html
"PostgreSQL 12 - 49.2. Logical Decoding Concepts") /
[11](/docs/11/logicaldecoding-explanation.html "PostgreSQL 11 - 49.2. Logical
Decoding Concepts") / [10](/docs/10/logicaldecoding-explanation.html
"PostgreSQL 10 - 49.2. Logical Decoding Concepts") /
[9.6](/docs/9.6/logicaldecoding-explanation.html "PostgreSQL 9.6 -
49.2. Logical Decoding Concepts") / [9.5](/docs/9.5/logicaldecoding-
explanation.html "PostgreSQL 9.5 - 49.2. Logical Decoding Concepts") /
[9.4](/docs/9.4/logicaldecoding-explanation.html "PostgreSQL 9.4 -
49.2. Logical Decoding Concepts")

__

49.2. Logical Decoding Concepts  
---  
[Prev](logicaldecoding-example.html "49.1. Logical Decoding Examples")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") | Chapter 49. Logical Decoding | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](logicaldecoding-walsender.html "49.3. Streaming Replication Protocol Interface")  
  
* * *

## 49.2. Logical Decoding Concepts #

[49.2.1. Logical Decoding](logicaldecoding-explanation.html#LOGICALDECODING-
EXPLANATION-LOG-DEC)

[49.2.2. Replication Slots](logicaldecoding-explanation.html#LOGICALDECODING-
REPLICATION-SLOTS)

[49.2.3. Output Plugins](logicaldecoding-explanation.html#LOGICALDECODING-
EXPLANATION-OUTPUT-PLUGINS)

[49.2.4. Exported Snapshots](logicaldecoding-explanation.html#LOGICALDECODING-
EXPLANATION-EXPORTED-SNAPSHOTS)

### 49.2.1. Logical Decoding #

Logical decoding is the process of extracting all persistent changes to a
database's tables into a coherent, easy to understand format which can be
interpreted without detailed knowledge of the database's internal state.

In PostgreSQL, logical decoding is implemented by decoding the contents of the
[write-ahead log](wal.html "Chapter 30. Reliability and the Write-Ahead Log"),
which describe changes on a storage level, into an application-specific form
such as a stream of tuples or SQL statements.

### 49.2.2. Replication Slots #

In the context of logical replication, a slot represents a stream of changes
that can be replayed to a client in the order they were made on the origin
server. Each slot streams a sequence of changes from a single database.

### Note

PostgreSQL also has streaming replication slots (see [Section 27.2.5](warm-
standby.html#STREAMING-REPLICATION "27.2.5. Streaming Replication")), but they
are used somewhat differently there.

A replication slot has an identifier that is unique across all databases in a
PostgreSQL cluster. Slots persist independently of the connection using them
and are crash-safe.

A logical slot will emit each change just once in normal operation. The
current position of each slot is persisted only at checkpoint, so in the case
of a crash the slot may return to an earlier LSN, which will then cause recent
changes to be sent again when the server restarts. Logical decoding clients
are responsible for avoiding ill effects from handling the same message more
than once. Clients may wish to record the last LSN they saw when decoding and
skip over any repeated data or (when using the replication protocol) request
that decoding start from that LSN rather than letting the server determine the
start point. The Replication Progress Tracking feature is designed for this
purpose, refer to [replication origins](replication-origins.html
"Chapter 50. Replication Progress Tracking").

Multiple independent slots may exist for a single database. Each slot has its
own state, allowing different consumers to receive changes from different
points in the database change stream. For most applications, a separate slot
will be required for each consumer.

A logical replication slot knows nothing about the state of the receiver(s).
It's even possible to have multiple different receivers using the same slot at
different times; they'll just get the changes following on from when the last
receiver stopped consuming them. Only one receiver may consume changes from a
slot at any given time.

A logical replication slot can also be created on a hot standby. To prevent
`VACUUM` from removing required rows from the system catalogs,
`hot_standby_feedback` should be set on the standby. In spite of that, if any
required rows get removed, the slot gets invalidated. It's highly recommended
to use a physical slot between the primary and the standby. Otherwise,
`hot_standby_feedback` will work but only while the connection is alive (for
example a node restart would break it). Then, the primary may delete system
catalog rows that could be needed by the logical decoding on the standby (as
it does not know about the catalog_xmin on the standby). Existing logical
slots on standby also get invalidated if `wal_level` on the primary is reduced
to less than `logical`. This is done as soon as the standby detects such a
change in the WAL stream. It means that, for walsenders which are lagging (if
any), some WAL records up to the `wal_level` parameter change on the primary
won't be decoded.

Creation of a logical slot requires information about all the currently
running transactions. On the primary, this information is available directly,
but on a standby, this information has to be obtained from primary. Thus, slot
creation may need to wait for some activity to happen on the primary. If the
primary is idle, creating a logical slot on standby may take noticeable time.
This can be sped up by calling the `pg_log_standby_snapshot` function on the
primary.

### Caution

Replication slots persist across crashes and know nothing about the state of
their consumer(s). They will prevent removal of required resources even when
there is no connection using them. This consumes storage because neither
required WAL nor required rows from the system catalogs can be removed by
`VACUUM` as long as they are required by a replication slot. In extreme cases
this could cause the database to shut down to prevent transaction ID
wraparound (see [Section 25.1.5](routine-vacuuming.html#VACUUM-FOR-WRAPAROUND
"25.1.5. Preventing Transaction ID Wraparound Failures")). So if a slot is no
longer required it should be dropped.

### 49.2.3. Output Plugins #

Output plugins transform the data from the write-ahead log's internal
representation into the format the consumer of a replication slot desires.

### 49.2.4. Exported Snapshots #

When a new replication slot is created using the streaming replication
interface (see [CREATE_REPLICATION_SLOT](protocol-replication.html#PROTOCOL-
REPLICATION-CREATE-REPLICATION-SLOT)), a snapshot is exported (see [Section
9.27.5](functions-admin.html#FUNCTIONS-SNAPSHOT-SYNCHRONIZATION
"9.27.5. Snapshot Synchronization Functions")), which will show exactly the
state of the database after which all changes will be included in the change
stream. This can be used to create a new replica by using [`SET TRANSACTION
SNAPSHOT`](sql-set-transaction.html "SET TRANSACTION") to read the state of
the database at the moment the slot was created. This transaction can then be
used to dump the database's state at that point in time, which afterwards can
be updated using the slot's contents without losing any changes.

Creation of a snapshot is not always possible. In particular, it will fail
when connected to a hot standby. Applications that do not require snapshot
export may suppress it with the `NOEXPORT_SNAPSHOT` option.

* * *

[Prev](logicaldecoding-example.html "49.1. Logical Decoding Examples")  | [Up](logicaldecoding.html "Chapter 49. Logical Decoding") |  [Next](logicaldecoding-walsender.html "49.3. Streaming Replication Protocol Interface")  
---|---|---  
49.1. Logical Decoding Examples  | [Home](index.html "PostgreSQL 16.9 Documentation") |  49.3. Streaming Replication Protocol Interface  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/logicaldecoding-
explanation.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

