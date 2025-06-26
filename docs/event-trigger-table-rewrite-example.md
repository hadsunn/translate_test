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

Supported Versions: [Current](/docs/current/event-trigger-table-rewrite-
example.html "PostgreSQL 17 - 40.5. A Table Rewrite Event Trigger Example")
([17](/docs/17/event-trigger-table-rewrite-example.html "PostgreSQL 17 -
40.5. A Table Rewrite Event Trigger Example")) / [16](/docs/16/event-trigger-
table-rewrite-example.html "PostgreSQL 16 - 40.5. A Table Rewrite Event
Trigger Example") / [15](/docs/15/event-trigger-table-rewrite-example.html
"PostgreSQL 15 - 40.5. A Table Rewrite Event Trigger Example") /
[14](/docs/14/event-trigger-table-rewrite-example.html "PostgreSQL 14 -
40.5. A Table Rewrite Event Trigger Example") / [13](/docs/13/event-trigger-
table-rewrite-example.html "PostgreSQL 13 - 40.5. A Table Rewrite Event
Trigger Example")

Development Versions: [18](/docs/18/event-trigger-table-rewrite-example.html
"PostgreSQL 18 - 40.5. A Table Rewrite Event Trigger Example") /
[devel](/docs/devel/event-trigger-table-rewrite-example.html "PostgreSQL devel
- 40.5. A Table Rewrite Event Trigger Example")

Unsupported versions: [12](/docs/12/event-trigger-table-rewrite-example.html
"PostgreSQL 12 - 40.5. A Table Rewrite Event Trigger Example") /
[11](/docs/11/event-trigger-table-rewrite-example.html "PostgreSQL 11 -
40.5. A Table Rewrite Event Trigger Example") / [10](/docs/10/event-trigger-
table-rewrite-example.html "PostgreSQL 10 - 40.5. A Table Rewrite Event
Trigger Example") / [9.6](/docs/9.6/event-trigger-table-rewrite-example.html
"PostgreSQL 9.6 - 40.5. A Table Rewrite Event Trigger Example") /
[9.5](/docs/9.5/event-trigger-table-rewrite-example.html "PostgreSQL 9.5 -
40.5. A Table Rewrite Event Trigger Example")

__

40.5. A Table Rewrite Event Trigger Example  
---  
[Prev](event-trigger-example.html "40.4. A Complete Event Trigger Example")  | [Up](event-triggers.html "Chapter 40. Event Triggers") | Chapter 40. Event Triggers | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](rules.html "Chapter 41. The Rule System")  
  
* * *

## 40.5. A Table Rewrite Event Trigger Example #

Thanks to the `table_rewrite` event, it is possible to implement a table
rewriting policy only allowing the rewrite in maintenance windows.

Here's an example implementing such a policy.

    
    
    CREATE OR REPLACE FUNCTION no_rewrite()
     RETURNS event_trigger
     LANGUAGE plpgsql AS
    $$
    ---
    --- Implement local Table Rewriting policy:
    ---   public.foo is not allowed rewriting, ever
    ---   other tables are only allowed rewriting between 1am and 6am
    ---   unless they have more than 100 blocks
    ---
    DECLARE
      table_oid oid := pg_event_trigger_table_rewrite_oid();
      current_hour integer := extract('hour' from current_time);
      pages integer;
      max_pages integer := 100;
    BEGIN
      IF pg_event_trigger_table_rewrite_oid() = 'public.foo'::regclass
      THEN
            RAISE EXCEPTION 'you''re not allowed to rewrite the table %',
                            table_oid::regclass;
      END IF;
    
      SELECT INTO pages relpages FROM pg_class WHERE oid = table_oid;
      IF pages > max_pages
      THEN
            RAISE EXCEPTION 'rewrites only allowed for table with less than % pages',
                            max_pages;
      END IF;
    
      IF current_hour NOT BETWEEN 1 AND 6
      THEN
            RAISE EXCEPTION 'rewrites only allowed between 1am and 6am';
      END IF;
    END;
    $$;
    
    CREATE EVENT TRIGGER no_rewrite_allowed
                      ON table_rewrite
       EXECUTE FUNCTION no_rewrite();
    

* * *

[Prev](event-trigger-example.html "40.4. A Complete Event Trigger Example")  | [Up](event-triggers.html "Chapter 40. Event Triggers") |  [Next](rules.html "Chapter 41. The Rule System")  
---|---|---  
40.4. A Complete Event Trigger Example  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 41. The Rule System  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/event-trigger-table-rewrite-
example.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

