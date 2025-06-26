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

Supported Versions: [Current](/docs/current/rules-materializedviews.html
"PostgreSQL 17 - 41.3. Materialized Views") ([17](/docs/17/rules-
materializedviews.html "PostgreSQL 17 - 41.3. Materialized Views")) /
[16](/docs/16/rules-materializedviews.html "PostgreSQL 16 - 41.3. Materialized
Views") / [15](/docs/15/rules-materializedviews.html "PostgreSQL 15 -
41.3. Materialized Views") / [14](/docs/14/rules-materializedviews.html
"PostgreSQL 14 - 41.3. Materialized Views") / [13](/docs/13/rules-
materializedviews.html "PostgreSQL 13 - 41.3. Materialized Views")

Development Versions: [18](/docs/18/rules-materializedviews.html "PostgreSQL
18 - 41.3. Materialized Views") / [devel](/docs/devel/rules-
materializedviews.html "PostgreSQL devel - 41.3. Materialized Views")

Unsupported versions: [12](/docs/12/rules-materializedviews.html "PostgreSQL
12 - 41.3. Materialized Views") / [11](/docs/11/rules-materializedviews.html
"PostgreSQL 11 - 41.3. Materialized Views") / [10](/docs/10/rules-
materializedviews.html "PostgreSQL 10 - 41.3. Materialized Views") /
[9.6](/docs/9.6/rules-materializedviews.html "PostgreSQL 9.6 -
41.3. Materialized Views") / [9.5](/docs/9.5/rules-materializedviews.html
"PostgreSQL 9.5 - 41.3. Materialized Views") / [9.4](/docs/9.4/rules-
materializedviews.html "PostgreSQL 9.4 - 41.3. Materialized Views") /
[9.3](/docs/9.3/rules-materializedviews.html "PostgreSQL 9.3 -
41.3. Materialized Views")

__

41.3. Materialized Views  
---  
[Prev](rules-views.html "41.2. Views and the Rule System")  | [Up](rules.html "Chapter 41. The Rule System") | Chapter 41. The Rule System | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](rules-update.html "41.4. Rules on INSERT, UPDATE, and DELETE")  
  
* * *

## 41.3. Materialized Views #

Materialized views in PostgreSQL use the rule system like views do, but
persist the results in a table-like form. The main differences between:

    
    
    CREATE MATERIALIZED VIEW mymatview AS SELECT * FROM mytab;
    

and:

    
    
    CREATE TABLE mymatview AS SELECT * FROM mytab;
    

are that the materialized view cannot subsequently be directly updated and
that the query used to create the materialized view is stored in exactly the
same way that a view's query is stored, so that fresh data can be generated
for the materialized view with:

    
    
    REFRESH MATERIALIZED VIEW mymatview;
    

The information about a materialized view in the PostgreSQL system catalogs is
exactly the same as it is for a table or view. So for the parser, a
materialized view is a relation, just like a table or a view. When a
materialized view is referenced in a query, the data is returned directly from
the materialized view, like from a table; the rule is only used for populating
the materialized view.

While access to the data stored in a materialized view is often much faster
than accessing the underlying tables directly or through a view, the data is
not always current; yet sometimes current data is not needed. Consider a table
which records sales:

    
    
    CREATE TABLE invoice (
        invoice_no    integer        PRIMARY KEY,
        seller_no     integer,       -- ID of salesperson
        invoice_date  date,          -- date of sale
        invoice_amt   numeric(13,2)  -- amount of sale
    );
    

If people want to be able to quickly graph historical sales data, they might
want to summarize, and they may not care about the incomplete data for the
current date:

    
    
    CREATE MATERIALIZED VIEW sales_summary AS
      SELECT
          seller_no,
          invoice_date,
          sum(invoice_amt)::numeric(13,2) as sales_amt
        FROM invoice
        WHERE invoice_date < CURRENT_DATE
        GROUP BY
          seller_no,
          invoice_date;
    
    CREATE UNIQUE INDEX sales_summary_seller
      ON sales_summary (seller_no, invoice_date);
    

This materialized view might be useful for displaying a graph in the dashboard
created for salespeople. A job could be scheduled to update the statistics
each night using this SQL statement:

    
    
    REFRESH MATERIALIZED VIEW sales_summary;
    

