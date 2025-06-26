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

Supported Versions: [Current](/docs/current/indexes-opclass.html "PostgreSQL
17 - 11.10. Operator Classes and Operator Families") ([17](/docs/17/indexes-
opclass.html "PostgreSQL 17 - 11.10. Operator Classes and Operator Families"))
/ [16](/docs/16/indexes-opclass.html "PostgreSQL 16 - 11.10. Operator Classes
and Operator Families") / [15](/docs/15/indexes-opclass.html "PostgreSQL 15 -
11.10. Operator Classes and Operator Families") / [14](/docs/14/indexes-
opclass.html "PostgreSQL 14 - 11.10. Operator Classes and Operator Families")
/ [13](/docs/13/indexes-opclass.html "PostgreSQL 13 - 11.10. Operator Classes
and Operator Families")

Development Versions: [18](/docs/18/indexes-opclass.html "PostgreSQL 18 -
11.10. Operator Classes and Operator Families") / [devel](/docs/devel/indexes-
opclass.html "PostgreSQL devel - 11.10. Operator Classes and Operator
Families")

Unsupported versions: [12](/docs/12/indexes-opclass.html "PostgreSQL 12 -
11.10. Operator Classes and Operator Families") / [11](/docs/11/indexes-
opclass.html "PostgreSQL 11 - 11.10. Operator Classes and Operator Families")
/ [10](/docs/10/indexes-opclass.html "PostgreSQL 10 - 11.10. Operator Classes
and Operator Families") / [9.6](/docs/9.6/indexes-opclass.html "PostgreSQL 9.6
- 11.10. Operator Classes and Operator Families") / [9.5](/docs/9.5/indexes-
opclass.html "PostgreSQL 9.5 - 11.10. Operator Classes and Operator Families")
/ [9.4](/docs/9.4/indexes-opclass.html "PostgreSQL 9.4 - 11.10. Operator
Classes and Operator Families") / [9.3](/docs/9.3/indexes-opclass.html
"PostgreSQL 9.3 - 11.10. Operator Classes and Operator Families") /
[9.2](/docs/9.2/indexes-opclass.html "PostgreSQL 9.2 - 11.10. Operator Classes
and Operator Families") / [9.1](/docs/9.1/indexes-opclass.html "PostgreSQL 9.1
- 11.10. Operator Classes and Operator Families") / [9.0](/docs/9.0/indexes-
opclass.html "PostgreSQL 9.0 - 11.10. Operator Classes and Operator Families")
/ [8.4](/docs/8.4/indexes-opclass.html "PostgreSQL 8.4 - 11.10. Operator
Classes and Operator Families") / [8.3](/docs/8.3/indexes-opclass.html
"PostgreSQL 8.3 - 11.10. Operator Classes and Operator Families") /
[8.2](/docs/8.2/indexes-opclass.html "PostgreSQL 8.2 - 11.10. Operator Classes
and Operator Families") / [8.1](/docs/8.1/indexes-opclass.html "PostgreSQL 8.1
- 11.10. Operator Classes and Operator Families") / [8.0](/docs/8.0/indexes-
opclass.html "PostgreSQL 8.0 - 11.10. Operator Classes and Operator Families")
/ [7.4](/docs/7.4/indexes-opclass.html "PostgreSQL 7.4 - 11.10. Operator
Classes and Operator Families") / [7.3](/docs/7.3/indexes-opclass.html
"PostgreSQL 7.3 - 11.10. Operator Classes and Operator Families") /
[7.2](/docs/7.2/indexes-opclass.html "PostgreSQL 7.2 - 11.10. Operator Classes
and Operator Families")

__

11.10. Operator Classes and Operator Families  
---  
[Prev](indexes-index-only-scans.html "11.9. Index-Only Scans and Covering Indexes")  | [Up](indexes.html "Chapter 11. Indexes") | Chapter 11. Indexes | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](indexes-collations.html "11.11. Indexes and Collations")  
  
* * *

## 11.10. Operator Classes and Operator Families #

An index definition can specify an _operator class_ for each column of an
index.

    
    
    CREATE INDEX _name_ ON _table_ (_column_ _opclass_ [ ( _opclass_options_ ) ] [_sort options_] [, ...]);
    

The operator class identifies the operators to be used by the index for that
column. For example, a B-tree index on the type `int4` would use the
`int4_ops` class; this operator class includes comparison functions for values
of type `int4`. In practice the default operator class for the column's data
type is usually sufficient. The main reason for having operator classes is
that for some data types, there could be more than one meaningful index
behavior. For example, we might want to sort a complex-number data type either
by absolute value or by real part. We could do this by defining two operator
classes for the data type and then selecting the proper class when making an
index. The operator class determines the basic sort ordering (which can then
be modified by adding sort options `COLLATE`, `ASC`/`DESC` and/or `NULLS
FIRST`/`NULLS LAST`).

There are also some built-in operator classes besides the default ones:

  * The operator classes `text_pattern_ops`, `varchar_pattern_ops`, and `bpchar_pattern_ops` support B-tree indexes on the types `text`, `varchar`, and `char` respectively. The difference from the default operator classes is that the values are compared strictly character by character rather than according to the locale-specific collation rules. This makes these operator classes suitable for use by queries involving pattern matching expressions (`LIKE` or POSIX regular expressions) when the database does not use the standard “C” locale. As an example, you might index a `varchar` column like this:
        
        CREATE INDEX test_index ON test_table (col varchar_pattern_ops);
        

Note that you should also create an index with the default operator class if
you want queries involving ordinary `<`, `<=`, `>`, or `>=` comparisons to use
an index. Such queries cannot use the `_`xxx`_ _pattern_ops` operator classes.
(Ordinary equality comparisons can use these operator classes, however.) It is
possible to create multiple indexes on the same column with different operator
classes. If you do use the C locale, you do not need the `_`xxx`_
_pattern_ops` operator classes, because an index with the default operator
class is usable for pattern-matching queries in the C locale.

The following query shows all defined operator classes:

    
    
    SELECT am.amname AS index_method,
           opc.opcname AS opclass_name,
           opc.opcintype::regtype AS indexed_type,
           opc.opcdefault AS is_default
        FROM pg_am am, pg_opclass opc
        WHERE opc.opcmethod = am.oid
        ORDER BY index_method, opclass_name;
    

An operator class is actually just a subset of a larger structure called an
_operator family_. In cases where several data types have similar behaviors,
it is frequently useful to define cross-data-type operators and allow these to
work with indexes. To do this, the operator classes for each of the types must
be grouped into the same operator family. The cross-type operators are members
of the family, but are not associated with any single class within the family.

This expanded version of the previous query shows the operator family each
operator class belongs to:

    
    
    SELECT am.amname AS index_method,
           opc.opcname AS opclass_name,
           opf.opfname AS opfamily_name,
           opc.opcintype::regtype AS indexed_type,
           opc.opcdefault AS is_default
        FROM pg_am am, pg_opclass opc, pg_opfamily opf
        WHERE opc.opcmethod = am.oid AND
              opc.opcfamily = opf.oid
        ORDER BY index_method, opclass_name;
    

This query shows all defined operator families and all the operators included
in each family:

    
    
    SELECT am.amname AS index_method,
           opf.opfname AS opfamily_name,
           amop.amopopr::regoperator AS opfamily_operator
        FROM pg_am am, pg_opfamily opf, pg_amop amop
        WHERE opf.opfmethod = am.oid AND
              amop.amopfamily = opf.oid
        ORDER BY index_method, opfamily_name, opfamily_operator;
    

### Tip

[psql](app-psql.html "psql") has commands `\dAc`, `\dAf`, and `\dAo`, which
provide slightly more sophisticated versions of these queries.

* * *

[Prev](indexes-index-only-scans.html "11.9. Index-Only Scans and Covering Indexes")  | [Up](indexes.html "Chapter 11. Indexes") |  [Next](indexes-collations.html "11.11. Indexes and Collations")  
---|---|---  
11.9. Index-Only Scans and Covering Indexes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  11.11. Indexes and Collations  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/indexes-opclass.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

