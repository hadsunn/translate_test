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

Supported Versions: [Current](/docs/current/pgtesttiming.html "PostgreSQL 17 -
pg_test_timing") ([17](/docs/17/pgtesttiming.html "PostgreSQL 17 -
pg_test_timing")) / [16](/docs/16/pgtesttiming.html "PostgreSQL 16 -
pg_test_timing") / [15](/docs/15/pgtesttiming.html "PostgreSQL 15 -
pg_test_timing") / [14](/docs/14/pgtesttiming.html "PostgreSQL 14 -
pg_test_timing") / [13](/docs/13/pgtesttiming.html "PostgreSQL 13 -
pg_test_timing")

Development Versions: [18](/docs/18/pgtesttiming.html "PostgreSQL 18 -
pg_test_timing") / [devel](/docs/devel/pgtesttiming.html "PostgreSQL devel -
pg_test_timing")

Unsupported versions: [12](/docs/12/pgtesttiming.html "PostgreSQL 12 -
pg_test_timing") / [11](/docs/11/pgtesttiming.html "PostgreSQL 11 -
pg_test_timing") / [10](/docs/10/pgtesttiming.html "PostgreSQL 10 -
pg_test_timing") / [9.6](/docs/9.6/pgtesttiming.html "PostgreSQL 9.6 -
pg_test_timing") / [9.5](/docs/9.5/pgtesttiming.html "PostgreSQL 9.5 -
pg_test_timing") / [9.4](/docs/9.4/pgtesttiming.html "PostgreSQL 9.4 -
pg_test_timing") / [9.3](/docs/9.3/pgtesttiming.html "PostgreSQL 9.3 -
pg_test_timing") / [9.2](/docs/9.2/pgtesttiming.html "PostgreSQL 9.2 -
pg_test_timing")

__

pg_test_timing  
---  
[Prev](pgtestfsync.html "pg_test_fsync")  | [Up](reference-server.html "PostgreSQL Server Applications") | PostgreSQL Server Applications | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pgupgrade.html "pg_upgrade")  
  
* * *

## pg_test_timing

pg_test_timing — measure timing overhead

## Synopsis

`pg_test_timing` [_`option`_...]

## Description

pg_test_timing is a tool to measure the timing overhead on your system and
confirm that the system time never moves backwards. Systems that are slow to
collect timing data can give less accurate `EXPLAIN ANALYZE` results.

## Options

pg_test_timing accepts the following command-line options:

`-d _`duration`_`  
`--duration=_`duration`_`

    

Specifies the test duration, in seconds. Longer durations give slightly better
accuracy, and are more likely to discover problems with the system clock
moving backwards. The default test duration is 3 seconds.

`-V`  
`--version`

    

Print the pg_test_timing version and exit.

`-?`  
`--help`

    

Show help about pg_test_timing command line arguments, and exit.

## Usage

### Interpreting Results

Good results will show most (>90%) individual timing calls take less than one
microsecond. Average per loop overhead will be even lower, below 100
nanoseconds. This example from an Intel i7-860 system using a TSC clock source
shows excellent performance:

    
    
    Testing timing overhead for 3 seconds.
    Per loop time including overhead: 35.96 ns
    Histogram of timing durations:
      < us   % of total      count
         1     96.40465   80435604
         2      3.59518    2999652
         4      0.00015        126
         8      0.00002         13
        16      0.00000          2
    

Note that different units are used for the per loop time than the histogram.
The loop can have resolution within a few nanoseconds (ns), while the
individual timing calls can only resolve down to one microsecond (us).

### Measuring Executor Timing Overhead

When the query executor is running a statement using `EXPLAIN ANALYZE`,
individual operations are timed as well as showing a summary. The overhead of
your system can be checked by counting rows with the psql program:

    
    
    CREATE TABLE t AS SELECT * FROM generate_series(1,100000);
    \timing
    SELECT COUNT(*) FROM t;
    EXPLAIN ANALYZE SELECT COUNT(*) FROM t;
    

The i7-860 system measured runs the count query in 9.8 ms while the `EXPLAIN
ANALYZE` version takes 16.6 ms, each processing just over 100,000 rows. That
6.8 ms difference means the timing overhead per row is 68 ns, about twice what
pg_test_timing estimated it would be. Even that relatively small amount of
overhead is making the fully timed count statement take almost 70% longer. On
more substantial queries, the timing overhead would be less problematic.

### Changing Time Sources

On some newer Linux systems, it's possible to change the clock source used to
collect timing data at any time. A second example shows the slowdown possible
from switching to the slower acpi_pm time source, on the same system used for
the fast results above:

    
    
    # cat /sys/devices/system/clocksource/clocksource0/available_clocksource
    tsc hpet acpi_pm
    # echo acpi_pm > /sys/devices/system/clocksource/clocksource0/current_clocksource
    # pg_test_timing
    Per loop time including overhead: 722.92 ns
    Histogram of timing durations:
      < us   % of total      count
         1     27.84870    1155682
         2     72.05956    2990371
         4      0.07810       3241
         8      0.01357        563
        16      0.00007          3
    

In this configuration, the sample `EXPLAIN ANALYZE` above takes 115.9 ms.
That's 1061 ns of timing overhead, again a small multiple of what's measured
directly by this utility. That much timing overhead means the actual query
itself is only taking a tiny fraction of the accounted for time, most of it is
being consumed in overhead instead. In this configuration, any `EXPLAIN
ANALYZE` totals involving many timed operations would be inflated
significantly by timing overhead.

FreeBSD also allows changing the time source on the fly, and it logs
information about the timer selected during boot:

    
    
    # dmesg | grep "Timecounter"
    Timecounter "ACPI-fast" frequency 3579545 Hz quality 900
    Timecounter "i8254" frequency 1193182 Hz quality 0
    Timecounters tick every 10.000 msec
    Timecounter "TSC" frequency 2531787134 Hz quality 800
    # sysctl kern.timecounter.hardware=TSC
    kern.timecounter.hardware: ACPI-fast -> TSC
    

Other systems may only allow setting the time source on boot. On older Linux
systems the "clock" kernel setting is the only way to make this sort of
change. And even on some more recent ones, the only option you'll see for a
clock source is "jiffies". Jiffies are the older Linux software clock
implementation, which can have good resolution when it's backed by fast enough
timing hardware, as in this example:

    
    
    $ cat /sys/devices/system/clocksource/clocksource0/available_clocksource
    jiffies
    $ dmesg | grep time.c
    time.c: Using 3.579545 MHz WALL PM GTOD PIT/TSC timer.
    time.c: Detected 2400.153 MHz processor.
    $ pg_test_timing
    Testing timing overhead for 3 seconds.
    Per timing duration including loop overhead: 97.75 ns
    Histogram of timing durations:
      < us   % of total      count
         1     90.23734   27694571
         2      9.75277    2993204
         4      0.00981       3010
         8      0.00007         22
        16      0.00000          1
        32      0.00000          1
    

### Clock Hardware and Timing Accuracy

Collecting accurate timing information is normally done on computers using
hardware clocks with various levels of accuracy. With some hardware the
operating systems can pass the system clock time almost directly to programs.
A system clock can also be derived from a chip that simply provides timing
interrupts, periodic ticks at some known time interval. In either case,
operating system kernels provide a clock source that hides these details. But
the accuracy of that clock source and how quickly it can return results varies
based on the underlying hardware.

Inaccurate time keeping can result in system instability. Test any change to
the clock source very carefully. Operating system defaults are sometimes made
to favor reliability over best accuracy. And if you are using a virtual
machine, look into the recommended time sources compatible with it. Virtual
hardware faces additional difficulties when emulating timers, and there are
often per operating system settings suggested by vendors.

The Time Stamp Counter (TSC) clock source is the most accurate one available
on current generation CPUs. It's the preferred way to track the system time
when it's supported by the operating system and the TSC clock is reliable.
There are several ways that TSC can fail to provide an accurate timing source,
making it unreliable. Older systems can have a TSC clock that varies based on
the CPU temperature, making it unusable for timing. Trying to use TSC on some
older multicore CPUs can give a reported time that's inconsistent among
multiple cores. This can result in the time going backwards, a problem this
program checks for. And even the newest systems can fail to provide accurate
TSC timing with very aggressive power saving configurations.

Newer operating systems may check for the known TSC problems and switch to a
slower, more stable clock source when they are seen. If your system supports
TSC time but doesn't default to that, it may be disabled for a good reason.
And some operating systems may not detect all the possible problems correctly,
or will allow using TSC even in situations where it's known to be inaccurate.

The High Precision Event Timer (HPET) is the preferred timer on systems where
it's available and TSC is not accurate. The timer chip itself is programmable
to allow up to 100 nanosecond resolution, but you may not see that much
accuracy in your system clock.

Advanced Configuration and Power Interface (ACPI) provides a Power Management
(PM) Timer, which Linux refers to as the acpi_pm. The clock derived from
acpi_pm will at best provide 300 nanosecond resolution.

Timers used on older PC hardware include the 8254 Programmable Interval Timer
(PIT), the real-time clock (RTC), the Advanced Programmable Interrupt
Controller (APIC) timer, and the Cyclone timer. These timers aim for
millisecond resolution.

## See Also

[EXPLAIN](sql-explain.html "EXPLAIN")

* * *

[Prev](pgtestfsync.html "pg_test_fsync")  | [Up](reference-server.html "PostgreSQL Server Applications") |  [Next](pgupgrade.html "pg_upgrade")  
---|---|---  
pg_test_fsync  | [Home](index.html "PostgreSQL 16.9 Documentation") |  pg_upgrade  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pgtesttiming.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