Another use for a materialized view is to allow faster access to data brought
across from a remote system through a foreign data wrapper. A simple example
using `file_fdw` is below, with timings, but since this is using cache on the
local system the performance difference compared to access to a remote system
would usually be greater than shown here. Notice we are also exploiting the
ability to put an index on the materialized view, whereas `file_fdw` does not
support indexes; this advantage might not apply for other sorts of foreign
data access.

Setup:

    
    
    CREATE EXTENSION file_fdw;
    CREATE SERVER local_file FOREIGN DATA WRAPPER file_fdw;
    CREATE FOREIGN TABLE words (word text NOT NULL)
      SERVER local_file
      OPTIONS (filename '/usr/share/dict/words');
    CREATE MATERIALIZED VIEW wrd AS SELECT * FROM words;
    CREATE UNIQUE INDEX wrd_word ON wrd (word);
    CREATE EXTENSION pg_trgm;
    CREATE INDEX wrd_trgm ON wrd USING gist (word gist_trgm_ops);
    VACUUM ANALYZE wrd;
    

Now let's spell-check a word. Using `file_fdw` directly:

    
    
    SELECT count(*) FROM words WHERE word = 'caterpiler';
    
     count
    -------
         0
    (1 row)
    

With `EXPLAIN ANALYZE`, we see:

    
    
     Aggregate  (cost=21763.99..21764.00 rows=1 width=0) (actual time=188.180..188.181 rows=1 loops=1)
       ->  Foreign Scan on words  (cost=0.00..21761.41 rows=1032 width=0) (actual time=188.177..188.177 rows=0 loops=1)
             Filter: (word = 'caterpiler'::text)
             Rows Removed by Filter: 479829
             Foreign File: /usr/share/dict/words
             Foreign File Size: 4953699
     Planning time: 0.118 ms
     Execution time: 188.273 ms
    

If the materialized view is used instead, the query is much faster:

    
    
     Aggregate  (cost=4.44..4.45 rows=1 width=0) (actual time=0.042..0.042 rows=1 loops=1)
       ->  Index Only Scan using wrd_word on wrd  (cost=0.42..4.44 rows=1 width=0) (actual time=0.039..0.039 rows=0 loops=1)
             Index Cond: (word = 'caterpiler'::text)
             Heap Fetches: 0
     Planning time: 0.164 ms
     Execution time: 0.117 ms
    

Either way, the word is spelled wrong, so let's look for what we might have
wanted. Again using `file_fdw` and `pg_trgm`:

    
    
    SELECT word FROM words ORDER BY word <-> 'caterpiler' LIMIT 10;
    
         word
    ---------------
     cater
     caterpillar
     Caterpillar
     caterpillars
     caterpillar's
     Caterpillar's
     caterer
     caterer's
     caters
     catered
    (10 rows)
    
    
    
     Limit  (cost=11583.61..11583.64 rows=10 width=32) (actual time=1431.591..1431.594 rows=10 loops=1)
       ->  Sort  (cost=11583.61..11804.76 rows=88459 width=32) (actual time=1431.589..1431.591 rows=10 loops=1)
             Sort Key: ((word <-> 'caterpiler'::text))
             Sort Method: top-N heapsort  Memory: 25kB
             ->  Foreign Scan on words  (cost=0.00..9672.05 rows=88459 width=32) (actual time=0.057..1286.455 rows=479829 loops=1)
                   Foreign File: /usr/share/dict/words
                   Foreign File Size: 4953699
     Planning time: 0.128 ms
     Execution time: 1431.679 ms
    

Using the materialized view:

    
    
     Limit  (cost=0.29..1.06 rows=10 width=10) (actual time=187.222..188.257 rows=10 loops=1)
       ->  Index Scan using wrd_trgm on wrd  (cost=0.29..37020.87 rows=479829 width=10) (actual time=187.219..188.252 rows=10 loops=1)
             Order By: (word <-> 'caterpiler'::text)
     Planning time: 0.196 ms
     Execution time: 198.640 ms
    

If you can tolerate periodic update of the remote data to the local database,
the performance benefit can be substantial.

* * *

[Prev](rules-views.html "41.2. Views and the Rule System")  | [Up](rules.html "Chapter 41. The Rule System") |  [Next](rules-update.html "41.4. Rules on INSERT, UPDATE, and DELETE")  
---|---|---  
41.2. Views and the Rule System  | [Home](index.html "PostgreSQL 16.9 Documentation") |  41.4. Rules on `INSERT`, `UPDATE`, and `DELETE`  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/rules-materializedviews.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

