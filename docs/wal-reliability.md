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

Supported Versions: [Current](/docs/current/wal-reliability.html "PostgreSQL
17 - 30.1. Reliability") ([17](/docs/17/wal-reliability.html "PostgreSQL 17 -
30.1. Reliability")) / [16](/docs/16/wal-reliability.html "PostgreSQL 16 -
30.1. Reliability") / [15](/docs/15/wal-reliability.html "PostgreSQL 15 -
30.1. Reliability") / [14](/docs/14/wal-reliability.html "PostgreSQL 14 -
30.1. Reliability") / [13](/docs/13/wal-reliability.html "PostgreSQL 13 -
30.1. Reliability")

Development Versions: [18](/docs/18/wal-reliability.html "PostgreSQL 18 -
30.1. Reliability") / [devel](/docs/devel/wal-reliability.html "PostgreSQL
devel - 30.1. Reliability")

Unsupported versions: [12](/docs/12/wal-reliability.html "PostgreSQL 12 -
30.1. Reliability") / [11](/docs/11/wal-reliability.html "PostgreSQL 11 -
30.1. Reliability") / [10](/docs/10/wal-reliability.html "PostgreSQL 10 -
30.1. Reliability") / [9.6](/docs/9.6/wal-reliability.html "PostgreSQL 9.6 -
30.1. Reliability") / [9.5](/docs/9.5/wal-reliability.html "PostgreSQL 9.5 -
30.1. Reliability") / [9.4](/docs/9.4/wal-reliability.html "PostgreSQL 9.4 -
30.1. Reliability") / [9.3](/docs/9.3/wal-reliability.html "PostgreSQL 9.3 -
30.1. Reliability") / [9.2](/docs/9.2/wal-reliability.html "PostgreSQL 9.2 -
30.1. Reliability") / [9.1](/docs/9.1/wal-reliability.html "PostgreSQL 9.1 -
30.1. Reliability") / [9.0](/docs/9.0/wal-reliability.html "PostgreSQL 9.0 -
30.1. Reliability") / [8.4](/docs/8.4/wal-reliability.html "PostgreSQL 8.4 -
30.1. Reliability") / [8.3](/docs/8.3/wal-reliability.html "PostgreSQL 8.3 -
30.1. Reliability") / [8.2](/docs/8.2/wal-reliability.html "PostgreSQL 8.2 -
30.1. Reliability")

__

30.1. Reliability  
---  
[Prev](wal.html "Chapter 30. Reliability and the Write-Ahead Log")  | [Up](wal.html "Chapter 30. Reliability and the Write-Ahead Log") | Chapter 30. Reliability and the Write-Ahead Log | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](checksums.html "30.2. Data Checksums")  
  
* * *

## 30.1. Reliability #

Reliability is an important property of any serious database system, and
PostgreSQL does everything possible to guarantee reliable operation. One
aspect of reliable operation is that all data recorded by a committed
transaction should be stored in a nonvolatile area that is safe from power
loss, operating system failure, and hardware failure (except failure of the
nonvolatile area itself, of course). Successfully writing the data to the
computer's permanent storage (disk drive or equivalent) ordinarily meets this
requirement. In fact, even if a computer is fatally damaged, if the disk
drives survive they can be moved to another computer with similar hardware and
all committed transactions will remain intact.

While forcing data to the disk platters periodically might seem like a simple
operation, it is not. Because disk drives are dramatically slower than main
memory and CPUs, several layers of caching exist between the computer's main
memory and the disk platters. First, there is the operating system's buffer
cache, which caches frequently requested disk blocks and combines disk writes.
Fortunately, all operating systems give applications a way to force writes
from the buffer cache to disk, and PostgreSQL uses those features. (See the
[wal_sync_method](runtime-config-wal.html#GUC-WAL-SYNC-METHOD) parameter to
adjust how this is done.)

Next, there might be a cache in the disk drive controller; this is
particularly common on RAID controller cards. Some of these caches are _write-
through_ , meaning writes are sent to the drive as soon as they arrive. Others
are _write-back_ , meaning data is sent to the drive at some later time. Such
caches can be a reliability hazard because the memory in the disk controller
cache is volatile, and will lose its contents in a power failure. Better
controller cards have _battery-backup units_ (BBUs), meaning the card has a
battery that maintains power to the cache in case of system power loss. After
power is restored the data will be written to the disk drives.

And finally, most disk drives have caches. Some are write-through while some
are write-back, and the same concerns about data loss exist for write-back
drive caches as for disk controller caches. Consumer-grade IDE and SATA drives
are particularly likely to have write-back caches that will not survive a
power failure. Many solid-state drives (SSD) also have volatile write-back
caches.

These caches can typically be disabled; however, the method for doing this
varies by operating system and drive type:

  * On Linux, IDE and SATA drives can be queried using `hdparm -I`; write caching is enabled if there is a `*` next to `Write cache`. `hdparm -W 0` can be used to turn off write caching. SCSI drives can be queried using [sdparm](http://sg.danny.cz/sg/sdparm.html). Use `sdparm --get=WCE` to check whether the write cache is enabled and `sdparm --clear=WCE` to disable it.

  * On FreeBSD, IDE drives can be queried using `camcontrol identify` and write caching turned off using `hw.ata.wc=0` in `/boot/loader.conf`; SCSI drives can be queried using `camcontrol identify`, and the write cache both queried and changed using `sdparm` when available.

  * On Solaris, the disk write cache is controlled by `format -e`. (The Solaris ZFS file system is safe with disk write-cache enabled because it issues its own disk cache flush commands.)

  * On Windows, if `wal_sync_method` is `open_datasync` (the default), write caching can be disabled by unchecking `My Computer\Open\_`disk drive`_ \Properties\Hardware\Properties\Policies\Enable write caching on the disk`. Alternatively, set `wal_sync_method` to `fdatasync` (NTFS only), `fsync` or `fsync_writethrough`, which prevent write caching.

  * On macOS, write caching can be prevented by setting `wal_sync_method` to `fsync_writethrough`.

Recent SATA drives (those following ATAPI-6 or later) offer a drive cache
flush command (`FLUSH CACHE EXT`), while SCSI drives have long supported a
similar command `SYNCHRONIZE CACHE`. These commands are not directly
accessible to PostgreSQL, but some file systems (e.g., ZFS, ext4) can use them
to flush data to the platters on write-back-enabled drives. Unfortunately,
such file systems behave suboptimally when combined with battery-backup unit
(BBU) disk controllers. In such setups, the synchronize command forces all
data from the controller cache to the disks, eliminating much of the benefit
of the BBU. You can run the [pg_test_fsync](pgtestfsync.html "pg_test_fsync")
program to see if you are affected. If you are affected, the performance
benefits of the BBU can be regained by turning off write barriers in the file
system or reconfiguring the disk controller, if that is an option. If write
barriers are turned off, make sure the battery remains functional; a faulty
battery can potentially lead to data loss. Hopefully file system and disk
controller designers will eventually address this suboptimal behavior.

When the operating system sends a write request to the storage hardware, there
is little it can do to make sure the data has arrived at a truly non-volatile
storage area. Rather, it is the administrator's responsibility to make certain
that all storage components ensure integrity for both data and file-system
metadata. Avoid disk controllers that have non-battery-backed write caches. At
the drive level, disable write-back caching if the drive cannot guarantee the
data will be written before shutdown. If you use SSDs, be aware that many of
these do not honor cache flush commands by default. You can test for reliable
I/O subsystem behavior using
[`diskchecker.pl`](https://brad.livejournal.com/2116715.html).

Another risk of data loss is posed by the disk platter write operations
themselves. Disk platters are divided into sectors, commonly 512 bytes each.
Every physical read or write operation processes a whole sector. When a write
request arrives at the drive, it might be for some multiple of 512 bytes
(PostgreSQL typically writes 8192 bytes, or 16 sectors, at a time), and the
process of writing could fail due to power loss at any time, meaning some of
the 512-byte sectors were written while others were not. To guard against such
failures, PostgreSQL periodically writes full page images to permanent WAL
storage _before_ modifying the actual page on disk. By doing this, during
crash recovery PostgreSQL can restore partially-written pages from WAL. If you
have file-system software that prevents partial page writes (e.g., ZFS), you
can turn off this page imaging by turning off the [full_page_writes](runtime-
config-wal.html#GUC-FULL-PAGE-WRITES) parameter. Battery-Backed Unit (BBU)
disk controllers do not prevent partial page writes unless they guarantee that
data is written to the BBU as full (8kB) pages.

PostgreSQL also protects against some kinds of data corruption on storage
devices that may occur because of hardware errors or media failure over time,
such as reading/writing garbage data.

  * Each individual record in a WAL file is protected by a CRC-32C (32-bit) check that allows us to tell if record contents are correct. The CRC value is set when we write each WAL record and checked during crash recovery, archive recovery and replication.

  * Data pages are not currently checksummed by default, though full page images recorded in WAL records will be protected; see [initdb](app-initdb.html#APP-INITDB-DATA-CHECKSUMS) for details about enabling data checksums.

  * Internal data structures such as `pg_xact`, `pg_subtrans`, `pg_multixact`, `pg_serial`, `pg_notify`, `pg_stat`, `pg_snapshots` are not directly checksummed, nor are pages protected by full page writes. However, where such data structures are persistent, WAL records are written that allow recent changes to be accurately rebuilt at crash recovery and those WAL records are protected as discussed above.

  * Individual state files in `pg_twophase` are protected by CRC-32C.

  * Temporary data files used in larger SQL queries for sorts, materializations and intermediate results are not currently checksummed, nor will WAL records be written for changes to those files.

PostgreSQL does not protect against correctable memory errors and it is
assumed you will operate using RAM that uses industry standard Error
Correcting Codes (ECC) or better protection.

* * *

[Prev](wal.html "Chapter 30. Reliability and the Write-Ahead Log")  | [Up](wal.html "Chapter 30. Reliability and the Write-Ahead Log") |  [Next](checksums.html "30.2. Data Checksums")  
---|---|---  
Chapter 30. Reliability and the Write-Ahead Log  | [Home](index.html "PostgreSQL 16.9 Documentation") |  30.2. Data Checksums  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/wal-reliability.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

