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

Supported Versions: [Current](/docs/current/datetime-config-files.html
"PostgreSQL 17 - B.4. Date/Time Configuration Files") ([17](/docs/17/datetime-
config-files.html "PostgreSQL 17 - B.4. Date/Time Configuration Files")) /
[16](/docs/16/datetime-config-files.html "PostgreSQL 16 - B.4. Date/Time
Configuration Files") / [15](/docs/15/datetime-config-files.html "PostgreSQL
15 - B.4. Date/Time Configuration Files") / [14](/docs/14/datetime-config-
files.html "PostgreSQL 14 - B.4. Date/Time Configuration Files") /
[13](/docs/13/datetime-config-files.html "PostgreSQL 13 - B.4. Date/Time
Configuration Files")

Development Versions: [18](/docs/18/datetime-config-files.html "PostgreSQL 18
- B.4. Date/Time Configuration Files") / [devel](/docs/devel/datetime-config-
files.html "PostgreSQL devel - B.4. Date/Time Configuration Files")

Unsupported versions: [12](/docs/12/datetime-config-files.html "PostgreSQL 12
- B.4. Date/Time Configuration Files") / [11](/docs/11/datetime-config-
files.html "PostgreSQL 11 - B.4. Date/Time Configuration Files") /
[10](/docs/10/datetime-config-files.html "PostgreSQL 10 - B.4. Date/Time
Configuration Files") / [9.6](/docs/9.6/datetime-config-files.html "PostgreSQL
9.6 - B.4. Date/Time Configuration Files") / [9.5](/docs/9.5/datetime-config-
files.html "PostgreSQL 9.5 - B.4. Date/Time Configuration Files") /
[9.4](/docs/9.4/datetime-config-files.html "PostgreSQL 9.4 - B.4. Date/Time
Configuration Files") / [9.3](/docs/9.3/datetime-config-files.html "PostgreSQL
9.3 - B.4. Date/Time Configuration Files") / [9.2](/docs/9.2/datetime-config-
files.html "PostgreSQL 9.2 - B.4. Date/Time Configuration Files") /
[9.1](/docs/9.1/datetime-config-files.html "PostgreSQL 9.1 - B.4. Date/Time
Configuration Files") / [9.0](/docs/9.0/datetime-config-files.html "PostgreSQL
9.0 - B.4. Date/Time Configuration Files") / [8.4](/docs/8.4/datetime-config-
files.html "PostgreSQL 8.4 - B.4. Date/Time Configuration Files") /
[8.3](/docs/8.3/datetime-config-files.html "PostgreSQL 8.3 - B.4. Date/Time
Configuration Files") / [8.2](/docs/8.2/datetime-config-files.html "PostgreSQL
8.2 - B.4. Date/Time Configuration Files")

__

B.4. Date/Time Configuration Files  
---  
[Prev](datetime-keywords.html "B.3. Date/Time Key Words")  | [Up](datetime-appendix.html "Appendix B. Date/Time Support") | Appendix B. Date/Time Support | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datetime-posix-timezone-specs.html "B.5. POSIX Time Zone Specifications")  
  
* * *

## B.4. Date/Time Configuration Files #

Since timezone abbreviations are not well standardized, PostgreSQL provides a
means to customize the set of abbreviations accepted by the server. The
[timezone_abbreviations](runtime-config-client.html#GUC-TIMEZONE-
ABBREVIATIONS) run-time parameter determines the active set of abbreviations.
While this parameter can be altered by any database user, the possible values
for it are under the control of the database administrator — they are in fact
names of configuration files stored in `.../share/timezonesets/` of the
installation directory. By adding or altering files in that directory, the
administrator can set local policy for timezone abbreviations.

`timezone_abbreviations` can be set to any file name found in
`.../share/timezonesets/`, if the file's name is entirely alphabetic. (The
prohibition against non-alphabetic characters in `timezone_abbreviations`
prevents reading files outside the intended directory, as well as reading
editor backup files and other extraneous files.)

A timezone abbreviation file can contain blank lines and comments beginning
with `#`. Non-comment lines must have one of these formats:

    
    
    _zone_abbreviation_ _offset_
    _zone_abbreviation_ _offset_ D
    _zone_abbreviation_ _time_zone_name_
    @INCLUDE _file_name_
    @OVERRIDE
    

A _`zone_abbreviation`_ is just the abbreviation being defined. An _`offset`_
is an integer giving the equivalent offset in seconds from UTC, positive being
east from Greenwich and negative being west. For example, -18000 would be five
hours west of Greenwich, or North American east coast standard time. `D`
indicates that the zone name represents local daylight-savings time rather
than standard time.

Alternatively, a _`time_zone_name`_ can be given, referencing a zone name
defined in the IANA timezone database. The zone's definition is consulted to
see whether the abbreviation is or has been in use in that zone, and if so,
the appropriate meaning is used — that is, the meaning that was currently in
use at the timestamp whose value is being determined, or the meaning in use
immediately before that if it wasn't current at that time, or the oldest
meaning if it was used only after that time. This behavior is essential for
dealing with abbreviations whose meaning has historically varied. It is also
allowed to define an abbreviation in terms of a zone name in which that
abbreviation does not appear; then using the abbreviation is just equivalent
to writing out the zone name.

### Tip

Using a simple integer _`offset`_ is preferred when defining an abbreviation
whose offset from UTC has never changed, as such abbreviations are much
cheaper to process than those that require consulting a time zone definition.

The `@INCLUDE` syntax allows inclusion of another file in the
`.../share/timezonesets/` directory. Inclusion can be nested, to a limited
depth.

The `@OVERRIDE` syntax indicates that subsequent entries in the file can
override previous entries (typically, entries obtained from included files).
Without this, conflicting definitions of the same timezone abbreviation are
considered an error.

In an unmodified installation, the file `Default` contains all the non-
conflicting time zone abbreviations for most of the world. Additional files
`Australia` and `India` are provided for those regions: these files first
include the `Default` file and then add or modify abbreviations as needed.

For reference purposes, a standard installation also contains files
`Africa.txt`, `America.txt`, etc., containing information about every time
zone abbreviation known to be in use according to the IANA timezone database.
The zone name definitions found in these files can be copied and pasted into a
custom configuration file as needed. Note that these files cannot be directly
referenced as `timezone_abbreviations` settings, because of the dot embedded
in their names.

### Note

If an error occurs while reading the time zone abbreviation set, no new value
is applied and the old set is kept. If the error occurs while starting the
database, startup fails.

### Caution

Time zone abbreviations defined in the configuration file override non-
timezone meanings built into PostgreSQL. For example, the `Australia`
configuration file defines `SAT` (for South Australian Standard Time). When
this file is active, `SAT` will not be recognized as an abbreviation for
Saturday.

### Caution

If you modify files in `.../share/timezonesets/`, it is up to you to make
backups — a normal database dump will not include this directory.

* * *

[Prev](datetime-keywords.html "B.3. Date/Time Key Words")  | [Up](datetime-appendix.html "Appendix B. Date/Time Support") |  [Next](datetime-posix-timezone-specs.html "B.5. POSIX Time Zone Specifications")  
---|---|---  
B.3. Date/Time Key Words  | [Home](index.html "PostgreSQL 16.9 Documentation") |  B.5. POSIX Time Zone Specifications  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datetime-config-files.html/)
to report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

