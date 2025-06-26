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

Supported Versions: [Current](/docs/current/datetime-julian-dates.html
"PostgreSQL 17 - B.7. Julian Dates") ([17](/docs/17/datetime-julian-dates.html
"PostgreSQL 17 - B.7. Julian Dates")) / [16](/docs/16/datetime-julian-
dates.html "PostgreSQL 16 - B.7. Julian Dates") / [15](/docs/15/datetime-
julian-dates.html "PostgreSQL 15 - B.7. Julian Dates") /
[14](/docs/14/datetime-julian-dates.html "PostgreSQL 14 - B.7. Julian Dates")
/ [13](/docs/13/datetime-julian-dates.html "PostgreSQL 13 - B.7. Julian
Dates")

Development Versions: [18](/docs/18/datetime-julian-dates.html "PostgreSQL 18
- B.7. Julian Dates") / [devel](/docs/devel/datetime-julian-dates.html
"PostgreSQL devel - B.7. Julian Dates")

Unsupported versions: [12](/docs/12/datetime-julian-dates.html "PostgreSQL 12
- B.7. Julian Dates") / [11](/docs/11/datetime-julian-dates.html "PostgreSQL
11 - B.7. Julian Dates") / [10](/docs/10/datetime-julian-dates.html
"PostgreSQL 10 - B.7. Julian Dates") / [9.6](/docs/9.6/datetime-julian-
dates.html "PostgreSQL 9.6 - B.7. Julian Dates")

__

B.7. Julian Dates  
---  
[Prev](datetime-units-history.html "B.6. History of Units")  | [Up](datetime-appendix.html "Appendix B. Date/Time Support") | Appendix B. Date/Time Support | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](sql-keywords-appendix.html "Appendix C. SQL Key Words")  
  
* * *

## B.7. Julian Dates #

The _Julian Date_ system is a method for numbering days. It is unrelated to
the Julian calendar, though it is confusingly named similarly to that
calendar. The Julian Date system was invented by the French scholar Joseph
Justus Scaliger (1540–1609) and probably takes its name from Scaliger's
father, the Italian scholar Julius Caesar Scaliger (1484–1558).

In the Julian Date system, each day has a sequential number, starting from JD
0 (which is sometimes called _the_ Julian Date). JD 0 corresponds to 1 January
4713 BC in the Julian calendar, or 24 November 4714 BC in the Gregorian
calendar. Julian Date counting is most often used by astronomers for labeling
their nightly observations, and therefore a date runs from noon UTC to the
next noon UTC, rather than from midnight to midnight: JD 0 designates the 24
hours from noon UTC on 24 November 4714 BC to noon UTC on 25 November 4714 BC.

Although PostgreSQL supports Julian Date notation for input and output of
dates (and also uses Julian dates for some internal datetime calculations), it
does not observe the nicety of having dates run from noon to noon. PostgreSQL
treats a Julian Date as running from local midnight to local midnight, the
same as a normal date.

This definition does, however, provide a way to obtain the astronomical
definition when you need it: do the arithmetic in time zone `UTC+12`. For
example,

    
    
    => SELECT extract(julian from '2021-06-23 7:00:00-04'::timestamptz at time zone 'UTC+12');
               extract
    ------------------------------
     2459388.95833333333333333333
    (1 row)
    => SELECT extract(julian from '2021-06-23 8:00:00-04'::timestamptz at time zone 'UTC+12');
                   extract
    --------------------------------------
     2459389.0000000000000000000000000000
    (1 row)
    => SELECT extract(julian from date '2021-06-23');
     extract
    ---------
     2459389
    (1 row)
    

* * *

[Prev](datetime-units-history.html "B.6. History of Units")  | [Up](datetime-appendix.html "Appendix B. Date/Time Support") |  [Next](sql-keywords-appendix.html "Appendix C. SQL Key Words")  
---|---|---  
B.6. History of Units  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Appendix C. SQL Key Words  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datetime-julian-dates.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

