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

Supported Versions: [16](/docs/16/brin-builtin-opclasses.html "PostgreSQL 16 -
71.2. Built-in Operator Classes") / [15](/docs/15/brin-builtin-opclasses.html
"PostgreSQL 15 - 71.2. Built-in Operator Classes") / [14](/docs/14/brin-
builtin-opclasses.html "PostgreSQL 14 - 71.2. Built-in Operator Classes") /
[13](/docs/13/brin-builtin-opclasses.html "PostgreSQL 13 - 71.2. Built-in
Operator Classes")

Unsupported versions: [12](/docs/12/brin-builtin-opclasses.html "PostgreSQL 12
- 71.2. Built-in Operator Classes") / [11](/docs/11/brin-builtin-
opclasses.html "PostgreSQL 11 - 71.2. Built-in Operator Classes") /
[10](/docs/10/brin-builtin-opclasses.html "PostgreSQL 10 - 71.2. Built-in
Operator Classes") / [9.6](/docs/9.6/brin-builtin-opclasses.html "PostgreSQL
9.6 - 71.2. Built-in Operator Classes") / [9.5](/docs/9.5/brin-builtin-
opclasses.html "PostgreSQL 9.5 - 71.2. Built-in Operator Classes")

__

71.2. Built-in Operator Classes  
---  
[Prev](brin-intro.html "71.1. Introduction")  | [Up](brin.html "Chapter 71. BRIN Indexes") | Chapter 71. BRIN Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](brin-extensibility.html "71.3. Extensibility")  
  
* * *

## 71.2. Built-in Operator Classes #

[71.2.1. Operator Class Parameters](brin-builtin-opclasses.html#BRIN-BUILTIN-
OPCLASSES--PARAMETERS)

The core PostgreSQL distribution includes the BRIN operator classes shown in
[Table 71.1](brin-builtin-opclasses.html#BRIN-BUILTIN-OPCLASSES-TABLE
"Table 71.1. Built-in BRIN Operator Classes").

The _minmax_ operator classes store the minimum and the maximum values
appearing in the indexed column within the range. The _inclusion_ operator
classes store a value which includes the values in the indexed column within
the range. The _bloom_ operator classes build a Bloom filter for all values in
the range. The _minmax-multi_ operator classes store multiple minimum and
maximum values, representing values appearing in the indexed column within the
range.

**Table  71.1. Built-in BRIN Operator Classes**

