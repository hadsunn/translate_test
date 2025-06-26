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

Supported Versions: [Current](/docs/current/ecpg-lo.html "PostgreSQL 17 -
36.12. Large Objects") ([17](/docs/17/ecpg-lo.html "PostgreSQL 17 -
36.12. Large Objects")) / [16](/docs/16/ecpg-lo.html "PostgreSQL 16 -
36.12. Large Objects") / [15](/docs/15/ecpg-lo.html "PostgreSQL 15 -
36.12. Large Objects") / [14](/docs/14/ecpg-lo.html "PostgreSQL 14 -
36.12. Large Objects") / [13](/docs/13/ecpg-lo.html "PostgreSQL 13 -
36.12. Large Objects")

Development Versions: [18](/docs/18/ecpg-lo.html "PostgreSQL 18 - 36.12. Large
Objects") / [devel](/docs/devel/ecpg-lo.html "PostgreSQL devel - 36.12. Large
Objects")

Unsupported versions: [12](/docs/12/ecpg-lo.html "PostgreSQL 12 - 36.12. Large
Objects") / [11](/docs/11/ecpg-lo.html "PostgreSQL 11 - 36.12. Large Objects")
/ [10](/docs/10/ecpg-lo.html "PostgreSQL 10 - 36.12. Large Objects") /
[9.6](/docs/9.6/ecpg-lo.html "PostgreSQL 9.6 - 36.12. Large Objects") /
[9.5](/docs/9.5/ecpg-lo.html "PostgreSQL 9.5 - 36.12. Large Objects") /
[9.4](/docs/9.4/ecpg-lo.html "PostgreSQL 9.4 - 36.12. Large Objects") /
[9.3](/docs/9.3/ecpg-lo.html "PostgreSQL 9.3 - 36.12. Large Objects") /
[9.2](/docs/9.2/ecpg-lo.html "PostgreSQL 9.2 - 36.12. Large Objects") /
[9.1](/docs/9.1/ecpg-lo.html "PostgreSQL 9.1 - 36.12. Large Objects")

__

36.12. Large Objects  
---  
[Prev](ecpg-library.html "36.11. Library Functions")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") | Chapter 36. ECPG — Embedded SQL in C | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](ecpg-cpp.html "36.13. C++ Applications")  
  
* * *

## 36.12. Large Objects #

Large objects are not directly supported by ECPG, but ECPG application can
manipulate large objects through the libpq large object functions, obtaining
the necessary `PGconn` object by calling the `ECPGget_PGconn()` function.
(However, use of the `ECPGget_PGconn()` function and touching `PGconn` objects
directly should be done very carefully and ideally not mixed with other ECPG
database access calls.)

For more details about the `ECPGget_PGconn()`, see [Section 36.11](ecpg-
library.html "36.11. Library Functions"). For information about the large
object function interface, see [Chapter 35](largeobjects.html
"Chapter 35. Large Objects").

Large object functions have to be called in a transaction block, so when
autocommit is off, `BEGIN` commands have to be issued explicitly.

[Example 36.2](ecpg-lo.html#ECPG-LO-EXAMPLE "Example 36.2. ECPG Program
Accessing Large Objects") shows an example program that illustrates how to
create, write, and read a large object in an ECPG application.

**Example  36.2. ECPG Program Accessing Large Objects**

    
    
    #include <stdio.h>
    #include <stdlib.h>
    #include <libpq-fe.h>
    #include <libpq/libpq-fs.h>
    
    EXEC SQL WHENEVER SQLERROR STOP;
    
    int
    main(void)
    {
        PGconn     *conn;
        Oid         loid;
        int         fd;
        char        buf[256];
        int         buflen = 256;
        char        buf2[256];
        int         rc;
    
        memset(buf, 1, buflen);
    
        EXEC SQL CONNECT TO testdb AS con1;
        EXEC SQL SELECT pg_catalog.set_config('search_path', '', false); EXEC SQL COMMIT;
    
        conn = ECPGget_PGconn("con1");
        printf("conn = %p\n", conn);
    
        /* create */
        loid = lo_create(conn, 0);
        if (loid &lt; 0)
            printf("lo_create() failed: %s", PQerrorMessage(conn));
    
        printf("loid = %d\n", loid);
    
        /* write test */
        fd = lo_open(conn, loid, INV_READ|INV_WRITE);
        if (fd &lt; 0)
            printf("lo_open() failed: %s", PQerrorMessage(conn));
    
        printf("fd = %d\n", fd);
    
        rc = lo_write(conn, fd, buf, buflen);
        if (rc &lt; 0)
            printf("lo_write() failed\n");
    
        rc = lo_close(conn, fd);
        if (rc &lt; 0)
            printf("lo_close() failed: %s", PQerrorMessage(conn));
    
        /* read test */
        fd = lo_open(conn, loid, INV_READ);
        if (fd &lt; 0)
            printf("lo_open() failed: %s", PQerrorMessage(conn));
    
        printf("fd = %d\n", fd);
    
        rc = lo_read(conn, fd, buf2, buflen);
        if (rc &lt; 0)
            printf("lo_read() failed\n");
    
        rc = lo_close(conn, fd);
        if (rc &lt; 0)
            printf("lo_close() failed: %s", PQerrorMessage(conn));
    
        /* check */
        rc = memcmp(buf, buf2, buflen);
        printf("memcmp() = %d\n", rc);
    
        /* cleanup */
        rc = lo_unlink(conn, loid);
        if (rc &lt; 0)
            printf("lo_unlink() failed: %s", PQerrorMessage(conn));
    
        EXEC SQL COMMIT;
        EXEC SQL DISCONNECT ALL;
        return 0;
    }
    

  

* * *

[Prev](ecpg-library.html "36.11. Library Functions")  | [Up](ecpg.html "Chapter 36. ECPG — Embedded SQL in C") |  [Next](ecpg-cpp.html "36.13. C++ Applications")  
---|---|---  
36.11. Library Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  36.13. C++ Applications  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/ecpg-lo.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

