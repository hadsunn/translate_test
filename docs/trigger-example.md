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

Supported Versions: [Current](/docs/current/trigger-example.html "PostgreSQL
17 - 39.4. A Complete Trigger Example") ([17](/docs/17/trigger-example.html
"PostgreSQL 17 - 39.4. A Complete Trigger Example")) / [16](/docs/16/trigger-
example.html "PostgreSQL 16 - 39.4. A Complete Trigger Example") /
[15](/docs/15/trigger-example.html "PostgreSQL 15 - 39.4. A Complete Trigger
Example") / [14](/docs/14/trigger-example.html "PostgreSQL 14 - 39.4. A
Complete Trigger Example") / [13](/docs/13/trigger-example.html "PostgreSQL 13
- 39.4. A Complete Trigger Example")

Development Versions: [18](/docs/18/trigger-example.html "PostgreSQL 18 -
39.4. A Complete Trigger Example") / [devel](/docs/devel/trigger-example.html
"PostgreSQL devel - 39.4. A Complete Trigger Example")

Unsupported versions: [12](/docs/12/trigger-example.html "PostgreSQL 12 -
39.4. A Complete Trigger Example") / [11](/docs/11/trigger-example.html
"PostgreSQL 11 - 39.4. A Complete Trigger Example") / [10](/docs/10/trigger-
example.html "PostgreSQL 10 - 39.4. A Complete Trigger Example") /
[9.6](/docs/9.6/trigger-example.html "PostgreSQL 9.6 - 39.4. A Complete
Trigger Example") / [9.5](/docs/9.5/trigger-example.html "PostgreSQL 9.5 -
39.4. A Complete Trigger Example") / [9.4](/docs/9.4/trigger-example.html
"PostgreSQL 9.4 - 39.4. A Complete Trigger Example") /
[9.3](/docs/9.3/trigger-example.html "PostgreSQL 9.3 - 39.4. A Complete
Trigger Example") / [9.2](/docs/9.2/trigger-example.html "PostgreSQL 9.2 -
39.4. A Complete Trigger Example") / [9.1](/docs/9.1/trigger-example.html
"PostgreSQL 9.1 - 39.4. A Complete Trigger Example") /
[9.0](/docs/9.0/trigger-example.html "PostgreSQL 9.0 - 39.4. A Complete
Trigger Example") / [8.4](/docs/8.4/trigger-example.html "PostgreSQL 8.4 -
39.4. A Complete Trigger Example") / [8.3](/docs/8.3/trigger-example.html
"PostgreSQL 8.3 - 39.4. A Complete Trigger Example") /
[8.2](/docs/8.2/trigger-example.html "PostgreSQL 8.2 - 39.4. A Complete
Trigger Example") / [8.1](/docs/8.1/trigger-example.html "PostgreSQL 8.1 -
39.4. A Complete Trigger Example") / [8.0](/docs/8.0/trigger-example.html
"PostgreSQL 8.0 - 39.4. A Complete Trigger Example") /
[7.4](/docs/7.4/trigger-example.html "PostgreSQL 7.4 - 39.4. A Complete
Trigger Example")

__

39.4. A Complete Trigger Example  
---  
[Prev](trigger-interface.html "39.3. Writing Trigger Functions in C")  | [Up](triggers.html "Chapter 39. Triggers") | Chapter 39. Triggers | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](event-triggers.html "Chapter 40. Event Triggers")  
  
* * *

## 39.4. A Complete Trigger Example #

Here is a very simple example of a trigger function written in C. (Examples of
triggers written in procedural languages can be found in the documentation of
the procedural languages.)

The function `trigf` reports the number of rows in the table `ttest` and skips
the actual operation if the command attempts to insert a null value into the
column `x`. (So the trigger acts as a not-null constraint but doesn't abort
the transaction.)

First, the table definition:

    
    
    CREATE TABLE ttest (
        x integer
    );
    

This is the source code of the trigger function:

    
    
    #include "postgres.h"
    #include "fmgr.h"
    #include "executor/spi.h"       /* this is what you need to work with SPI */
    #include "commands/trigger.h"   /* ... triggers ... */
    #include "utils/rel.h"          /* ... and relations */
    
    PG_MODULE_MAGIC;
    
    PG_FUNCTION_INFO_V1(trigf);
    
    Datum
    trigf(PG_FUNCTION_ARGS)
    {
        TriggerData *trigdata = (TriggerData *) fcinfo->context;
        TupleDesc   tupdesc;
        HeapTuple   rettuple;
        char       *when;
        bool        checknull = false;
        bool        isnull;
        int         ret, i;
    
        /* make sure it's called as a trigger at all */
        if (!CALLED_AS_TRIGGER(fcinfo))
            elog(ERROR, "trigf: not called by trigger manager");
    
        /* tuple to return to executor */
        if (TRIGGER_FIRED_BY_UPDATE(trigdata->tg_event))
            rettuple = trigdata->tg_newtuple;
        else
            rettuple = trigdata->tg_trigtuple;
    
        /* check for null values */
        if (!TRIGGER_FIRED_BY_DELETE(trigdata->tg_event)
            && TRIGGER_FIRED_BEFORE(trigdata->tg_event))
            checknull = true;
    
        if (TRIGGER_FIRED_BEFORE(trigdata->tg_event))
            when = "before";
        else
            when = "after ";
    
        tupdesc = trigdata->tg_relation->rd_att;
    
        /* connect to SPI manager */
        if ((ret = SPI_connect()) < 0)
            elog(ERROR, "trigf (fired %s): SPI_connect returned %d", when, ret);
    
        /* get number of rows in table */
        ret = SPI_exec("SELECT count(*) FROM ttest", 0);
    
        if (ret < 0)
            elog(ERROR, "trigf (fired %s): SPI_exec returned %d", when, ret);
    
        /* count(*) returns int8, so be careful to convert */
        i = DatumGetInt64(SPI_getbinval(SPI_tuptable->vals[0],
                                        SPI_tuptable->tupdesc,
                                        1,
                                        &isnull));
    
        elog (INFO, "trigf (fired %s): there are %d rows in ttest", when, i);
    
        SPI_finish();
    
        if (checknull)
        {
            SPI_getbinval(rettuple, tupdesc, 1, &isnull);
            if (isnull)
                rettuple = NULL;
        }
    
        return PointerGetDatum(rettuple);
    }
    
    

After you have compiled the source code (see [Section
38.10.5](xfunc-c.html#DFUNC "38.10.5. Compiling and Linking Dynamically-Loaded
Functions")), declare the function and the triggers:

    
    
    CREATE FUNCTION trigf() RETURNS trigger
        AS '_filename_ '
        LANGUAGE C;
    
    CREATE TRIGGER tbefore BEFORE INSERT OR UPDATE OR DELETE ON ttest
        FOR EACH ROW EXECUTE FUNCTION trigf();
    
    CREATE TRIGGER tafter AFTER INSERT OR UPDATE OR DELETE ON ttest
        FOR EACH ROW EXECUTE FUNCTION trigf();
    

Now you can test the operation of the trigger:

    
    
    => INSERT INTO ttest VALUES (NULL);
    INFO:  trigf (fired before): there are 0 rows in ttest
    INSERT 0 0
    
    -- Insertion skipped and AFTER trigger is not fired
    
    => SELECT * FROM ttest;
     x
    ---
    (0 rows)
    
    => INSERT INTO ttest VALUES (1);
    INFO:  trigf (fired before): there are 0 rows in ttest
    INFO:  trigf (fired after ): there are 1 rows in ttest
                                           ^^^^^^^^
                                 remember what we said about visibility.
    INSERT 167793 1
    vac=> SELECT * FROM ttest;
     x
    ---
     1
    (1 row)
    
    => INSERT INTO ttest SELECT x * 2 FROM ttest;
    INFO:  trigf (fired before): there are 1 rows in ttest
    INFO:  trigf (fired after ): there are 2 rows in ttest
                                           ^^^^^^
                                 remember what we said about visibility.
    INSERT 167794 1
    => SELECT * FROM ttest;
     x
    ---
     1
     2
    (2 rows)
    
    => UPDATE ttest SET x = NULL WHERE x = 2;
    INFO:  trigf (fired before): there are 2 rows in ttest
    UPDATE 0
    => UPDATE ttest SET x = 4 WHERE x = 2;
    INFO:  trigf (fired before): there are 2 rows in ttest
    INFO:  trigf (fired after ): there are 2 rows in ttest
    UPDATE 1
    vac=> SELECT * FROM ttest;
     x
    ---
     1
     4
    (2 rows)
    
    => DELETE FROM ttest;
    INFO:  trigf (fired before): there are 2 rows in ttest
    INFO:  trigf (fired before): there are 1 rows in ttest
    INFO:  trigf (fired after ): there are 0 rows in ttest
    INFO:  trigf (fired after ): there are 0 rows in ttest
                                           ^^^^^^
                                 remember what we said about visibility.
    DELETE 2
    => SELECT * FROM ttest;
     x
    ---
    (0 rows)
    

There are more complex examples in `src/test/regress/regress.c` and in
[spi](contrib-spi.html "F.41. spi — Server Programming Interface
features/examples").

* * *

[Prev](trigger-interface.html "39.3. Writing Trigger Functions in C")  | [Up](triggers.html "Chapter 39. Triggers") |  [Next](event-triggers.html "Chapter 40. Event Triggers")  
---|---|---  
39.3. Writing Trigger Functions in C  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 40. Event Triggers  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/trigger-example.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

