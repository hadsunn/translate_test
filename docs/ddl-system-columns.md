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

Supported Versions: [Current](/docs/current/ddl-system-columns.html
"PostgreSQL 17 - 5.5. System Columns") ([17](/docs/17/ddl-system-columns.html
"PostgreSQL 17 - 5.5. System Columns")) / [16](/docs/16/ddl-system-
columns.html "PostgreSQL 16 - 5.5. System Columns") / [15](/docs/15/ddl-
system-columns.html "PostgreSQL 15 - 5.5. System Columns") /
[14](/docs/14/ddl-system-columns.html "PostgreSQL 14 - 5.5. System Columns") /
[13](/docs/13/ddl-system-columns.html "PostgreSQL 13 - 5.5. System Columns")

Development Versions: [18](/docs/18/ddl-system-columns.html "PostgreSQL 18 -
5.5. System Columns") / [devel](/docs/devel/ddl-system-columns.html
"PostgreSQL devel - 5.5. System Columns")

Unsupported versions: [12](/docs/12/ddl-system-columns.html "PostgreSQL 12 -
5.5. System Columns") / [11](/docs/11/ddl-system-columns.html "PostgreSQL 11 -
5.5. System Columns") / [10](/docs/10/ddl-system-columns.html "PostgreSQL 10 -
5.5. System Columns") / [9.6](/docs/9.6/ddl-system-columns.html "PostgreSQL
9.6 - 5.5. System Columns") / [9.5](/docs/9.5/ddl-system-columns.html
"PostgreSQL 9.5 - 5.5. System Columns") / [9.4](/docs/9.4/ddl-system-
columns.html "PostgreSQL 9.4 - 5.5. System Columns") / [9.3](/docs/9.3/ddl-
system-columns.html "PostgreSQL 9.3 - 5.5. System Columns") /
[9.2](/docs/9.2/ddl-system-columns.html "PostgreSQL 9.2 - 5.5. System
Columns") / [9.1](/docs/9.1/ddl-system-columns.html "PostgreSQL 9.1 -
5.5. System Columns") / [9.0](/docs/9.0/ddl-system-columns.html "PostgreSQL
9.0 - 5.5. System Columns") / [8.4](/docs/8.4/ddl-system-columns.html
"PostgreSQL 8.4 - 5.5. System Columns") / [8.3](/docs/8.3/ddl-system-
columns.html "PostgreSQL 8.3 - 5.5. System Columns") / [8.2](/docs/8.2/ddl-
system-columns.html "PostgreSQL 8.2 - 5.5. System Columns") /
[8.1](/docs/8.1/ddl-system-columns.html "PostgreSQL 8.1 - 5.5. System
Columns") / [8.0](/docs/8.0/ddl-system-columns.html "PostgreSQL 8.0 -
5.5. System Columns") / [7.4](/docs/7.4/ddl-system-columns.html "PostgreSQL
7.4 - 5.5. System Columns") / [7.3](/docs/7.3/ddl-system-columns.html
"PostgreSQL 7.3 - 5.5. System Columns")

__

5.5. System Columns  
---  
[Prev](ddl-constraints.html "5.4. Constraints")  | [Up](ddl.html "Chapter 5. Data Definition") | Chapter 5. Data Definition | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ddl-alter.html "5.6. Modifying Tables")  
  
* * *

## 5.5. System Columns #

Every table has several _system columns_ that are implicitly defined by the
system. Therefore, these names cannot be used as names of user-defined
columns. (Note that these restrictions are separate from whether the name is a
key word or not; quoting a name will not allow you to escape these
restrictions.) You do not really need to be concerned about these columns;
just know they exist.

`tableoid` #

    

The OID of the table containing this row. This column is particularly handy
for queries that select from partitioned tables (see [Section 5.11](ddl-
partitioning.html "5.11. Table Partitioning")) or inheritance hierarchies (see
[Section 5.10](ddl-inherit.html "5.10. Inheritance")), since without it, it's
difficult to tell which individual table a row came from. The `tableoid` can
be joined against the `oid` column of `pg_class` to obtain the table name.

`xmin` #

    

The identity (transaction ID) of the inserting transaction for this row
version. (A row version is an individual state of a row; each update of a row
creates a new row version for the same logical row.)

`cmin` #

    

The command identifier (starting at zero) within the inserting transaction.

`xmax` #

    

The identity (transaction ID) of the deleting transaction, or zero for an
undeleted row version. It is possible for this column to be nonzero in a
visible row version. That usually indicates that the deleting transaction
hasn't committed yet, or that an attempted deletion was rolled back.

`cmax` #

    

The command identifier within the deleting transaction, or zero.

`ctid` #

    

The physical location of the row version within its table. Note that although
the `ctid` can be used to locate the row version very quickly, a row's `ctid`
will change if it is updated or moved by `VACUUM FULL`. Therefore `ctid` is
useless as a long-term row identifier. A primary key should be used to
identify logical rows.

Transaction identifiers are also 32-bit quantities. In a long-lived database
it is possible for transaction IDs to wrap around. This is not a fatal problem
given appropriate maintenance procedures; see [Chapter 25](maintenance.html
"Chapter 25. Routine Database Maintenance Tasks") for details. It is unwise,
however, to depend on the uniqueness of transaction IDs over the long term
(more than one billion transactions).

Command identifiers are also 32-bit quantities. This creates a hard limit of
232 (4 billion) SQL commands within a single transaction. In practice this
limit is not a problem — note that the limit is on the number of SQL commands,
not the number of rows processed. Also, only commands that actually modify the
database contents will consume a command identifier.

* * *

[Prev](ddl-constraints.html "5.4. Constraints")  | [Up](ddl.html "Chapter 5. Data Definition") |  [Next](ddl-alter.html "5.6. Modifying Tables")  
---|---|---  
5.4. Constraints  | [Home](index.html "PostgreSQL 16.9 Documentation") |  5.6. Modifying Tables  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ddl-system-columns.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

