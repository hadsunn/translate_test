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

Supported Versions: [Current](/docs/current/datetime-invalid-input.html
"PostgreSQL 17 - B.2. Handling of Invalid or Ambiguous Timestamps")
([17](/docs/17/datetime-invalid-input.html "PostgreSQL 17 - B.2. Handling of
Invalid or Ambiguous Timestamps")) / [16](/docs/16/datetime-invalid-input.html
"PostgreSQL 16 - B.2. Handling of Invalid or Ambiguous Timestamps") /
[15](/docs/15/datetime-invalid-input.html "PostgreSQL 15 - B.2. Handling of
Invalid or Ambiguous Timestamps") / [14](/docs/14/datetime-invalid-input.html
"PostgreSQL 14 - B.2. Handling of Invalid or Ambiguous Timestamps") /
[13](/docs/13/datetime-invalid-input.html "PostgreSQL 13 - B.2. Handling of
Invalid or Ambiguous Timestamps")

Development Versions: [18](/docs/18/datetime-invalid-input.html "PostgreSQL 18
- B.2. Handling of Invalid or Ambiguous Timestamps") /
[devel](/docs/devel/datetime-invalid-input.html "PostgreSQL devel -
B.2. Handling of Invalid or Ambiguous Timestamps")

Unsupported versions: [12](/docs/12/datetime-invalid-input.html "PostgreSQL 12
- B.2. Handling of Invalid or Ambiguous Timestamps") / [11](/docs/11/datetime-
invalid-input.html "PostgreSQL 11 - B.2. Handling of Invalid or Ambiguous
Timestamps") / [10](/docs/10/datetime-invalid-input.html "PostgreSQL 10 -
B.2. Handling of Invalid or Ambiguous Timestamps") / [9.6](/docs/9.6/datetime-
invalid-input.html "PostgreSQL 9.6 - B.2. Handling of Invalid or Ambiguous
Timestamps") / [9.5](/docs/9.5/datetime-invalid-input.html "PostgreSQL 9.5 -
B.2. Handling of Invalid or Ambiguous Timestamps") / [9.4](/docs/9.4/datetime-
invalid-input.html "PostgreSQL 9.4 - B.2. Handling of Invalid or Ambiguous
Timestamps")

__

B.2. Handling of Invalid or Ambiguous Timestamps  
---  
[Prev](datetime-input-rules.html "B.1. Date/Time Input Interpretation")  | [Up](datetime-appendix.html "Appendix B. Date/Time Support") | Appendix B. Date/Time Support | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datetime-keywords.html "B.3. Date/Time Key Words")  
  
* * *

## B.2. Handling of Invalid or Ambiguous Timestamps #

Ordinarily, if a date/time string is syntactically valid but contains out-of-
range field values, an error will be thrown. For example, input specifying the
31st of February will be rejected.

During a daylight-savings-time transition, it is possible for a seemingly
valid timestamp string to represent a nonexistent or ambiguous timestamp. Such
cases are not rejected; the ambiguity is resolved by determining which UTC
offset to apply. For example, supposing that the [TimeZone](runtime-config-
client.html#GUC-TIMEZONE) parameter is set to `America/New_York`, consider

    
    
    => SELECT '2018-03-11 02:30'::timestamptz;
          timestamptz
    ------------------------
     2018-03-11 03:30:00-04
    (1 row)
    

Because that day was a spring-forward transition date in that time zone, there
was no civil time instant 2:30AM; clocks jumped forward from 2AM EST to 3AM
EDT. PostgreSQL interprets the given time as if it were standard time (UTC-5),
which then renders as 3:30AM EDT (UTC-4).

Conversely, consider the behavior during a fall-back transition:

    
    
    => SELECT '2018-11-04 01:30'::timestamptz;
          timestamptz
    ------------------------
     2018-11-04 01:30:00-05
    (1 row)
    

On that date, there were two possible interpretations of 1:30AM; there was
1:30AM EDT, and then an hour later after clocks jumped back from 2AM EDT to
1AM EST, there was 1:30AM EST. Again, PostgreSQL interprets the given time as
if it were standard time (UTC-5). We can force the other interpretation by
specifying daylight-savings time:

    
    
    => SELECT '2018-11-04 01:30 EDT'::timestamptz;
          timestamptz
    ------------------------
     2018-11-04 01:30:00-04
    (1 row)
    

The precise rule that is applied in such cases is that an invalid timestamp
that appears to fall within a jump-forward daylight savings transition is
assigned the UTC offset that prevailed in the time zone just before the
transition, while an ambiguous timestamp that could fall on either side of a
jump-back transition is assigned the UTC offset that prevailed just after the
transition. In most time zones this is equivalent to saying that “the
standard-time interpretation is preferred when in doubt”.

In all cases, the UTC offset associated with a timestamp can be specified
explicitly, using either a numeric UTC offset or a time zone abbreviation that
corresponds to a fixed UTC offset. The rule just given applies only when it is
necessary to infer a UTC offset for a time zone in which the offset varies.

* * *

[Prev](datetime-input-rules.html "B.1. Date/Time Input Interpretation")  | [Up](datetime-appendix.html "Appendix B. Date/Time Support") |  [Next](datetime-keywords.html "B.3. Date/Time Key Words")  
---|---|---  
B.1. Date/Time Input Interpretation  | [Home](index.html "PostgreSQL 16.9 Documentation") |  B.3. Date/Time Key Words  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datetime-invalid-input.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