Name | Indexable Operators  
---|---  
`bit_minmax_ops` | `= (bit,bit)`  
`< (bit,bit)`  
`> (bit,bit)`  
`<= (bit,bit)`  
`>= (bit,bit)`  
`box_inclusion_ops` | `@> (box,point)`  
`<< (box,box)`  
`&< (box,box)`  
`&> (box,box)`  
`>> (box,box)`  
`<@ (box,box)`  
`@> (box,box)`  
`~= (box,box)`  
`&& (box,box)`  
`<<| (box,box)`  
`&<| (box,box)`  
`|&> (box,box)`  
`|>> (box,box)`  
`bpchar_bloom_ops` | `= (character,character)`  
`bpchar_minmax_ops` | `= (character,character)`  
`< (character,character)`  
`<= (character,character)`  
`> (character,character)`  
`>= (character,character)`  
`bytea_bloom_ops` | `= (bytea,bytea)`  
`bytea_minmax_ops` | `= (bytea,bytea)`  
`< (bytea,bytea)`  
`<= (bytea,bytea)`  
`> (bytea,bytea)`  
`>= (bytea,bytea)`  
`char_bloom_ops` | `= ("char","char")`  
`char_minmax_ops` | `= ("char","char")`  
`< ("char","char")`  
`<= ("char","char")`  
`> ("char","char")`  
`>= ("char","char")`  
`date_bloom_ops` | `= (date,date)`  
`date_minmax_ops` | `= (date,date)`  
`< (date,date)`  
`<= (date,date)`  
`> (date,date)`  
`>= (date,date)`  
`date_minmax_multi_ops` | `= (date,date)`  
`< (date,date)`  
`<= (date,date)`  
`> (date,date)`  
`>= (date,date)`  
`float4_bloom_ops` | `= (float4,float4)`  
`float4_minmax_ops` | `= (float4,float4)`  
`< (float4,float4)`  
`> (float4,float4)`  
`<= (float4,float4)`  
`>= (float4,float4)`  
`float4_minmax_multi_ops` | `= (float4,float4)`  
`< (float4,float4)`  
`> (float4,float4)`  
`<= (float4,float4)`  
`>= (float4,float4)`  
`float8_bloom_ops` | `= (float8,float8)`  
`float8_minmax_ops` | `= (float8,float8)`  
`< (float8,float8)`  
`<= (float8,float8)`  
`> (float8,float8)`  
`>= (float8,float8)`  
`float8_minmax_multi_ops` | `= (float8,float8)`  
`< (float8,float8)`  
`<= (float8,float8)`  
`> (float8,float8)`  
`>= (float8,float8)`  
`inet_inclusion_ops` | `<< (inet,inet)`  
`<<= (inet,inet)`  
`>> (inet,inet)`  
`>>= (inet,inet)`  
`= (inet,inet)`  
`&& (inet,inet)`  
`inet_bloom_ops` | `= (inet,inet)`  
`inet_minmax_ops` | `= (inet,inet)`  
`< (inet,inet)`  
`<= (inet,inet)`  
`> (inet,inet)`  
`>= (inet,inet)`  
`inet_minmax_multi_ops` | `= (inet,inet)`  
`< (inet,inet)`  
`<= (inet,inet)`  
`> (inet,inet)`  
`>= (inet,inet)`  
`int2_bloom_ops` | `= (int2,int2)`  
`int2_minmax_ops` | `= (int2,int2)`  
`< (int2,int2)`  
`> (int2,int2)`  
`<= (int2,int2)`  
`>= (int2,int2)`  
`int2_minmax_multi_ops` | `= (int2,int2)`  
`< (int2,int2)`  
`> (int2,int2)`  
`<= (int2,int2)`  
`>= (int2,int2)`  
`int4_bloom_ops` | `= (int4,int4)`  
`int4_minmax_ops` | `= (int4,int4)`  
`< (int4,int4)`  
`> (int4,int4)`  
`<= (int4,int4)`  
`>= (int4,int4)`  
`int4_minmax_multi_ops` | `= (int4,int4)`  
`< (int4,int4)`  
`> (int4,int4)`  
`<= (int4,int4)`  
`>= (int4,int4)`  
`int8_bloom_ops` | `= (bigint,bigint)`  
`int8_minmax_ops` | `= (bigint,bigint)`  
`< (bigint,bigint)`  
`> (bigint,bigint)`  
`<= (bigint,bigint)`  
`>= (bigint,bigint)`  
`int8_minmax_multi_ops` | `= (bigint,bigint)`  
`< (bigint,bigint)`  
`> (bigint,bigint)`  
`<= (bigint,bigint)`  
`>= (bigint,bigint)`  
`interval_bloom_ops` | `= (interval,interval)`  
`interval_minmax_ops` | `= (interval,interval)`  
`< (interval,interval)`  
`<= (interval,interval)`  
`> (interval,interval)`  
`>= (interval,interval)`  
`interval_minmax_multi_ops` | `= (interval,interval)`  
`< (interval,interval)`  
`<= (interval,interval)`  
`> (interval,interval)`  
`>= (interval,interval)`  
`macaddr_bloom_ops` | `= (macaddr,macaddr)`  
`macaddr_minmax_ops` | `= (macaddr,macaddr)`  
`< (macaddr,macaddr)`  
`<= (macaddr,macaddr)`  
`> (macaddr,macaddr)`  
`>= (macaddr,macaddr)`  
`macaddr_minmax_multi_ops` | `= (macaddr,macaddr)`  
`< (macaddr,macaddr)`  
`<= (macaddr,macaddr)`  
`> (macaddr,macaddr)`  
`>= (macaddr,macaddr)`  
`macaddr8_bloom_ops` | `= (macaddr8,macaddr8)`  
`macaddr8_minmax_ops` | `= (macaddr8,macaddr8)`  
`< (macaddr8,macaddr8)`  
`<= (macaddr8,macaddr8)`  
`> (macaddr8,macaddr8)`  
`>= (macaddr8,macaddr8)`  
`macaddr8_minmax_multi_ops` | `= (macaddr8,macaddr8)`  
`< (macaddr8,macaddr8)`  
`<= (macaddr8,macaddr8)`  
`> (macaddr8,macaddr8)`  
`>= (macaddr8,macaddr8)`  
`name_bloom_ops` | `= (name,name)`  
`name_minmax_ops` | `= (name,name)`  
`< (name,name)`  
`<= (name,name)`  
`> (name,name)`  
`>= (name,name)`  
`numeric_bloom_ops` | `= (numeric,numeric)`  
`numeric_minmax_ops` | `= (numeric,numeric)`  
`< (numeric,numeric)`  
`<= (numeric,numeric)`  
`> (numeric,numeric)`  
`>= (numeric,numeric)`  
`numeric_minmax_multi_ops` | `= (numeric,numeric)`  
`< (numeric,numeric)`  
`<= (numeric,numeric)`  
`> (numeric,numeric)`  
`>= (numeric,numeric)`  
`oid_bloom_ops` | `= (oid,oid)`  
`oid_minmax_ops` | `= (oid,oid)`  
`< (oid,oid)`  
`> (oid,oid)`  
`<= (oid,oid)`  
`>= (oid,oid)`  
`oid_minmax_multi_ops` | `= (oid,oid)`  
`< (oid,oid)`  
`> (oid,oid)`  
`<= (oid,oid)`  
`>= (oid,oid)`  
`pg_lsn_bloom_ops` | `= (pg_lsn,pg_lsn)`  
`pg_lsn_minmax_ops` | `= (pg_lsn,pg_lsn)`  
`< (pg_lsn,pg_lsn)`  
`> (pg_lsn,pg_lsn)`  
`<= (pg_lsn,pg_lsn)`  
`>= (pg_lsn,pg_lsn)`  
`pg_lsn_minmax_multi_ops` | `= (pg_lsn,pg_lsn)`  
`< (pg_lsn,pg_lsn)`  
`> (pg_lsn,pg_lsn)`  
`<= (pg_lsn,pg_lsn)`  
`>= (pg_lsn,pg_lsn)`  
`range_inclusion_ops` | `= (anyrange,anyrange)`  
`< (anyrange,anyrange)`  
`<= (anyrange,anyrange)`  
`>= (anyrange,anyrange)`  
`> (anyrange,anyrange)`  
`&& (anyrange,anyrange)`  
`@> (anyrange,anyelement)`  
`@> (anyrange,anyrange)`  
`<@ (anyrange,anyrange)`  
`<< (anyrange,anyrange)`  
`>> (anyrange,anyrange)`  
`&< (anyrange,anyrange)`  
`&> (anyrange,anyrange)`  
`-|- (anyrange,anyrange)`  
`text_bloom_ops` | `= (text,text)`  
`text_minmax_ops` | `= (text,text)`  
`< (text,text)`  
`<= (text,text)`  
`> (text,text)`  
`>= (text,text)`  
`tid_bloom_ops` | `= (tid,tid)`  
`tid_minmax_ops` | `= (tid,tid)`  
`< (tid,tid)`  
`> (tid,tid)`  
`<= (tid,tid)`  
`>= (tid,tid)`  
`tid_minmax_multi_ops` | `= (tid,tid)`  
`< (tid,tid)`  
`> (tid,tid)`  
`<= (tid,tid)`  
`>= (tid,tid)`  
`timestamp_bloom_ops` | `= (timestamp,timestamp)`  
`timestamp_minmax_ops` | `= (timestamp,timestamp)`  
`< (timestamp,timestamp)`  
`<= (timestamp,timestamp)`  
`> (timestamp,timestamp)`  
`>= (timestamp,timestamp)`  
`timestamp_minmax_multi_ops` | `= (timestamp,timestamp)`  
`< (timestamp,timestamp)`  
`<= (timestamp,timestamp)`  
`> (timestamp,timestamp)`  
`>= (timestamp,timestamp)`  
`timestamptz_bloom_ops` | `= (timestamptz,timestamptz)`  
`timestamptz_minmax_ops` | `= (timestamptz,timestamptz)`  
`< (timestamptz,timestamptz)`  
`<= (timestamptz,timestamptz)`  
`> (timestamptz,timestamptz)`  
`>= (timestamptz,timestamptz)`  
`timestamptz_minmax_multi_ops` | `= (timestamptz,timestamptz)`  
`< (timestamptz,timestamptz)`  
`<= (timestamptz,timestamptz)`  
`> (timestamptz,timestamptz)`  
`>= (timestamptz,timestamptz)`  
`time_bloom_ops` | `= (time,time)`  
`time_minmax_ops` | `= (time,time)`  
`< (time,time)`  
`<= (time,time)`  
`> (time,time)`  
`>= (time,time)`  
`time_minmax_multi_ops` | `= (time,time)`  
`< (time,time)`  
`<= (time,time)`  
`> (time,time)`  
`>= (time,time)`  
`timetz_bloom_ops` | `= (timetz,timetz)`  
`timetz_minmax_ops` | `= (timetz,timetz)`  
`< (timetz,timetz)`  
`<= (timetz,timetz)`  
`> (timetz,timetz)`  
`>= (timetz,timetz)`  
`timetz_minmax_multi_ops` | `= (timetz,timetz)`  
`< (timetz,timetz)`  
`<= (timetz,timetz)`  
`> (timetz,timetz)`  
`>= (timetz,timetz)`  
`uuid_bloom_ops` | `= (uuid,uuid)`  
`uuid_minmax_ops` | `= (uuid,uuid)`  
`< (uuid,uuid)`  
`> (uuid,uuid)`  
`<= (uuid,uuid)`  
`>= (uuid,uuid)`  
`uuid_minmax_multi_ops` | `= (uuid,uuid)`  
`< (uuid,uuid)`  
`> (uuid,uuid)`  
`<= (uuid,uuid)`  
`>= (uuid,uuid)`  
`varbit_minmax_ops` | `= (varbit,varbit)`  
`< (varbit,varbit)`  
`> (varbit,varbit)`  
`<= (varbit,varbit)`  
`>= (varbit,varbit)`  
  
  

