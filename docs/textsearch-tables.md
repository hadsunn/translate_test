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

Supported Versions: [Current](/docs/current/textsearch-tables.html "PostgreSQL
17 - 12.2. Tables and Indexes") ([17](/docs/17/textsearch-tables.html
"PostgreSQL 17 - 12.2. Tables and Indexes")) / [16](/docs/16/textsearch-
tables.html "PostgreSQL 16 - 12.2. Tables and Indexes") /
[15](/docs/15/textsearch-tables.html "PostgreSQL 15 - 12.2. Tables and
Indexes") / [14](/docs/14/textsearch-tables.html "PostgreSQL 14 - 12.2. Tables
and Indexes") / [13](/docs/13/textsearch-tables.html "PostgreSQL 13 -
12.2. Tables and Indexes")

Development Versions: [18](/docs/18/textsearch-tables.html "PostgreSQL 18 -
12.2. Tables and Indexes") / [devel](/docs/devel/textsearch-tables.html
"PostgreSQL devel - 12.2. Tables and Indexes")

Unsupported versions: [12](/docs/12/textsearch-tables.html "PostgreSQL 12 -
12.2. Tables and Indexes") / [11](/docs/11/textsearch-tables.html "PostgreSQL
11 - 12.2. Tables and Indexes") / [10](/docs/10/textsearch-tables.html
"PostgreSQL 10 - 12.2. Tables and Indexes") / [9.6](/docs/9.6/textsearch-
tables.html "PostgreSQL 9.6 - 12.2. Tables and Indexes") /
[9.5](/docs/9.5/textsearch-tables.html "PostgreSQL 9.5 - 12.2. Tables and
Indexes") / [9.4](/docs/9.4/textsearch-tables.html "PostgreSQL 9.4 -
12.2. Tables and Indexes") / [9.3](/docs/9.3/textsearch-tables.html
"PostgreSQL 9.3 - 12.2. Tables and Indexes") / [9.2](/docs/9.2/textsearch-
tables.html "PostgreSQL 9.2 - 12.2. Tables and Indexes") /
[9.1](/docs/9.1/textsearch-tables.html "PostgreSQL 9.1 - 12.2. Tables and
Indexes") / [9.0](/docs/9.0/textsearch-tables.html "PostgreSQL 9.0 -
12.2. Tables and Indexes") / [8.4](/docs/8.4/textsearch-tables.html
"PostgreSQL 8.4 - 12.2. Tables and Indexes") / [8.3](/docs/8.3/textsearch-
tables.html "PostgreSQL 8.3 - 12.2. Tables and Indexes")

__

12.2. Tables and Indexes  
---  
[Prev](textsearch-intro.html "12.1. Introduction")  | [Up](textsearch.html "Chapter 12. Full Text Search") | Chapter 12. Full Text Search | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](textsearch-controls.html "12.3. Controlling Text Search")  
  
* * *

## 12.2. Tables and Indexes #

