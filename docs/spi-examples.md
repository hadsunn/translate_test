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

Supported Versions: [Current](/docs/current/spi-examples.html "PostgreSQL 17 -
47.6. Examples") ([17](/docs/17/spi-examples.html "PostgreSQL 17 -
47.6. Examples")) / [16](/docs/16/spi-examples.html "PostgreSQL 16 -
47.6. Examples") / [15](/docs/15/spi-examples.html "PostgreSQL 15 -
47.6. Examples") / [14](/docs/14/spi-examples.html "PostgreSQL 14 -
47.6. Examples") / [13](/docs/13/spi-examples.html "PostgreSQL 13 -
47.6. Examples")

Development Versions: [18](/docs/18/spi-examples.html "PostgreSQL 18 -
47.6. Examples") / [devel](/docs/devel/spi-examples.html "PostgreSQL devel -
47.6. Examples")

Unsupported versions: [12](/docs/12/spi-examples.html "PostgreSQL 12 -
47.6. Examples") / [11](/docs/11/spi-examples.html "PostgreSQL 11 -
47.6. Examples") / [10](/docs/10/spi-examples.html "PostgreSQL 10 -
47.6. Examples") / [9.6](/docs/9.6/spi-examples.html "PostgreSQL 9.6 -
47.6. Examples") / [9.5](/docs/9.5/spi-examples.html "PostgreSQL 9.5 -
47.6. Examples") / [9.4](/docs/9.4/spi-examples.html "PostgreSQL 9.4 -
47.6. Examples") / [9.3](/docs/9.3/spi-examples.html "PostgreSQL 9.3 -
47.6. Examples") / [9.2](/docs/9.2/spi-examples.html "PostgreSQL 9.2 -
47.6. Examples") / [9.1](/docs/9.1/spi-examples.html "PostgreSQL 9.1 -
47.6. Examples") / [9.0](/docs/9.0/spi-examples.html "PostgreSQL 9.0 -
47.6. Examples") / [8.4](/docs/8.4/spi-examples.html "PostgreSQL 8.4 -
47.6. Examples") / [8.3](/docs/8.3/spi-examples.html "PostgreSQL 8.3 -
47.6. Examples") / [8.2](/docs/8.2/spi-examples.html "PostgreSQL 8.2 -
47.6. Examples") / [8.1](/docs/8.1/spi-examples.html "PostgreSQL 8.1 -
47.6. Examples") / [8.0](/docs/8.0/spi-examples.html "PostgreSQL 8.0 -
47.6. Examples") / [7.4](/docs/7.4/spi-examples.html "PostgreSQL 7.4 -
47.6. Examples") / [7.3](/docs/7.3/spi-examples.html "PostgreSQL 7.3 -
47.6. Examples") / [7.2](/docs/7.2/spi-examples.html "PostgreSQL 7.2 -
47.6. Examples") / [7.1](/docs/7.1/spi-examples.html "PostgreSQL 7.1 -
47.6. Examples")

__

47.6. Examples  
---  
[Prev](spi-visibility.html "47.5. Visibility of Data Changes")  | [Up](spi.html "Chapter 47. Server Programming Interface") | Chapter 47. Server Programming Interface | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](bgworker.html "Chapter 48. Background Worker Processes")  
  
* * *

## 47.6. Examples #

This section contains a very simple example of SPI usage. The C function
`execq` takes an SQL command as its first argument and a row count as its
second, executes the command using `SPI_exec` and returns the number of rows
that were processed by the command. You can find more complex examples for SPI
in the source tree in `src/test/regress/regress.c` and in the [spi](contrib-
spi.html "F.41. spi — Server Programming Interface features/examples") module.

    
    
    #include "postgres.h"
    
    #include "executor/spi.h"
    #include "utils/builtins.h"
    
    PG_MODULE_MAGIC;
    
    PG_FUNCTION_INFO_V1(execq);
    
    Datum
    execq(PG_FUNCTION_ARGS)
    {
        char *command;
        int cnt;
        int ret;
        uint64 proc;
    
        /* Convert given text object to a C string */
        command = text_to_cstring(PG_GETARG_TEXT_PP(0));
        cnt = PG_GETARG_INT32(1);
    
        SPI_connect();
    
        ret = SPI_exec(command, cnt);
    
        proc = SPI_processed;
    
        /*
         * If some rows were fetched, print them via elog(INFO).
         */
        if (ret > 0 && SPI_tuptable != NULL)
        {
            SPITupleTable *tuptable = SPI_tuptable;
            TupleDesc tupdesc = tuptable->tupdesc;
            char buf[8192];
            uint64 j;
    
            for (j = 0; j < tuptable->numvals; j++)
            {
                HeapTuple tuple = tuptable->vals[j];
                int i;
    
                for (i = 1, buf[0] = 0; i <= tupdesc->natts; i++)
                    snprintf(buf + strlen(buf), sizeof(buf) - strlen(buf), " %s%s",
                            SPI_getvalue(tuple, tupdesc, i),
                            (i == tupdesc->natts) ? " " : " |");
                elog(INFO, "EXECQ: %s", buf);
            }
        }
    
        SPI_finish();
        pfree(command);
    
        PG_RETURN_INT64(proc);
    }
    

This is how you declare the function after having compiled it into a shared
library (details are in [Section 38.10.5](xfunc-c.html#DFUNC
"38.10.5. Compiling and Linking Dynamically-Loaded Functions").):

    
    
    CREATE FUNCTION execq(text, integer) RETURNS int8
        AS '_filename_ '
        LANGUAGE C STRICT;
    

Here is a sample session:

    
    
    => SELECT execq('CREATE TABLE a (x integer)', 0);
     execq
    -------
         0
    (1 row)
    
    => INSERT INTO a VALUES (execq('INSERT INTO a VALUES (0)', 0));
    INSERT 0 1
    => SELECT execq('SELECT * FROM a', 0);
    INFO:  EXECQ:  0    _-- inserted by execq_
    INFO:  EXECQ:  1    _-- returned by execq and inserted by upper INSERT_
    
     execq
    -------
         2
    (1 row)
    
    => SELECT execq('INSERT INTO a SELECT x + 2 FROM a RETURNING *', 1);
    INFO:  EXECQ:  2    _-- 0 + 2, then execution was stopped by count_
     execq
    -------
         1
    (1 row)
    
    => SELECT execq('SELECT * FROM a', 10);
    INFO:  EXECQ:  0
    INFO:  EXECQ:  1
    INFO:  EXECQ:  2
    
     execq
    -------
         3              _-- 10 is the max value only, 3 is the real number of rows_
    (1 row)
    
    => SELECT execq('INSERT INTO a SELECT x + 10 FROM a', 1);
     execq
    -------
         3              _-- all rows processed; count does not stop it, because nothing is returned_
    (1 row)
    
    => SELECT * FROM a;
     x
    ----
      0
      1
      2
     10
     11
     12
    (6 rows)
    
    => DELETE FROM a;
    DELETE 6
    => INSERT INTO a VALUES (execq('SELECT * FROM a', 0) + 1);
    INSERT 0 1
    => SELECT * FROM a;
     x
    ---
     1                  _-- 0 (no rows in a) + 1_
    (1 row)
    
    => INSERT INTO a VALUES (execq('SELECT * FROM a', 0) + 1);
    INFO:  EXECQ:  1
    INSERT 0 1
    => SELECT * FROM a;
     x
    ---
     1
     2                  _-- 1 (there was one row in a) + 1_
    (2 rows)
    
    _-- This demonstrates the data changes visibility rule._
    _-- execq is called twice and sees different numbers of rows each time:_
    
    => INSERT INTO a SELECT execq('SELECT * FROM a', 0) * x FROM a;
    INFO:  EXECQ:  1    _-- results from first execq_
    INFO:  EXECQ:  2
    INFO:  EXECQ:  1    _-- results from second execq_
    INFO:  EXECQ:  2
    INFO:  EXECQ:  2
    INSERT 0 2
    => SELECT * FROM a;
     x
    ---
     1
     2
     2                  _-- 2 rows * 1 (x in first row)_
     6                  _-- 3 rows (2 + 1 just inserted) * 2 (x in second row)_
    (4 rows)
    

* * *

[Prev](spi-visibility.html "47.5. Visibility of Data Changes")  | [Up](spi.html "Chapter 47. Server Programming Interface") |  [Next](bgworker.html "Chapter 48. Background Worker Processes")  
---|---|---  
47.5. Visibility of Data Changes  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 48. Background Worker Processes  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-examples.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