### 71.2.1. Operator Class Parameters #

Some of the built-in operator classes allow specifying parameters affecting
behavior of the operator class. Each operator class has its own set of allowed
parameters. Only the `bloom` and `minmax-multi` operator classes allow
specifying parameters:

bloom operator classes accept these parameters:

`n_distinct_per_range`

    

Defines the estimated number of distinct non-null values in the block range,
used by BRIN bloom indexes for sizing of the Bloom filter. It behaves
similarly to `n_distinct` option for [ALTER TABLE](sql-altertable.html "ALTER
TABLE"). When set to a positive value, each block range is assumed to contain
this number of distinct non-null values. When set to a negative value, which
must be greater than or equal to -1, the number of distinct non-null values is
assumed to grow linearly with the maximum possible number of tuples in the
block range (about 290 rows per block). The default value is `-0.1`, and the
minimum number of distinct non-null values is `16`.

`false_positive_rate`

    

Defines the desired false positive rate used by BRIN bloom indexes for sizing
of the Bloom filter. The values must be between 0.0001 and 0.25. The default
value is 0.01, which is 1% false positive rate.

minmax-multi operator classes accept these parameters:

`values_per_range`

    

Defines the maximum number of values stored by BRIN minmax indexes to
summarize a block range. Each value may represent either a point, or a
boundary of an interval. Values must be between 8 and 256, and the default
value is 32.

* * *

[Prev](brin-intro.html "71.1. Introduction")  | [Up](brin.html "Chapter 71. BRIN Indexes") |  [Next](brin-extensibility.html "71.3. Extensibility")  
---|---|---  
71.1. Introduction  | [Home](index.html "PostgreSQL 16.9 Documentation") |  71.3. Extensibility  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/brin-builtin-opclasses.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

