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

Supported Versions: [Current](/docs/current/datetime-units-history.html
"PostgreSQL 17 - B.6. History of Units") ([17](/docs/17/datetime-units-
history.html "PostgreSQL 17 - B.6. History of Units")) /
[16](/docs/16/datetime-units-history.html "PostgreSQL 16 - B.6. History of
Units") / [15](/docs/15/datetime-units-history.html "PostgreSQL 15 -
B.6. History of Units") / [14](/docs/14/datetime-units-history.html
"PostgreSQL 14 - B.6. History of Units") / [13](/docs/13/datetime-units-
history.html "PostgreSQL 13 - B.6. History of Units")

Development Versions: [18](/docs/18/datetime-units-history.html "PostgreSQL 18
- B.6. History of Units") / [devel](/docs/devel/datetime-units-history.html
"PostgreSQL devel - B.6. History of Units")

Unsupported versions: [12](/docs/12/datetime-units-history.html "PostgreSQL 12
- B.6. History of Units") / [11](/docs/11/datetime-units-history.html
"PostgreSQL 11 - B.6. History of Units") / [10](/docs/10/datetime-units-
history.html "PostgreSQL 10 - B.6. History of Units") /
[9.6](/docs/9.6/datetime-units-history.html "PostgreSQL 9.6 - B.6. History of
Units") / [9.5](/docs/9.5/datetime-units-history.html "PostgreSQL 9.5 -
B.6. History of Units") / [9.4](/docs/9.4/datetime-units-history.html
"PostgreSQL 9.4 - B.6. History of Units") / [9.3](/docs/9.3/datetime-units-
history.html "PostgreSQL 9.3 - B.6. History of Units") /
[9.2](/docs/9.2/datetime-units-history.html "PostgreSQL 9.2 - B.6. History of
Units") / [9.1](/docs/9.1/datetime-units-history.html "PostgreSQL 9.1 -
B.6. History of Units") / [9.0](/docs/9.0/datetime-units-history.html
"PostgreSQL 9.0 - B.6. History of Units") / [8.4](/docs/8.4/datetime-units-
history.html "PostgreSQL 8.4 - B.6. History of Units") /
[8.3](/docs/8.3/datetime-units-history.html "PostgreSQL 8.3 - B.6. History of
Units") / [8.2](/docs/8.2/datetime-units-history.html "PostgreSQL 8.2 -
B.6. History of Units") / [8.1](/docs/8.1/datetime-units-history.html
"PostgreSQL 8.1 - B.6. History of Units") / [8.0](/docs/8.0/datetime-units-
history.html "PostgreSQL 8.0 - B.6. History of Units") /
[7.4](/docs/7.4/datetime-units-history.html "PostgreSQL 7.4 - B.6. History of
Units")

__

B.6. History of Units  
---  
[Prev](datetime-posix-timezone-specs.html "B.5. POSIX Time Zone Specifications")  | [Up](datetime-appendix.html "Appendix B. Date/Time Support") | Appendix B. Date/Time Support | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datetime-julian-dates.html "B.7. Julian Dates")  
  
* * *

## B.6. History of Units #

The SQL standard states that “Within the definition of a ‘datetime literal’,
the ‘datetime values’ are constrained by the natural rules for dates and times
according to the Gregorian calendar”. PostgreSQL follows the SQL standard's
lead by counting dates exclusively in the Gregorian calendar, even for years
before that calendar was in use. This rule is known as the _proleptic
Gregorian calendar_.

The Julian calendar was introduced by Julius Caesar in 45 BC. It was in common
use in the Western world until the year 1582, when countries started changing
to the Gregorian calendar. In the Julian calendar, the tropical year is
approximated as 365 1/4 days = 365.25 days. This gives an error of about 1 day
in 128 years.

The accumulating calendar error prompted Pope Gregory XIII to reform the
calendar in accordance with instructions from the Council of Trent. In the
Gregorian calendar, the tropical year is approximated as 365 + 97 / 400 days =
365.2425 days. Thus it takes approximately 3300 years for the tropical year to
shift one day with respect to the Gregorian calendar.

The approximation 365+97/400 is achieved by having 97 leap years every 400
years, using the following rules:

Every year divisible by 4 is a leap year.  
---  
However, every year divisible by 100 is not a leap year.  
However, every year divisible by 400 is a leap year after all.  
  
So, 1700, 1800, 1900, 2100, and 2200 are not leap years. But 1600, 2000, and
2400 are leap years. By contrast, in the older Julian calendar all years
divisible by 4 are leap years.

The papal bull of February 1582 decreed that 10 days should be dropped from
October 1582 so that 15 October should follow immediately after 4 October.
This was observed in Italy, Poland, Portugal, and Spain. Other Catholic
countries followed shortly after, but Protestant countries were reluctant to
change, and the Greek Orthodox countries didn't change until the start of the
20th century. The reform was observed by Great Britain and its dominions
(including what is now the USA) in 1752. Thus 2 September 1752 was followed by
14 September 1752. This is why Unix systems that have the `cal` program
produce the following:

    
    
    $ **cal 9 1752**
       September 1752
     S  M Tu  W Th  F  S
           1  2 14 15 16
    17 18 19 20 21 22 23
    24 25 26 27 28 29 30
    

But, of course, this calendar is only valid for Great Britain and dominions,
not other places. Since it would be difficult and confusing to try to track
the actual calendars that were in use in various places at various times,
PostgreSQL does not try, but rather follows the Gregorian calendar rules for
all dates, even though this method is not historically accurate.

Different calendars have been developed in various parts of the world, many
predating the Gregorian system. For example, the beginnings of the Chinese
calendar can be traced back to the 14th century BC. Legend has it that the
Emperor Huangdi invented that calendar in 2637 BC. The People's Republic of
China uses the Gregorian calendar for civil purposes. The Chinese calendar is
used for determining festivals.

* * *

[Prev](datetime-posix-timezone-specs.html "B.5. POSIX Time Zone Specifications")  | [Up](datetime-appendix.html "Appendix B. Date/Time Support") |  [Next](datetime-julian-dates.html "B.7. Julian Dates")  
---|---|---  
B.5. POSIX Time Zone Specifications  | [Home](index.html "PostgreSQL 16.9 Documentation") |  B.7. Julian Dates  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datetime-units-history.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

