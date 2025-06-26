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

Supported Versions: [Current](/docs/current/datatype-xml.html "PostgreSQL 17 -
8.13. XML Type") ([17](/docs/17/datatype-xml.html "PostgreSQL 17 - 8.13. XML
Type")) / [16](/docs/16/datatype-xml.html "PostgreSQL 16 - 8.13. XML Type") /
[15](/docs/15/datatype-xml.html "PostgreSQL 15 - 8.13. XML Type") /
[14](/docs/14/datatype-xml.html "PostgreSQL 14 - 8.13. XML Type") /
[13](/docs/13/datatype-xml.html "PostgreSQL 13 - 8.13. XML Type")

Development Versions: [18](/docs/18/datatype-xml.html "PostgreSQL 18 -
8.13. XML Type") / [devel](/docs/devel/datatype-xml.html "PostgreSQL devel -
8.13. XML Type")

Unsupported versions: [12](/docs/12/datatype-xml.html "PostgreSQL 12 -
8.13. XML Type") / [11](/docs/11/datatype-xml.html "PostgreSQL 11 - 8.13. XML
Type") / [10](/docs/10/datatype-xml.html "PostgreSQL 10 - 8.13. XML Type") /
[9.6](/docs/9.6/datatype-xml.html "PostgreSQL 9.6 - 8.13. XML Type") /
[9.5](/docs/9.5/datatype-xml.html "PostgreSQL 9.5 - 8.13. XML Type") /
[9.4](/docs/9.4/datatype-xml.html "PostgreSQL 9.4 - 8.13. XML Type") /
[9.3](/docs/9.3/datatype-xml.html "PostgreSQL 9.3 - 8.13. XML Type") /
[9.2](/docs/9.2/datatype-xml.html "PostgreSQL 9.2 - 8.13. XML Type") /
[9.1](/docs/9.1/datatype-xml.html "PostgreSQL 9.1 - 8.13. XML Type") /
[9.0](/docs/9.0/datatype-xml.html "PostgreSQL 9.0 - 8.13. XML Type") /
[8.4](/docs/8.4/datatype-xml.html "PostgreSQL 8.4 - 8.13. XML Type") /
[8.3](/docs/8.3/datatype-xml.html "PostgreSQL 8.3 - 8.13. XML Type") /
[8.2](/docs/8.2/datatype-xml.html "PostgreSQL 8.2 - 8.13. XML Type")

__

8.13. XML Type  
---  
[Prev](datatype-uuid.html "8.12. UUID Type")  | [Up](datatype.html "Chapter 8. Data Types") | Chapter 8. Data Types | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datatype-json.html "8.14. JSON Types")  
  
* * *

## 8.13. XML Type #

[8.13.1. Creating XML Values](datatype-xml.html#DATATYPE-XML-CREATING)

[8.13.2. Encoding Handling](datatype-xml.html#DATATYPE-XML-ENCODING-HANDLING)

[8.13.3. Accessing XML Values](datatype-xml.html#DATATYPE-XML-ACCESSING-XML-
VALUES)

The `xml` data type can be used to store XML data. Its advantage over storing
XML data in a `text` field is that it checks the input values for well-
formedness, and there are support functions to perform type-safe operations on
it; see [Section 9.15](functions-xml.html "9.15. XML Functions"). Use of this
data type requires the installation to have been built with `configure --with-
libxml`.

The `xml` type can store well-formed “documents”, as defined by the XML
standard, as well as “content” fragments, which are defined by reference to
the more permissive [“document node”](https://www.w3.org/TR/2010/REC-xpath-
datamodel-20101214/#DocumentNode) of the XQuery and XPath data model. Roughly,
this means that content fragments can have more than one top-level element or
character node. The expression `_`xmlvalue`_ IS DOCUMENT` can be used to
evaluate whether a particular `xml` value is a full document or only a content
fragment.

Limits and compatibility notes for the `xml` data type can be found in
[Section D.3](xml-limits-conformance.html "D.3. XML Limits and Conformance to
SQL/XML").

### 8.13.1. Creating XML Values #

To produce a value of type `xml` from character data, use the function
`xmlparse`:

    
    
    XMLPARSE ( { DOCUMENT | CONTENT } _value_)
    

Examples:

    
    
    XMLPARSE (DOCUMENT '<?xml version="1.0"?><book><title>Manual</title><chapter>...</chapter></book>')
    XMLPARSE (CONTENT 'abc<foo>bar</foo><bar>foo</bar>')
    

While this is the only way to convert character strings into XML values
according to the SQL standard, the PostgreSQL-specific syntaxes:

    
    
    xml '<foo>bar</foo>'
    '<foo>bar</foo>'::xml
    

can also be used.

The `xml` type does not validate input values against a document type
declaration (DTD), even when the input value specifies a DTD. There is also
currently no built-in support for validating against other XML schema
languages such as XML Schema.

The inverse operation, producing a character string value from `xml`, uses the
function `xmlserialize`:

    
    
    XMLSERIALIZE ( { DOCUMENT | CONTENT } _value_ AS _type_ [ [ NO ] INDENT ] )
    

_`type`_ can be `character`, `character varying`, or `text` (or an alias for
one of those). Again, according to the SQL standard, this is the only way to
convert between type `xml` and character types, but PostgreSQL also allows you
to simply cast the value.

The `INDENT` option causes the result to be pretty-printed, while `NO INDENT`
(which is the default) just emits the original input string. Casting to a
character type likewise produces the original string.

When a character string value is cast to or from type `xml` without going
through `XMLPARSE` or `XMLSERIALIZE`, respectively, the choice of `DOCUMENT`
versus `CONTENT` is determined by the “XML option” session configuration
parameter, which can be set using the standard command:

    
    
    SET XML OPTION { DOCUMENT | CONTENT };
    

or the more PostgreSQL-like syntax

    
    
    SET xmloption TO { DOCUMENT | CONTENT };
    

The default is `CONTENT`, so all forms of XML data are allowed.

### 8.13.2. Encoding Handling #

Care must be taken when dealing with multiple character encodings on the
client, server, and in the XML data passed through them. When using the text
mode to pass queries to the server and query results to the client (which is
the normal mode), PostgreSQL converts all character data passed between the
client and the server and vice versa to the character encoding of the
respective end; see [Section 24.3](multibyte.html "24.3. Character Set
Support"). This includes string representations of XML values, such as in the
above examples. This would ordinarily mean that encoding declarations
contained in XML data can become invalid as the character data is converted to
other encodings while traveling between client and server, because the
embedded encoding declaration is not changed. To cope with this behavior,
encoding declarations contained in character strings presented for input to
the `xml` type are _ignored_ , and content is assumed to be in the current
server encoding. Consequently, for correct processing, character strings of
XML data must be sent from the client in the current client encoding. It is
the responsibility of the client to either convert documents to the current
client encoding before sending them to the server, or to adjust the client
encoding appropriately. On output, values of type `xml` will not have an
encoding declaration, and clients should assume all data is in the current
client encoding.

When using binary mode to pass query parameters to the server and query
results back to the client, no encoding conversion is performed, so the
situation is different. In this case, an encoding declaration in the XML data
will be observed, and if it is absent, the data will be assumed to be in UTF-8
(as required by the XML standard; note that PostgreSQL does not support
UTF-16). On output, data will have an encoding declaration specifying the
client encoding, unless the client encoding is UTF-8, in which case it will be
omitted.

Needless to say, processing XML data with PostgreSQL will be less error-prone
and more efficient if the XML data encoding, client encoding, and server
encoding are the same. Since XML data is internally processed in UTF-8,
computations will be most efficient if the server encoding is also UTF-8.

### Caution

Some XML-related functions may not work at all on non-ASCII data when the
server encoding is not UTF-8. This is known to be an issue for `xmltable()`
and `xpath()` in particular.

### 8.13.3. Accessing XML Values #

The `xml` data type is unusual in that it does not provide any comparison
operators. This is because there is no well-defined and universally useful
comparison algorithm for XML data. One consequence of this is that you cannot
retrieve rows by comparing an `xml` column against a search value. XML values
should therefore typically be accompanied by a separate key field such as an
ID. An alternative solution for comparing XML values is to convert them to
character strings first, but note that character string comparison has little
to do with a useful XML comparison method.

Since there are no comparison operators for the `xml` data type, it is not
possible to create an index directly on a column of this type. If speedy
searches in XML data are desired, possible workarounds include casting the
expression to a character string type and indexing that, or indexing an XPath
expression. Of course, the actual query would have to be adjusted to search by
the indexed expression.

The text-search functionality in PostgreSQL can also be used to speed up full-
document searches of XML data. The necessary preprocessing support is,
however, not yet available in the PostgreSQL distribution.

* * *

[Prev](datatype-uuid.html "8.12. UUID Type")  | [Up](datatype.html "Chapter 8. Data Types") |  [Next](datatype-json.html "8.14. JSON Types")  
---|---|---  
8.12. UUID Type  | [Home](index.html "PostgreSQL 16.9 Documentation") |  8.14. JSON Types  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datatype-xml.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

