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

Supported Versions: [Current](/docs/current/functions-enum.html "PostgreSQL 17
- 9.10. Enum Support Functions") ([17](/docs/17/functions-enum.html
"PostgreSQL 17 - 9.10. Enum Support Functions")) / [16](/docs/16/functions-
enum.html "PostgreSQL 16 - 9.10. Enum Support Functions") /
[15](/docs/15/functions-enum.html "PostgreSQL 15 - 9.10. Enum Support
Functions") / [14](/docs/14/functions-enum.html "PostgreSQL 14 - 9.10. Enum
Support Functions") / [13](/docs/13/functions-enum.html "PostgreSQL 13 -
9.10. Enum Support Functions")

Development Versions: [18](/docs/18/functions-enum.html "PostgreSQL 18 -
9.10. Enum Support Functions") / [devel](/docs/devel/functions-enum.html
"PostgreSQL devel - 9.10. Enum Support Functions")

Unsupported versions: [12](/docs/12/functions-enum.html "PostgreSQL 12 -
9.10. Enum Support Functions") / [11](/docs/11/functions-enum.html "PostgreSQL
11 - 9.10. Enum Support Functions") / [10](/docs/10/functions-enum.html
"PostgreSQL 10 - 9.10. Enum Support Functions") / [9.6](/docs/9.6/functions-
enum.html "PostgreSQL 9.6 - 9.10. Enum Support Functions") /
[9.5](/docs/9.5/functions-enum.html "PostgreSQL 9.5 - 9.10. Enum Support
Functions") / [9.4](/docs/9.4/functions-enum.html "PostgreSQL 9.4 - 9.10. Enum
Support Functions") / [9.3](/docs/9.3/functions-enum.html "PostgreSQL 9.3 -
9.10. Enum Support Functions") / [9.2](/docs/9.2/functions-enum.html
"PostgreSQL 9.2 - 9.10. Enum Support Functions") / [9.1](/docs/9.1/functions-
enum.html "PostgreSQL 9.1 - 9.10. Enum Support Functions") /
[9.0](/docs/9.0/functions-enum.html "PostgreSQL 9.0 - 9.10. Enum Support
Functions") / [8.4](/docs/8.4/functions-enum.html "PostgreSQL 8.4 - 9.10. Enum
Support Functions") / [8.3](/docs/8.3/functions-enum.html "PostgreSQL 8.3 -
9.10. Enum Support Functions")

__

9.10. Enum Support Functions  
---  
[Prev](functions-datetime.html "9.9. Date/Time Functions and Operators")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions-geometry.html "9.11. Geometric Functions and Operators")  
  
* * *

## 9.10. Enum Support Functions #

For enum types (described in [Section 8.7](datatype-enum.html "8.7. Enumerated
Types")), there are several functions that allow cleaner programming without
hard-coding particular values of an enum type. These are listed in [Table
9.35](functions-enum.html#FUNCTIONS-ENUM-TABLE "Table 9.35. Enum Support
Functions"). The examples assume an enum type created as:

    
    
    CREATE TYPE rainbow AS ENUM ('red', 'orange', 'yellow', 'green', 'blue', 'purple');
    

**Table  9.35. Enum Support Functions**

Function Description Example(s)  
---  
`enum_first` ( `anyenum` ) → `anyenum` Returns the first value of the input
enum type. `enum_first(null::rainbow)` → `red`  
`enum_last` ( `anyenum` ) → `anyenum` Returns the last value of the input enum
type. `enum_last(null::rainbow)` → `purple`  
`enum_range` ( `anyenum` ) → `anyarray` Returns all values of the input enum
type in an ordered array. `enum_range(null::rainbow)` →
`{red,orange,yellow,​green,blue,purple}`  
`enum_range` ( `anyenum`, `anyenum` ) → `anyarray` Returns the range between
the two given enum values, as an ordered array. The values must be from the
same enum type. If the first parameter is null, the result will start with the
first value of the enum type. If the second parameter is null, the result will
end with the last value of the enum type. `enum_range('orange'::rainbow,
'green'::rainbow)` → `{orange,yellow,green}` `enum_range(NULL,
'green'::rainbow)` → `{red,orange,​yellow,green}`
`enum_range('orange'::rainbow, NULL)` → `{orange,yellow,green,​blue,purple}`  
  
  

Notice that except for the two-argument form of `enum_range`, these functions
disregard the specific value passed to them; they care only about its declared
data type. Either null or a specific value of the type can be passed, with the
same result. It is more common to apply these functions to a table column or
function argument than to a hardwired type name as used in the examples.

* * *

[Prev](functions-datetime.html "9.9. Date/Time Functions and Operators")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](functions-geometry.html "9.11. Geometric Functions and Operators")  
---|---|---  
9.9. Date/Time Functions and Operators  | [Home](index.html "PostgreSQL 16.9 Documentation") |  9.11. Geometric Functions and Operators  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-enum.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