[12.2.1. Searching a Table](textsearch-tables.html#TEXTSEARCH-TABLES-SEARCH)

[12.2.2. Creating Indexes](textsearch-tables.html#TEXTSEARCH-TABLES-INDEX)

The examples in the previous section illustrated full text matching using
simple constant strings. This section shows how to search table data,
optionally using indexes.

### 12.2.1. Searching a Table #

It is possible to do a full text search without an index. A simple query to
print the `title` of each row that contains the word `friend` in its `body`
field is:

    
    
    SELECT title
    FROM pgweb
    WHERE to_tsvector('english', body) @@ to_tsquery('english', 'friend');
    

This will also find related words such as `friends` and `friendly`, since all
these are reduced to the same normalized lexeme.

The query above specifies that the `english` configuration is to be used to
parse and normalize the strings. Alternatively we could omit the configuration
parameters:

    
    
    SELECT title
    FROM pgweb
    WHERE to_tsvector(body) @@ to_tsquery('friend');
    

This query will use the configuration set by
[default_text_search_config](runtime-config-client.html#GUC-DEFAULT-TEXT-
SEARCH-CONFIG).

A more complex example is to select the ten most recent documents that contain
`create` and `table` in the `title` or `body`:

    
    
    SELECT title
    FROM pgweb
    WHERE to_tsvector(title || ' ' || body) @@ to_tsquery('create & table')
    ORDER BY last_mod_date DESC
    LIMIT 10;
    

For clarity we omitted the `coalesce` function calls which would be needed to
find rows that contain `NULL` in one of the two fields.

Although these queries will work without an index, most applications will find
this approach too slow, except perhaps for occasional ad-hoc searches.
Practical use of text searching usually requires creating an index.

### 12.2.2. Creating Indexes #

We can create a GIN index ([Section 12.9](textsearch-indexes.html
"12.9. Preferred Index Types for Text Search")) to speed up text searches:

    
    
    CREATE INDEX pgweb_idx ON pgweb USING GIN (to_tsvector('english', body));
    

Notice that the 2-argument version of `to_tsvector` is used. Only text search
functions that specify a configuration name can be used in expression indexes
([Section 11.7](indexes-expressional.html "11.7. Indexes on Expressions")).
This is because the index contents must be unaffected by
[default_text_search_config](runtime-config-client.html#GUC-DEFAULT-TEXT-
SEARCH-CONFIG). If they were affected, the index contents might be
inconsistent because different entries could contain `tsvector`s that were
created with different text search configurations, and there would be no way
to guess which was which. It would be impossible to dump and restore such an
index correctly.

Because the two-argument version of `to_tsvector` was used in the index above,
only a query reference that uses the 2-argument version of `to_tsvector` with
the same configuration name will use that index. That is, `WHERE
to_tsvector('english', body) @@ 'a & b'` can use the index, but `WHERE
to_tsvector(body) @@ 'a & b'` cannot. This ensures that an index will be used
only with the same configuration used to create the index entries.

It is possible to set up more complex expression indexes wherein the
configuration name is specified by another column, e.g.:

    
    
    CREATE INDEX pgweb_idx ON pgweb USING GIN (to_tsvector(config_name, body));
    

where `config_name` is a column in the `pgweb` table. This allows mixed
configurations in the same index while recording which configuration was used
for each index entry. This would be useful, for example, if the document
collection contained documents in different languages. Again, queries that are
meant to use the index must be phrased to match, e.g., `WHERE
to_tsvector(config_name, body) @@ 'a & b'`.

Indexes can even concatenate columns:

    
    
    CREATE INDEX pgweb_idx ON pgweb USING GIN (to_tsvector('english', title || ' ' || body));
    

Another approach is to create a separate `tsvector` column to hold the output
of `to_tsvector`. To keep this column automatically up to date with its source
data, use a stored generated column. This example is a concatenation of
`title` and `body`, using `coalesce` to ensure that one field will still be
indexed when the other is `NULL`:

    
    
    ALTER TABLE pgweb
        ADD COLUMN textsearchable_index_col tsvector
                   GENERATED ALWAYS AS (to_tsvector('english', coalesce(title, '') || ' ' || coalesce(body, ''))) STORED;
    

Then we create a GIN index to speed up the search:

    
    
    CREATE INDEX textsearch_idx ON pgweb USING GIN (textsearchable_index_col);
    

Now we are ready to perform a fast full text search:

    
    
    SELECT title
    FROM pgweb
    WHERE textsearchable_index_col @@ to_tsquery('create & table')
    ORDER BY last_mod_date DESC
    LIMIT 10;
    

One advantage of the separate-column approach over an expression index is that
it is not necessary to explicitly specify the text search configuration in
queries in order to make use of the index. As shown in the example above, the
query can depend on `default_text_search_config`. Another advantage is that
searches will be faster, since it will not be necessary to redo the
`to_tsvector` calls to verify index matches. (This is more important when
using a GiST index than a GIN index; see [Section 12.9](textsearch-
indexes.html "12.9. Preferred Index Types for Text Search").) The expression-
index approach is simpler to set up, however, and it requires less disk space
since the `tsvector` representation is not stored explicitly.

* * *

[Prev](textsearch-intro.html "12.1. Introduction")  | [Up](textsearch.html "Chapter 12. Full Text Search") |  [Next](textsearch-controls.html "12.3. Controlling Text Search")  
---|---|---  
12.1. Introduction  | [Home](index.html "PostgreSQL 16.9 Documentation") |  12.3. Controlling Text Search  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/textsearch-tables.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

