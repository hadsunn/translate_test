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

Supported Versions: [Current](/docs/current/xml-limits-conformance.html
"PostgreSQL 17 - D.3. XML Limits and Conformance to SQL/XML")
([17](/docs/17/xml-limits-conformance.html "PostgreSQL 17 - D.3. XML Limits
and Conformance to SQL/XML")) / [16](/docs/16/xml-limits-conformance.html
"PostgreSQL 16 - D.3. XML Limits and Conformance to SQL/XML") /
[15](/docs/15/xml-limits-conformance.html "PostgreSQL 15 - D.3. XML Limits and
Conformance to SQL/XML") / [14](/docs/14/xml-limits-conformance.html
"PostgreSQL 14 - D.3. XML Limits and Conformance to SQL/XML") /
[13](/docs/13/xml-limits-conformance.html "PostgreSQL 13 - D.3. XML Limits and
Conformance to SQL/XML")

Development Versions: [18](/docs/18/xml-limits-conformance.html "PostgreSQL 18
- D.3. XML Limits and Conformance to SQL/XML") / [devel](/docs/devel/xml-
limits-conformance.html "PostgreSQL devel - D.3. XML Limits and Conformance to
SQL/XML")

Unsupported versions: [12](/docs/12/xml-limits-conformance.html "PostgreSQL 12
- D.3. XML Limits and Conformance to SQL/XML") / [11](/docs/11/xml-limits-
conformance.html "PostgreSQL 11 - D.3. XML Limits and Conformance to SQL/XML")
/ [10](/docs/10/xml-limits-conformance.html "PostgreSQL 10 - D.3. XML Limits
and Conformance to SQL/XML")

__

D.3. XML Limits and Conformance to SQL/XML  
---  
[Prev](unsupported-features-sql-standard.html "D.2. Unsupported Features")  | [Up](features.html "Appendix D. SQL Conformance") | Appendix D. SQL Conformance | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](release.html "Appendix E. Release Notes")  
  
* * *

## D.3. XML Limits and Conformance to SQL/XML #

[D.3.1. Queries Are Restricted to XPath 1.0](xml-limits-
conformance.html#FUNCTIONS-XML-LIMITS-XPATH1)

[D.3.2. Incidental Limits of the Implementation](xml-limits-
conformance.html#FUNCTIONS-XML-LIMITS-POSTGRESQL)

Significant revisions to the XML-related specifications in ISO/IEC 9075-14
(SQL/XML) were introduced with SQL:2006. PostgreSQL's implementation of the
XML data type and related functions largely follows the earlier 2003 edition,
with some borrowing from later editions. In particular:

  * Where the current standard provides a family of XML data types to hold “document” or “content” in untyped or XML Schema-typed variants, and a type `XML(SEQUENCE)` to hold arbitrary pieces of XML content, PostgreSQL provides the single `xml` type, which can hold “document” or “content”. There is no equivalent of the standard's “sequence” type.

  * PostgreSQL provides two functions introduced in SQL:2006, but in variants that use the XPath 1.0 language, rather than XML Query as specified for them in the standard.

This section presents some of the resulting differences you may encounter.

### D.3.1. Queries Are Restricted to XPath 1.0 #

The PostgreSQL-specific functions `xpath()` and `xpath_exists()` query XML
documents using the XPath language. PostgreSQL also provides XPath-only
variants of the standard functions `XMLEXISTS` and `XMLTABLE`, which
officially use the XQuery language. For all of these functions, PostgreSQL
relies on the libxml2 library, which provides only XPath 1.0.

There is a strong connection between the XQuery language and XPath versions
2.0 and later: any expression that is syntactically valid and executes
successfully in both produces the same result (with a minor exception for
expressions containing numeric character references or predefined entity
references, which XQuery replaces with the corresponding character while XPath
leaves them alone). But there is no such connection between these languages
and XPath 1.0; it was an earlier language and differs in many respects.

There are two categories of limitation to keep in mind: the restriction from
XQuery to XPath for the functions specified in the SQL standard, and the
restriction of XPath to version 1.0 for both the standard and the PostgreSQL-
specific functions.

#### D.3.1.1. Restriction of XQuery to XPath #

Features of XQuery beyond those of XPath include:

  * XQuery expressions can construct and return new XML nodes, in addition to all possible XPath values. XPath can create and return values of the atomic types (numbers, strings, and so on) but can only return XML nodes that were already present in documents supplied as input to the expression.

  * XQuery has control constructs for iteration, sorting, and grouping.

  * XQuery allows declaration and use of local functions.

Recent XPath versions begin to offer capabilities overlapping with these (such
as functional-style `for-each` and `sort`, anonymous functions, and `parse-
xml` to create a node from a string), but such features were not available
before XPath 3.0.

#### D.3.1.2. Restriction of XPath to 1.0 #

For developers familiar with XQuery and XPath 2.0 or later, XPath 1.0 presents
a number of differences to contend with:

  * The fundamental type of an XQuery/XPath expression, the `sequence`, which can contain XML nodes, atomic values, or both, does not exist in XPath 1.0. A 1.0 expression can only produce a node-set (containing zero or more XML nodes), or a single atomic value.

  * Unlike an XQuery/XPath sequence, which can contain any desired items in any desired order, an XPath 1.0 node-set has no guaranteed order and, like any set, does not allow multiple appearances of the same item.

### Note

The libxml2 library does seem to always return node-sets to PostgreSQL with
their members in the same relative order they had in the input document. Its
documentation does not commit to this behavior, and an XPath 1.0 expression
cannot control it.

  * While XQuery/XPath provides all of the types defined in XML Schema and many operators and functions over those types, XPath 1.0 has only node-sets and the three atomic types `boolean`, `double`, and `string`.

  * XPath 1.0 has no conditional operator. An XQuery/XPath expression such as `if ( hat ) then hat/@size else "no hat"` has no XPath 1.0 equivalent.

  * XPath 1.0 has no ordering comparison operator for strings. Both `"cat" < "dog"` and `"cat" > "dog"` are false, because each is a numeric comparison of two `NaN`s. In contrast, `=` and `!=` do compare the strings as strings.

  * XPath 1.0 blurs the distinction between _value comparisons_ and _general comparisons_ as XQuery/XPath define them. Both `sale/@hatsize = 7` and `sale/@customer = "alice"` are existentially quantified comparisons, true if there is any `sale` with the given value for the attribute, but `sale/@taxable = false()` is a value comparison to the _effective boolean value_ of a whole node-set. It is true only if no `sale` has a `taxable` attribute at all.

  * In the XQuery/XPath data model, a _document node_ can have either document form (i.e., exactly one top-level element, with only comments and processing instructions outside of it) or content form (with those constraints relaxed). Its equivalent in XPath 1.0, the _root node_ , can only be in document form. This is part of the reason an `xml` value passed as the context item to any PostgreSQL XPath-based function must be in document form.

The differences highlighted here are not all of them. In XQuery and the 2.0
and later versions of XPath, there is an XPath 1.0 compatibility mode, and the
W3C lists of [function library changes](https://www.w3.org/TR/2010/REC-xpath-
functions-20101214/#xpath1-compatibility) and [language
changes](https://www.w3.org/TR/xpath20/#id-backwards-compatibility) applied in
that mode offer a more complete (but still not exhaustive) account of the
differences. The compatibility mode cannot make the later languages exactly
equivalent to XPath 1.0.

#### D.3.1.3. Mappings between SQL and XML Data Types and Values #

In SQL:2006 and later, both directions of conversion between standard SQL data
types and the XML Schema types are specified precisely. However, the rules are
expressed using the types and semantics of XQuery/XPath, and have no direct
application to the different data model of XPath 1.0.

When PostgreSQL maps SQL data values to XML (as in `xmlelement`), or XML to
SQL (as in the output columns of `xmltable`), except for a few cases treated
specially, PostgreSQL simply assumes that the XML data type's XPath 1.0 string
form will be valid as the text-input form of the SQL datatype, and conversely.
This rule has the virtue of simplicity while producing, for many data types,
results similar to the mappings specified in the standard.

Where interoperability with other systems is a concern, for some data types,
it may be necessary to use data type formatting functions (such as those in
[Section 9.8](functions-formatting.html "9.8. Data Type Formatting
Functions")) explicitly to produce the standard mappings.

### D.3.2. Incidental Limits of the Implementation #

This section concerns limits that are not inherent in the libxml2 library, but
apply to the current implementation in PostgreSQL.

#### D.3.2.1. Only `BY VALUE` Passing Mechanism Is Supported #

The SQL standard defines two _passing mechanisms_ that apply when passing an
XML argument from SQL to an XML function or receiving a result: `BY REF`, in
which a particular XML value retains its node identity, and `BY VALUE`, in
which the content of the XML is passed but node identity is not preserved. A
mechanism can be specified before a list of parameters, as the default
mechanism for all of them, or after any parameter, to override the default.

To illustrate the difference, if _`x`_ is an XML value, these two queries in
an SQL:2006 environment would produce true and false, respectively:

    
    
    SELECT XMLQUERY('$a is $b' PASSING BY REF _x_ AS a, _x_ AS b NULL ON EMPTY);
    SELECT XMLQUERY('$a is $b' PASSING BY VALUE _x_ AS a, _x_ AS b NULL ON EMPTY);
    

PostgreSQL will accept `BY VALUE` or `BY REF` in an `XMLEXISTS` or `XMLTABLE`
construct, but it ignores them. The `xml` data type holds a character-string
serialized representation, so there is no node identity to preserve, and
passing is always effectively `BY VALUE`.

#### D.3.2.2. Cannot Pass Named Parameters to Queries #

The XPath-based functions support passing one parameter to serve as the XPath
expression's context item, but do not support passing additional values to be
available to the expression as named parameters.

#### D.3.2.3. No `XML(SEQUENCE)` Type #

The PostgreSQL `xml` data type can only hold a value in `DOCUMENT` or
`CONTENT` form. An XQuery/XPath expression context item must be a single XML
node or atomic value, but XPath 1.0 further restricts it to be only an XML
node, and has no node type allowing `CONTENT`. The upshot is that a well-
formed `DOCUMENT` is the only form of XML value that PostgreSQL can supply as
an XPath context item.

* * *

[Prev](unsupported-features-sql-standard.html "D.2. Unsupported Features")  | [Up](features.html "Appendix D. SQL Conformance") |  [Next](release.html "Appendix E. Release Notes")  
---|---|---  
D.2. Unsupported Features  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Appendix E. Release Notes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/xml-limits-conformance.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

