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

Supported Versions: [Current](/docs/current/functions-xml.html "PostgreSQL 17
- 9.15. XML Functions") ([17](/docs/17/functions-xml.html "PostgreSQL 17 -
9.15. XML Functions")) / [16](/docs/16/functions-xml.html "PostgreSQL 16 -
9.15. XML Functions") / [15](/docs/15/functions-xml.html "PostgreSQL 15 -
9.15. XML Functions") / [14](/docs/14/functions-xml.html "PostgreSQL 14 -
9.15. XML Functions") / [13](/docs/13/functions-xml.html "PostgreSQL 13 -
9.15. XML Functions")

Development Versions: [18](/docs/18/functions-xml.html "PostgreSQL 18 -
9.15. XML Functions") / [devel](/docs/devel/functions-xml.html "PostgreSQL
devel - 9.15. XML Functions")

Unsupported versions: [12](/docs/12/functions-xml.html "PostgreSQL 12 -
9.15. XML Functions") / [11](/docs/11/functions-xml.html "PostgreSQL 11 -
9.15. XML Functions") / [10](/docs/10/functions-xml.html "PostgreSQL 10 -
9.15. XML Functions") / [9.6](/docs/9.6/functions-xml.html "PostgreSQL 9.6 -
9.15. XML Functions") / [9.5](/docs/9.5/functions-xml.html "PostgreSQL 9.5 -
9.15. XML Functions") / [9.4](/docs/9.4/functions-xml.html "PostgreSQL 9.4 -
9.15. XML Functions") / [9.3](/docs/9.3/functions-xml.html "PostgreSQL 9.3 -
9.15. XML Functions") / [9.2](/docs/9.2/functions-xml.html "PostgreSQL 9.2 -
9.15. XML Functions") / [9.1](/docs/9.1/functions-xml.html "PostgreSQL 9.1 -
9.15. XML Functions") / [9.0](/docs/9.0/functions-xml.html "PostgreSQL 9.0 -
9.15. XML Functions") / [8.4](/docs/8.4/functions-xml.html "PostgreSQL 8.4 -
9.15. XML Functions") / [8.3](/docs/8.3/functions-xml.html "PostgreSQL 8.3 -
9.15. XML Functions")

__

9.15. XML Functions  
---  
[Prev](functions-uuid.html "9.14. UUID Functions")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions-json.html "9.16. JSON Functions and Operators")  
  
* * *

## 9.15. XML Functions #

[9.15.1. Producing XML Content](functions-xml.html#FUNCTIONS-PRODUCING-XML)

[9.15.2. XML Predicates](functions-xml.html#FUNCTIONS-XML-PREDICATES)

[9.15.3. Processing XML](functions-xml.html#FUNCTIONS-XML-PROCESSING)

[9.15.4. Mapping Tables to XML](functions-xml.html#FUNCTIONS-XML-MAPPING)

The functions and function-like expressions described in this section operate
on values of type `xml`. See [Section 8.13](datatype-xml.html "8.13. XML
Type") for information about the `xml` type. The function-like expressions
`xmlparse` and `xmlserialize` for converting to and from type `xml` are
documented there, not in this section.

Use of most of these functions requires PostgreSQL to have been built with
`configure --with-libxml`.

### 9.15.1. Producing XML Content #

A set of functions and function-like expressions is available for producing
XML content from SQL data. As such, they are particularly suitable for
formatting query results into XML documents for processing in client
applications.

#### 9.15.1.1. `xmlcomment` #

    
    
    xmlcomment ( text ) → xml
    

The function `xmlcomment` creates an XML value containing an XML comment with
the specified text as content. The text cannot contain “`--`” or end with a
“`-`”, otherwise the resulting construct would not be a valid XML comment. If
the argument is null, the result is null.

Example:

    
    
    SELECT xmlcomment('hello');
    
      xmlcomment
    --------------
     <!--hello-->
    

#### 9.15.1.2. `xmlconcat` #

    
    
    xmlconcat ( xml [, ...] ) → xml
    

The function `xmlconcat` concatenates a list of individual XML values to
create a single value containing an XML content fragment. Null values are
omitted; the result is only null if there are no nonnull arguments.

Example:

    
    
    SELECT xmlconcat('<abc/>', '<bar>foo</bar>');
    
          xmlconcat
    ----------------------
     <abc/><bar>foo</bar>
    

XML declarations, if present, are combined as follows. If all argument values
have the same XML version declaration, that version is used in the result,
else no version is used. If all argument values have the standalone
declaration value “yes”, then that value is used in the result. If all
argument values have a standalone declaration value and at least one is “no”,
then that is used in the result. Else the result will have no standalone
declaration. If the result is determined to require a standalone declaration
but no version declaration, a version declaration with version 1.0 will be
used because XML requires an XML declaration to contain a version declaration.
Encoding declarations are ignored and removed in all cases.

Example:

    
    
    SELECT xmlconcat('<?xml version="1.1"?><foo/>', '<?xml version="1.1" standalone="no"?><bar/>');
    
                 xmlconcat
    -----------------------------------
     <?xml version="1.1"?><foo/><bar/>
    

#### 9.15.1.3. `xmlelement` #

    
    
    xmlelement ( NAME _name_ [, XMLATTRIBUTES ( _attvalue_ [ AS _attname_ ] [, ...] ) ] [, _content_ [, ...]] ) → xml
    

The `xmlelement` expression produces an XML element with the given name,
attributes, and content. The _`name`_ and _`attname`_ items shown in the
syntax are simple identifiers, not values. The _`attvalue`_ and _`content`_
items are expressions, which can yield any PostgreSQL data type. The
argument(s) within `XMLATTRIBUTES` generate attributes of the XML element; the
_`content`_ value(s) are concatenated to form its content.

Examples:

    
    
    SELECT xmlelement(name foo);
    
     xmlelement
    ------------
     <foo/>
    
    SELECT xmlelement(name foo, xmlattributes('xyz' as bar));
    
        xmlelement
    ------------------
     <foo bar="xyz"/>
    
    SELECT xmlelement(name foo, xmlattributes(current_date as bar), 'cont', 'ent');
    
                 xmlelement
    -------------------------------------
     <foo bar="2007-01-26">content</foo>
    

Element and attribute names that are not valid XML names are escaped by
replacing the offending characters by the sequence `_x _`HHHH`_ _`, where
_`HHHH`_ is the character's Unicode codepoint in hexadecimal notation. For
example:

    
    
    SELECT xmlelement(name "foo$bar", xmlattributes('xyz' as "a&b"));
    
                xmlelement
    ----------------------------------
     <foo_x0024_bar a_x0026_b="xyz"/>
    

An explicit attribute name need not be specified if the attribute value is a
column reference, in which case the column's name will be used as the
attribute name by default. In other cases, the attribute must be given an
explicit name. So this example is valid:

    
    
    CREATE TABLE test (a xml, b xml);
    SELECT xmlelement(name test, xmlattributes(a, b)) FROM test;
    

But these are not:

    
    
    SELECT xmlelement(name test, xmlattributes('constant'), a, b) FROM test;
    SELECT xmlelement(name test, xmlattributes(func(a, b))) FROM test;
    

Element content, if specified, will be formatted according to its data type.
If the content is itself of type `xml`, complex XML documents can be
constructed. For example:

    
    
    SELECT xmlelement(name foo, xmlattributes('xyz' as bar),
                                xmlelement(name abc),
                                xmlcomment('test'),
                                xmlelement(name xyz));
    
                      xmlelement
    ----------------------------------------------
     <foo bar="xyz"><abc/><!--test--><xyz/></foo>
    

Content of other types will be formatted into valid XML character data. This
means in particular that the characters <, >, and & will be converted to
entities. Binary data (data type `bytea`) will be represented in base64 or hex
encoding, depending on the setting of the configuration parameter
[xmlbinary](runtime-config-client.html#GUC-XMLBINARY). The particular behavior
for individual data types is expected to evolve in order to align the
PostgreSQL mappings with those specified in SQL:2006 and later, as discussed
in [Section D.3.1.3](xml-limits-conformance.html#FUNCTIONS-XML-LIMITS-CASTS
"D.3.1.3. Mappings between SQL and XML Data Types and Values").

#### 9.15.1.4. `xmlforest` #

    
    
    xmlforest ( _content_ [ AS _name_ ] [, ...] ) → xml
    

The `xmlforest` expression produces an XML forest (sequence) of elements using
the given names and content. As for `xmlelement`, each _`name`_ must be a
simple identifier, while the _`content`_ expressions can have any data type.

Examples:

    
    
    SELECT xmlforest('abc' AS foo, 123 AS bar);
    
              xmlforest
    ------------------------------
     <foo>abc</foo><bar>123</bar>
    
    
    SELECT xmlforest(table_name, column_name)
    FROM information_schema.columns
    WHERE table_schema = 'pg_catalog';
    
                                    xmlforest
    ------------------------------------​-----------------------------------
     <table_name>pg_authid</table_name>​<column_name>rolname</column_name>
     <table_name>pg_authid</table_name>​<column_name>rolsuper</column_name>
     ...
    

As seen in the second example, the element name can be omitted if the content
value is a column reference, in which case the column name is used by default.
Otherwise, a name must be specified.

Element names that are not valid XML names are escaped as shown for
`xmlelement` above. Similarly, content data is escaped to make valid XML
content, unless it is already of type `xml`.

Note that XML forests are not valid XML documents if they consist of more than
one element, so it might be useful to wrap `xmlforest` expressions in
`xmlelement`.

#### 9.15.1.5. `xmlpi` #

    
    
    xmlpi ( NAME _name_ [, _content_ ] ) → xml
    

The `xmlpi` expression creates an XML processing instruction. As for
`xmlelement`, the _`name`_ must be a simple identifier, while the _`content`_
expression can have any data type. The _`content`_ , if present, must not
contain the character sequence `?>`.

Example:

    
    
    SELECT xmlpi(name php, 'echo "hello world";');
    
                xmlpi
    -----------------------------
     <?php echo "hello world";?>
    

#### 9.15.1.6. `xmlroot` #

    
    
    xmlroot ( xml, VERSION {text|NO VALUE} [, STANDALONE {YES|NO|NO VALUE} ] ) → xml
    

The `xmlroot` expression alters the properties of the root node of an XML
value. If a version is specified, it replaces the value in the root node's
version declaration; if a standalone setting is specified, it replaces the
value in the root node's standalone declaration.

    
    
    SELECT xmlroot(xmlparse(document '<?xml version="1.1"?><content>abc</content>'),
                   version '1.0', standalone yes);
    
                    xmlroot
    ----------------------------------------
     <?xml version="1.0" standalone="yes"?>
     <content>abc</content>
    

#### 9.15.1.7. `xmlagg` #

    
    
    xmlagg ( xml ) → xml
    

The function `xmlagg` is, unlike the other functions described here, an
aggregate function. It concatenates the input values to the aggregate function
call, much like `xmlconcat` does, except that concatenation occurs across rows
rather than across expressions in a single row. See [Section 9.21](functions-
aggregate.html "9.21. Aggregate Functions") for additional information about
aggregate functions.

Example:

    
    
    CREATE TABLE test (y int, x xml);
    INSERT INTO test VALUES (1, '<foo>abc</foo>');
    INSERT INTO test VALUES (2, '<bar/>');
    SELECT xmlagg(x) FROM test;
            xmlagg
    ----------------------
     <foo>abc</foo><bar/>
    

To determine the order of the concatenation, an `ORDER BY` clause may be added
to the aggregate call as described in [Section 4.2.7](sql-
expressions.html#SYNTAX-AGGREGATES "4.2.7. Aggregate Expressions"). For
example:

    
    
    SELECT xmlagg(x ORDER BY y DESC) FROM test;
            xmlagg
    ----------------------
     <bar/><foo>abc</foo>
    

The following non-standard approach used to be recommended in previous
versions, and may still be useful in specific cases:

    
    
    SELECT xmlagg(x) FROM (SELECT * FROM test ORDER BY y DESC) AS tab;
            xmlagg
    ----------------------
     <bar/><foo>abc</foo>
    

### 9.15.2. XML Predicates #

The expressions described in this section check properties of `xml` values.

#### 9.15.2.1. `IS DOCUMENT` #

    
    
    xml IS DOCUMENT → boolean
    

The expression `IS DOCUMENT` returns true if the argument XML value is a
proper XML document, false if it is not (that is, it is a content fragment),
or null if the argument is null. See [Section 8.13](datatype-xml.html
"8.13. XML Type") about the difference between documents and content
fragments.

#### 9.15.2.2. `IS NOT DOCUMENT` #

    
    
    xml IS NOT DOCUMENT → boolean
    

The expression `IS NOT DOCUMENT` returns false if the argument XML value is a
proper XML document, true if it is not (that is, it is a content fragment), or
null if the argument is null.

#### 9.15.2.3. `XMLEXISTS` #

    
    
    XMLEXISTS ( text PASSING [BY {REF|VALUE}] xml [BY {REF|VALUE}] ) → boolean
    

The function `xmlexists` evaluates an XPath 1.0 expression (the first
argument), with the passed XML value as its context item. The function returns
false if the result of that evaluation yields an empty node-set, true if it
yields any other value. The function returns null if any argument is null. A
nonnull value passed as the context item must be an XML document, not a
content fragment or any non-XML value.

Example:

    
    
    SELECT xmlexists('//town[text() = ''Toronto'']' PASSING BY VALUE '<towns><town>Toronto</town><town>Ottawa</town></towns>');
    
     xmlexists
    ------------
     t
    (1 row)
    

The `BY REF` and `BY VALUE` clauses are accepted in PostgreSQL, but are
ignored, as discussed in [Section D.3.2](xml-limits-
conformance.html#FUNCTIONS-XML-LIMITS-POSTGRESQL "D.3.2. Incidental Limits of
the Implementation").

In the SQL standard, the `xmlexists` function evaluates an expression in the
XML Query language, but PostgreSQL allows only an XPath 1.0 expression, as
discussed in [Section D.3.1](xml-limits-conformance.html#FUNCTIONS-XML-LIMITS-
XPATH1 "D.3.1. Queries Are Restricted to XPath 1.0").

#### 9.15.2.4. `xml_is_well_formed` #

    
    
    xml_is_well_formed ( text ) → boolean
    xml_is_well_formed_document ( text ) → boolean
    xml_is_well_formed_content ( text ) → boolean
    

These functions check whether a `text` string represents well-formed XML,
returning a Boolean result. `xml_is_well_formed_document` checks for a well-
formed document, while `xml_is_well_formed_content` checks for well-formed
content. `xml_is_well_formed` does the former if the [xmloption](runtime-
config-client.html#GUC-XMLOPTION) configuration parameter is set to
`DOCUMENT`, or the latter if it is set to `CONTENT`. This means that
`xml_is_well_formed` is useful for seeing whether a simple cast to type `xml`
will succeed, whereas the other two functions are useful for seeing whether
the corresponding variants of `XMLPARSE` will succeed.

Examples:

    
    
    SET xmloption TO DOCUMENT;
    SELECT xml_is_well_formed('<>');
     xml_is_well_formed
    --------------------
     f
    (1 row)
    
    SELECT xml_is_well_formed('<abc/>');
     xml_is_well_formed
    --------------------
     t
    (1 row)
    
    SET xmloption TO CONTENT;
    SELECT xml_is_well_formed('abc');
     xml_is_well_formed
    --------------------
     t
    (1 row)
    
    SELECT xml_is_well_formed_document('<pg:foo xmlns:pg="http://postgresql.org/stuff">bar</pg:foo>');
     xml_is_well_formed_document
    -----------------------------
     t
    (1 row)
    
    SELECT xml_is_well_formed_document('<pg:foo xmlns:pg="http://postgresql.org/stuff">bar</my:foo>');
     xml_is_well_formed_document
    -----------------------------
     f
    (1 row)
    

The last example shows that the checks include whether namespaces are
correctly matched.

### 9.15.3. Processing XML #

To process values of data type `xml`, PostgreSQL offers the functions `xpath`
and `xpath_exists`, which evaluate XPath 1.0 expressions, and the `XMLTABLE`
table function.

#### 9.15.3.1. `xpath` #

    
    
    xpath ( _xpath_ text, _xml_ xml [, _nsarray_ text[] ] ) → xml[]
    

The function `xpath` evaluates the XPath 1.0 expression _`xpath`_ (given as
text) against the XML value _`xml`_. It returns an array of XML values
corresponding to the node-set produced by the XPath expression. If the XPath
expression returns a scalar value rather than a node-set, a single-element
array is returned.

The second argument must be a well formed XML document. In particular, it must
have a single root node element.

The optional third argument of the function is an array of namespace mappings.
This array should be a two-dimensional `text` array with the length of the
second axis being equal to 2 (i.e., it should be an array of arrays, each of
which consists of exactly 2 elements). The first element of each array entry
is the namespace name (alias), the second the namespace URI. It is not
required that aliases provided in this array be the same as those being used
in the XML document itself (in other words, both in the XML document and in
the `xpath` function context, aliases are _local_).

Example:

    
    
    SELECT xpath('/my:a/text()', '<my:a xmlns:my="http://example.com">test</my:a>',
                 ARRAY[ARRAY['my', 'http://example.com']]);
    
     xpath
    --------
     {test}
    (1 row)
    

To deal with default (anonymous) namespaces, do something like this:

    
    
    SELECT xpath('//mydefns:b/text()', '<a xmlns="http://example.com"><b>test</b></a>',
                 ARRAY[ARRAY['mydefns', 'http://example.com']]);
    
     xpath
    --------
     {test}
    (1 row)
    

#### 9.15.3.2. `xpath_exists` #

    
    
    xpath_exists ( _xpath_ text, _xml_ xml [, _nsarray_ text[] ] ) → boolean
    

The function `xpath_exists` is a specialized form of the `xpath` function.
Instead of returning the individual XML values that satisfy the XPath 1.0
expression, this function returns a Boolean indicating whether the query was
satisfied or not (specifically, whether it produced any value other than an
empty node-set). This function is equivalent to the `XMLEXISTS` predicate,
except that it also offers support for a namespace mapping argument.

Example:

    
    
    SELECT xpath_exists('/my:a/text()', '<my:a xmlns:my="http://example.com">test</my:a>',
                         ARRAY[ARRAY['my', 'http://example.com']]);
    
     xpath_exists
    --------------
     t
    (1 row)
    

#### 9.15.3.3. `xmltable` #

    
    
    XMLTABLE (
        [ XMLNAMESPACES ( _namespace_uri_ AS _namespace_name_ [, ...] ), ]
        _row_expression_ PASSING [BY {REF|VALUE}] _document_expression_ [BY {REF|VALUE}]
        COLUMNS _name_ { _type_ [PATH _column_expression_] [DEFAULT _default_expression_] [NOT NULL | NULL]
                      | FOR ORDINALITY }
                [, ...]
    ) → setof record
    

The `xmltable` expression produces a table based on an XML value, an XPath
filter to extract rows, and a set of column definitions. Although it
syntactically resembles a function, it can only appear as a table in a query's
`FROM` clause.

The optional `XMLNAMESPACES` clause gives a comma-separated list of namespace
definitions, where each _`namespace_uri`_ is a `text` expression and each
_`namespace_name`_ is a simple identifier. It specifies the XML namespaces
used in the document and their aliases. A default namespace specification is
not currently supported.

The required _`row_expression`_ argument is an XPath 1.0 expression (given as
`text`) that is evaluated, passing the XML value _`document_expression`_ as
its context item, to obtain a set of XML nodes. These nodes are what
`xmltable` transforms into output rows. No rows will be produced if the
_`document_expression`_ is null, nor if the _`row_expression`_ produces an
empty node-set or any value other than a node-set.

_`document_expression`_ provides the context item for the _`row_expression`_.
It must be a well-formed XML document; fragments/forests are not accepted. The
`BY REF` and `BY VALUE` clauses are accepted but ignored, as discussed in
[Section D.3.2](xml-limits-conformance.html#FUNCTIONS-XML-LIMITS-POSTGRESQL
"D.3.2. Incidental Limits of the Implementation").

In the SQL standard, the `xmltable` function evaluates expressions in the XML
Query language, but PostgreSQL allows only XPath 1.0 expressions, as discussed
in [Section D.3.1](xml-limits-conformance.html#FUNCTIONS-XML-LIMITS-XPATH1
"D.3.1. Queries Are Restricted to XPath 1.0").

The required `COLUMNS` clause specifies the column(s) that will be produced in
the output table. See the syntax summary above for the format. A name is
required for each column, as is a data type (unless `FOR ORDINALITY` is
specified, in which case type `integer` is implicit). The path, default and
nullability clauses are optional.

A column marked `FOR ORDINALITY` will be populated with row numbers, starting
with 1, in the order of nodes retrieved from the _`row_expression`_ 's result
node-set. At most one column may be marked `FOR ORDINALITY`.

### Note

XPath 1.0 does not specify an order for nodes in a node-set, so code that
relies on a particular order of the results will be implementation-dependent.
Details can be found in [Section D.3.1.2](xml-limits-conformance.html#XML-
XPATH-1-SPECIFICS "D.3.1.2. Restriction of XPath to 1.0").

The _`column_expression`_ for a column is an XPath 1.0 expression that is
evaluated for each row, with the current node from the _`row_expression`_
result as its context item, to find the value of the column. If no
_`column_expression`_ is given, then the column name is used as an implicit
path.

If a column's XPath expression returns a non-XML value (which is limited to
string, boolean, or double in XPath 1.0) and the column has a PostgreSQL type
other than `xml`, the column will be set as if by assigning the value's string
representation to the PostgreSQL type. (If the value is a boolean, its string
representation is taken to be `1` or `0` if the output column's type category
is numeric, otherwise `true` or `false`.)

If a column's XPath expression returns a non-empty set of XML nodes and the
column's PostgreSQL type is `xml`, the column will be assigned the expression
result exactly, if it is of document or content form. [8]

A non-XML result assigned to an `xml` output column produces content, a single
text node with the string value of the result. An XML result assigned to a
column of any other type may not have more than one node, or an error is
raised. If there is exactly one node, the column will be set as if by
assigning the node's string value (as defined for the XPath 1.0 `string`
function) to the PostgreSQL type.

The string value of an XML element is the concatenation, in document order, of
all text nodes contained in that element and its descendants. The string value
of an element with no descendant text nodes is an empty string (not `NULL`).
Any `xsi:nil` attributes are ignored. Note that the whitespace-only `text()`
node between two non-text elements is preserved, and that leading whitespace
on a `text()` node is not flattened. The XPath 1.0 `string` function may be
consulted for the rules defining the string value of other XML node types and
non-XML values.

The conversion rules presented here are not exactly those of the SQL standard,
as discussed in [Section D.3.1.3](xml-limits-conformance.html#FUNCTIONS-XML-
LIMITS-CASTS "D.3.1.3. Mappings between SQL and XML Data Types and Values").

If the path expression returns an empty node-set (typically, when it does not
match) for a given row, the column will be set to `NULL`, unless a
_`default_expression`_ is specified; then the value resulting from evaluating
that expression is used.

A _`default_expression`_ , rather than being evaluated immediately when
`xmltable` is called, is evaluated each time a default is needed for the
column. If the expression qualifies as stable or immutable, the repeat
evaluation may be skipped. This means that you can usefully use volatile
functions like `nextval` in _`default_expression`_.

Columns may be marked `NOT NULL`. If the _`column_expression`_ for a `NOT
NULL` column does not match anything and there is no `DEFAULT` or the
_`default_expression`_ also evaluates to null, an error is reported.

Examples:

    
    
    CREATE TABLE xmldata AS SELECT
    xml $$
    <ROWS>
      <ROW id="1">
        <COUNTRY_ID>AU</COUNTRY_ID>
        <COUNTRY_NAME>Australia</COUNTRY_NAME>
      </ROW>
      <ROW id="5">
        <COUNTRY_ID>JP</COUNTRY_ID>
        <COUNTRY_NAME>Japan</COUNTRY_NAME>
        <PREMIER_NAME>Shinzo Abe</PREMIER_NAME>
        <SIZE unit="sq_mi">145935</SIZE>
      </ROW>
      <ROW id="6">
        <COUNTRY_ID>SG</COUNTRY_ID>
        <COUNTRY_NAME>Singapore</COUNTRY_NAME>
        <SIZE unit="sq_km">697</SIZE>
      </ROW>
    </ROWS>
    $$ AS data;
    
    SELECT xmltable.*
      FROM xmldata,
           XMLTABLE('//ROWS/ROW'
                    PASSING data
                    COLUMNS id int PATH '@id',
                            ordinality FOR ORDINALITY,
                            "COUNTRY_NAME" text,
                            country_id text PATH 'COUNTRY_ID',
                            size_sq_km float PATH 'SIZE[@unit = "sq_km"]',
                            size_other text PATH
                                 'concat(SIZE[@unit!="sq_km"], " ", SIZE[@unit!="sq_km"]/@unit)',
                            premier_name text PATH 'PREMIER_NAME' DEFAULT 'not specified');
    
     id | ordinality | COUNTRY_NAME | country_id | size_sq_km |  size_other  | premier_name
    ----+------------+--------------+------------+------------+--------------+---------------
      1 |          1 | Australia    | AU         |            |              | not specified
      5 |          2 | Japan        | JP         |            | 145935 sq_mi | Shinzo Abe
      6 |          3 | Singapore    | SG         |        697 |              | not specified
    

The following example shows concatenation of multiple text() nodes, usage of
the column name as XPath filter, and the treatment of whitespace, XML comments
and processing instructions:

    
    
    CREATE TABLE xmlelements AS SELECT
    xml $$
      <root>
       <element>  Hello<!-- xyxxz -->2a2<?aaaaa?> <!--x-->  bbb<x>xxx</x>CC  </element>
      </root>
    $$ AS data;
    
    SELECT xmltable.*
      FROM xmlelements, XMLTABLE('/root' PASSING data COLUMNS element text);
             element
    -------------------------
       Hello2a2   bbbxxxCC
    

The following example illustrates how the `XMLNAMESPACES` clause can be used
to specify a list of namespaces used in the XML document as well as in the
XPath expressions:

    
    
    WITH xmldata(data) AS (VALUES ('
    <example xmlns="http://example.com/myns" xmlns:B="http://example.com/b">
     <item foo="1" B:bar="2"/>
     <item foo="3" B:bar="4"/>
     <item foo="4" B:bar="5"/>
    </example>'::xml)
    )
    SELECT xmltable.*
      FROM XMLTABLE(XMLNAMESPACES('http://example.com/myns' AS x,
                                  'http://example.com/b' AS "B"),
                 '/x:example/x:item'
                    PASSING (SELECT data FROM xmldata)
                    COLUMNS foo int PATH '@foo',
                      bar int PATH '@B:bar');
     foo | bar
    -----+-----
       1 |   2
       3 |   4
       4 |   5
    (3 rows)
    

### 9.15.4. Mapping Tables to XML #

The following functions map the contents of relational tables to XML values.
They can be thought of as XML export functionality:

    
    
    table_to_xml ( _table_ regclass, _nulls_ boolean,
                   _tableforest_ boolean, _targetns_ text ) → xml
    query_to_xml ( _query_ text, _nulls_ boolean,
                   _tableforest_ boolean, _targetns_ text ) → xml
    cursor_to_xml ( _cursor_ refcursor, _count_ integer, _nulls_ boolean,
                    _tableforest_ boolean, _targetns_ text ) → xml
    

`table_to_xml` maps the content of the named table, passed as parameter
_`table`_. The `regclass` type accepts strings identifying tables using the
usual notation, including optional schema qualification and double quotes (see
[Section 8.19](datatype-oid.html "8.19. Object Identifier Types") for
details). `query_to_xml` executes the query whose text is passed as parameter
_`query`_ and maps the result set. `cursor_to_xml` fetches the indicated
number of rows from the cursor specified by the parameter _`cursor`_. This
variant is recommended if large tables have to be mapped, because the result
value is built up in memory by each function.

If _`tableforest`_ is false, then the resulting XML document looks like this:

    
    
    <tablename>
      <row>
        <columnname1>data</columnname1>
        <columnname2>data</columnname2>
      </row>
    
      <row>
        ...
      </row>
    
      ...
    </tablename>
    

If _`tableforest`_ is true, the result is an XML content fragment that looks
like this:

    
    
    <tablename>
      <columnname1>data</columnname1>
      <columnname2>data</columnname2>
    </tablename>
    
    <tablename>
      ...
    </tablename>
    
    ...
    

If no table name is available, that is, when mapping a query or a cursor, the
string `table` is used in the first format, `row` in the second format.

The choice between these formats is up to the user. The first format is a
proper XML document, which will be important in many applications. The second
format tends to be more useful in the `cursor_to_xml` function if the result
values are to be reassembled into one document later on. The functions for
producing XML content discussed above, in particular `xmlelement`, can be used
to alter the results to taste.

The data values are mapped in the same way as described for the function
`xmlelement` above.

The parameter _`nulls`_ determines whether null values should be included in
the output. If true, null values in columns are represented as:

    
    
    <columnname xsi:nil="true"/>
    

where `xsi` is the XML namespace prefix for XML Schema Instance. An
appropriate namespace declaration will be added to the result value. If false,
columns containing null values are simply omitted from the output.

The parameter _`targetns`_ specifies the desired XML namespace of the result.
If no particular namespace is wanted, an empty string should be passed.

The following functions return XML Schema documents describing the mappings
performed by the corresponding functions above:

    
    
    table_to_xmlschema ( _table_ regclass, _nulls_ boolean,
                         _tableforest_ boolean, _targetns_ text ) → xml
    query_to_xmlschema ( _query_ text, _nulls_ boolean,
                         _tableforest_ boolean, _targetns_ text ) → xml
    cursor_to_xmlschema ( _cursor_ refcursor, _nulls_ boolean,
                          _tableforest_ boolean, _targetns_ text ) → xml
    

It is essential that the same parameters are passed in order to obtain
matching XML data mappings and XML Schema documents.

The following functions produce XML data mappings and the corresponding XML
Schema in one document (or forest), linked together. They can be useful where
self-contained and self-describing results are wanted:

    
    
    table_to_xml_and_xmlschema ( _table_ regclass, _nulls_ boolean,
                                 _tableforest_ boolean, _targetns_ text ) → xml
    query_to_xml_and_xmlschema ( _query_ text, _nulls_ boolean,
                                 _tableforest_ boolean, _targetns_ text ) → xml
    

In addition, the following functions are available to produce analogous
mappings of entire schemas or the entire current database:

    
    
    schema_to_xml ( _schema_ name, _nulls_ boolean,
                    _tableforest_ boolean, _targetns_ text ) → xml
    schema_to_xmlschema ( _schema_ name, _nulls_ boolean,
                          _tableforest_ boolean, _targetns_ text ) → xml
    schema_to_xml_and_xmlschema ( _schema_ name, _nulls_ boolean,
                                  _tableforest_ boolean, _targetns_ text ) → xml
    
    database_to_xml ( _nulls_ boolean,
                      _tableforest_ boolean, _targetns_ text ) → xml
    database_to_xmlschema ( _nulls_ boolean,
                            _tableforest_ boolean, _targetns_ text ) → xml
    database_to_xml_and_xmlschema ( _nulls_ boolean,
                                    _tableforest_ boolean, _targetns_ text ) → xml
    

These functions ignore tables that are not readable by the current user. The
database-wide functions additionally ignore schemas that the current user does
not have `USAGE` (lookup) privilege for.

Note that these potentially produce a lot of data, which needs to be built up
in memory. When requesting content mappings of large schemas or databases, it
might be worthwhile to consider mapping the tables separately instead,
possibly even through a cursor.

The result of a schema content mapping looks like this:

    
    
    <schemaname>
    
    table1-mapping
    
    table2-mapping
    
    ...
    
    </schemaname>

where the format of a table mapping depends on the _`tableforest`_ parameter
as explained above.

The result of a database content mapping looks like this:

    
    
    <dbname>
    
    <schema1name>
      ...
    </schema1name>
    
    <schema2name>
      ...
    </schema2name>
    
    ...
    
    </dbname>

where the schema mapping is as above.

As an example of using the output produced by these functions, [Example
9.1](functions-xml.html#XSLT-XML-HTML "Example 9.1. XSLT Stylesheet for
Converting SQL/XML Output to HTML") shows an XSLT stylesheet that converts the
output of `table_to_xml_and_xmlschema` to an HTML document containing a
tabular rendition of the table data. In a similar manner, the results from
these functions can be converted into other XML-based formats.

**Example  9.1. XSLT Stylesheet for Converting SQL/XML Output to HTML**

    
    
    <?xml version="1.0"?>
    <xsl:stylesheet version="1.0"
        xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
        xmlns:xsd="http://www.w3.org/2001/XMLSchema"
        xmlns="http://www.w3.org/1999/xhtml"
    >
    
      <xsl:output method="xml"
          doctype-system="http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"
          doctype-public="-//W3C/DTD XHTML 1.0 Strict//EN"
          indent="yes"/>
    
      <xsl:template match="/*">
        <xsl:variable name="schema" select="//xsd:schema"/>
        <xsl:variable name="tabletypename"
                      select="$schema/xsd:element[@name=name(current())]/@type"/>
        <xsl:variable name="rowtypename"
                      select="$schema/xsd:complexType[@name=$tabletypename]/xsd:sequence/xsd:element[@name='row']/@type"/>
    
        <html>
          <head>
            <title><xsl:value-of select="name(current())"/></title>
          </head>
          <body>
            <table>
              <tr>
                <xsl:for-each select="$schema/xsd:complexType[@name=$rowtypename]/xsd:sequence/xsd:element/@name">
                  <th><xsl:value-of select="."/></th>
                </xsl:for-each>
              </tr>
    
              <xsl:for-each select="row">
                <tr>
                  <xsl:for-each select="*">
                    <td><xsl:value-of select="."/></td>
                  </xsl:for-each>
                </tr>
              </xsl:for-each>
            </table>
          </body>
        </html>
      </xsl:template>
    
    </xsl:stylesheet>
    

  

  

* * *

[8] A result containing more than one element node at the top level, or non-
whitespace text outside of an element, is an example of content form. An XPath
result can be of neither form, for example if it returns an attribute node
selected from the element that contains it. Such a result will be put into
content form with each such disallowed node replaced by its string value, as
defined for the XPath 1.0 `string` function.

* * *

[Prev](functions-uuid.html "9.14. UUID Functions")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](functions-json.html "9.16. JSON Functions and Operators")  
---|---|---  
9.14. UUID Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  9.16. JSON Functions and Operators  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-xml.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

