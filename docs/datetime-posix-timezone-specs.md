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

Supported Versions: [Current](/docs/current/datetime-posix-timezone-specs.html
"PostgreSQL 17 - B.5. POSIX Time Zone Specifications")
([17](/docs/17/datetime-posix-timezone-specs.html "PostgreSQL 17 - B.5. POSIX
Time Zone Specifications")) / [16](/docs/16/datetime-posix-timezone-specs.html
"PostgreSQL 16 - B.5. POSIX Time Zone Specifications") /
[15](/docs/15/datetime-posix-timezone-specs.html "PostgreSQL 15 - B.5. POSIX
Time Zone Specifications") / [14](/docs/14/datetime-posix-timezone-specs.html
"PostgreSQL 14 - B.5. POSIX Time Zone Specifications") /
[13](/docs/13/datetime-posix-timezone-specs.html "PostgreSQL 13 - B.5. POSIX
Time Zone Specifications")

Development Versions: [18](/docs/18/datetime-posix-timezone-specs.html
"PostgreSQL 18 - B.5. POSIX Time Zone Specifications") /
[devel](/docs/devel/datetime-posix-timezone-specs.html "PostgreSQL devel -
B.5. POSIX Time Zone Specifications")

Unsupported versions: [12](/docs/12/datetime-posix-timezone-specs.html
"PostgreSQL 12 - B.5. POSIX Time Zone Specifications") /
[11](/docs/11/datetime-posix-timezone-specs.html "PostgreSQL 11 - B.5. POSIX
Time Zone Specifications") / [10](/docs/10/datetime-posix-timezone-specs.html
"PostgreSQL 10 - B.5. POSIX Time Zone Specifications") /
[9.6](/docs/9.6/datetime-posix-timezone-specs.html "PostgreSQL 9.6 -
B.5. POSIX Time Zone Specifications") / [9.5](/docs/9.5/datetime-posix-
timezone-specs.html "PostgreSQL 9.5 - B.5. POSIX Time Zone Specifications")

__

B.5. POSIX Time Zone Specifications  
---  
[Prev](datetime-config-files.html "B.4. Date/Time Configuration Files")  | [Up](datetime-appendix.html "Appendix B. Date/Time Support") | Appendix B. Date/Time Support | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datetime-units-history.html "B.6. History of Units")  
  
* * *

## B.5. POSIX Time Zone Specifications #

PostgreSQL can accept time zone specifications that are written according to
the POSIX standard's rules for the `TZ` environment variable. POSIX time zone
specifications are inadequate to deal with the complexity of real-world time
zone history, but there are sometimes reasons to use them.

A POSIX time zone specification has the form

    
    
    _STD_ _offset_ [ _DST_ [ _dstoffset_ ] [ , _rule_ ] ]
    

(For readability, we show spaces between the fields, but spaces should not be
used in practice.) The fields are:

  * _`STD`_ is the zone abbreviation to be used for standard time.

  * _`offset`_ is the zone's standard-time offset from UTC.

  * _`DST`_ is the zone abbreviation to be used for daylight-savings time. If this field and the following ones are omitted, the zone uses a fixed UTC offset with no daylight-savings rule.

  * _`dstoffset`_ is the daylight-savings offset from UTC. This field is typically omitted, since it defaults to one hour less than the standard-time _`offset`_ , which is usually the right thing.

  * _`rule`_ defines the rule for when daylight savings is in effect, as described below.

In this syntax, a zone abbreviation can be a string of letters, such as `EST`,
or an arbitrary string surrounded by angle brackets, such as `<UTC-05>`. Note
that the zone abbreviations given here are only used for output, and even then
only in some timestamp output formats. The zone abbreviations recognized in
timestamp input are determined as explained in [Section B.4](datetime-config-
files.html "B.4. Date/Time Configuration Files").

The offset fields specify the hours, and optionally minutes and seconds,
difference from UTC. They have the format _`hh`_[`:`_`mm`_[`:`_`ss`_]]
optionally with a leading sign (`+` or `-`). The positive sign is used for
zones _west_ of Greenwich. (Note that this is the opposite of the ISO-8601
sign convention used elsewhere in PostgreSQL.) _`hh`_ can have one or two
digits; _`mm`_ and _`ss`_ (if used) must have two.

The daylight-savings transition _`rule`_ has the format

    
    
    _dstdate_ [ / _dsttime_ ] , _stddate_ [ / _stdtime_ ]
    

(As before, spaces should not be included in practice.) The _`dstdate`_ and
_`dsttime`_ fields define when daylight-savings time starts, while _`stddate`_
and _`stdtime`_ define when standard time starts. (In some cases, notably in
zones south of the equator, the former might be later in the year than the
latter.) The date fields have one of these formats:

_`n`_

    

A plain integer denotes a day of the year, counting from zero to 364, or to
365 in leap years.

`J` _`n`_

    

In this form, _`n`_ counts from 1 to 365, and February 29 is not counted even
if it is present. (Thus, a transition occurring on February 29 could not be
specified this way. However, days after February have the same numbers whether
it's a leap year or not, so that this form is usually more useful than the
plain-integer form for transitions on fixed dates.)

`M` _`m`_`.`_`n`_`.`_`d`_

    

This form specifies a transition that always happens during the same month and
on the same day of the week. _`m`_ identifies the month, from 1 to 12. _`n`_
specifies the _`n`_ 'th occurrence of the weekday identified by _`d`_. _`n`_
is a number between 1 and 4, or 5 meaning the last occurrence of that weekday
in the month (which could be the fourth or the fifth). _`d`_ is a number
between 0 and 6, with 0 indicating Sunday. For example, `M3.2.0` means “the
second Sunday in March”.

### Note

The `M` format is sufficient to describe many common daylight-savings
transition laws. But note that none of these variants can deal with daylight-
savings law changes, so in practice the historical data stored for named time
zones (in the IANA time zone database) is necessary to interpret past time
stamps correctly.

The time fields in a transition rule have the same format as the offset fields
described previously, except that they cannot contain signs. They define the
current local time at which the change to the other time occurs. If omitted,
they default to `02:00:00`.

If a daylight-savings abbreviation is given but the transition _`rule`_ field
is omitted, the fallback behavior is to use the rule `M3.2.0,M11.1.0`, which
corresponds to USA practice as of 2020 (that is, spring forward on the second
Sunday of March, fall back on the first Sunday of November, both transitions
occurring at 2AM prevailing time). Note that this rule does not give correct
USA transition dates for years before 2007.

As an example, `CET-1CEST,M3.5.0,M10.5.0/3` describes current (as of 2020)
timekeeping practice in Paris. This specification says that standard time has
the abbreviation `CET` and is one hour ahead (east) of UTC; daylight savings
time has the abbreviation `CEST` and is implicitly two hours ahead of UTC;
daylight savings time begins on the last Sunday in March at 2AM CET and ends
on the last Sunday in October at 3AM CEST.

The four timezone names `EST5EDT`, `CST6CDT`, `MST7MDT`, and `PST8PDT` look
like they are POSIX zone specifications. However, they actually are treated as
named time zones because (for historical reasons) there are files by those
names in the IANA time zone database. The practical implication of this is
that these zone names will produce valid historical USA daylight-savings
transitions, even when a plain POSIX specification would not.

One should be wary that it is easy to misspell a POSIX-style time zone
specification, since there is no check on the reasonableness of the zone
abbreviation(s). For example, `SET TIMEZONE TO FOOBAR0` will work, leaving the
system effectively using a rather peculiar abbreviation for UTC.

* * *

[Prev](datetime-config-files.html "B.4. Date/Time Configuration Files")  | [Up](datetime-appendix.html "Appendix B. Date/Time Support") |  [Next](datetime-units-history.html "B.6. History of Units")  
---|---|---  
B.4. Date/Time Configuration Files  | [Home](index.html "PostgreSQL 16.9 Documentation") |  B.6. History of Units  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datetime-posix-timezone-
specs.html/) to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

