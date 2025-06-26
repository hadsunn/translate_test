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

Supported Versions: [Current](/docs/current/libpq-example.html "PostgreSQL 17
- 34.22. Example Programs") ([17](/docs/17/libpq-example.html "PostgreSQL 17 -
34.22. Example Programs")) / [16](/docs/16/libpq-example.html "PostgreSQL 16 -
34.22. Example Programs") / [15](/docs/15/libpq-example.html "PostgreSQL 15 -
34.22. Example Programs") / [14](/docs/14/libpq-example.html "PostgreSQL 14 -
34.22. Example Programs") / [13](/docs/13/libpq-example.html "PostgreSQL 13 -
34.22. Example Programs")

Development Versions: [18](/docs/18/libpq-example.html "PostgreSQL 18 -
34.22. Example Programs") / [devel](/docs/devel/libpq-example.html "PostgreSQL
devel - 34.22. Example Programs")

Unsupported versions: [12](/docs/12/libpq-example.html "PostgreSQL 12 -
34.22. Example Programs") / [11](/docs/11/libpq-example.html "PostgreSQL 11 -
34.22. Example Programs") / [10](/docs/10/libpq-example.html "PostgreSQL 10 -
34.22. Example Programs") / [9.6](/docs/9.6/libpq-example.html "PostgreSQL 9.6
- 34.22. Example Programs") / [9.5](/docs/9.5/libpq-example.html "PostgreSQL
9.5 - 34.22. Example Programs") / [9.4](/docs/9.4/libpq-example.html
"PostgreSQL 9.4 - 34.22. Example Programs") / [9.3](/docs/9.3/libpq-
example.html "PostgreSQL 9.3 - 34.22. Example Programs") /
[9.2](/docs/9.2/libpq-example.html "PostgreSQL 9.2 - 34.22. Example Programs")
/ [9.1](/docs/9.1/libpq-example.html "PostgreSQL 9.1 - 34.22. Example
Programs") / [9.0](/docs/9.0/libpq-example.html "PostgreSQL 9.0 -
34.22. Example Programs") / [8.4](/docs/8.4/libpq-example.html "PostgreSQL 8.4
- 34.22. Example Programs") / [8.3](/docs/8.3/libpq-example.html "PostgreSQL
8.3 - 34.22. Example Programs") / [8.2](/docs/8.2/libpq-example.html
"PostgreSQL 8.2 - 34.22. Example Programs") / [8.1](/docs/8.1/libpq-
example.html "PostgreSQL 8.1 - 34.22. Example Programs") /
[8.0](/docs/8.0/libpq-example.html "PostgreSQL 8.0 - 34.22. Example Programs")
/ [7.4](/docs/7.4/libpq-example.html "PostgreSQL 7.4 - 34.22. Example
Programs") / [7.3](/docs/7.3/libpq-example.html "PostgreSQL 7.3 -
34.22. Example Programs") / [7.2](/docs/7.2/libpq-example.html "PostgreSQL 7.2
- 34.22. Example Programs") / [7.1](/docs/7.1/libpq-example.html "PostgreSQL
7.1 - 34.22. Example Programs")

__

34.22. Example Programs  
---  
[Prev](libpq-build.html "34.21. Building libpq Programs")  | [Up](libpq.html "Chapter 34. libpq — C Library") | Chapter 34. libpq — C Library | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](largeobjects.html "Chapter 35. Large Objects")  
  
* * *

## 34.22. Example Programs #

These examples and others can be found in the directory `src/test/examples` in
the source code distribution.

**Example  34.1. libpq Example Program 1**

    
    
    
    /*
     * src/test/examples/testlibpq.c
     *
     *
     * testlibpq.c
     *
     *      Test the C version of libpq, the PostgreSQL frontend library.
     */
    #include <stdio.h>
    #include <stdlib.h>
    #include "libpq-fe.h"
    
    static void
    exit_nicely(PGconn *conn)
    {
        PQfinish(conn);
        exit(1);
    }
    
    int
    main(int argc, char **argv)
    {
        const char *conninfo;
        PGconn     *conn;
        PGresult   *res;
        int         nFields;
        int         i,
                    j;
    
        /*
         * If the user supplies a parameter on the command line, use it as the
         * conninfo string; otherwise default to setting dbname=postgres and using
         * environment variables or defaults for all other connection parameters.
         */
        if (argc > 1)
            conninfo = argv[1];
        else
            conninfo = "dbname = postgres";
    
        /* Make a connection to the database */
        conn = PQconnectdb(conninfo);
    
        /* Check to see that the backend connection was successfully made */
        if (PQstatus(conn) != CONNECTION_OK)
        {
            fprintf(stderr, "%s", PQerrorMessage(conn));
            exit_nicely(conn);
        }
    
        /* Set always-secure search path, so malicious users can't take control. */
        res = PQexec(conn,
                     "SELECT pg_catalog.set_config('search_path', '', false)");
        if (PQresultStatus(res) != PGRES_TUPLES_OK)
        {
            fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
            PQclear(res);
            exit_nicely(conn);
        }
    
        /*
         * Should PQclear PGresult whenever it is no longer needed to avoid memory
         * leaks
         */
        PQclear(res);
    
        /*
         * Our test case here involves using a cursor, for which we must be inside
         * a transaction block.  We could do the whole thing with a single
         * PQexec() of "select * from pg_database", but that's too trivial to make
         * a good example.
         */
    
        /* Start a transaction block */
        res = PQexec(conn, "BEGIN");
        if (PQresultStatus(res) != PGRES_COMMAND_OK)
        {
            fprintf(stderr, "BEGIN command failed: %s", PQerrorMessage(conn));
            PQclear(res);
            exit_nicely(conn);
        }
        PQclear(res);
    
        /*
         * Fetch rows from pg_database, the system catalog of databases
         */
        res = PQexec(conn, "DECLARE myportal CURSOR FOR select * from pg_database");
        if (PQresultStatus(res) != PGRES_COMMAND_OK)
        {
            fprintf(stderr, "DECLARE CURSOR failed: %s", PQerrorMessage(conn));
            PQclear(res);
            exit_nicely(conn);
        }
        PQclear(res);
    
        res = PQexec(conn, "FETCH ALL in myportal");
        if (PQresultStatus(res) != PGRES_TUPLES_OK)
        {
            fprintf(stderr, "FETCH ALL failed: %s", PQerrorMessage(conn));
            PQclear(res);
            exit_nicely(conn);
        }
    
        /* first, print out the attribute names */
        nFields = PQnfields(res);
        for (i = 0; i < nFields; i++)
            printf("%-15s", PQfname(res, i));
        printf("\n\n");
    
        /* next, print out the rows */
        for (i = 0; i < PQntuples(res); i++)
        {
            for (j = 0; j < nFields; j++)
                printf("%-15s", PQgetvalue(res, i, j));
            printf("\n");
        }
    
        PQclear(res);
    
        /* close the portal ... we don't bother to check for errors ... */
        res = PQexec(conn, "CLOSE myportal");
        PQclear(res);
    
        /* end the transaction */
        res = PQexec(conn, "END");
        PQclear(res);
    
        /* close the connection to the database and cleanup */
        PQfinish(conn);
    
        return 0;
    }
    
    

  

**Example  34.2. libpq Example Program 2**

    
    
    
    /*
     * src/test/examples/testlibpq2.c
     *
     *
     * testlibpq2.c
     *      Test of the asynchronous notification interface
     *
     * Start this program, then from psql in another window do
     *   NOTIFY TBL2;
     * Repeat four times to get this program to exit.
     *
     * Or, if you want to get fancy, try this:
     * populate a database with the following commands
     * (provided in src/test/examples/testlibpq2.sql):
     *
     *   CREATE SCHEMA TESTLIBPQ2;
     *   SET search_path = TESTLIBPQ2;
     *   CREATE TABLE TBL1 (i int4);
     *   CREATE TABLE TBL2 (i int4);
     *   CREATE RULE r1 AS ON INSERT TO TBL1 DO
     *     (INSERT INTO TBL2 VALUES (new.i); NOTIFY TBL2);
     *
     * Start this program, then from psql do this four times:
     *
     *   INSERT INTO TESTLIBPQ2.TBL1 VALUES (10);
     */
    
    #ifdef WIN32
    #include <windows.h>
    #endif
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    #include <errno.h>
    #include <sys/select.h>
    #include <sys/time.h>
    #include <sys/types.h>
    
    #include "libpq-fe.h"
    
    static void
    exit_nicely(PGconn *conn)
    {
        PQfinish(conn);
        exit(1);
    }
    
    int
    main(int argc, char **argv)
    {
        const char *conninfo;
        PGconn     *conn;
        PGresult   *res;
        PGnotify   *notify;
        int         nnotifies;
    
        /*
         * If the user supplies a parameter on the command line, use it as the
         * conninfo string; otherwise default to setting dbname=postgres and using
         * environment variables or defaults for all other connection parameters.
         */
        if (argc > 1)
            conninfo = argv[1];
        else
            conninfo = "dbname = postgres";
    
        /* Make a connection to the database */
        conn = PQconnectdb(conninfo);
    
        /* Check to see that the backend connection was successfully made */
        if (PQstatus(conn) != CONNECTION_OK)
        {
            fprintf(stderr, "%s", PQerrorMessage(conn));
            exit_nicely(conn);
        }
    
        /* Set always-secure search path, so malicious users can't take control. */
        res = PQexec(conn,
                     "SELECT pg_catalog.set_config('search_path', '', false)");
        if (PQresultStatus(res) != PGRES_TUPLES_OK)
        {
            fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
            PQclear(res);
            exit_nicely(conn);
        }
    
        /*
         * Should PQclear PGresult whenever it is no longer needed to avoid memory
         * leaks
         */
        PQclear(res);
    
        /*
         * Issue LISTEN command to enable notifications from the rule's NOTIFY.
         */
        res = PQexec(conn, "LISTEN TBL2");
        if (PQresultStatus(res) != PGRES_COMMAND_OK)
        {
            fprintf(stderr, "LISTEN command failed: %s", PQerrorMessage(conn));
            PQclear(res);
            exit_nicely(conn);
        }
        PQclear(res);
    
        /* Quit after four notifies are received. */
        nnotifies = 0;
        while (nnotifies < 4)
        {
            /*
             * Sleep until something happens on the connection.  We use select(2)
             * to wait for input, but you could also use poll() or similar
             * facilities.
             */
            int         sock;
            fd_set      input_mask;
    
            sock = PQsocket(conn);
    
            if (sock < 0)
                break;              /* shouldn't happen */
    
            FD_ZERO(&input_mask);
            FD_SET(sock, &input_mask);
    
            if (select(sock + 1, &input_mask, NULL, NULL, NULL) < 0)
            {
                fprintf(stderr, "select() failed: %s\n", strerror(errno));
                exit_nicely(conn);
            }
    
            /* Now check for input */
            PQconsumeInput(conn);
            while ((notify = PQnotifies(conn)) != NULL)
            {
                fprintf(stderr,
                        "ASYNC NOTIFY of '%s' received from backend PID %d\n",
                        notify->relname, notify->be_pid);
                PQfreemem(notify);
                nnotifies++;
                PQconsumeInput(conn);
            }
        }
    
        fprintf(stderr, "Done.\n");
    
        /* close the connection to the database and cleanup */
        PQfinish(conn);
    
        return 0;
    }
    
    

  

**Example  34.3. libpq Example Program 3**

    
    
    
    /*
     * src/test/examples/testlibpq3.c
     *
     *
     * testlibpq3.c
     *      Test out-of-line parameters and binary I/O.
     *
     * Before running this, populate a database with the following commands
     * (provided in src/test/examples/testlibpq3.sql):
     *
     * CREATE SCHEMA testlibpq3;
     * SET search_path = testlibpq3;
     * SET standard_conforming_strings = ON;
     * CREATE TABLE test1 (i int4, t text, b bytea);
     * INSERT INTO test1 values (1, 'joe''s place', '\000\001\002\003\004');
     * INSERT INTO test1 values (2, 'ho there', '\004\003\002\001\000');
     *
     * The expected output is:
     *
     * tuple 0: got
     *  i = (4 bytes) 1
     *  t = (11 bytes) 'joe's place'
     *  b = (5 bytes) \000\001\002\003\004
     *
     * tuple 0: got
     *  i = (4 bytes) 2
     *  t = (8 bytes) 'ho there'
     *  b = (5 bytes) \004\003\002\001\000
     */
    
    #ifdef WIN32
    #include <windows.h>
    #endif
    
    #include <stdio.h>
    #include <stdlib.h>
    #include <stdint.h>
    #include <string.h>
    #include <sys/types.h>
    #include "libpq-fe.h"
    
    /* for ntohl/htonl */
    #include <netinet/in.h>
    #include <arpa/inet.h>
    
    
    static void
    exit_nicely(PGconn *conn)
    {
        PQfinish(conn);
        exit(1);
    }
    
    /*
     * This function prints a query result that is a binary-format fetch from
     * a table defined as in the comment above.  We split it out because the
     * main() function uses it twice.
     */
    static void
    show_binary_results(PGresult *res)
    {
        int         i,
                    j;
        int         i_fnum,
                    t_fnum,
                    b_fnum;
    
        /* Use PQfnumber to avoid assumptions about field order in result */
        i_fnum = PQfnumber(res, "i");
        t_fnum = PQfnumber(res, "t");
        b_fnum = PQfnumber(res, "b");
    
        for (i = 0; i < PQntuples(res); i++)
        {
            char       *iptr;
            char       *tptr;
            char       *bptr;
            int         blen;
            int         ival;
    
            /* Get the field values (we ignore possibility they are null!) */
            iptr = PQgetvalue(res, i, i_fnum);
            tptr = PQgetvalue(res, i, t_fnum);
            bptr = PQgetvalue(res, i, b_fnum);
    
            /*
             * The binary representation of INT4 is in network byte order, which
             * we'd better coerce to the local byte order.
             */
            ival = ntohl(*((uint32_t *) iptr));
    
            /*
             * The binary representation of TEXT is, well, text, and since libpq
             * was nice enough to append a zero byte to it, it'll work just fine
             * as a C string.
             *
             * The binary representation of BYTEA is a bunch of bytes, which could
             * include embedded nulls so we have to pay attention to field length.
             */
            blen = PQgetlength(res, i, b_fnum);
    
            printf("tuple %d: got\n", i);
            printf(" i = (%d bytes) %d\n",
                   PQgetlength(res, i, i_fnum), ival);
            printf(" t = (%d bytes) '%s'\n",
                   PQgetlength(res, i, t_fnum), tptr);
            printf(" b = (%d bytes) ", blen);
            for (j = 0; j < blen; j++)
                printf("\\%03o", bptr[j]);
            printf("\n\n");
        }
    }
    
    int
    main(int argc, char **argv)
    {
        const char *conninfo;
        PGconn     *conn;
        PGresult   *res;
        const char *paramValues[1];
        int         paramLengths[1];
        int         paramFormats[1];
        uint32_t    binaryIntVal;
    
        /*
         * If the user supplies a parameter on the command line, use it as the
         * conninfo string; otherwise default to setting dbname=postgres and using
         * environment variables or defaults for all other connection parameters.
         */
        if (argc > 1)
            conninfo = argv[1];
        else
            conninfo = "dbname = postgres";
    
        /* Make a connection to the database */
        conn = PQconnectdb(conninfo);
    
        /* Check to see that the backend connection was successfully made */
        if (PQstatus(conn) != CONNECTION_OK)
        {
            fprintf(stderr, "%s", PQerrorMessage(conn));
            exit_nicely(conn);
        }
    
        /* Set always-secure search path, so malicious users can't take control. */
        res = PQexec(conn, "SET search_path = testlibpq3");
        if (PQresultStatus(res) != PGRES_COMMAND_OK)
        {
            fprintf(stderr, "SET failed: %s", PQerrorMessage(conn));
            PQclear(res);
            exit_nicely(conn);
        }
        PQclear(res);
    
        /*
         * The point of this program is to illustrate use of PQexecParams() with
         * out-of-line parameters, as well as binary transmission of data.
         *
         * This first example transmits the parameters as text, but receives the
         * results in binary format.  By using out-of-line parameters we can avoid
         * a lot of tedious mucking about with quoting and escaping, even though
         * the data is text.  Notice how we don't have to do anything special with
         * the quote mark in the parameter value.
         */
    
        /* Here is our out-of-line parameter value */
        paramValues[0] = "joe's place";
    
        res = PQexecParams(conn,
                           "SELECT * FROM test1 WHERE t = $1",
                           1,       /* one param */
                           NULL,    /* let the backend deduce param type */
                           paramValues,
                           NULL,    /* don't need param lengths since text */
                           NULL,    /* default to all text params */
                           1);      /* ask for binary results */
    
        if (PQresultStatus(res) != PGRES_TUPLES_OK)
        {
            fprintf(stderr, "SELECT failed: %s", PQerrorMessage(conn));
            PQclear(res);
            exit_nicely(conn);
        }
    
        show_binary_results(res);
    
        PQclear(res);
    
        /*
         * In this second example we transmit an integer parameter in binary form,
         * and again retrieve the results in binary form.
         *
         * Although we tell PQexecParams we are letting the backend deduce
         * parameter type, we really force the decision by casting the parameter
         * symbol in the query text.  This is a good safety measure when sending
         * binary parameters.
         */
    
        /* Convert integer value "2" to network byte order */
        binaryIntVal = htonl((uint32_t) 2);
    
        /* Set up parameter arrays for PQexecParams */
        paramValues[0] = (char *) &binaryIntVal;
        paramLengths[0] = sizeof(binaryIntVal);
        paramFormats[0] = 1;        /* binary */
    
        res = PQexecParams(conn,
                           "SELECT * FROM test1 WHERE i = $1::int4",
                           1,       /* one param */
                           NULL,    /* let the backend deduce param type */
                           paramValues,
                           paramLengths,
                           paramFormats,
                           1);      /* ask for binary results */
    
        if (PQresultStatus(res) != PGRES_TUPLES_OK)
        {
            fprintf(stderr, "SELECT failed: %s", PQerrorMessage(conn));
            PQclear(res);
            exit_nicely(conn);
        }
    
        show_binary_results(res);
    
        PQclear(res);
    
        /* close the connection to the database and cleanup */
        PQfinish(conn);
    
        return 0;
    }
    
    

  

* * *

[Prev](libpq-build.html "34.21. Building libpq Programs")  | [Up](libpq.html "Chapter 34. libpq — C Library") |  [Next](largeobjects.html "Chapter 35. Large Objects")  
---|---|---  
34.21. Building libpq Programs  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 35. Large Objects  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/libpq-example.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

