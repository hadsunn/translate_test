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

Supported Versions: [Current](/docs/current/oid2name.html "PostgreSQL 17 -
oid2name") ([17](/docs/17/oid2name.html "PostgreSQL 17 - oid2name")) /
[16](/docs/16/oid2name.html "PostgreSQL 16 - oid2name") /
[15](/docs/15/oid2name.html "PostgreSQL 15 - oid2name") /
[14](/docs/14/oid2name.html "PostgreSQL 14 - oid2name") /
[13](/docs/13/oid2name.html "PostgreSQL 13 - oid2name")

Development Versions: [18](/docs/18/oid2name.html "PostgreSQL 18 - oid2name")
/ [devel](/docs/devel/oid2name.html "PostgreSQL devel - oid2name")

Unsupported versions: [12](/docs/12/oid2name.html "PostgreSQL 12 - oid2name")
/ [11](/docs/11/oid2name.html "PostgreSQL 11 - oid2name") /
[10](/docs/10/oid2name.html "PostgreSQL 10 - oid2name") /
[9.6](/docs/9.6/oid2name.html "PostgreSQL 9.6 - oid2name") /
[9.5](/docs/9.5/oid2name.html "PostgreSQL 9.5 - oid2name") /
[9.4](/docs/9.4/oid2name.html "PostgreSQL 9.4 - oid2name") /
[9.3](/docs/9.3/oid2name.html "PostgreSQL 9.3 - oid2name") /
[9.2](/docs/9.2/oid2name.html "PostgreSQL 9.2 - oid2name") /
[9.1](/docs/9.1/oid2name.html "PostgreSQL 9.1 - oid2name") /
[9.0](/docs/9.0/oid2name.html "PostgreSQL 9.0 - oid2name") /
[8.4](/docs/8.4/oid2name.html "PostgreSQL 8.4 - oid2name") /
[8.3](/docs/8.3/oid2name.html "PostgreSQL 8.3 - oid2name")

__

oid2name  
---  
[Prev](contrib-prog-client.html "G.1. Client Applications")  | [Up](contrib-prog-client.html "G.1. Client Applications") | G.1. Client Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](vacuumlo.html "vacuumlo")  
  
* * *

## oid2name

oid2name — resolve OIDs and file nodes in a PostgreSQL data directory

## Synopsis

`oid2name` [_`option`_...]

## Description

oid2name is a utility program that helps administrators to examine the file
structure used by PostgreSQL. To make use of it, you need to be familiar with
the database file structure, which is described in [Chapter 73](storage.html
"Chapter 73. Database Physical Storage").

### Note

The name “oid2name” is historical, and is actually rather misleading, since
most of the time when you use it, you will really be concerned with tables'
filenode numbers (which are the file names visible in the database
directories). Be sure you understand the difference between table OIDs and
table filenodes!

oid2name connects to a target database and extracts OID, filenode, and/or
table name information. You can also have it show database OIDs or tablespace
OIDs.

## Options

oid2name accepts the following command-line arguments:

`-f _`filenode`_`  
`--filenode=_`filenode`_`

    

show info for table with filenode _`filenode`_.

`-i`  
`--indexes`

    

include indexes and sequences in the listing.

`-o _`oid`_`  
`--oid=_`oid`_`

    

show info for table with OID _`oid`_.

`-q`  
`--quiet`

    

omit headers (useful for scripting).

`-s`  
`--tablespaces`

    

show tablespace OIDs.

`-S`  
`--system-objects`

    

include system objects (those in `information_schema`, `pg_toast` and
`pg_catalog` schemas).

`-t _`tablename_pattern`_`  
`--table=_`tablename_pattern`_`

    

show info for table(s) matching _`tablename_pattern`_.

`-V`  
`--version`

    

Print the oid2name version and exit.

`-x`  
`--extended`

    

display more information about each object shown: tablespace name, schema
name, and OID.

`-?`  
`--help`

    

Show help about oid2name command line arguments, and exit.

oid2name also accepts the following command-line arguments for connection
parameters:

`-d _`database`_`  
`--dbname=_`database`_`

    

database to connect to.

`-h _`host`_`  
`--host=_`host`_`

    

database server's host.

`-H _`host`_`

    

database server's host. Use of this parameter is _deprecated_ as of PostgreSQL
12.

`-p _`port`_`  
`--port=_`port`_`

    

database server's port.

`-U _`username`_`  
`--username=_`username`_`

    

user name to connect as.

