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

Supported Versions: [Current](/docs/current/catalog-pg-enum.html "PostgreSQL
17 - 53.20. pg_enum") ([17](/docs/17/catalog-pg-enum.html "PostgreSQL 17 -
53.20. pg_enum")) / [16](/docs/16/catalog-pg-enum.html "PostgreSQL 16 -
53.20. pg_enum") / [15](/docs/15/catalog-pg-enum.html "PostgreSQL 15 -
53.20. pg_enum") / [14](/docs/14/catalog-pg-enum.html "PostgreSQL 14 -
53.20. pg_enum") / [13](/docs/13/catalog-pg-enum.html "PostgreSQL 13 -
53.20. pg_enum")

Development Versions: [18](/docs/18/catalog-pg-enum.html "PostgreSQL 18 -
53.20. pg_enum") / [devel](/docs/devel/catalog-pg-enum.html "PostgreSQL devel
- 53.20. pg_enum")

Unsupported versions: [12](/docs/12/catalog-pg-enum.html "PostgreSQL 12 -
53.20. pg_enum") / [11](/docs/11/catalog-pg-enum.html "PostgreSQL 11 -
53.20. pg_enum") / [10](/docs/10/catalog-pg-enum.html "PostgreSQL 10 -
53.20. pg_enum") / [9.6](/docs/9.6/catalog-pg-enum.html "PostgreSQL 9.6 -
53.20. pg_enum") / [9.5](/docs/9.5/catalog-pg-enum.html "PostgreSQL 9.5 -
53.20. pg_enum") / [9.4](/docs/9.4/catalog-pg-enum.html "PostgreSQL 9.4 -
53.20. pg_enum") / [9.3](/docs/9.3/catalog-pg-enum.html "PostgreSQL 9.3 -
53.20. pg_enum") / [9.2](/docs/9.2/catalog-pg-enum.html "PostgreSQL 9.2 -
53.20. pg_enum") / [9.1](/docs/9.1/catalog-pg-enum.html "PostgreSQL 9.1 -
53.20. pg_enum") / [9.0](/docs/9.0/catalog-pg-enum.html "PostgreSQL 9.0 -
53.20. pg_enum") / [8.4](/docs/8.4/catalog-pg-enum.html "PostgreSQL 8.4 -
53.20. pg_enum") / [8.3](/docs/8.3/catalog-pg-enum.html "PostgreSQL 8.3 -
53.20. pg_enum")

__

53.20. `pg_enum`  
---  
[Prev](catalog-pg-description.html "53.19. pg_description")  | [Up](catalogs.html "Chapter 53. System Catalogs") | Chapter 53. System Catalogs | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](catalog-pg-event-trigger.html "53.21. pg_event_trigger")  
  
* * *

## 53.20. `pg_enum` #

The `pg_enum` catalog contains entries showing the values and labels for each
enum type. The internal representation of a given enum value is actually the
OID of its associated row in `pg_enum`.

**Table  53.20. `pg_enum` Columns**

Column Type Description  
---  
`oid` `oid` Row identifier  
`enumtypid` `oid` (references [`pg_type`](catalog-pg-type.html
"53.64. pg_type").`oid`) The OID of the [`pg_type`](catalog-pg-type.html
"53.64. pg_type") entry owning this enum value  
`enumsortorder` `float4` The sort position of this enum value within its enum
type  
`enumlabel` `name` The textual label for this enum value  
  
  

The OIDs for `pg_enum` rows follow a special rule: even-numbered OIDs are
guaranteed to be ordered in the same way as the sort ordering of their enum
type. That is, if two even OIDs belong to the same enum type, the smaller OID
must have the smaller `enumsortorder` value. Odd-numbered OID values need bear
no relationship to the sort order. This rule allows the enum comparison
routines to avoid catalog lookups in many common cases. The routines that
create and alter enum types attempt to assign even OIDs to enum values
whenever possible.

When an enum type is created, its members are assigned sort-order positions
1.._`n`_. But members added later might be given negative or fractional values
of `enumsortorder`. The only requirement on these values is that they be
correctly ordered and unique within each enum type.

* * *

[Prev](catalog-pg-description.html "53.19. pg_description")  | [Up](catalogs.html "Chapter 53. System Catalogs") |  [Next](catalog-pg-event-trigger.html "53.21. pg_event_trigger")  
---|---|---  
53.19. `pg_description`  | [Home](index.html "PostgreSQL 16.9 Documentation") |  53.21. `pg_event_trigger`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/catalog-pg-enum.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

