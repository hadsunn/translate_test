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

Supported Versions: [16](/docs/16/disk-usage.html "PostgreSQL 16 -
29.1. Determining Disk Usage") / [15](/docs/15/disk-usage.html "PostgreSQL 15
- 29.1. Determining Disk Usage") / [14](/docs/14/disk-usage.html "PostgreSQL
14 - 29.1. Determining Disk Usage") / [13](/docs/13/disk-usage.html
"PostgreSQL 13 - 29.1. Determining Disk Usage")

Unsupported versions: [12](/docs/12/disk-usage.html "PostgreSQL 12 -
29.1. Determining Disk Usage") / [11](/docs/11/disk-usage.html "PostgreSQL 11
- 29.1. Determining Disk Usage") / [10](/docs/10/disk-usage.html "PostgreSQL
10 - 29.1. Determining Disk Usage") / [9.6](/docs/9.6/disk-usage.html
"PostgreSQL 9.6 - 29.1. Determining Disk Usage") / [9.5](/docs/9.5/disk-
usage.html "PostgreSQL 9.5 - 29.1. Determining Disk Usage") /
[9.4](/docs/9.4/disk-usage.html "PostgreSQL 9.4 - 29.1. Determining Disk
Usage") / [9.3](/docs/9.3/disk-usage.html "PostgreSQL 9.3 - 29.1. Determining
Disk Usage") / [9.2](/docs/9.2/disk-usage.html "PostgreSQL 9.2 -
29.1. Determining Disk Usage") / [9.1](/docs/9.1/disk-usage.html "PostgreSQL
9.1 - 29.1. Determining Disk Usage") / [9.0](/docs/9.0/disk-usage.html
"PostgreSQL 9.0 - 29.1. Determining Disk Usage") / [8.4](/docs/8.4/disk-
usage.html "PostgreSQL 8.4 - 29.1. Determining Disk Usage") /
[8.3](/docs/8.3/disk-usage.html "PostgreSQL 8.3 - 29.1. Determining Disk
Usage") / [8.2](/docs/8.2/disk-usage.html "PostgreSQL 8.2 - 29.1. Determining
Disk Usage")

__

29.1. Determining Disk Usage  
---  
[Prev](diskusage.html "Chapter 29. Monitoring Disk Usage")  | [Up](diskusage.html "Chapter 29. Monitoring Disk Usage") | Chapter 29. Monitoring Disk Usage | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](disk-full.html "29.2. Disk Full Failure")  
  
* * *

## 29.1. Determining Disk Usage #

Each table has a primary heap disk file where most of the data is stored. If
the table has any columns with potentially-wide values, there also might be a
TOAST file associated with the table, which is used to store values too wide
to fit comfortably in the main table (see [Section 73.2](storage-toast.html
"73.2. TOAST")). There will be one valid index on the TOAST table, if present.
There also might be indexes associated with the base table. Each table and
index is stored in a separate disk file — possibly more than one file, if the
file would exceed one gigabyte. Naming conventions for these files are
described in [Section 73.1](storage-file-layout.html "73.1. Database File
Layout").

You can monitor disk space in three ways: using the SQL functions listed in
[Table 9.96](functions-admin.html#FUNCTIONS-ADMIN-DBSIZE "Table 9.96. Database
Object Size Functions"), using the [oid2name](oid2name.html "oid2name")
module, or using manual inspection of the system catalogs. The SQL functions
are the easiest to use and are generally recommended. The remainder of this
section shows how to do it by inspection of the system catalogs.

Using psql on a recently vacuumed or analyzed database, you can issue queries
to see the disk usage of any table:

    
    
    SELECT pg_relation_filepath(oid), relpages FROM pg_class WHERE relname = 'customer';
    
     pg_relation_filepath | relpages
    ----------------------+----------
     base/16384/16806     |       60
    (1 row)
    

Each page is typically 8 kilobytes. (Remember, `relpages` is only updated by
`VACUUM`, `ANALYZE`, and a few DDL commands such as `CREATE INDEX`.) The file
path name is of interest if you want to examine the table's disk file
directly.

To show the space used by TOAST tables, use a query like the following:

    
    
    SELECT relname, relpages
    FROM pg_class,
         (SELECT reltoastrelid
          FROM pg_class
          WHERE relname = 'customer') AS ss
    WHERE oid = ss.reltoastrelid OR
          oid = (SELECT indexrelid
                 FROM pg_index
                 WHERE indrelid = ss.reltoastrelid)
    ORDER BY relname;
    
           relname        | relpages
    ----------------------+----------
     pg_toast_16806       |        0
     pg_toast_16806_index |        1
    

You can easily display index sizes, too:

    
    
    SELECT c2.relname, c2.relpages
    FROM pg_class c, pg_class c2, pg_index i
    WHERE c.relname = 'customer' AND
          c.oid = i.indrelid AND
          c2.oid = i.indexrelid
    ORDER BY c2.relname;
    
          relname      | relpages
    -------------------+----------
     customer_id_index |       26
    

It is easy to find your largest tables and indexes using this information:

    
    
    SELECT relname, relpages
    FROM pg_class
    ORDER BY relpages DESC;
    
           relname        | relpages
    ----------------------+----------
     bigtable             |     3290
     customer             |     3144
    

* * *

[Prev](diskusage.html "Chapter 29. Monitoring Disk Usage")  | [Up](diskusage.html "Chapter 29. Monitoring Disk Usage") |  [Next](disk-full.html "29.2. Disk Full Failure")  
---|---|---  
Chapter 29. Monitoring Disk Usage  | [Home](index.html "PostgreSQL 16.9 Documentation") |  29.2. Disk Full Failure  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/disk-usage.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

