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

Supported Versions: [Current](/docs/current/index-api.html "PostgreSQL 17 -
64.1. Basic API Structure for Indexes") ([17](/docs/17/index-api.html
"PostgreSQL 17 - 64.1. Basic API Structure for Indexes")) /
[16](/docs/16/index-api.html "PostgreSQL 16 - 64.1. Basic API Structure for
Indexes") / [15](/docs/15/index-api.html "PostgreSQL 15 - 64.1. Basic API
Structure for Indexes") / [14](/docs/14/index-api.html "PostgreSQL 14 -
64.1. Basic API Structure for Indexes") / [13](/docs/13/index-api.html
"PostgreSQL 13 - 64.1. Basic API Structure for Indexes")

Development Versions: [18](/docs/18/index-api.html "PostgreSQL 18 -
64.1. Basic API Structure for Indexes") / [devel](/docs/devel/index-api.html
"PostgreSQL devel - 64.1. Basic API Structure for Indexes")

Unsupported versions: [12](/docs/12/index-api.html "PostgreSQL 12 -
64.1. Basic API Structure for Indexes") / [11](/docs/11/index-api.html
"PostgreSQL 11 - 64.1. Basic API Structure for Indexes") /
[10](/docs/10/index-api.html "PostgreSQL 10 - 64.1. Basic API Structure for
Indexes") / [9.6](/docs/9.6/index-api.html "PostgreSQL 9.6 - 64.1. Basic API
Structure for Indexes")

__

64.1. Basic API Structure for Indexes  
---  
[Prev](indexam.html "Chapter 64. Index Access Method Interface Definition")  | [Up](indexam.html "Chapter 64. Index Access Method Interface Definition") | Chapter 64. Index Access Method Interface Definition | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](index-functions.html "64.2. Index Access Method Functions")  
  
* * *

## 64.1. Basic API Structure for Indexes #

Each index access method is described by a row in the [`pg_am`](catalog-pg-
am.html "53.3. pg_am") system catalog. The `pg_am` entry specifies a name and
a _handler function_ for the index access method. These entries can be created
and deleted using the [CREATE ACCESS METHOD](sql-create-access-method.html
"CREATE ACCESS METHOD") and [DROP ACCESS METHOD](sql-drop-access-method.html
"DROP ACCESS METHOD") SQL commands.

