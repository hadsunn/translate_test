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

Supported Versions: [Current](/docs/current/plpgsql-trigger.html "PostgreSQL
17 - 43.10. Trigger Functions") ([17](/docs/17/plpgsql-trigger.html
"PostgreSQL 17 - 43.10. Trigger Functions")) / [16](/docs/16/plpgsql-
trigger.html "PostgreSQL 16 - 43.10. Trigger Functions") /
[15](/docs/15/plpgsql-trigger.html "PostgreSQL 15 - 43.10. Trigger Functions")
/ [14](/docs/14/plpgsql-trigger.html "PostgreSQL 14 - 43.10. Trigger
Functions") / [13](/docs/13/plpgsql-trigger.html "PostgreSQL 13 -
43.10. Trigger Functions")

Development Versions: [18](/docs/18/plpgsql-trigger.html "PostgreSQL 18 -
43.10. Trigger Functions") / [devel](/docs/devel/plpgsql-trigger.html
"PostgreSQL devel - 43.10. Trigger Functions")

Unsupported versions: [12](/docs/12/plpgsql-trigger.html "PostgreSQL 12 -
43.10. Trigger Functions") / [11](/docs/11/plpgsql-trigger.html "PostgreSQL 11
- 43.10. Trigger Functions") / [10](/docs/10/plpgsql-trigger.html "PostgreSQL
10 - 43.10. Trigger Functions") / [9.6](/docs/9.6/plpgsql-trigger.html
"PostgreSQL 9.6 - 43.10. Trigger Functions") / [9.5](/docs/9.5/plpgsql-
trigger.html "PostgreSQL 9.5 - 43.10. Trigger Functions") /
[9.4](/docs/9.4/plpgsql-trigger.html "PostgreSQL 9.4 - 43.10. Trigger
Functions") / [9.3](/docs/9.3/plpgsql-trigger.html "PostgreSQL 9.3 -
43.10. Trigger Functions") / [9.2](/docs/9.2/plpgsql-trigger.html "PostgreSQL
9.2 - 43.10. Trigger Functions") / [9.1](/docs/9.1/plpgsql-trigger.html
"PostgreSQL 9.1 - 43.10. Trigger Functions") / [9.0](/docs/9.0/plpgsql-
trigger.html "PostgreSQL 9.0 - 43.10. Trigger Functions") /
[8.4](/docs/8.4/plpgsql-trigger.html "PostgreSQL 8.4 - 43.10. Trigger
Functions") / [8.3](/docs/8.3/plpgsql-trigger.html "PostgreSQL 8.3 -
43.10. Trigger Functions") / [8.2](/docs/8.2/plpgsql-trigger.html "PostgreSQL
8.2 - 43.10. Trigger Functions") / [8.1](/docs/8.1/plpgsql-trigger.html
"PostgreSQL 8.1 - 43.10. Trigger Functions") / [8.0](/docs/8.0/plpgsql-
trigger.html "PostgreSQL 8.0 - 43.10. Trigger Functions") /
[7.4](/docs/7.4/plpgsql-trigger.html "PostgreSQL 7.4 - 43.10. Trigger
Functions") / [7.3](/docs/7.3/plpgsql-trigger.html "PostgreSQL 7.3 -
43.10. Trigger Functions") / [7.2](/docs/7.2/plpgsql-trigger.html "PostgreSQL
7.2 - 43.10. Trigger Functions") / [7.1](/docs/7.1/plpgsql-trigger.html
"PostgreSQL 7.1 - 43.10. Trigger Functions")

__

43.10. Trigger Functions  
---  
[Prev](plpgsql-errors-and-messages.html "43.9. Errors and Messages")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") | Chapter 43. PL/pgSQL — SQL Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpgsql-implementation.html "43.11. PL/pgSQL under the Hood")  
  
* * *

## 43.10. Trigger Functions #

[43.10.1. Triggers on Data Changes](plpgsql-trigger.html#PLPGSQL-DML-TRIGGER)

[43.10.2. Triggers on Events](plpgsql-trigger.html#PLPGSQL-EVENT-TRIGGER)

PL/pgSQL can be used to define trigger functions on data changes or database
events. A trigger function is created with the `CREATE FUNCTION` command,
declaring it as a function with no arguments and a return type of `trigger`
(for data change triggers) or `event_trigger` (for database event triggers).
Special local variables named `TG__`something`_` are automatically defined to
describe the condition that triggered the call.

### 43.10.1. Triggers on Data Changes #

A [data change trigger](triggers.html "Chapter 39. Triggers") is declared as a
function with no arguments and a return type of `trigger`. Note that the
function must be declared with no arguments even if it expects to receive some
arguments specified in `CREATE TRIGGER` — such arguments are passed via
`TG_ARGV`, as described below.

When a PL/pgSQL function is called as a trigger, several special variables are
created automatically in the top-level block. They are:

`NEW` `record` #

    

new database row for `INSERT`/`UPDATE` operations in row-level triggers. This
variable is null in statement-level triggers and for `DELETE` operations.

`OLD` `record` #

    

old database row for `UPDATE`/`DELETE` operations in row-level triggers. This
variable is null in statement-level triggers and for `INSERT` operations.

`TG_NAME` `name` #

    

name of the trigger which fired.

`TG_WHEN` `text` #

    

`BEFORE`, `AFTER`, or `INSTEAD OF`, depending on the trigger's definition.

`TG_LEVEL` `text` #

    

`ROW` or `STATEMENT`, depending on the trigger's definition.

`TG_OP` `text` #

    

operation for which the trigger was fired: `INSERT`, `UPDATE`, `DELETE`, or
`TRUNCATE`.

`TG_RELID` `oid` (references [`pg_class`](catalog-pg-class.html
"53.11. pg_class").`oid`) #

    

object ID of the table that caused the trigger invocation.

`TG_RELNAME` `name` #

    

table that caused the trigger invocation. This is now deprecated, and could
disappear in a future release. Use `TG_TABLE_NAME` instead.

`TG_TABLE_NAME` `name` #

    

table that caused the trigger invocation.

`TG_TABLE_SCHEMA` `name` #

    

schema of the table that caused the trigger invocation.

`TG_NARGS` `integer` #

    

number of arguments given to the trigger function in the `CREATE TRIGGER`
statement.

`TG_ARGV` `text[]` #

    

arguments from the `CREATE TRIGGER` statement. The index counts from 0.
Invalid indexes (less than 0 or greater than or equal to `tg_nargs`) result in
a null value.

A trigger function must return either `NULL` or a record/row value having
exactly the structure of the table the trigger was fired for.

Row-level triggers fired `BEFORE` can return null to signal the trigger
manager to skip the rest of the operation for this row (i.e., subsequent
triggers are not fired, and the `INSERT`/`UPDATE`/`DELETE` does not occur for
this row). If a nonnull value is returned then the operation proceeds with
that row value. Returning a row value different from the original value of
`NEW` alters the row that will be inserted or updated. Thus, if the trigger
function wants the triggering action to succeed normally without altering the
row value, `NEW` (or a value equal thereto) has to be returned. To alter the
row to be stored, it is possible to replace single values directly in `NEW`
and return the modified `NEW`, or to build a complete new record/row to
return. In the case of a before-trigger on `DELETE`, the returned value has no
direct effect, but it has to be nonnull to allow the trigger action to
proceed. Note that `NEW` is null in `DELETE` triggers, so returning that is
usually not sensible. The usual idiom in `DELETE` triggers is to return `OLD`.

`INSTEAD OF` triggers (which are always row-level triggers, and may only be
used on views) can return null to signal that they did not perform any
updates, and that the rest of the operation for this row should be skipped
(i.e., subsequent triggers are not fired, and the row is not counted in the
rows-affected status for the surrounding `INSERT`/`UPDATE`/`DELETE`).
Otherwise a nonnull value should be returned, to signal that the trigger
performed the requested operation. For `INSERT` and `UPDATE` operations, the
return value should be `NEW`, which the trigger function may modify to support
`INSERT RETURNING` and `UPDATE RETURNING` (this will also affect the row value
passed to any subsequent triggers, or passed to a special `EXCLUDED` alias
reference within an `INSERT` statement with an `ON CONFLICT DO UPDATE`
clause). For `DELETE` operations, the return value should be `OLD`.

The return value of a row-level trigger fired `AFTER` or a statement-level
trigger fired `BEFORE` or `AFTER` is always ignored; it might as well be null.
However, any of these types of triggers might still abort the entire operation
by raising an error.

[Example 43.3](plpgsql-trigger.html#PLPGSQL-TRIGGER-EXAMPLE "Example 43.3. A
PL/pgSQL Trigger Function") shows an example of a trigger function in
PL/pgSQL.

**Example  43.3. A PL/pgSQL Trigger Function**

This example trigger ensures that any time a row is inserted or updated in the
table, the current user name and time are stamped into the row. And it checks
that an employee's name is given and that the salary is a positive value.

    
    
    CREATE TABLE emp (
        empname           text,
        salary            integer,
        last_date         timestamp,
        last_user         text
    );
    
    CREATE FUNCTION emp_stamp() RETURNS trigger AS $emp_stamp$
        BEGIN
            -- Check that empname and salary are given
            IF NEW.empname IS NULL THEN
                RAISE EXCEPTION 'empname cannot be null';
            END IF;
            IF NEW.salary IS NULL THEN
                RAISE EXCEPTION '% cannot have null salary', NEW.empname;
            END IF;
    
            -- Who works for us when they must pay for it?
            IF NEW.salary < 0 THEN
                RAISE EXCEPTION '% cannot have a negative salary', NEW.empname;
            END IF;
    
            -- Remember who changed the payroll when
            NEW.last_date := current_timestamp;
            NEW.last_user := current_user;
            RETURN NEW;
        END;
    $emp_stamp$ LANGUAGE plpgsql;
    
    CREATE TRIGGER emp_stamp BEFORE INSERT OR UPDATE ON emp
        FOR EACH ROW EXECUTE FUNCTION emp_stamp();
    

  

Another way to log changes to a table involves creating a new table that holds
a row for each insert, update, or delete that occurs. This approach can be
thought of as auditing changes to a table. [Example 43.4](plpgsql-
trigger.html#PLPGSQL-TRIGGER-AUDIT-EXAMPLE "Example 43.4. A PL/pgSQL Trigger
Function for Auditing") shows an example of an audit trigger function in
PL/pgSQL.

**Example  43.4. A PL/pgSQL Trigger Function for Auditing**

This example trigger ensures that any insert, update or delete of a row in the
`emp` table is recorded (i.e., audited) in the `emp_audit` table. The current
time and user name are stamped into the row, together with the type of
operation performed on it.

    
    
    CREATE TABLE emp (
        empname           text NOT NULL,
        salary            integer
    );
    
    CREATE TABLE emp_audit(
        operation         char(1)   NOT NULL,
        stamp             timestamp NOT NULL,
        userid            text      NOT NULL,
        empname           text      NOT NULL,
        salary            integer
    );
    
    CREATE OR REPLACE FUNCTION process_emp_audit() RETURNS TRIGGER AS $emp_audit$
        BEGIN
            --
            -- Create a row in emp_audit to reflect the operation performed on emp,
            -- making use of the special variable TG_OP to work out the operation.
            --
            IF (TG_OP = 'DELETE') THEN
                INSERT INTO emp_audit SELECT 'D', now(), current_user, OLD.*;
            ELSIF (TG_OP = 'UPDATE') THEN
                INSERT INTO emp_audit SELECT 'U', now(), current_user, NEW.*;
            ELSIF (TG_OP = 'INSERT') THEN
                INSERT INTO emp_audit SELECT 'I', now(), current_user, NEW.*;
            END IF;
            RETURN NULL; -- result is ignored since this is an AFTER trigger
        END;
    $emp_audit$ LANGUAGE plpgsql;
    
    CREATE TRIGGER emp_audit
    AFTER INSERT OR UPDATE OR DELETE ON emp
        FOR EACH ROW EXECUTE FUNCTION process_emp_audit();
    

  

A variation of the previous example uses a view joining the main table to the
audit table, to show when each entry was last modified. This approach still
records the full audit trail of changes to the table, but also presents a
simplified view of the audit trail, showing just the last modified timestamp
derived from the audit trail for each entry. [Example 43.5](plpgsql-
trigger.html#PLPGSQL-VIEW-TRIGGER-AUDIT-EXAMPLE "Example 43.5. A PL/pgSQL View
Trigger Function for Auditing") shows an example of an audit trigger on a view
in PL/pgSQL.

**Example  43.5. A PL/pgSQL View Trigger Function for Auditing**

This example uses a trigger on the view to make it updatable, and ensure that
any insert, update or delete of a row in the view is recorded (i.e., audited)
in the `emp_audit` table. The current time and user name are recorded,
together with the type of operation performed, and the view displays the last
modified time of each row.

    
    
    CREATE TABLE emp (
        empname           text PRIMARY KEY,
        salary            integer
    );
    
    CREATE TABLE emp_audit(
        operation         char(1)   NOT NULL,
        userid            text      NOT NULL,
        empname           text      NOT NULL,
        salary            integer,
        stamp             timestamp NOT NULL
    );
    
    CREATE VIEW emp_view AS
        SELECT e.empname,
               e.salary,
               max(ea.stamp) AS last_updated
          FROM emp e
          LEFT JOIN emp_audit ea ON ea.empname = e.empname
         GROUP BY 1, 2;
    
    CREATE OR REPLACE FUNCTION update_emp_view() RETURNS TRIGGER AS $$
        BEGIN
            --
            -- Perform the required operation on emp, and create a row in emp_audit
            -- to reflect the change made to emp.
            --
            IF (TG_OP = 'DELETE') THEN
                DELETE FROM emp WHERE empname = OLD.empname;
                IF NOT FOUND THEN RETURN NULL; END IF;
    
                OLD.last_updated = now();
                INSERT INTO emp_audit VALUES('D', current_user, OLD.*);
                RETURN OLD;
            ELSIF (TG_OP = 'UPDATE') THEN
                UPDATE emp SET salary = NEW.salary WHERE empname = OLD.empname;
                IF NOT FOUND THEN RETURN NULL; END IF;
    
                NEW.last_updated = now();
                INSERT INTO emp_audit VALUES('U', current_user, NEW.*);
                RETURN NEW;
            ELSIF (TG_OP = 'INSERT') THEN
                INSERT INTO emp VALUES(NEW.empname, NEW.salary);
    
                NEW.last_updated = now();
                INSERT INTO emp_audit VALUES('I', current_user, NEW.*);
                RETURN NEW;
            END IF;
        END;
    $$ LANGUAGE plpgsql;
    
    CREATE TRIGGER emp_audit
    INSTEAD OF INSERT OR UPDATE OR DELETE ON emp_view
        FOR EACH ROW EXECUTE FUNCTION update_emp_view();
    

  

One use of triggers is to maintain a summary table of another table. The
resulting summary can be used in place of the original table for certain
queries — often with vastly reduced run times. This technique is commonly used
in Data Warehousing, where the tables of measured or observed data (called
fact tables) might be extremely large. [Example 43.6](plpgsql-
trigger.html#PLPGSQL-TRIGGER-SUMMARY-EXAMPLE "Example 43.6. A PL/pgSQL Trigger
Function for Maintaining a Summary Table") shows an example of a trigger
function in PL/pgSQL that maintains a summary table for a fact table in a data
warehouse.

**Example  43.6. A PL/pgSQL Trigger Function for Maintaining a Summary Table**

The schema detailed here is partly based on the _Grocery Store_ example from
_The Data Warehouse Toolkit_ by Ralph Kimball.

    
    
    --
    -- Main tables - time dimension and sales fact.
    --
    CREATE TABLE time_dimension (
        time_key                    integer NOT NULL,
        day_of_week                 integer NOT NULL,
        day_of_month                integer NOT NULL,
        month                       integer NOT NULL,
        quarter                     integer NOT NULL,
        year                        integer NOT NULL
    );
    CREATE UNIQUE INDEX time_dimension_key ON time_dimension(time_key);
    
    CREATE TABLE sales_fact (
        time_key                    integer NOT NULL,
        product_key                 integer NOT NULL,
        store_key                   integer NOT NULL,
        amount_sold                 numeric(12,2) NOT NULL,
        units_sold                  integer NOT NULL,
        amount_cost                 numeric(12,2) NOT NULL
    );
    CREATE INDEX sales_fact_time ON sales_fact(time_key);
    
    --
    -- Summary table - sales by time.
    --
    CREATE TABLE sales_summary_bytime (
        time_key                    integer NOT NULL,
        amount_sold                 numeric(15,2) NOT NULL,
        units_sold                  numeric(12) NOT NULL,
        amount_cost                 numeric(15,2) NOT NULL
    );
    CREATE UNIQUE INDEX sales_summary_bytime_key ON sales_summary_bytime(time_key);
    
    --
    -- Function and trigger to amend summarized column(s) on UPDATE, INSERT, DELETE.
    --
    CREATE OR REPLACE FUNCTION maint_sales_summary_bytime() RETURNS TRIGGER
    AS $maint_sales_summary_bytime$
        DECLARE
            delta_time_key          integer;
            delta_amount_sold       numeric(15,2);
            delta_units_sold        numeric(12);
            delta_amount_cost       numeric(15,2);
        BEGIN
    
            -- Work out the increment/decrement amount(s).
            IF (TG_OP = 'DELETE') THEN
    
                delta_time_key = OLD.time_key;
                delta_amount_sold = -1 * OLD.amount_sold;
                delta_units_sold = -1 * OLD.units_sold;
                delta_amount_cost = -1 * OLD.amount_cost;
    
            ELSIF (TG_OP = 'UPDATE') THEN
    
                -- forbid updates that change the time_key -
                -- (probably not too onerous, as DELETE + INSERT is how most
                -- changes will be made).
                IF ( OLD.time_key != NEW.time_key) THEN
                    RAISE EXCEPTION 'Update of time_key : % -> % not allowed',
                                                          OLD.time_key, NEW.time_key;
                END IF;
    
                delta_time_key = OLD.time_key;
                delta_amount_sold = NEW.amount_sold - OLD.amount_sold;
                delta_units_sold = NEW.units_sold - OLD.units_sold;
                delta_amount_cost = NEW.amount_cost - OLD.amount_cost;
    
            ELSIF (TG_OP = 'INSERT') THEN
    
                delta_time_key = NEW.time_key;
                delta_amount_sold = NEW.amount_sold;
                delta_units_sold = NEW.units_sold;
                delta_amount_cost = NEW.amount_cost;
    
            END IF;
    
    
            -- Insert or update the summary row with the new values.
            <<insert_update>>
            LOOP
                UPDATE sales_summary_bytime
                    SET amount_sold = amount_sold + delta_amount_sold,
                        units_sold = units_sold + delta_units_sold,
                        amount_cost = amount_cost + delta_amount_cost
                    WHERE time_key = delta_time_key;
    
                EXIT insert_update WHEN found;
    
                BEGIN
                    INSERT INTO sales_summary_bytime (
                                time_key,
                                amount_sold,
                                units_sold,
                                amount_cost)
                        VALUES (
                                delta_time_key,
                                delta_amount_sold,
                                delta_units_sold,
                                delta_amount_cost
                               );
    
                    EXIT insert_update;
    
                EXCEPTION
                    WHEN UNIQUE_VIOLATION THEN
                        -- do nothing
                END;
            END LOOP insert_update;
    
            RETURN NULL;
    
        END;
    $maint_sales_summary_bytime$ LANGUAGE plpgsql;
    
    CREATE TRIGGER maint_sales_summary_bytime
    AFTER INSERT OR UPDATE OR DELETE ON sales_fact
        FOR EACH ROW EXECUTE FUNCTION maint_sales_summary_bytime();
    
    INSERT INTO sales_fact VALUES(1,1,1,10,3,15);
    INSERT INTO sales_fact VALUES(1,2,1,20,5,35);
    INSERT INTO sales_fact VALUES(2,2,1,40,15,135);
    INSERT INTO sales_fact VALUES(2,3,1,10,1,13);
    SELECT * FROM sales_summary_bytime;
    DELETE FROM sales_fact WHERE product_key = 1;
    SELECT * FROM sales_summary_bytime;
    UPDATE sales_fact SET units_sold = units_sold * 2;
    SELECT * FROM sales_summary_bytime;
    

  

`AFTER` triggers can also make use of _transition tables_ to inspect the
entire set of rows changed by the triggering statement. The `CREATE TRIGGER`
command assigns names to one or both transition tables, and then the function
can refer to those names as though they were read-only temporary tables.
[Example 43.7](plpgsql-trigger.html#PLPGSQL-TRIGGER-AUDIT-TRANSITION-EXAMPLE
"Example 43.7. Auditing with Transition Tables") shows an example.

**Example  43.7. Auditing with Transition Tables**

This example produces the same results as [Example 43.4](plpgsql-
trigger.html#PLPGSQL-TRIGGER-AUDIT-EXAMPLE "Example 43.4. A PL/pgSQL Trigger
Function for Auditing"), but instead of using a trigger that fires for every
row, it uses a trigger that fires once per statement, after collecting the
relevant information in a transition table. This can be significantly faster
than the row-trigger approach when the invoking statement has modified many
rows. Notice that we must make a separate trigger declaration for each kind of
event, since the `REFERENCING` clauses must be different for each case. But
this does not stop us from using a single trigger function if we choose. (In
practice, it might be better to use three separate functions and avoid the
run-time tests on `TG_OP`.)

    
    
    CREATE TABLE emp (
        empname           text NOT NULL,
        salary            integer
    );
    
    CREATE TABLE emp_audit(
        operation         char(1)   NOT NULL,
        stamp             timestamp NOT NULL,
        userid            text      NOT NULL,
        empname           text      NOT NULL,
        salary            integer
    );
    
    CREATE OR REPLACE FUNCTION process_emp_audit() RETURNS TRIGGER AS $emp_audit$
        BEGIN
            --
            -- Create rows in emp_audit to reflect the operations performed on emp,
            -- making use of the special variable TG_OP to work out the operation.
            --
            IF (TG_OP = 'DELETE') THEN
                INSERT INTO emp_audit
                    SELECT 'D', now(), current_user, o.* FROM old_table o;
            ELSIF (TG_OP = 'UPDATE') THEN
                INSERT INTO emp_audit
                    SELECT 'U', now(), current_user, n.* FROM new_table n;
            ELSIF (TG_OP = 'INSERT') THEN
                INSERT INTO emp_audit
                    SELECT 'I', now(), current_user, n.* FROM new_table n;
            END IF;
            RETURN NULL; -- result is ignored since this is an AFTER trigger
        END;
    $emp_audit$ LANGUAGE plpgsql;
    
    CREATE TRIGGER emp_audit_ins
        AFTER INSERT ON emp
        REFERENCING NEW TABLE AS new_table
        FOR EACH STATEMENT EXECUTE FUNCTION process_emp_audit();
    CREATE TRIGGER emp_audit_upd
        AFTER UPDATE ON emp
        REFERENCING OLD TABLE AS old_table NEW TABLE AS new_table
        FOR EACH STATEMENT EXECUTE FUNCTION process_emp_audit();
    CREATE TRIGGER emp_audit_del
        AFTER DELETE ON emp
        REFERENCING OLD TABLE AS old_table
        FOR EACH STATEMENT EXECUTE FUNCTION process_emp_audit();
    

  

### 43.10.2. Triggers on Events #

PL/pgSQL can be used to define [event triggers](event-triggers.html
"Chapter 40. Event Triggers"). PostgreSQL requires that a function that is to
be called as an event trigger must be declared as a function with no arguments
and a return type of `event_trigger`.

When a PL/pgSQL function is called as an event trigger, several special
variables are created automatically in the top-level block. They are:

`TG_EVENT` `text` #

    

event the trigger is fired for.

`TG_TAG` `text` #

    

command tag for which the trigger is fired.

[Example 43.8](plpgsql-trigger.html#PLPGSQL-EVENT-TRIGGER-EXAMPLE
"Example 43.8. A PL/pgSQL Event Trigger Function") shows an example of an
event trigger function in PL/pgSQL.

**Example  43.8. A PL/pgSQL Event Trigger Function**

This example trigger simply raises a `NOTICE` message each time a supported
command is executed.

    
    
    CREATE OR REPLACE FUNCTION snitch() RETURNS event_trigger AS $$
    BEGIN
        RAISE NOTICE 'snitch: % %', tg_event, tg_tag;
    END;
    $$ LANGUAGE plpgsql;
    
    CREATE EVENT TRIGGER snitch ON ddl_command_start EXECUTE FUNCTION snitch();
    

  

* * *

[Prev](plpgsql-errors-and-messages.html "43.9. Errors and Messages")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") |  [Next](plpgsql-implementation.html "43.11. PL/pgSQL under the Hood")  
---|---|---  
43.9. Errors and Messages  | [Home](index.html "PostgreSQL 16.9 Documentation") |  43.11. PL/pgSQL under the Hood  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpgsql-trigger.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

