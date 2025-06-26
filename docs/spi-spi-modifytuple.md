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

Supported Versions: [Current](/docs/current/spi-spi-modifytuple.html
"PostgreSQL 17 - SPI_modifytuple") ([17](/docs/17/spi-spi-modifytuple.html
"PostgreSQL 17 - SPI_modifytuple")) / [16](/docs/16/spi-spi-modifytuple.html
"PostgreSQL 16 - SPI_modifytuple") / [15](/docs/15/spi-spi-modifytuple.html
"PostgreSQL 15 - SPI_modifytuple") / [14](/docs/14/spi-spi-modifytuple.html
"PostgreSQL 14 - SPI_modifytuple") / [13](/docs/13/spi-spi-modifytuple.html
"PostgreSQL 13 - SPI_modifytuple")

Development Versions: [18](/docs/18/spi-spi-modifytuple.html "PostgreSQL 18 -
SPI_modifytuple") / [devel](/docs/devel/spi-spi-modifytuple.html "PostgreSQL
devel - SPI_modifytuple")

Unsupported versions: [12](/docs/12/spi-spi-modifytuple.html "PostgreSQL 12 -
SPI_modifytuple") / [11](/docs/11/spi-spi-modifytuple.html "PostgreSQL 11 -
SPI_modifytuple") / [10](/docs/10/spi-spi-modifytuple.html "PostgreSQL 10 -
SPI_modifytuple") / [9.6](/docs/9.6/spi-spi-modifytuple.html "PostgreSQL 9.6 -
SPI_modifytuple") / [9.5](/docs/9.5/spi-spi-modifytuple.html "PostgreSQL 9.5 -
SPI_modifytuple") / [9.4](/docs/9.4/spi-spi-modifytuple.html "PostgreSQL 9.4 -
SPI_modifytuple") / [9.3](/docs/9.3/spi-spi-modifytuple.html "PostgreSQL 9.3 -
SPI_modifytuple") / [9.2](/docs/9.2/spi-spi-modifytuple.html "PostgreSQL 9.2 -
SPI_modifytuple") / [9.1](/docs/9.1/spi-spi-modifytuple.html "PostgreSQL 9.1 -
SPI_modifytuple") / [9.0](/docs/9.0/spi-spi-modifytuple.html "PostgreSQL 9.0 -
SPI_modifytuple") / [8.4](/docs/8.4/spi-spi-modifytuple.html "PostgreSQL 8.4 -
SPI_modifytuple") / [8.3](/docs/8.3/spi-spi-modifytuple.html "PostgreSQL 8.3 -
SPI_modifytuple") / [8.2](/docs/8.2/spi-spi-modifytuple.html "PostgreSQL 8.2 -
SPI_modifytuple") / [8.1](/docs/8.1/spi-spi-modifytuple.html "PostgreSQL 8.1 -
SPI_modifytuple") / [8.0](/docs/8.0/spi-spi-modifytuple.html "PostgreSQL 8.0 -
SPI_modifytuple") / [7.4](/docs/7.4/spi-spi-modifytuple.html "PostgreSQL 7.4 -
SPI_modifytuple")

__

SPI_modifytuple  
---  
[Prev](spi-spi-returntuple.html "SPI_returntuple")  | [Up](spi-memory.html "47.3. Memory Management") | 47.3. Memory Management | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](spi-spi-freetuple.html "SPI_freetuple")  
  
* * *

## SPI_modifytuple

SPI_modifytuple — create a row by replacing selected fields of a given row

## Synopsis

    
    
    HeapTuple SPI_modifytuple(Relation _rel_ , HeapTuple _row_ , int _ncols_ ,
                              int * _colnum_ , Datum * _values_ , const char * _nulls_)
    

## Description

`SPI_modifytuple` creates a new row by substituting new values for selected
columns, copying the original row's columns at other positions. The input row
is not modified. The new row is returned in the upper executor context.

This function can only be used while connected to SPI. Otherwise, it returns
NULL and sets `SPI_result` to `SPI_ERROR_UNCONNECTED`.

## Arguments

`Relation _`rel`_`

    

Used only as the source of the row descriptor for the row. (Passing a relation
rather than a row descriptor is a misfeature.)

`HeapTuple _`row`_`

    

row to be modified

`int _`ncols`_`

    

number of columns to be changed

`int * _`colnum`_`

    

an array of length _`ncols`_ , containing the numbers of the columns that are
to be changed (column numbers start at 1)

`Datum * _`values`_`

    

an array of length _`ncols`_ , containing the new values for the specified
columns

`const char * _`nulls`_`

    

an array of length _`ncols`_ , describing which new values are null

If _`nulls`_ is `NULL` then `SPI_modifytuple` assumes that no new values are
null. Otherwise, each entry of the _`nulls`_ array should be `' '` if the
corresponding new value is non-null, or `'n'` if the corresponding new value
is null. (In the latter case, the actual value in the corresponding _`values`_
entry doesn't matter.) Note that _`nulls`_ is not a text string, just an
array: it does not need a `'\0'` terminator.

## Return Value

new row with modifications, allocated in the upper executor context, or `NULL`
on error (see `SPI_result` for an error indication)

On error, `SPI_result` is set as follows:

`SPI_ERROR_ARGUMENT`

    

if _`rel`_ is `NULL`, or if _`row`_ is `NULL`, or if _`ncols`_ is less than or
equal to 0, or if _`colnum`_ is `NULL`, or if _`values`_ is `NULL`.

`SPI_ERROR_NOATTRIBUTE`

    

if _`colnum`_ contains an invalid column number (less than or equal to 0 or
greater than the number of columns in _`row`_)

`SPI_ERROR_UNCONNECTED`

    

if SPI is not active

* * *

[Prev](spi-spi-returntuple.html "SPI_returntuple")  | [Up](spi-memory.html "47.3. Memory Management") |  [Next](spi-spi-freetuple.html "SPI_freetuple")  
---|---|---  
SPI_returntuple  | [Home](index.html "PostgreSQL 16.9 Documentation") |  SPI_freetuple  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/spi-spi-modifytuple.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

