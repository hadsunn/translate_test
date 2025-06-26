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

Supported Versions: [Current](/docs/current/pltcl-trigger.html "PostgreSQL 17
- 44.6. Trigger Functions in PL/Tcl") ([17](/docs/17/pltcl-trigger.html
"PostgreSQL 17 - 44.6. Trigger Functions in PL/Tcl")) / [16](/docs/16/pltcl-
trigger.html "PostgreSQL 16 - 44.6. Trigger Functions in PL/Tcl") /
[15](/docs/15/pltcl-trigger.html "PostgreSQL 15 - 44.6. Trigger Functions in
PL/Tcl") / [14](/docs/14/pltcl-trigger.html "PostgreSQL 14 - 44.6. Trigger
Functions in PL/Tcl") / [13](/docs/13/pltcl-trigger.html "PostgreSQL 13 -
44.6. Trigger Functions in PL/Tcl")

Development Versions: [18](/docs/18/pltcl-trigger.html "PostgreSQL 18 -
44.6. Trigger Functions in PL/Tcl") / [devel](/docs/devel/pltcl-trigger.html
"PostgreSQL devel - 44.6. Trigger Functions in PL/Tcl")

Unsupported versions: [12](/docs/12/pltcl-trigger.html "PostgreSQL 12 -
44.6. Trigger Functions in PL/Tcl") / [11](/docs/11/pltcl-trigger.html
"PostgreSQL 11 - 44.6. Trigger Functions in PL/Tcl") / [10](/docs/10/pltcl-
trigger.html "PostgreSQL 10 - 44.6. Trigger Functions in PL/Tcl") /
[9.6](/docs/9.6/pltcl-trigger.html "PostgreSQL 9.6 - 44.6. Trigger Functions
in PL/Tcl") / [9.5](/docs/9.5/pltcl-trigger.html "PostgreSQL 9.5 -
44.6. Trigger Functions in PL/Tcl") / [9.4](/docs/9.4/pltcl-trigger.html
"PostgreSQL 9.4 - 44.6. Trigger Functions in PL/Tcl") / [9.3](/docs/9.3/pltcl-
trigger.html "PostgreSQL 9.3 - 44.6. Trigger Functions in PL/Tcl") /
[9.2](/docs/9.2/pltcl-trigger.html "PostgreSQL 9.2 - 44.6. Trigger Functions
in PL/Tcl") / [9.1](/docs/9.1/pltcl-trigger.html "PostgreSQL 9.1 -
44.6. Trigger Functions in PL/Tcl") / [9.0](/docs/9.0/pltcl-trigger.html
"PostgreSQL 9.0 - 44.6. Trigger Functions in PL/Tcl") / [8.4](/docs/8.4/pltcl-
trigger.html "PostgreSQL 8.4 - 44.6. Trigger Functions in PL/Tcl") /
[8.3](/docs/8.3/pltcl-trigger.html "PostgreSQL 8.3 - 44.6. Trigger Functions
in PL/Tcl") / [8.2](/docs/8.2/pltcl-trigger.html "PostgreSQL 8.2 -
44.6. Trigger Functions in PL/Tcl") / [8.1](/docs/8.1/pltcl-trigger.html
"PostgreSQL 8.1 - 44.6. Trigger Functions in PL/Tcl") / [8.0](/docs/8.0/pltcl-
trigger.html "PostgreSQL 8.0 - 44.6. Trigger Functions in PL/Tcl") /
[7.4](/docs/7.4/pltcl-trigger.html "PostgreSQL 7.4 - 44.6. Trigger Functions
in PL/Tcl")

__

44.6. Trigger Functions in PL/Tcl  
---  
[Prev](pltcl-dbaccess.html "44.5. Database Access from PL/Tcl")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") | Chapter 44. PL/Tcl — Tcl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pltcl-event-trigger.html "44.7. Event Trigger Functions in PL/Tcl")  
  
* * *

## 44.6. Trigger Functions in PL/Tcl #

Trigger functions can be written in PL/Tcl. PostgreSQL requires that a
function that is to be called as a trigger must be declared as a function with
no arguments and a return type of `trigger`.

The information from the trigger manager is passed to the function body in the
following variables:

`$TG_name`

    

The name of the trigger from the `CREATE TRIGGER` statement.

`$TG_relid`

    

The object ID of the table that caused the trigger function to be invoked.

`$TG_table_name`

    

The name of the table that caused the trigger function to be invoked.

`$TG_table_schema`

    

The schema of the table that caused the trigger function to be invoked.

`$TG_relatts`

    

A Tcl list of the table column names, prefixed with an empty list element. So
looking up a column name in the list with Tcl's `lsearch` command returns the
element's number starting with 1 for the first column, the same way the
columns are customarily numbered in PostgreSQL. (Empty list elements also
appear in the positions of columns that have been dropped, so that the
attribute numbering is correct for columns to their right.)

`$TG_when`

    

The string `BEFORE`, `AFTER`, or `INSTEAD OF`, depending on the type of
trigger event.

`$TG_level`

    

The string `ROW` or `STATEMENT` depending on the type of trigger event.

`$TG_op`

    

The string `INSERT`, `UPDATE`, `DELETE`, or `TRUNCATE` depending on the type
of trigger event.

`$NEW`

    

An associative array containing the values of the new table row for `INSERT`
or `UPDATE` actions, or empty for `DELETE`. The array is indexed by column
name. Columns that are null will not appear in the array. This is not set for
statement-level triggers.

`$OLD`

    

An associative array containing the values of the old table row for `UPDATE`
or `DELETE` actions, or empty for `INSERT`. The array is indexed by column
name. Columns that are null will not appear in the array. This is not set for
statement-level triggers.

`$args`

    

A Tcl list of the arguments to the function as given in the `CREATE TRIGGER`
statement. These arguments are also accessible as `$1` ... `$_`n`_` in the
function body.

The return value from a trigger function can be one of the strings `OK` or
`SKIP`, or a list of column name/value pairs. If the return value is `OK`, the
operation (`INSERT`/`UPDATE`/`DELETE`) that fired the trigger will proceed
normally. `SKIP` tells the trigger manager to silently suppress the operation
for this row. If a list is returned, it tells PL/Tcl to return a modified row
to the trigger manager; the contents of the modified row are specified by the
column names and values in the list. Any columns not mentioned in the list are
set to null. Returning a modified row is only meaningful for row-level
`BEFORE` `INSERT` or `UPDATE` triggers, for which the modified row will be
inserted instead of the one given in `$NEW`; or for row-level `INSTEAD OF`
`INSERT` or `UPDATE` triggers where the returned row is used as the source
data for `INSERT RETURNING` or `UPDATE RETURNING` clauses. In row-level
`BEFORE` `DELETE` or `INSTEAD OF` `DELETE` triggers, returning a modified row
has the same effect as returning `OK`, that is the operation proceeds. The
trigger return value is ignored for all other types of triggers.

### Tip

The result list can be made from an array representation of the modified tuple
with the `array get` Tcl command.

Here's a little example trigger function that forces an integer value in a
table to keep track of the number of updates that are performed on the row.
For new rows inserted, the value is initialized to 0 and then incremented on
every update operation.

    
    
    CREATE FUNCTION trigfunc_modcount() RETURNS trigger AS $$
        switch $TG_op {
            INSERT {
                set NEW($1) 0
            }
            UPDATE {
                set NEW($1) $OLD($1)
                incr NEW($1)
            }
            default {
                return OK
            }
        }
        return [array get NEW]
    $$ LANGUAGE pltcl;
    
    CREATE TABLE mytab (num integer, description text, modcnt integer);
    
    CREATE TRIGGER trig_mytab_modcount BEFORE INSERT OR UPDATE ON mytab
        FOR EACH ROW EXECUTE FUNCTION trigfunc_modcount('modcnt');
    

Notice that the trigger function itself does not know the column name; that's
supplied from the trigger arguments. This lets the trigger function be reused
with different tables.

* * *

[Prev](pltcl-dbaccess.html "44.5. Database Access from PL/Tcl")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") |  [Next](pltcl-event-trigger.html "44.7. Event Trigger Functions in PL/Tcl")  
---|---|---  
44.5. Database Access from PL/Tcl  | [Home](index.html "PostgreSQL 16.9 Documentation") |  44.7. Event Trigger Functions in PL/Tcl  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pltcl-trigger.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