To display specific tables, select which tables to show by using `-o`, `-f`
and/or `-t`. `-o` takes an OID, `-f` takes a filenode, and `-t` takes a table
name (actually, it's a `LIKE` pattern, so you can use things like `foo%`). You
can use as many of these options as you like, and the listing will include all
objects matched by any of the options. But note that these options can only
show objects in the database given by `-d`.

If you don't give any of `-o`, `-f` or `-t`, but do give `-d`, it will list
all tables in the database named by `-d`. In this mode, the `-S` and `-i`
options control what gets listed.

If you don't give `-d` either, it will show a listing of database OIDs.
Alternatively you can give `-s` to get a tablespace listing.

## Environment

`PGHOST`  
`PGPORT`  
`PGUSER`

    

Default connection parameters.

This utility, like most other PostgreSQL utilities, also uses the environment
variables supported by libpq (see [Section 34.15](libpq-envars.html
"34.15. Environment Variables")).

The environment variable `PG_COLOR` specifies whether to use color in
diagnostic messages. Possible values are `always`, `auto` and `never`.

## Notes

oid2name requires a running database server with non-corrupt system catalogs.
It is therefore of only limited use for recovering from catastrophic database
corruption situations.

## Examples

    
    
    $ # what's in this database server, anyway?
    $ oid2name
    All databases:
        Oid  Database Name  Tablespace
    ----------------------------------
      17228       alvherre  pg_default
      17255     regression  pg_default
      17227      template0  pg_default
          1      template1  pg_default
    
    $ oid2name -s
    All tablespaces:
         Oid  Tablespace Name
    -------------------------
        1663       pg_default
        1664        pg_global
      155151         fastdisk
      155152          bigdisk
    
    $ # OK, let's look into database alvherre
    $ cd $PGDATA/base/17228
    
    $ # get top 10 db objects in the default tablespace, ordered by size
    $ ls -lS * | head -10
    -rw-------  1 alvherre alvherre 136536064 sep 14 09:51 155173
    -rw-------  1 alvherre alvherre  17965056 sep 14 09:51 1155291
    -rw-------  1 alvherre alvherre   1204224 sep 14 09:51 16717
    -rw-------  1 alvherre alvherre    581632 sep  6 17:51 1255
    -rw-------  1 alvherre alvherre    237568 sep 14 09:50 16674
    -rw-------  1 alvherre alvherre    212992 sep 14 09:51 1249
    -rw-------  1 alvherre alvherre    204800 sep 14 09:51 16684
    -rw-------  1 alvherre alvherre    196608 sep 14 09:50 16700
    -rw-------  1 alvherre alvherre    163840 sep 14 09:50 16699
    -rw-------  1 alvherre alvherre    122880 sep  6 17:51 16751
    
    $ # I wonder what file 155173 is ...
    $ oid2name -d alvherre -f 155173
    From database "alvherre":
      Filenode  Table Name
    ----------------------
        155173    accounts
    
    $ # you can ask for more than one object
    $ oid2name -d alvherre -f 155173 -f 1155291
    From database "alvherre":
      Filenode     Table Name
    -------------------------
        155173       accounts
       1155291  accounts_pkey
    
    $ # you can mix the options, and get more details with -x
    $ oid2name -d alvherre -t accounts -f 1155291 -x
    From database "alvherre":
      Filenode     Table Name      Oid  Schema  Tablespace
    ------------------------------------------------------
        155173       accounts   155173  public  pg_default
       1155291  accounts_pkey  1155291  public  pg_default
    
    $ # show disk space for every db object
    $ du [0-9]* |
    > while read SIZE FILENODE
    > do
    >   echo "$SIZE       `oid2name -q -d alvherre -i -f $FILENODE`"
    > done
    16            1155287  branches_pkey
    16            1155289  tellers_pkey
    17561            1155291  accounts_pkey
    ...
    
    $ # same, but sort by size
    $ du [0-9]* | sort -rn | while read SIZE FN
    > do
    >   echo "$SIZE   `oid2name -q -d alvherre -f $FN`"
    > done
    133466             155173    accounts
    17561            1155291  accounts_pkey
    1177              16717  pg_proc_proname_args_nsp_index
    ...
    
    $ # If you want to see what's in tablespaces, use the pg_tblspc directory
    $ cd $PGDATA/pg_tblspc
    $ oid2name -s
    All tablespaces:
         Oid  Tablespace Name
    -------------------------
        1663       pg_default
        1664        pg_global
      155151         fastdisk
      155152          bigdisk
    
    $ # what databases have objects in tablespace "fastdisk"?
    $ ls -d 155151/*
    155151/17228/  155151/PG_VERSION
    
    $ # Oh, what was database 17228 again?
    $ oid2name
    All databases:
        Oid  Database Name  Tablespace
    ----------------------------------
      17228       alvherre  pg_default
      17255     regression  pg_default
      17227      template0  pg_default
          1      template1  pg_default
    
    $ # Let's see what objects does this database have in the tablespace.
    $ cd 155151/17228
    $ ls -l
    total 0
    -rw-------  1 postgres postgres 0 sep 13 23:20 155156
    
    $ # OK, this is a pretty small table ... but which one is it?
    $ oid2name -d alvherre -f 155156
    From database "alvherre":
      Filenode  Table Name
    ----------------------
        155156         foo
    

## Author

B. Palmer `<[bpalmer@crimelabs.net](mailto:bpalmer@crimelabs.net)>`

* * *

[Prev](contrib-prog-client.html "G.1. Client Applications")  | [Up](contrib-prog-client.html "G.1. Client Applications") |  [Next](vacuumlo.html "vacuumlo")  
---|---|---  
G.1. Client Applications  | [Home](index.html "PostgreSQL 16.9 Documentation") |  vacuumlo  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/oid2name.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