An index access method handler function must be declared to accept a single
argument of type `internal` and to return the pseudo-type `index_am_handler`.
The argument is a dummy value that simply serves to prevent handler functions
from being called directly from SQL commands. The result of the function must
be a palloc'd struct of type `IndexAmRoutine`, which contains everything that
the core code needs to know to make use of the index access method. The
`IndexAmRoutine` struct, also called the access method's _API struct_ ,
includes fields specifying assorted fixed properties of the access method,
such as whether it can support multicolumn indexes. More importantly, it
contains pointers to support functions for the access method, which do all of
the real work to access indexes. These support functions are plain C functions
and are not visible or callable at the SQL level. The support functions are
described in [Section 64.2](index-functions.html "64.2. Index Access Method
Functions").

The structure `IndexAmRoutine` is defined thus:

    
    
    typedef struct IndexAmRoutine
    {
        NodeTag     type;
    
        /*
         * Total number of strategies (operators) by which we can traverse/search
         * this AM.  Zero if AM does not have a fixed set of strategy assignments.
         */
        uint16      amstrategies;
        /* total number of support functions that this AM uses */
        uint16      amsupport;
        /* opclass options support function number or 0 */
        uint16      amoptsprocnum;
        /* does AM support ORDER BY indexed column's value? */
        bool        amcanorder;
        /* does AM support ORDER BY result of an operator on indexed column? */
        bool        amcanorderbyop;
        /* does AM support backward scanning? */
        bool        amcanbackward;
        /* does AM support UNIQUE indexes? */
        bool        amcanunique;
        /* does AM support multi-column indexes? */
        bool        amcanmulticol;
        /* does AM require scans to have a constraint on the first index column? */
        bool        amoptionalkey;
        /* does AM handle ScalarArrayOpExpr quals? */
        bool        amsearcharray;
        /* does AM handle IS NULL/IS NOT NULL quals? */
        bool        amsearchnulls;
        /* can index storage data type differ from column data type? */
        bool        amstorage;
        /* can an index of this type be clustered on? */
        bool        amclusterable;
        /* does AM handle predicate locks? */
        bool        ampredlocks;
        /* does AM support parallel scan? */
        bool        amcanparallel;
        /* does AM support columns included with clause INCLUDE? */
        bool        amcaninclude;
        /* does AM use maintenance_work_mem? */
        bool        amusemaintenanceworkmem;
        /* does AM summarize tuples, with at least all tuples in the block
         * summarized in one summary */
        bool        amsummarizing;
        /* OR of parallel vacuum flags */
        uint8       amparallelvacuumoptions;
        /* type of data stored in index, or InvalidOid if variable */
        Oid         amkeytype;
    
        /* interface functions */
        ambuild_function ambuild;
        ambuildempty_function ambuildempty;
        aminsert_function aminsert;
        ambulkdelete_function ambulkdelete;
        amvacuumcleanup_function amvacuumcleanup;
        amcanreturn_function amcanreturn;   /* can be NULL */
        amcostestimate_function amcostestimate;
        amoptions_function amoptions;
        amproperty_function amproperty;     /* can be NULL */
        ambuildphasename_function ambuildphasename;   /* can be NULL */
        amvalidate_function amvalidate;
        amadjustmembers_function amadjustmembers; /* can be NULL */
        ambeginscan_function ambeginscan;
        amrescan_function amrescan;
        amgettuple_function amgettuple;     /* can be NULL */
        amgetbitmap_function amgetbitmap;   /* can be NULL */
        amendscan_function amendscan;
        ammarkpos_function ammarkpos;       /* can be NULL */
        amrestrpos_function amrestrpos;     /* can be NULL */
    
        /* interface functions to support parallel index scans */
        amestimateparallelscan_function amestimateparallelscan;    /* can be NULL */
        aminitparallelscan_function aminitparallelscan;    /* can be NULL */
        amparallelrescan_function amparallelrescan;    /* can be NULL */
    } IndexAmRoutine;
    

To be useful, an index access method must also have one or more _operator
families_ and _operator classes_ defined in [`pg_opfamily`](catalog-pg-
opfamily.html "53.35. pg_opfamily"), [`pg_opclass`](catalog-pg-opclass.html
"53.33. pg_opclass"), [`pg_amop`](catalog-pg-amop.html "53.4. pg_amop"), and
[`pg_amproc`](catalog-pg-amproc.html "53.5. pg_amproc"). These entries allow
the planner to determine what kinds of query qualifications can be used with
indexes of this access method. Operator families and classes are described in
[Section 38.16](xindex.html "38.16. Interfacing Extensions to Indexes"), which
is prerequisite material for reading this chapter.

An individual index is defined by a [`pg_class`](catalog-pg-class.html
"53.11. pg_class") entry that describes it as a physical relation, plus a
[`pg_index`](catalog-pg-index.html "53.26. pg_index") entry that shows the
logical content of the index — that is, the set of index columns it has and
the semantics of those columns, as captured by the associated operator
classes. The index columns (key values) can be either simple columns of the
underlying table or expressions over the table rows. The index access method
normally has no interest in where the index key values come from (it is always
handed precomputed key values) but it will be very interested in the operator
class information in `pg_index`. Both of these catalog entries can be accessed
as part of the `Relation` data structure that is passed to all operations on
the index.

Some of the flag fields of `IndexAmRoutine` have nonobvious implications. The
requirements of `amcanunique` are discussed in [Section 64.5](index-unique-
checks.html "64.5. Index Uniqueness Checks"). The `amcanmulticol` flag asserts
that the access method supports multi-key-column indexes, while
`amoptionalkey` asserts that it allows scans where no indexable restriction
clause is given for the first index column. When `amcanmulticol` is false,
`amoptionalkey` essentially says whether the access method supports full-index
scans without any restriction clause. Access methods that support multiple
index columns _must_ support scans that omit restrictions on any or all of the
columns after the first; however they are permitted to require some
restriction to appear for the first index column, and this is signaled by
setting `amoptionalkey` false. One reason that an index AM might set
`amoptionalkey` false is if it doesn't index null values. Since most indexable
operators are strict and hence cannot return true for null inputs, it is at
first sight attractive to not store index entries for null values: they could
never be returned by an index scan anyway. However, this argument fails when
an index scan has no restriction clause for a given index column. In practice
this means that indexes that have `amoptionalkey` true must index nulls, since
the planner might decide to use such an index with no scan keys at all. A
related restriction is that an index access method that supports multiple
index columns _must_ support indexing null values in columns after the first,
because the planner will assume the index can be used for queries that do not
restrict these columns. For example, consider an index on (a,b) and a query
with `WHERE a = 4`. The system will assume the index can be used to scan for
rows with `a = 4`, which is wrong if the index omits rows where `b` is null.
It is, however, OK to omit rows where the first indexed column is null. An
index access method that does index nulls may also set `amsearchnulls`,
indicating that it supports `IS NULL` and `IS NOT NULL` clauses as search
conditions.

The `amcaninclude` flag indicates whether the access method supports
“included” columns, that is it can store (without processing) additional
columns beyond the key column(s). The requirements of the preceding paragraph
apply only to the key columns. In particular, the combination of
`amcanmulticol`=`false` and `amcaninclude`=`true` is sensible: it means that
there can only be one key column, but there can also be included column(s).
Also, included columns must be allowed to be null, independently of
`amoptionalkey`.

The `amsummarizing` flag indicates whether the access method summarizes the
indexed tuples, with summarizing granularity of at least per block. Access
methods that do not point to individual tuples, but to block ranges (like
BRIN), may allow the HOT optimization to continue. This does not apply to
attributes referenced in index predicates, an update of such an attribute
always disables HOT.

* * *

[Prev](indexam.html "Chapter 64. Index Access Method Interface Definition")  | [Up](indexam.html "Chapter 64. Index Access Method Interface Definition") |  [Next](index-functions.html "64.2. Index Access Method Functions")  
---|---|---  
Chapter 64. Index Access Method Interface Definition  | [Home](index.html "PostgreSQL 16.9 Documentation") |  64.2. Index Access Method Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/index-api.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

