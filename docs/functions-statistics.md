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

Supported Versions: [Current](/docs/current/functions-statistics.html
"PostgreSQL 17 - 9.30. Statistics Information Functions")
([17](/docs/17/functions-statistics.html "PostgreSQL 17 - 9.30. Statistics
Information Functions")) / [16](/docs/16/functions-statistics.html "PostgreSQL
16 - 9.30. Statistics Information Functions") / [15](/docs/15/functions-
statistics.html "PostgreSQL 15 - 9.30. Statistics Information Functions") /
[14](/docs/14/functions-statistics.html "PostgreSQL 14 - 9.30. Statistics
Information Functions") / [13](/docs/13/functions-statistics.html "PostgreSQL
13 - 9.30. Statistics Information Functions")

Development Versions: [18](/docs/18/functions-statistics.html "PostgreSQL 18 -
9.30. Statistics Information Functions") / [devel](/docs/devel/functions-
statistics.html "PostgreSQL devel - 9.30. Statistics Information Functions")

Unsupported versions: [12](/docs/12/functions-statistics.html "PostgreSQL 12 -
9.30. Statistics Information Functions")

__

9.30. Statistics Information Functions  
---  
[Prev](functions-event-triggers.html "9.29. Event Trigger Functions")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](typeconv.html "Chapter 10. Type Conversion")  
  
* * *

## 9.30. Statistics Information Functions #

[9.30.1. Inspecting MCV Lists](functions-statistics.html#FUNCTIONS-STATISTICS-
MCV)

PostgreSQL provides a function to inspect complex statistics defined using the
`CREATE STATISTICS` command.

### 9.30.1. Inspecting MCV Lists #

    
    
    pg_mcv_list_items ( pg_mcv_list ) → setof record
    

`pg_mcv_list_items` returns a set of records describing all items stored in a
multi-column MCV list. It returns the following columns:

Name | Type | Description  
---|---|---  
`index` | `integer` | index of the item in the MCV list  
`values` | `text[]` | values stored in the MCV item  
`nulls` | `boolean[]` | flags identifying `NULL` values  
`frequency` | `double precision` | frequency of this MCV item  
`base_frequency` | `double precision` | base frequency of this MCV item  
  
The `pg_mcv_list_items` function can be used like this:

    
    
    SELECT m.* FROM pg_statistic_ext join pg_statistic_ext_data on (oid = stxoid),
                    pg_mcv_list_items(stxdmcv) m WHERE stxname = 'stts';
    

Values of the `pg_mcv_list` type can be obtained only from the
`pg_statistic_ext_data`.`stxdmcv` column.

* * *

[Prev](functions-event-triggers.html "9.29. Event Trigger Functions")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](typeconv.html "Chapter 10. Type Conversion")  
---|---|---  
9.29. Event Trigger Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 10. Type Conversion  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-statistics.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

