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

Supported Versions: [Current](/docs/current/earthdistance.html "PostgreSQL 17
- F.15. earthdistance — calculate great-circle distances")
([17](/docs/17/earthdistance.html "PostgreSQL 17 - F.15. earthdistance —
calculate great-circle distances")) / [16](/docs/16/earthdistance.html
"PostgreSQL 16 - F.15. earthdistance — calculate great-circle distances") /
[15](/docs/15/earthdistance.html "PostgreSQL 15 - F.15. earthdistance —
calculate great-circle distances") / [14](/docs/14/earthdistance.html
"PostgreSQL 14 - F.15. earthdistance — calculate great-circle distances") /
[13](/docs/13/earthdistance.html "PostgreSQL 13 - F.15. earthdistance —
calculate great-circle distances")

Development Versions: [18](/docs/18/earthdistance.html "PostgreSQL 18 -
F.15. earthdistance — calculate great-circle distances") /
[devel](/docs/devel/earthdistance.html "PostgreSQL devel - F.15. earthdistance
— calculate great-circle distances")

Unsupported versions: [12](/docs/12/earthdistance.html "PostgreSQL 12 -
F.15. earthdistance — calculate great-circle distances") /
[11](/docs/11/earthdistance.html "PostgreSQL 11 - F.15. earthdistance —
calculate great-circle distances") / [10](/docs/10/earthdistance.html
"PostgreSQL 10 - F.15. earthdistance — calculate great-circle distances") /
[9.6](/docs/9.6/earthdistance.html "PostgreSQL 9.6 - F.15. earthdistance —
calculate great-circle distances") / [9.5](/docs/9.5/earthdistance.html
"PostgreSQL 9.5 - F.15. earthdistance — calculate great-circle distances") /
[9.4](/docs/9.4/earthdistance.html "PostgreSQL 9.4 - F.15. earthdistance —
calculate great-circle distances") / [9.3](/docs/9.3/earthdistance.html
"PostgreSQL 9.3 - F.15. earthdistance — calculate great-circle distances") /
[9.2](/docs/9.2/earthdistance.html "PostgreSQL 9.2 - F.15. earthdistance —
calculate great-circle distances") / [9.1](/docs/9.1/earthdistance.html
"PostgreSQL 9.1 - F.15. earthdistance — calculate great-circle distances") /
[9.0](/docs/9.0/earthdistance.html "PostgreSQL 9.0 - F.15. earthdistance —
calculate great-circle distances") / [8.4](/docs/8.4/earthdistance.html
"PostgreSQL 8.4 - F.15. earthdistance — calculate great-circle distances") /
[8.3](/docs/8.3/earthdistance.html "PostgreSQL 8.3 - F.15. earthdistance —
calculate great-circle distances")

__

F.15. earthdistance — calculate great-circle distances  
---  
[Prev](dict-xsyn.html "F.14. dict_xsyn — example synonym full-text search dictionary")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") | Appendix F. Additional Supplied Modules and Extensions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](file-fdw.html "F.16. file_fdw — access data files in the server's file system")  
  
* * *

## F.15. earthdistance — calculate great-circle distances #

[F.15.1. Cube-Based Earth Distances](earthdistance.html#EARTHDISTANCE-CUBE-
BASED)

[F.15.2. Point-Based Earth Distances](earthdistance.html#EARTHDISTANCE-POINT-
BASED)

The `earthdistance` module provides two different approaches to calculating
great circle distances on the surface of the Earth. The one described first
depends on the `cube` module. The second one is based on the built-in `point`
data type, using longitude and latitude for the coordinates.

In this module, the Earth is assumed to be perfectly spherical. (If that's too
inaccurate for you, you might want to look at the
[PostGIS](https://postgis.net/) project.)

The `cube` module must be installed before `earthdistance` can be installed
(although you can use the `CASCADE` option of `CREATE EXTENSION` to install
both in one command).

### Caution

It is strongly recommended that `earthdistance` and `cube` be installed in the
same schema, and that that schema be one for which CREATE privilege has not
been and will not be granted to any untrusted users. Otherwise there are
installation-time security hazards if `earthdistance`'s schema contains
objects defined by a hostile user. Furthermore, when using `earthdistance`'s
functions after installation, the entire search path should contain only
trusted schemas.

### F.15.1. Cube-Based Earth Distances #

Data is stored in cubes that are points (both corners are the same) using 3
coordinates representing the x, y, and z distance from the center of the
Earth. A [](glossary.html#GLOSSARY-DOMAIN)[domain](glossary.html#GLOSSARY-
DOMAIN "Domain") `earth` over type `cube` is provided, which includes
constraint checks that the value meets these restrictions and is reasonably
close to the actual surface of the Earth.

The radius of the Earth is obtained from the `earth()` function. It is given
in meters. But by changing this one function you can change the module to use
some other units, or to use a different value of the radius that you feel is
more appropriate.

This package has applications to astronomical databases as well. Astronomers
will probably want to change `earth()` to return a radius of `180/pi()` so
that distances are in degrees.

Functions are provided to support input in latitude and longitude (in
degrees), to support output of latitude and longitude, to calculate the great
circle distance between two points and to easily specify a bounding box usable
for index searches.

The provided functions are shown in [Table
F.5](earthdistance.html#EARTHDISTANCE-CUBE-FUNCTIONS "Table F.5. Cube-Based
Earthdistance Functions").

**Table  F.5. Cube-Based Earthdistance Functions**

Function Description  
---  
`earth` () → `float8` Returns the assumed radius of the Earth.  
`sec_to_gc` ( `float8` ) → `float8` Converts the normal straight line (secant)
distance between two points on the surface of the Earth to the great circle
distance between them.  
`gc_to_sec` ( `float8` ) → `float8` Converts the great circle distance between
two points on the surface of the Earth to the normal straight line (secant)
distance between them.  
`ll_to_earth` ( `float8`, `float8` ) → `earth` Returns the location of a point
on the surface of the Earth given its latitude (argument 1) and longitude
(argument 2) in degrees.  
`latitude` ( `earth` ) → `float8` Returns the latitude in degrees of a point
on the surface of the Earth.  
`longitude` ( `earth` ) → `float8` Returns the longitude in degrees of a point
on the surface of the Earth.  
`earth_distance` ( `earth`, `earth` ) → `float8` Returns the great circle
distance between two points on the surface of the Earth.  
`earth_box` ( `earth`, `float8` ) → `cube` Returns a box suitable for an
indexed search using the `cube` `@>` operator for points within a given great
circle distance of a location. Some points in this box are further than the
specified great circle distance from the location, so a second check using
`earth_distance` should be included in the query.  
  
  

### F.15.2. Point-Based Earth Distances #

The second part of the module relies on representing Earth locations as values
of type `point`, in which the first component is taken to represent longitude
in degrees, and the second component is taken to represent latitude in
degrees. Points are taken as (longitude, latitude) and not vice versa because
longitude is closer to the intuitive idea of x-axis and latitude to y-axis.

A single operator is provided, shown in [Table
F.6](earthdistance.html#EARTHDISTANCE-POINT-OPERATORS "Table F.6. Point-Based
Earthdistance Operators").

**Table  F.6. Point-Based Earthdistance Operators**

Operator Description  
---  
`point` `<@>` `point` → `float8` Computes the distance in statute miles
between two points on the Earth's surface.  
  
  

Note that unlike the `cube`-based part of the module, units are hardwired
here: changing the `earth()` function will not affect the results of this
operator.

One disadvantage of the longitude/latitude representation is that you need to
be careful about the edge conditions near the poles and near +/- 180 degrees
of longitude. The `cube`-based representation avoids these discontinuities.

* * *

[Prev](dict-xsyn.html "F.14. dict_xsyn — example synonym full-text search dictionary")  | [Up](contrib.html "Appendix F. Additional Supplied Modules and Extensions") |  [Next](file-fdw.html "F.16. file_fdw — access data files in the server's file system")  
---|---|---  
F.14. dict_xsyn — example synonym full-text search dictionary  | [Home](index.html "PostgreSQL 16.9 Documentation") |  F.16. file_fdw — access data files in the server's file system  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/earthdistance.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

