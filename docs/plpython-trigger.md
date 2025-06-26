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

Supported Versions: [Current](/docs/current/plpython-trigger.html "PostgreSQL
17 - 46.5. Trigger Functions") ([17](/docs/17/plpython-trigger.html
"PostgreSQL 17 - 46.5. Trigger Functions")) / [16](/docs/16/plpython-
trigger.html "PostgreSQL 16 - 46.5. Trigger Functions") /
[15](/docs/15/plpython-trigger.html "PostgreSQL 15 - 46.5. Trigger Functions")
/ [14](/docs/14/plpython-trigger.html "PostgreSQL 14 - 46.5. Trigger
Functions") / [13](/docs/13/plpython-trigger.html "PostgreSQL 13 -
46.5. Trigger Functions")

Development Versions: [18](/docs/18/plpython-trigger.html "PostgreSQL 18 -
46.5. Trigger Functions") / [devel](/docs/devel/plpython-trigger.html
"PostgreSQL devel - 46.5. Trigger Functions")

Unsupported versions: [12](/docs/12/plpython-trigger.html "PostgreSQL 12 -
46.5. Trigger Functions") / [11](/docs/11/plpython-trigger.html "PostgreSQL 11
- 46.5. Trigger Functions") / [10](/docs/10/plpython-trigger.html "PostgreSQL
10 - 46.5. Trigger Functions") / [9.6](/docs/9.6/plpython-trigger.html
"PostgreSQL 9.6 - 46.5. Trigger Functions") / [9.5](/docs/9.5/plpython-
trigger.html "PostgreSQL 9.5 - 46.5. Trigger Functions") /
[9.4](/docs/9.4/plpython-trigger.html "PostgreSQL 9.4 - 46.5. Trigger
Functions") / [9.3](/docs/9.3/plpython-trigger.html "PostgreSQL 9.3 -
46.5. Trigger Functions") / [9.2](/docs/9.2/plpython-trigger.html "PostgreSQL
9.2 - 46.5. Trigger Functions") / [9.1](/docs/9.1/plpython-trigger.html
"PostgreSQL 9.1 - 46.5. Trigger Functions") / [9.0](/docs/9.0/plpython-
trigger.html "PostgreSQL 9.0 - 46.5. Trigger Functions") /
[8.4](/docs/8.4/plpython-trigger.html "PostgreSQL 8.4 - 46.5. Trigger
Functions") / [8.3](/docs/8.3/plpython-trigger.html "PostgreSQL 8.3 -
46.5. Trigger Functions") / [8.2](/docs/8.2/plpython-trigger.html "PostgreSQL
8.2 - 46.5. Trigger Functions") / [8.1](/docs/8.1/plpython-trigger.html
"PostgreSQL 8.1 - 46.5. Trigger Functions") / [8.0](/docs/8.0/plpython-
trigger.html "PostgreSQL 8.0 - 46.5. Trigger Functions") /
[7.4](/docs/7.4/plpython-trigger.html "PostgreSQL 7.4 - 46.5. Trigger
Functions") / [7.3](/docs/7.3/plpython-trigger.html "PostgreSQL 7.3 -
46.5. Trigger Functions")

__

46.5. Trigger Functions  
---  
[Prev](plpython-do.html "46.4. Anonymous Code Blocks")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") | Chapter 46. PL/Python — Python Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](plpython-database.html "46.6. Database Access")  
  
* * *

## 46.5. Trigger Functions #

When a function is used as a trigger, the dictionary `TD` contains trigger-
related values:

`TD["event"]`

    

contains the event as a string: `INSERT`, `UPDATE`, `DELETE`, or `TRUNCATE`.

`TD["when"]`

    

contains one of `BEFORE`, `AFTER`, or `INSTEAD OF`.

`TD["level"]`

    

contains `ROW` or `STATEMENT`.

`TD["new"]`  
`TD["old"]`

    

For a row-level trigger, one or both of these fields contain the respective
trigger rows, depending on the trigger event.

`TD["name"]`

    

contains the trigger name.

`TD["table_name"]`

    

contains the name of the table on which the trigger occurred.

`TD["table_schema"]`

    

contains the schema of the table on which the trigger occurred.

`TD["relid"]`

    

contains the OID of the table on which the trigger occurred.

`TD["args"]`

    

If the `CREATE TRIGGER` command included arguments, they are available in
`TD["args"][0]` to `TD["args"][_`n`_ -1]`.

If `TD["when"]` is `BEFORE` or `INSTEAD OF` and `TD["level"]` is `ROW`, you
can return `None` or `"OK"` from the Python function to indicate the row is
unmodified, `"SKIP"` to abort the event, or if `TD["event"]` is `INSERT` or
`UPDATE` you can return `"MODIFY"` to indicate you've modified the new row.
Otherwise the return value is ignored.

* * *

[Prev](plpython-do.html "46.4. Anonymous Code Blocks")  | [Up](plpython.html "Chapter 46. PL/Python — Python Procedural Language") |  [Next](plpython-database.html "46.6. Database Access")  
---|---|---  
46.4. Anonymous Code Blocks  | [Home](index.html "PostgreSQL 16.9 Documentation") |  46.6. Database Access  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpython-trigger.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

