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

Supported Versions: [Current](/docs/current/plpgsql-porting.html "PostgreSQL
17 - 43.13. Porting from Oracle PL/SQL") ([17](/docs/17/plpgsql-porting.html
"PostgreSQL 17 - 43.13. Porting from Oracle PL/SQL")) / [16](/docs/16/plpgsql-
porting.html "PostgreSQL 16 - 43.13. Porting from Oracle PL/SQL") /
[15](/docs/15/plpgsql-porting.html "PostgreSQL 15 - 43.13. Porting from Oracle
PL/SQL") / [14](/docs/14/plpgsql-porting.html "PostgreSQL 14 - 43.13. Porting
from Oracle PL/SQL") / [13](/docs/13/plpgsql-porting.html "PostgreSQL 13 -
43.13. Porting from Oracle PL/SQL")

Development Versions: [18](/docs/18/plpgsql-porting.html "PostgreSQL 18 -
43.13. Porting from Oracle PL/SQL") / [devel](/docs/devel/plpgsql-porting.html
"PostgreSQL devel - 43.13. Porting from Oracle PL/SQL")

Unsupported versions: [12](/docs/12/plpgsql-porting.html "PostgreSQL 12 -
43.13. Porting from Oracle PL/SQL") / [11](/docs/11/plpgsql-porting.html
"PostgreSQL 11 - 43.13. Porting from Oracle PL/SQL") / [10](/docs/10/plpgsql-
porting.html "PostgreSQL 10 - 43.13. Porting from Oracle PL/SQL") /
[9.6](/docs/9.6/plpgsql-porting.html "PostgreSQL 9.6 - 43.13. Porting from
Oracle PL/SQL") / [9.5](/docs/9.5/plpgsql-porting.html "PostgreSQL 9.5 -
43.13. Porting from Oracle PL/SQL") / [9.4](/docs/9.4/plpgsql-porting.html
"PostgreSQL 9.4 - 43.13. Porting from Oracle PL/SQL") /
[9.3](/docs/9.3/plpgsql-porting.html "PostgreSQL 9.3 - 43.13. Porting from
Oracle PL/SQL") / [9.2](/docs/9.2/plpgsql-porting.html "PostgreSQL 9.2 -
43.13. Porting from Oracle PL/SQL") / [9.1](/docs/9.1/plpgsql-porting.html
"PostgreSQL 9.1 - 43.13. Porting from Oracle PL/SQL") /
[9.0](/docs/9.0/plpgsql-porting.html "PostgreSQL 9.0 - 43.13. Porting from
Oracle PL/SQL") / [8.4](/docs/8.4/plpgsql-porting.html "PostgreSQL 8.4 -
43.13. Porting from Oracle PL/SQL") / [8.3](/docs/8.3/plpgsql-porting.html
"PostgreSQL 8.3 - 43.13. Porting from Oracle PL/SQL") /
[8.2](/docs/8.2/plpgsql-porting.html "PostgreSQL 8.2 - 43.13. Porting from
Oracle PL/SQL") / [8.1](/docs/8.1/plpgsql-porting.html "PostgreSQL 8.1 -
43.13. Porting from Oracle PL/SQL") / [8.0](/docs/8.0/plpgsql-porting.html
"PostgreSQL 8.0 - 43.13. Porting from Oracle PL/SQL") /
[7.4](/docs/7.4/plpgsql-porting.html "PostgreSQL 7.4 - 43.13. Porting from
Oracle PL/SQL") / [7.3](/docs/7.3/plpgsql-porting.html "PostgreSQL 7.3 -
43.13. Porting from Oracle PL/SQL") / [7.2](/docs/7.2/plpgsql-porting.html
"PostgreSQL 7.2 - 43.13. Porting from Oracle PL/SQL") /
[7.1](/docs/7.1/plpgsql-porting.html "PostgreSQL 7.1 - 43.13. Porting from
Oracle PL/SQL")

__

43.13. Porting from Oracle PL/SQL  
---  
[Prev](plpgsql-development-tips.html "43.12. Tips for Developing in PL/pgSQL")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") | Chapter 43. PL/pgSQL — SQL Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language")  
  
* * *

## 43.13. Porting from Oracle PL/SQL #

[43.13.1. Porting Examples](plpgsql-porting.html#PLPGSQL-PORTING-EXAMPLES)

[43.13.2. Other Things to Watch For](plpgsql-porting.html#PLPGSQL-PORTING-
OTHER)

[43.13.3. Appendix](plpgsql-porting.html#PLPGSQL-PORTING-APPENDIX)

This section explains differences between PostgreSQL's PL/pgSQL language and
Oracle's PL/SQL language, to help developers who port applications from
Oracle® to PostgreSQL.

PL/pgSQL is similar to PL/SQL in many aspects. It is a block-structured,
imperative language, and all variables have to be declared. Assignments,
loops, and conditionals are similar. The main differences you should keep in
mind when porting from PL/SQL to PL/pgSQL are:

  * If a name used in an SQL command could be either a column name of a table used in the command or a reference to a variable of the function, PL/SQL treats it as a column name. By default, PL/pgSQL will throw an error complaining that the name is ambiguous. You can specify `plpgsql.variable_conflict` = `use_column` to change this behavior to match PL/SQL, as explained in [Section 43.11.1](plpgsql-implementation.html#PLPGSQL-VAR-SUBST "43.11.1. Variable Substitution"). It's often best to avoid such ambiguities in the first place, but if you have to port a large amount of code that depends on this behavior, setting `variable_conflict` may be the best solution.

  * In PostgreSQL the function body must be written as a string literal. Therefore you need to use dollar quoting or escape single quotes in the function body. (See [Section 43.12.1](plpgsql-development-tips.html#PLPGSQL-QUOTE-TIPS "43.12.1. Handling of Quotation Marks").)

  * Data type names often need translation. For example, in Oracle string values are commonly declared as being of type `varchar2`, which is a non-SQL-standard type. In PostgreSQL, use type `varchar` or `text` instead. Similarly, replace type `number` with `numeric`, or use some other numeric data type if there's a more appropriate one.

  * Instead of packages, use schemas to organize your functions into groups.

  * Since there are no packages, there are no package-level variables either. This is somewhat annoying. You can keep per-session state in temporary tables instead.

  * Integer `FOR` loops with `REVERSE` work differently: PL/SQL counts down from the second number to the first, while PL/pgSQL counts down from the first number to the second, requiring the loop bounds to be swapped when porting. This incompatibility is unfortunate but is unlikely to be changed. (See [Section 43.6.5.5](plpgsql-control-structures.html#PLPGSQL-INTEGER-FOR "43.6.5.5. FOR \(Integer Variant\)").)

  * `FOR` loops over queries (other than cursors) also work differently: the target variable(s) must have been declared, whereas PL/SQL always declares them implicitly. An advantage of this is that the variable values are still accessible after the loop exits.

  * There are various notational differences for the use of cursor variables.

### 43.13.1. Porting Examples #

[Example 43.9](plpgsql-porting.html#PGSQL-PORTING-EX1 "Example 43.9. Porting a
Simple Function from PL/SQL to PL/pgSQL") shows how to port a simple function
from PL/SQL to PL/pgSQL.

**Example  43.9. Porting a Simple Function from PL/SQL to PL/pgSQL**

Here is an Oracle PL/SQL function:

    
    
    CREATE OR REPLACE FUNCTION cs_fmt_browser_version(v_name varchar2,
                                                      v_version varchar2)
    RETURN varchar2 IS
    BEGIN
        IF v_version IS NULL THEN
            RETURN v_name;
        END IF;
        RETURN v_name || '/' || v_version;
    END;
    /
    show errors;
    

Let's go through this function and see the differences compared to PL/pgSQL:

  * The type name `varchar2` has to be changed to `varchar` or `text`. In the examples in this section, we'll use `varchar`, but `text` is often a better choice if you do not need specific string length limits.

  * The `RETURN` key word in the function prototype (not the function body) becomes `RETURNS` in PostgreSQL. Also, `IS` becomes `AS`, and you need to add a `LANGUAGE` clause because PL/pgSQL is not the only possible function language.

  * In PostgreSQL, the function body is considered to be a string literal, so you need to use quote marks or dollar quotes around it. This substitutes for the terminating `/` in the Oracle approach.

  * The `show errors` command does not exist in PostgreSQL, and is not needed since errors are reported automatically.

This is how this function would look when ported to PostgreSQL:

    
    
    CREATE OR REPLACE FUNCTION cs_fmt_browser_version(v_name varchar,
                                                      v_version varchar)
    RETURNS varchar AS $$
    BEGIN
        IF v_version IS NULL THEN
            RETURN v_name;
        END IF;
        RETURN v_name || '/' || v_version;
    END;
    $$ LANGUAGE plpgsql;
    

  

[Example 43.10](plpgsql-porting.html#PLPGSQL-PORTING-EX2
"Example 43.10. Porting a Function that Creates Another Function from PL/SQL
to PL/pgSQL") shows how to port a function that creates another function and
how to handle the ensuing quoting problems.

**Example  43.10. Porting a Function that Creates Another Function from PL/SQL
to PL/pgSQL**

The following procedure grabs rows from a `SELECT` statement and builds a
large function with the results in `IF` statements, for the sake of
efficiency.

This is the Oracle version:

    
    
    CREATE OR REPLACE PROCEDURE cs_update_referrer_type_proc IS
        CURSOR referrer_keys IS
            SELECT * FROM cs_referrer_keys
            ORDER BY try_order;
        func_cmd VARCHAR(4000);
    BEGIN
        func_cmd := 'CREATE OR REPLACE FUNCTION cs_find_referrer_type(v_host IN VARCHAR2,
                     v_domain IN VARCHAR2, v_url IN VARCHAR2) RETURN VARCHAR2 IS BEGIN';
    
        FOR referrer_key IN referrer_keys LOOP
            func_cmd := func_cmd ||
              ' IF v_' || referrer_key.kind
              || ' LIKE ''' || referrer_key.key_string
              || ''' THEN RETURN ''' || referrer_key.referrer_type
              || '''; END IF;';
        END LOOP;
    
        func_cmd := func_cmd || ' RETURN NULL; END;';
    
        EXECUTE IMMEDIATE func_cmd;
    END;
    /
    show errors;
    

Here is how this function would end up in PostgreSQL:

    
    
    CREATE OR REPLACE PROCEDURE cs_update_referrer_type_proc() AS $func$
    DECLARE
        referrer_keys CURSOR IS
            SELECT * FROM cs_referrer_keys
            ORDER BY try_order;
        func_body text;
        func_cmd text;
    BEGIN
        func_body := 'BEGIN';
    
        FOR referrer_key IN referrer_keys LOOP
            func_body := func_body ||
              ' IF v_' || referrer_key.kind
              || ' LIKE ' || quote_literal(referrer_key.key_string)
              || ' THEN RETURN ' || quote_literal(referrer_key.referrer_type)
              || '; END IF;' ;
        END LOOP;
    
        func_body := func_body || ' RETURN NULL; END;';
    
        func_cmd :=
          'CREATE OR REPLACE FUNCTION cs_find_referrer_type(v_host varchar,
                                                            v_domain varchar,
                                                            v_url varchar)
            RETURNS varchar AS '
          || quote_literal(func_body)
          || ' LANGUAGE plpgsql;' ;
    
        EXECUTE func_cmd;
    END;
    $func$ LANGUAGE plpgsql;
    

Notice how the body of the function is built separately and passed through
`quote_literal` to double any quote marks in it. This technique is needed
because we cannot safely use dollar quoting for defining the new function: we
do not know for sure what strings will be interpolated from the
`referrer_key.key_string` field. (We are assuming here that
`referrer_key.kind` can be trusted to always be `host`, `domain`, or `url`,
but `referrer_key.key_string` might be anything, in particular it might
contain dollar signs.) This function is actually an improvement on the Oracle
original, because it will not generate broken code when
`referrer_key.key_string` or `referrer_key.referrer_type` contain quote marks.

  

[Example 43.11](plpgsql-porting.html#PLPGSQL-PORTING-EX3
"Example 43.11. Porting a Procedure With String Manipulation and OUT
Parameters from PL/SQL to PL/pgSQL") shows how to port a function with `OUT`
parameters and string manipulation. PostgreSQL does not have a built-in
`instr` function, but you can create one using a combination of other
functions. In [Section 43.13.3](plpgsql-porting.html#PLPGSQL-PORTING-APPENDIX
"43.13.3. Appendix") there is a PL/pgSQL implementation of `instr` that you
can use to make your porting easier.

**Example  43.11. Porting a Procedure With String Manipulation and `OUT`
Parameters from PL/SQL to PL/pgSQL**

The following Oracle PL/SQL procedure is used to parse a URL and return
several elements (host, path, and query).

This is the Oracle version:

    
    
    CREATE OR REPLACE PROCEDURE cs_parse_url(
        v_url IN VARCHAR2,
        v_host OUT VARCHAR2,  -- This will be passed back
        v_path OUT VARCHAR2,  -- This one too
        v_query OUT VARCHAR2) -- And this one
    IS
        a_pos1 INTEGER;
        a_pos2 INTEGER;
    BEGIN
        v_host := NULL;
        v_path := NULL;
        v_query := NULL;
        a_pos1 := instr(v_url, '//');
    
        IF a_pos1 = 0 THEN
            RETURN;
        END IF;
        a_pos2 := instr(v_url, '/', a_pos1 + 2);
        IF a_pos2 = 0 THEN
            v_host := substr(v_url, a_pos1 + 2);
            v_path := '/';
            RETURN;
        END IF;
    
        v_host := substr(v_url, a_pos1 + 2, a_pos2 - a_pos1 - 2);
        a_pos1 := instr(v_url, '?', a_pos2 + 1);
    
        IF a_pos1 = 0 THEN
            v_path := substr(v_url, a_pos2);
            RETURN;
        END IF;
    
        v_path := substr(v_url, a_pos2, a_pos1 - a_pos2);
        v_query := substr(v_url, a_pos1 + 1);
    END;
    /
    show errors;
    

Here is a possible translation into PL/pgSQL:

    
    
    CREATE OR REPLACE FUNCTION cs_parse_url(
        v_url IN VARCHAR,
        v_host OUT VARCHAR,  -- This will be passed back
        v_path OUT VARCHAR,  -- This one too
        v_query OUT VARCHAR) -- And this one
    AS $$
    DECLARE
        a_pos1 INTEGER;
        a_pos2 INTEGER;
    BEGIN
        v_host := NULL;
        v_path := NULL;
        v_query := NULL;
        a_pos1 := instr(v_url, '//');
    
        IF a_pos1 = 0 THEN
            RETURN;
        END IF;
        a_pos2 := instr(v_url, '/', a_pos1 + 2);
        IF a_pos2 = 0 THEN
            v_host := substr(v_url, a_pos1 + 2);
            v_path := '/';
            RETURN;
        END IF;
    
        v_host := substr(v_url, a_pos1 + 2, a_pos2 - a_pos1 - 2);
        a_pos1 := instr(v_url, '?', a_pos2 + 1);
    
        IF a_pos1 = 0 THEN
            v_path := substr(v_url, a_pos2);
            RETURN;
        END IF;
    
        v_path := substr(v_url, a_pos2, a_pos1 - a_pos2);
        v_query := substr(v_url, a_pos1 + 1);
    END;
    $$ LANGUAGE plpgsql;
    

This function could be used like this:

    
    
    SELECT * FROM cs_parse_url('http://foobar.com/query.cgi?baz');
    

  

[Example 43.12](plpgsql-porting.html#PLPGSQL-PORTING-EX4
"Example 43.12. Porting a Procedure from PL/SQL to PL/pgSQL") shows how to
port a procedure that uses numerous features that are specific to Oracle.

**Example  43.12. Porting a Procedure from PL/SQL to PL/pgSQL**

The Oracle version:

    
    
    CREATE OR REPLACE PROCEDURE cs_create_job(v_job_id IN INTEGER) IS
        a_running_job_count INTEGER;
    BEGIN
        LOCK TABLE cs_jobs IN EXCLUSIVE MODE;
    
        SELECT count(*) INTO a_running_job_count FROM cs_jobs WHERE end_stamp IS NULL;
    
        IF a_running_job_count > 0 THEN
            COMMIT; -- free lock
            raise_application_error(-20000,
                     'Unable to create a new job: a job is currently running.');
        END IF;
    
        DELETE FROM cs_active_job;
        INSERT INTO cs_active_job(job_id) VALUES (v_job_id);
    
        BEGIN
            INSERT INTO cs_jobs (job_id, start_stamp) VALUES (v_job_id, now());
        EXCEPTION
            WHEN dup_val_on_index THEN NULL; -- don't worry if it already exists
        END;
        COMMIT;
    END;
    /
    show errors
    

This is how we could port this procedure to PL/pgSQL:

    
    
    CREATE OR REPLACE PROCEDURE cs_create_job(v_job_id integer) AS $$
    DECLARE
        a_running_job_count integer;
    BEGIN
        LOCK TABLE cs_jobs IN EXCLUSIVE MODE;
    
        SELECT count(*) INTO a_running_job_count FROM cs_jobs WHERE end_stamp IS NULL;
    
        IF a_running_job_count > 0 THEN
            COMMIT; -- free lock
            RAISE EXCEPTION 'Unable to create a new job: a job is currently running'; -- (1)
        END IF;
    
        DELETE FROM cs_active_job;
        INSERT INTO cs_active_job(job_id) VALUES (v_job_id);
    
        BEGIN
            INSERT INTO cs_jobs (job_id, start_stamp) VALUES (v_job_id, now());
        EXCEPTION
            WHEN unique_violation THEN -- (2)
                -- don't worry if it already exists
        END;
        COMMIT;
    END;
    $$ LANGUAGE plpgsql;
    

(1) |  The syntax of `RAISE` is considerably different from Oracle's statement, although the basic case `RAISE` _`exception_name`_ works similarly.  
---|---  
(2) |  The exception names supported by PL/pgSQL are different from Oracle's. The set of built-in exception names is much larger (see [Appendix A](errcodes-appendix.html "Appendix A. PostgreSQL Error Codes")). There is not currently a way to declare user-defined exception names, although you can throw user-chosen SQLSTATE values instead.  
  
  

### 43.13.2. Other Things to Watch For #

This section explains a few other things to watch for when porting Oracle
PL/SQL functions to PostgreSQL.

#### 43.13.2.1. Implicit Rollback after Exceptions #

In PL/pgSQL, when an exception is caught by an `EXCEPTION` clause, all
database changes since the block's `BEGIN` are automatically rolled back. That
is, the behavior is equivalent to what you'd get in Oracle with:

    
    
    BEGIN
        SAVEPOINT s1;
        ... code here ...
    EXCEPTION
        WHEN ... THEN
            ROLLBACK TO s1;
            ... code here ...
        WHEN ... THEN
            ROLLBACK TO s1;
            ... code here ...
    END;
    

If you are translating an Oracle procedure that uses `SAVEPOINT` and `ROLLBACK
TO` in this style, your task is easy: just omit the `SAVEPOINT` and `ROLLBACK
TO`. If you have a procedure that uses `SAVEPOINT` and `ROLLBACK TO` in a
different way then some actual thought will be required.

#### 43.13.2.2. `EXECUTE` #

The PL/pgSQL version of `EXECUTE` works similarly to the PL/SQL version, but
you have to remember to use `quote_literal` and `quote_ident` as described in
[Section 43.5.4](plpgsql-statements.html#PLPGSQL-STATEMENTS-EXECUTING-DYN
"43.5.4. Executing Dynamic Commands"). Constructs of the type `EXECUTE 'SELECT
* FROM $1';` will not work reliably unless you use these functions.

#### 43.13.2.3. Optimizing PL/pgSQL Functions #

PostgreSQL gives you two function creation modifiers to optimize execution:
“volatility” (whether the function always returns the same result when given
the same arguments) and “strictness” (whether the function returns null if any
argument is null). Consult the [CREATE FUNCTION](sql-createfunction.html
"CREATE FUNCTION") reference page for details.

When making use of these optimization attributes, your `CREATE FUNCTION`
statement might look something like this:

    
    
    CREATE FUNCTION foo(...) RETURNS integer AS $$
    ...
    $$ LANGUAGE plpgsql STRICT IMMUTABLE;
    

### 43.13.3. Appendix #

This section contains the code for a set of Oracle-compatible `instr`
functions that you can use to simplify your porting efforts.

    
    
    --
    -- instr functions that mimic Oracle's counterpart
    -- Syntax: instr(string1, string2 [, n [, m]])
    -- where [] denotes optional parameters.
    --
    -- Search string1, beginning at the nth character, for the mth occurrence
    -- of string2.  If n is negative, search backwards, starting at the abs(n)'th
    -- character from the end of string1.
    -- If n is not passed, assume 1 (search starts at first character).
    -- If m is not passed, assume 1 (find first occurrence).
    -- Returns starting index of string2 in string1, or 0 if string2 is not found.
    --
    
    CREATE FUNCTION instr(varchar, varchar) RETURNS integer AS $$
    BEGIN
        RETURN instr($1, $2, 1);
    END;
    $$ LANGUAGE plpgsql STRICT IMMUTABLE;
    
    
    CREATE FUNCTION instr(string varchar, string_to_search_for varchar,
                          beg_index integer)
    RETURNS integer AS $$
    DECLARE
        pos integer NOT NULL DEFAULT 0;
        temp_str varchar;
        beg integer;
        length integer;
        ss_length integer;
    BEGIN
        IF beg_index > 0 THEN
            temp_str := substring(string FROM beg_index);
            pos := position(string_to_search_for IN temp_str);
    
            IF pos = 0 THEN
                RETURN 0;
            ELSE
                RETURN pos + beg_index - 1;
            END IF;
        ELSIF beg_index < 0 THEN
            ss_length := char_length(string_to_search_for);
            length := char_length(string);
            beg := length + 1 + beg_index;
    
            WHILE beg > 0 LOOP
                temp_str := substring(string FROM beg FOR ss_length);
                IF string_to_search_for = temp_str THEN
                    RETURN beg;
                END IF;
    
                beg := beg - 1;
            END LOOP;
    
            RETURN 0;
        ELSE
            RETURN 0;
        END IF;
    END;
    $$ LANGUAGE plpgsql STRICT IMMUTABLE;
    
    
    CREATE FUNCTION instr(string varchar, string_to_search_for varchar,
                          beg_index integer, occur_index integer)
    RETURNS integer AS $$
    DECLARE
        pos integer NOT NULL DEFAULT 0;
        occur_number integer NOT NULL DEFAULT 0;
        temp_str varchar;
        beg integer;
        i integer;
        length integer;
        ss_length integer;
    BEGIN
        IF occur_index <= 0 THEN
            RAISE 'argument ''%'' is out of range', occur_index
              USING ERRCODE = '22003';
        END IF;
    
        IF beg_index > 0 THEN
            beg := beg_index - 1;
            FOR i IN 1..occur_index LOOP
                temp_str := substring(string FROM beg + 1);
                pos := position(string_to_search_for IN temp_str);
                IF pos = 0 THEN
                    RETURN 0;
                END IF;
                beg := beg + pos;
            END LOOP;
    
            RETURN beg;
        ELSIF beg_index < 0 THEN
            ss_length := char_length(string_to_search_for);
            length := char_length(string);
            beg := length + 1 + beg_index;
    
            WHILE beg > 0 LOOP
                temp_str := substring(string FROM beg FOR ss_length);
                IF string_to_search_for = temp_str THEN
                    occur_number := occur_number + 1;
                    IF occur_number = occur_index THEN
                        RETURN beg;
                    END IF;
                END IF;
    
                beg := beg - 1;
            END LOOP;
    
            RETURN 0;
        ELSE
            RETURN 0;
        END IF;
    END;
    $$ LANGUAGE plpgsql STRICT IMMUTABLE;
    
    

* * *

[Prev](plpgsql-development-tips.html "43.12. Tips for Developing in PL/pgSQL")  | [Up](plpgsql.html "Chapter 43. PL/pgSQL — SQL Procedural Language") |  [Next](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language")  
---|---|---  
43.12. Tips for Developing in PL/pgSQL  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 44. PL/Tcl — Tcl Procedural Language  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/plpgsql-porting.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

