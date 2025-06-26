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

Supported Versions: [Current](/docs/current/xml2.html "PostgreSQL 17 -
F.50. xml2 — XPath querying and XSLT functionality") ([17](/docs/17/xml2.html
"PostgreSQL 17 - F.50. xml2 — XPath querying and XSLT functionality")) /
[16](/docs/16/xml2.html "PostgreSQL 16 - F.50. xml2 — XPath querying and XSLT
functionality") / [15](/docs/15/xml2.html "PostgreSQL 15 - F.50. xml2 — XPath
querying and XSLT functionality") / [14](/docs/14/xml2.html "PostgreSQL 14 -
F.50. xml2 — XPath querying and XSLT functionality") / [13](/docs/13/xml2.html
"PostgreSQL 13 - F.50. xml2 — XPath querying and XSLT functionality")

Development Versions: [18](/docs/18/xml2.html "PostgreSQL 18 - F.50. xml2 —
XPath querying and XSLT functionality") / [devel](/docs/devel/xml2.html
"PostgreSQL devel - F.50. xml2 — XPath querying and XSLT functionality")

Unsupported versions: [12](/docs/12/xml2.html "PostgreSQL 12 - F.50. xml2 —
XPath querying and XSLT functionality") / [11](/docs/11/xml2.html "PostgreSQL
11 - F.50. xml2 — XPath querying and XSLT functionality") /
[10](/docs/10/xml2.html "PostgreSQL 10 - F.50. xml2 — XPath querying and XSLT
functionality") / [9.6](/docs/9.6/xml2.html "PostgreSQL 9.6 - F.50. xml2 —
XPath querying and XSLT functionality") / [9.5](/docs/9.5/xml2.html
"PostgreSQL 9.5 - F.50. xml2 — XPath querying and XSLT functionality") /
[9.4](/docs/9.4/xml2.html "PostgreSQL 9.4 - F.50. xml2 — XPath querying and
XSLT functionality") / [9.3](/docs/9.3/xml2.html "PostgreSQL 9.3 - F.50. xml2
— XPath querying and XSLT functionality") / [9.2](/docs/9.2/xml2.html
"PostgreSQL 9.2 - F.50. xml2 — XPath querying and XSLT functionality") /
[9.1](/docs/9.1/xml2.html "PostgreSQL 9.1 - F.50. xml2 — XPath querying and
XSLT functionality") / [9.0](/docs/9.0/xml2.html "PostgreSQL 9.0 - F.50. xml2
— XPath querying and XSLT functionality") / [8.4](/docs/8.4/xml2.html
"PostgreSQL 8.4 - F.50. xml2 — XPath querying and XSLT functionality") /
[8.3](/docs/8.3/xml2.html "PostgreSQL 8.3 - F.50. xml2 — XPath querying and
XSLT functionality")

__

F.50. xml2 — XPath querying and XSLT functionality  
---  
[Prev](uuid-ossp.html "F.49. uuid-ossp — a UUID generator")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](contrib-prog.html "Appendix G. Additional Supplied Programs")  
  
* * *

## F.50. xml2 — XPath querying and XSLT functionality #

[F.50.1. Deprecation Notice](xml2.html#XML2-DEPRECATION)

[F.50.2. Description of Functions](xml2.html#XML2-FUNCTIONS)

[F.50.3. `xpath_table`](xml2.html#XML2-XPATH-TABLE)

[F.50.4. XSLT Functions](xml2.html#XML2-XSLT)

[F.50.5. Author](xml2.html#XML2-AUTHOR)

The `xml2` module provides XPath querying and XSLT functionality.

### F.50.1. Deprecation Notice #

From PostgreSQL 8.3 on, there is XML-related functionality based on the
SQL/XML standard in the core server. That functionality covers XML syntax
checking and XPath queries, which is what this module does, and more, but the
API is not at all compatible. It is planned that this module will be removed
in a future version of PostgreSQL in favor of the newer standard API, so you
are encouraged to try converting your applications. If you find that some of
the functionality of this module is not available in an adequate form with the
newer API, please explain your issue to `<[pgsql-
hackers@lists.postgresql.org](mailto:pgsql-hackers@lists.postgresql.org)>` so
that the deficiency can be addressed.

### F.50.2. Description of Functions #

[Table F.36](xml2.html#XML2-FUNCTIONS-TABLE "Table F.36. xml2 Functions")
shows the functions provided by this module. These functions provide
straightforward XML parsing and XPath queries.

**Table  F.36. `xml2` Functions**

Function Description  
---  
`xml_valid` ( _`document`_ `text` ) → `boolean` Parses the given document and
returns true if the document is well-formed XML. (Note: this is an alias for
the standard PostgreSQL function `xml_is_well_formed()`. The name
`xml_valid()` is technically incorrect since validity and well-formedness have
different meanings in XML.)  
`xpath_string` ( _`document`_ `text`, _`query`_ `text` ) → `text` Evaluates
the XPath query on the supplied document, and casts the result to `text`.  
`xpath_number` ( _`document`_ `text`, _`query`_ `text` ) → `real` Evaluates
the XPath query on the supplied document, and casts the result to `real`.  
`xpath_bool` ( _`document`_ `text`, _`query`_ `text` ) → `boolean` Evaluates
the XPath query on the supplied document, and casts the result to `boolean`.  
`xpath_nodeset` ( _`document`_ `text`, _`query`_ `text`, _`toptag`_ `text`,
_`itemtag`_ `text` ) → `text` Evaluates the query on the document and wraps
the result in XML tags. If the result is multivalued, the output will look
like:

    
    
    <toptag>
    <itemtag>Value 1 which could be an XML fragment</itemtag>
    <itemtag>Value 2....</itemtag>
    </toptag>
    

If either _`toptag`_ or _`itemtag`_ is an empty string, the relevant tag is
omitted.  
`xpath_nodeset` ( _`document`_ `text`, _`query`_ `text`, _`itemtag`_ `text` )
→ `text` Like `xpath_nodeset(document, query, toptag, itemtag)` but result
omits _`toptag`_.  
`xpath_nodeset` ( _`document`_ `text`, _`query`_ `text` ) → `text` Like
`xpath_nodeset(document, query, toptag, itemtag)` but result omits both tags.  
`xpath_list` ( _`document`_ `text`, _`query`_ `text`, _`separator`_ `text` ) →
`text` Evaluates the query on the document and returns multiple values
separated by the specified separator, for example `Value 1,Value 2,Value 3` if
_`separator`_ is `,`.  
`xpath_list` ( _`document`_ `text`, _`query`_ `text` ) → `text` This is a
wrapper for the above function that uses `,` as the separator.  
  
  

### F.50.3. `xpath_table` #

    
    
    xpath_table(text key, text document, text relation, text xpaths, text criteria) returns setof record
    

`xpath_table` is a table function that evaluates a set of XPath queries on
each of a set of documents and returns the results as a table. The primary key
field from the original document table is returned as the first column of the
result so that the result set can readily be used in joins. The parameters are
described in [Table F.37](xml2.html#XML2-XPATH-TABLE-PARAMETERS
"Table F.37. xpath_table Parameters").

**Table  F.37. `xpath_table` Parameters**

Parameter | Description  
---|---  
_`key`_ |  the name of the “key” field — this is just a field to be used as the first column of the output table, i.e., it identifies the record from which each output row came (see note below about multiple values)  
_`document`_ |  the name of the field containing the XML document  
_`relation`_ |  the name of the table or view containing the documents  
_`xpaths`_ |  one or more XPath expressions, separated by `|`  
_`criteria`_ |  the contents of the WHERE clause. This cannot be omitted, so use `true` or `1=1` if you want to process all the rows in the relation  
  
  

These parameters (except the XPath strings) are just substituted into a plain
SQL SELECT statement, so you have some flexibility — the statement is

`SELECT <key>, <document> FROM <relation> WHERE <criteria>`

so those parameters can be _anything_ valid in those particular locations. The
result from this SELECT needs to return exactly two columns (which it will
unless you try to list multiple fields for key or document). Beware that this
simplistic approach requires that you validate any user-supplied values to
avoid SQL injection attacks.

The function has to be used in a `FROM` expression, with an `AS` clause to
specify the output columns; for example

    
    
    SELECT * FROM
    xpath_table('article_id',
                'article_xml',
                'articles',
                '/article/author|/article/pages|/article/title',
                'date_entered > ''2003-01-01'' ')
    AS t(article_id integer, author text, page_count integer, title text);
    

The `AS` clause defines the names and types of the columns in the output
table. The first is the “key” field and the rest correspond to the XPath
queries. If there are more XPath queries than result columns, the extra
queries will be ignored. If there are more result columns than XPath queries,
the extra columns will be NULL.

Notice that this example defines the `page_count` result column as an integer.
The function deals internally with string representations, so when you say you
want an integer in the output, it will take the string representation of the
XPath result and use PostgreSQL input functions to transform it into an
integer (or whatever type the `AS` clause requests). An error will result if
it can't do this — for example if the result is empty — so you may wish to
just stick to `text` as the column type if you think your data has any
problems.

The calling `SELECT` statement doesn't necessarily have to be just `SELECT *`
— it can reference the output columns by name or join them to other tables.
The function produces a virtual table with which you can perform any operation
you wish (e.g., aggregation, joining, sorting etc.). So we could also have:

    
    
    SELECT t.title, p.fullname, p.email
    FROM xpath_table('article_id', 'article_xml', 'articles',
                     '/article/title|/article/author/@id',
                     'xpath_string(article_xml,''/article/@date'') > ''2003-03-20'' ')
           AS t(article_id integer, title text, author_id integer),
         tblPeopleInfo AS p
    WHERE t.author_id = p.person_id;
    

as a more complicated example. Of course, you could wrap all of this in a view
for convenience.

#### F.50.3.1. Multivalued Results #

The `xpath_table` function assumes that the results of each XPath query might
be multivalued, so the number of rows returned by the function may not be the
same as the number of input documents. The first row returned contains the
first result from each query, the second row the second result from each
query. If one of the queries has fewer values than the others, null values
will be returned instead.

In some cases, a user will know that a given XPath query will return only a
single result (perhaps a unique document identifier) — if used alongside an
XPath query returning multiple results, the single-valued result will appear
only on the first row of the result. The solution to this is to use the key
field as part of a join against a simpler XPath query. As an example:

    
    
    CREATE TABLE test (
        id int PRIMARY KEY,
        xml text
    );
    
    INSERT INTO test VALUES (1, '<doc num="C1">
    <line num="L1"><a>1</a><b>2</b><c>3</c></line>
    <line num="L2"><a>11</a><b>22</b><c>33</c></line>
    </doc>');
    
    INSERT INTO test VALUES (2, '<doc num="C2">
    <line num="L1"><a>111</a><b>222</b><c>333</c></line>
    <line num="L2"><a>111</a><b>222</b><c>333</c></line>
    </doc>');
    
    SELECT * FROM
      xpath_table('id','xml','test',
                  '/doc/@num|/doc/line/@num|/doc/line/a|/doc/line/b|/doc/line/c',
                  'true')
      AS t(id int, doc_num varchar(10), line_num varchar(10), val1 int, val2 int, val3 int)
    WHERE id = 1 ORDER BY doc_num, line_num
    
     id | doc_num | line_num | val1 | val2 | val3
    ----+---------+----------+------+------+------
      1 | C1      | L1       |    1 |    2 |    3
      1 |         | L2       |   11 |   22 |   33
    

To get `doc_num` on every line, the solution is to use two invocations of
`xpath_table` and join the results:

    
    
    SELECT t.*,i.doc_num FROM
      xpath_table('id', 'xml', 'test',
                  '/doc/line/@num|/doc/line/a|/doc/line/b|/doc/line/c',
                  'true')
        AS t(id int, line_num varchar(10), val1 int, val2 int, val3 int),
      xpath_table('id', 'xml', 'test', '/doc/@num', 'true')
        AS i(id int, doc_num varchar(10))
    WHERE i.id=t.id AND i.id=1
    ORDER BY doc_num, line_num;
    
     id | line_num | val1 | val2 | val3 | doc_num
    ----+----------+------+------+------+---------
      1 | L1       |    1 |    2 |    3 | C1
      1 | L2       |   11 |   22 |   33 | C1
    (2 rows)
    

### F.50.4. XSLT Functions #

The following functions are available if libxslt is installed:

#### F.50.4.1. `xslt_process` #

    
    
    xslt_process(text document, text stylesheet, text paramlist) returns text
    

This function applies the XSL stylesheet to the document and returns the
transformed result. The `paramlist` is a list of parameter assignments to be
used in the transformation, specified in the form `a=1,b=2`. Note that the
parameter parsing is very simple-minded: parameter values cannot contain
commas!

There is also a two-parameter version of `xslt_process` which does not pass
any parameters to the transformation.

### F.50.5. Author #

John Gray `<[jgray@azuli.co.uk](mailto:jgray@azuli.co.uk)>`

Development of this module was sponsored by Torchbox Ltd. (www.torchbox.com).
It has the same BSD license as PostgreSQL.

* * *

[Prev](uuid-ossp.html "F.49. uuid-ossp — a UUID generator")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](contrib-prog.html "Appendix G. Additional Supplied Programs")  
---|---|---  
F.49. uuid-ossp — a UUID generator  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Appendix G. Additional Supplied Programs  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/xml2.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

