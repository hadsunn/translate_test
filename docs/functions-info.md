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

Supported Versions: [Current](/docs/current/functions-info.html "PostgreSQL 17
- 9.26. System Information Functions and Operators") ([17](/docs/17/functions-
info.html "PostgreSQL 17 - 9.26. System Information Functions and Operators"))
/ [16](/docs/16/functions-info.html "PostgreSQL 16 - 9.26. System Information
Functions and Operators") / [15](/docs/15/functions-info.html "PostgreSQL 15 -
9.26. System Information Functions and Operators") / [14](/docs/14/functions-
info.html "PostgreSQL 14 - 9.26. System Information Functions and Operators")
/ [13](/docs/13/functions-info.html "PostgreSQL 13 - 9.26. System Information
Functions and Operators")

Development Versions: [18](/docs/18/functions-info.html "PostgreSQL 18 -
9.26. System Information Functions and Operators") /
[devel](/docs/devel/functions-info.html "PostgreSQL devel - 9.26. System
Information Functions and Operators")

Unsupported versions: [12](/docs/12/functions-info.html "PostgreSQL 12 -
9.26. System Information Functions and Operators") / [11](/docs/11/functions-
info.html "PostgreSQL 11 - 9.26. System Information Functions and Operators")
/ [10](/docs/10/functions-info.html "PostgreSQL 10 - 9.26. System Information
Functions and Operators") / [9.6](/docs/9.6/functions-info.html "PostgreSQL
9.6 - 9.26. System Information Functions and Operators") /
[9.5](/docs/9.5/functions-info.html "PostgreSQL 9.5 - 9.26. System Information
Functions and Operators") / [9.4](/docs/9.4/functions-info.html "PostgreSQL
9.4 - 9.26. System Information Functions and Operators") /
[9.3](/docs/9.3/functions-info.html "PostgreSQL 9.3 - 9.26. System Information
Functions and Operators") / [9.2](/docs/9.2/functions-info.html "PostgreSQL
9.2 - 9.26. System Information Functions and Operators") /
[9.1](/docs/9.1/functions-info.html "PostgreSQL 9.1 - 9.26. System Information
Functions and Operators") / [9.0](/docs/9.0/functions-info.html "PostgreSQL
9.0 - 9.26. System Information Functions and Operators") /
[8.4](/docs/8.4/functions-info.html "PostgreSQL 8.4 - 9.26. System Information
Functions and Operators") / [8.3](/docs/8.3/functions-info.html "PostgreSQL
8.3 - 9.26. System Information Functions and Operators") /
[8.2](/docs/8.2/functions-info.html "PostgreSQL 8.2 - 9.26. System Information
Functions and Operators") / [8.1](/docs/8.1/functions-info.html "PostgreSQL
8.1 - 9.26. System Information Functions and Operators") /
[8.0](/docs/8.0/functions-info.html "PostgreSQL 8.0 - 9.26. System Information
Functions and Operators")

__

9.26. System Information Functions and Operators  
---  
[Prev](functions-srf.html "9.25. Set Returning Functions")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions-admin.html "9.27. System Administration Functions")  
  
* * *

## 9.26. System Information Functions and Operators #

[9.26.1. Session Information Functions](functions-info.html#FUNCTIONS-INFO-
SESSION)

[9.26.2. Access Privilege Inquiry Functions](functions-info.html#FUNCTIONS-
INFO-ACCESS)

[9.26.3. Schema Visibility Inquiry Functions](functions-info.html#FUNCTIONS-
INFO-SCHEMA)

[9.26.4. System Catalog Information Functions](functions-info.html#FUNCTIONS-
INFO-CATALOG)

[9.26.5. Object Information and Addressing Functions](functions-
info.html#FUNCTIONS-INFO-OBJECT)

[9.26.6. Comment Information Functions](functions-info.html#FUNCTIONS-INFO-
COMMENT)

[9.26.7. Data Validity Checking Functions](functions-info.html#FUNCTIONS-INFO-
VALIDITY)

[9.26.8. Transaction ID and Snapshot Information Functions](functions-
info.html#FUNCTIONS-INFO-SNAPSHOT)

[9.26.9. Committed Transaction Information Functions](functions-
info.html#FUNCTIONS-INFO-COMMIT-TIMESTAMP)

[9.26.10. Control Data Functions](functions-info.html#FUNCTIONS-INFO-
CONTROLDATA)

The functions described in this section are used to obtain various information
about a PostgreSQL installation.

### 9.26.1. Session Information Functions #

[Table 9.67](functions-info.html#FUNCTIONS-INFO-SESSION-TABLE
"Table 9.67. Session Information Functions") shows several functions that
extract session and system information.

In addition to the functions listed in this section, there are a number of
functions related to the statistics system that also provide system
information. See [Section 28.2.25](monitoring-stats.html#MONITORING-STATS-
FUNCTIONS "28.2.25. Statistics Functions") for more information.

**Table  9.67. Session Information Functions**

Function Description  
---  
`current_catalog` → `name` `current_database` () → `name` Returns the name of
the current database. (Databases are called “catalogs” in the SQL standard, so
`current_catalog` is the standard's spelling.)  
`current_query` () → `text` Returns the text of the currently executing query,
as submitted by the client (which might contain more than one statement).  
`current_role` → `name` This is equivalent to `current_user`.  
`current_schema` → `name` `current_schema` () → `name` Returns the name of the
schema that is first in the search path (or a null value if the search path is
empty). This is the schema that will be used for any tables or other named
objects that are created without specifying a target schema.  
`current_schemas` ( _`include_implicit`_ `boolean` ) → `name[]` Returns an
array of the names of all schemas presently in the effective search path, in
their priority order. (Items in the current [search_path](runtime-config-
client.html#GUC-SEARCH-PATH) setting that do not correspond to existing,
searchable schemas are omitted.) If the Boolean argument is `true`, then
implicitly-searched system schemas such as `pg_catalog` are included in the
result.  
`current_user` → `name` Returns the user name of the current execution
context.  
`inet_client_addr` () → `inet` Returns the IP address of the current client,
or `NULL` if the current connection is via a Unix-domain socket.  
`inet_client_port` () → `integer` Returns the IP port number of the current
client, or `NULL` if the current connection is via a Unix-domain socket.  
`inet_server_addr` () → `inet` Returns the IP address on which the server
accepted the current connection, or `NULL` if the current connection is via a
Unix-domain socket.  
`inet_server_port` () → `integer` Returns the IP port number on which the
server accepted the current connection, or `NULL` if the current connection is
via a Unix-domain socket.  
`pg_backend_pid` () → `integer` Returns the process ID of the server process
attached to the current session.  
`pg_blocking_pids` ( `integer` ) → `integer[]` Returns an array of the process
ID(s) of the sessions that are blocking the server process with the specified
process ID from acquiring a lock, or an empty array if there is no such server
process or it is not blocked. One server process blocks another if it either
holds a lock that conflicts with the blocked process's lock request (hard
block), or is waiting for a lock that would conflict with the blocked
process's lock request and is ahead of it in the wait queue (soft block). When
using parallel queries the result always lists client-visible process IDs
(that is, `pg_backend_pid` results) even if the actual lock is held or awaited
by a child worker process. As a result of that, there may be duplicated PIDs
in the result. Also note that when a prepared transaction holds a conflicting
lock, it will be represented by a zero process ID. Frequent calls to this
function could have some impact on database performance, because it needs
exclusive access to the lock manager's shared state for a short time.  
`pg_conf_load_time` () → `timestamp with time zone` Returns the time when the
server configuration files were last loaded. If the current session was alive
at the time, this will be the time when the session itself re-read the
configuration files (so the reading will vary a little in different sessions).
Otherwise it is the time when the postmaster process re-read the configuration
files.  
`pg_current_logfile` ( [ `text` ] ) → `text` Returns the path name of the log
file currently in use by the logging collector. The path includes the
[log_directory](runtime-config-logging.html#GUC-LOG-DIRECTORY) directory and
the individual log file name. The result is `NULL` if the logging collector is
disabled. When multiple log files exist, each in a different format,
`pg_current_logfile` without an argument returns the path of the file having
the first format found in the ordered list: `stderr`, `csvlog`, `jsonlog`.
`NULL` is returned if no log file has any of these formats. To request
information about a specific log file format, supply either `csvlog`,
`jsonlog` or `stderr` as the value of the optional parameter. The result is
`NULL` if the log format requested is not configured in
[log_destination](runtime-config-logging.html#GUC-LOG-DESTINATION). The result
reflects the contents of the `current_logfiles` file.  
`pg_my_temp_schema` () → `oid` Returns the OID of the current session's
temporary schema, or zero if it has none (because it has not created any
temporary tables).  
`pg_is_other_temp_schema` ( `oid` ) → `boolean` Returns true if the given OID
is the OID of another session's temporary schema. (This can be useful, for
example, to exclude other sessions' temporary tables from a catalog display.)  
`pg_jit_available` () → `boolean` Returns true if a JIT compiler extension is
available (see [Chapter 32](jit.html "Chapter 32. Just-in-Time Compilation
\(JIT\)")) and the [jit](runtime-config-query.html#GUC-JIT) configuration
parameter is set to `on`.  
`pg_listening_channels` () → `setof text` Returns the set of names of
asynchronous notification channels that the current session is listening to.  
`pg_notification_queue_usage` () → `double precision` Returns the fraction
(0–1) of the asynchronous notification queue's maximum size that is currently
occupied by notifications that are waiting to be processed. See [LISTEN](sql-
listen.html "LISTEN") and [NOTIFY](sql-notify.html "NOTIFY") for more
information.  
`pg_postmaster_start_time` () → `timestamp with time zone` Returns the time
when the server started.  
`pg_safe_snapshot_blocking_pids` ( `integer` ) → `integer[]` Returns an array
of the process ID(s) of the sessions that are blocking the server process with
the specified process ID from acquiring a safe snapshot, or an empty array if
there is no such server process or it is not blocked. A session running a
`SERIALIZABLE` transaction blocks a `SERIALIZABLE READ ONLY DEFERRABLE`
transaction from acquiring a snapshot until the latter determines that it is
safe to avoid taking any predicate locks. See [Section 13.2.3](transaction-
iso.html#XACT-SERIALIZABLE "13.2.3. Serializable Isolation Level") for more
information about serializable and deferrable transactions. Frequent calls to
this function could have some impact on database performance, because it needs
access to the predicate lock manager's shared state for a short time.  
`pg_trigger_depth` () → `integer` Returns the current nesting level of
PostgreSQL triggers (0 if not called, directly or indirectly, from inside a
trigger).  
`session_user` → `name` Returns the session user's name.  
`system_user` → `text` Returns the authentication method and the identity (if
any) that the user presented during the authentication cycle before they were
assigned a database role. It is represented as `auth_method:identity` or
`NULL` if the user has not been authenticated (for example if [Trust
authentication](auth-trust.html "21.4. Trust Authentication") has been used).  
`user` → `name` This is equivalent to `current_user`.  
`version` () → `text` Returns a string describing the PostgreSQL server's
version. You can also get this information from [server_version](runtime-
config-preset.html#GUC-SERVER-VERSION), or for a machine-readable version use
[server_version_num](runtime-config-preset.html#GUC-SERVER-VERSION-NUM).
Software developers should use `server_version_num` (available since 8.2) or
[`PQserverVersion`](libpq-status.html#LIBPQ-PQSERVERVERSION) instead of
parsing the text version.  
  
  

### Note

`current_catalog`, `current_role`, `current_schema`, `current_user`,
`session_user`, and `user` have special syntactic status in SQL: they must be
called without trailing parentheses. In PostgreSQL, parentheses can optionally
be used with `current_schema`, but not with the others.

The `session_user` is normally the user who initiated the current database
connection; but superusers can change this setting with [SET SESSION
AUTHORIZATION](sql-set-session-authorization.html "SET SESSION
AUTHORIZATION"). The `current_user` is the user identifier that is applicable
for permission checking. Normally it is equal to the session user, but it can
be changed with [SET ROLE](sql-set-role.html "SET ROLE"). It also changes
during the execution of functions with the attribute `SECURITY DEFINER`. In
Unix parlance, the session user is the “real user” and the current user is the
“effective user”. `current_role` and `user` are synonyms for `current_user`.
(The SQL standard draws a distinction between `current_role` and
`current_user`, but PostgreSQL does not, since it unifies users and roles into
a single kind of entity.)

### 9.26.2. Access Privilege Inquiry Functions #

[Table 9.68](functions-info.html#FUNCTIONS-INFO-ACCESS-TABLE
"Table 9.68. Access Privilege Inquiry Functions") lists functions that allow
querying object access privileges programmatically. (See [Section 5.7](ddl-
priv.html "5.7. Privileges") for more information about privileges.) In these
functions, the user whose privileges are being inquired about can be specified
by name or by OID (`pg_authid`.`oid`), or if the name is given as `public`
then the privileges of the PUBLIC pseudo-role are checked. Also, the _`user`_
argument can be omitted entirely, in which case the `current_user` is assumed.
The object that is being inquired about can be specified either by name or by
OID, too. When specifying by name, a schema name can be included if relevant.
The access privilege of interest is specified by a text string, which must
evaluate to one of the appropriate privilege keywords for the object's type
(e.g., `SELECT`). Optionally, `WITH GRANT OPTION` can be added to a privilege
type to test whether the privilege is held with grant option. Also, multiple
privilege types can be listed separated by commas, in which case the result
will be true if any of the listed privileges is held. (Case of the privilege
string is not significant, and extra whitespace is allowed between but not
within privilege names.) Some examples:

    
    
    SELECT has_table_privilege('myschema.mytable', 'select');
    SELECT has_table_privilege('joe', 'mytable', 'INSERT, SELECT WITH GRANT OPTION');
    

**Table  9.68. Access Privilege Inquiry Functions**

Function Description  
---  
`has_any_column_privilege` ( [ _`user`_ `name` or `oid`, ] _`table`_ `text` or
`oid`, _`privilege`_ `text` ) → `boolean` Does user have privilege for any
column of table? This succeeds either if the privilege is held for the whole
table, or if there is a column-level grant of the privilege for at least one
column. Allowable privilege types are `SELECT`, `INSERT`, `UPDATE`, and
`REFERENCES`.  
`has_column_privilege` ( [ _`user`_ `name` or `oid`, ] _`table`_ `text` or
`oid`, _`column`_ `text` or `smallint`, _`privilege`_ `text` ) → `boolean`
Does user have privilege for the specified table column? This succeeds either
if the privilege is held for the whole table, or if there is a column-level
grant of the privilege for the column. The column can be specified by name or
by attribute number (`pg_attribute`.`attnum`). Allowable privilege types are
`SELECT`, `INSERT`, `UPDATE`, and `REFERENCES`.  
`has_database_privilege` ( [ _`user`_ `name` or `oid`, ] _`database`_ `text`
or `oid`, _`privilege`_ `text` ) → `boolean` Does user have privilege for
database? Allowable privilege types are `CREATE`, `CONNECT`, `TEMPORARY`, and
`TEMP` (which is equivalent to `TEMPORARY`).  
`has_foreign_data_wrapper_privilege` ( [ _`user`_ `name` or `oid`, ] _`fdw`_
`text` or `oid`, _`privilege`_ `text` ) → `boolean` Does user have privilege
for foreign-data wrapper? The only allowable privilege type is `USAGE`.  
`has_function_privilege` ( [ _`user`_ `name` or `oid`, ] _`function`_ `text`
or `oid`, _`privilege`_ `text` ) → `boolean` Does user have privilege for
function? The only allowable privilege type is `EXECUTE`. When specifying a
function by name rather than by OID, the allowed input is the same as for the
`regprocedure` data type (see [Section 8.19](datatype-oid.html "8.19. Object
Identifier Types")). An example is:

    
    
    SELECT has_function_privilege('joeuser', 'myfunc(int, text)', 'execute');
      
  
`has_language_privilege` ( [ _`user`_ `name` or `oid`, ] _`language`_ `text`
or `oid`, _`privilege`_ `text` ) → `boolean` Does user have privilege for
language? The only allowable privilege type is `USAGE`.  
`has_parameter_privilege` ( [ _`user`_ `name` or `oid`, ] _`parameter`_
`text`, _`privilege`_ `text` ) → `boolean` Does user have privilege for
configuration parameter? The parameter name is case-insensitive. Allowable
privilege types are `SET` and `ALTER SYSTEM`.  
`has_schema_privilege` ( [ _`user`_ `name` or `oid`, ] _`schema`_ `text` or
`oid`, _`privilege`_ `text` ) → `boolean` Does user have privilege for schema?
Allowable privilege types are `CREATE` and `USAGE`.  
`has_sequence_privilege` ( [ _`user`_ `name` or `oid`, ] _`sequence`_ `text`
or `oid`, _`privilege`_ `text` ) → `boolean` Does user have privilege for
sequence? Allowable privilege types are `USAGE`, `SELECT`, and `UPDATE`.  
`has_server_privilege` ( [ _`user`_ `name` or `oid`, ] _`server`_ `text` or
`oid`, _`privilege`_ `text` ) → `boolean` Does user have privilege for foreign
server? The only allowable privilege type is `USAGE`.  
`has_table_privilege` ( [ _`user`_ `name` or `oid`, ] _`table`_ `text` or
`oid`, _`privilege`_ `text` ) → `boolean` Does user have privilege for table?
Allowable privilege types are `SELECT`, `INSERT`, `UPDATE`, `DELETE`,
`TRUNCATE`, `REFERENCES`, and `TRIGGER`.  
`has_tablespace_privilege` ( [ _`user`_ `name` or `oid`, ] _`tablespace`_
`text` or `oid`, _`privilege`_ `text` ) → `boolean` Does user have privilege
for tablespace? The only allowable privilege type is `CREATE`.  
`has_type_privilege` ( [ _`user`_ `name` or `oid`, ] _`type`_ `text` or `oid`,
_`privilege`_ `text` ) → `boolean` Does user have privilege for data type? The
only allowable privilege type is `USAGE`. When specifying a type by name
rather than by OID, the allowed input is the same as for the `regtype` data
type (see [Section 8.19](datatype-oid.html "8.19. Object Identifier Types")).  
`pg_has_role` ( [ _`user`_ `name` or `oid`, ] _`role`_ `text` or `oid`,
_`privilege`_ `text` ) → `boolean` Does user have privilege for role?
Allowable privilege types are `MEMBER`, `USAGE`, and `SET`. `MEMBER` denotes
direct or indirect membership in the role without regard to what specific
privileges may be conferred. `USAGE` denotes whether the privileges of the
role are immediately available without doing `SET ROLE`, while `SET` denotes
whether it is possible to change to the role using the `SET ROLE` command.
`WITH ADMIN OPTION` or `WITH GRANT OPTION` can be added to any of these
privilege types to test whether the `ADMIN` privilege is held (all six
spellings test the same thing). This function does not allow the special case
of setting _`user`_ to `public`, because the PUBLIC pseudo-role can never be a
member of real roles.  
`row_security_active` ( _`table`_ `text` or `oid` ) → `boolean` Is row-level
security active for the specified table in the context of the current user and
current environment?  
  
  

[Table 9.69](functions-info.html#FUNCTIONS-ACLITEM-OP-TABLE
"Table 9.69. aclitem Operators") shows the operators available for the
`aclitem` type, which is the catalog representation of access privileges. See
[Section 5.7](ddl-priv.html "5.7. Privileges") for information about how to
read access privilege values.

**Table  9.69. `aclitem` Operators**

Operator Description Example(s)  
---  
`aclitem` `=` `aclitem` → `boolean` Are `aclitem`s equal? (Notice that type
`aclitem` lacks the usual set of comparison operators; it has only equality.
In turn, `aclitem` arrays can only be compared for equality.)
`'calvin=r*w/hobbes'::aclitem = 'calvin=r*w*/hobbes'::aclitem` → `f`  
`aclitem[]` `@>` `aclitem` → `boolean` Does array contain the specified
privileges? (This is true if there is an array entry that matches the
`aclitem`'s grantee and grantor, and has at least the specified set of
privileges.) `'{calvin=r*w/hobbes,hobbes=r*w*/postgres}'::aclitem[] @>
'calvin=r*/hobbes'::aclitem` → `t`  
`aclitem[]` `~` `aclitem` → `boolean` This is a deprecated alias for `@>`.
`'{calvin=r*w/hobbes,hobbes=r*w*/postgres}'::aclitem[] ~
'calvin=r*/hobbes'::aclitem` → `t`  
  
  

[Table 9.70](functions-info.html#FUNCTIONS-ACLITEM-FN-TABLE
"Table 9.70. aclitem Functions") shows some additional functions to manage the
`aclitem` type.

**Table  9.70. `aclitem` Functions**

Function Description  
---  
`acldefault` ( _`type`_ `"char"`, _`ownerId`_ `oid` ) → `aclitem[]` Constructs
an `aclitem` array holding the default access privileges for an object of type
_`type`_ belonging to the role with OID _`ownerId`_. This represents the
access privileges that will be assumed when an object's ACL entry is null.
(The default access privileges are described in [Section 5.7](ddl-priv.html
"5.7. Privileges").) The _`type`_ parameter must be one of 'c' for `COLUMN`,
'r' for `TABLE` and table-like objects, 's' for `SEQUENCE`, 'd' for
`DATABASE`, 'f' for `FUNCTION` or `PROCEDURE`, 'l' for `LANGUAGE`, 'L' for
`LARGE OBJECT`, 'n' for `SCHEMA`, 'p' for `PARAMETER`, 't' for `TABLESPACE`,
'F' for `FOREIGN DATA WRAPPER`, 'S' for `FOREIGN SERVER`, or 'T' for `TYPE` or
`DOMAIN`.  
`aclexplode` ( `aclitem[]` ) → `setof record` ( _`grantor`_ `oid`, _`grantee`_
`oid`, _`privilege_type`_ `text`, _`is_grantable`_ `boolean` ) Returns the
`aclitem` array as a set of rows. If the grantee is the pseudo-role PUBLIC, it
is represented by zero in the _`grantee`_ column. Each granted privilege is
represented as `SELECT`, `INSERT`, etc (see [Table 5.1](ddl-
priv.html#PRIVILEGE-ABBREVS-TABLE "Table 5.1. ACL Privilege Abbreviations")
for a full list). Note that each privilege is broken out as a separate row, so
only one keyword appears in the _`privilege_type`_ column.  
`makeaclitem` ( _`grantee`_ `oid`, _`grantor`_ `oid`, _`privileges`_ `text`,
_`is_grantable`_ `boolean` ) → `aclitem` Constructs an `aclitem` with the
given properties. _`privileges`_ is a comma-separated list of privilege names
such as `SELECT`, `INSERT`, etc, all of which are set in the result. (Case of
the privilege string is not significant, and extra whitespace is allowed
between but not within privilege names.)  
  
  

### 9.26.3. Schema Visibility Inquiry Functions #

[Table 9.71](functions-info.html#FUNCTIONS-INFO-SCHEMA-TABLE
"Table 9.71. Schema Visibility Inquiry Functions") shows functions that
determine whether a certain object is _visible_ in the current schema search
path. For example, a table is said to be visible if its containing schema is
in the search path and no table of the same name appears earlier in the search
path. This is equivalent to the statement that the table can be referenced by
name without explicit schema qualification. Thus, to list the names of all
visible tables:

    
    
    SELECT relname FROM pg_class WHERE pg_table_is_visible(oid);
    

For functions and operators, an object in the search path is said to be
visible if there is no object of the same name _and argument data type(s)_
earlier in the path. For operator classes and families, both the name and the
associated index access method are considered.

**Table  9.71. Schema Visibility Inquiry Functions**

Function Description  
---  
`pg_collation_is_visible` ( _`collation`_ `oid` ) → `boolean` Is collation
visible in search path?  
`pg_conversion_is_visible` ( _`conversion`_ `oid` ) → `boolean` Is conversion
visible in search path?  
`pg_function_is_visible` ( _`function`_ `oid` ) → `boolean` Is function
visible in search path? (This also works for procedures and aggregates.)  
`pg_opclass_is_visible` ( _`opclass`_ `oid` ) → `boolean` Is operator class
visible in search path?  
`pg_operator_is_visible` ( _`operator`_ `oid` ) → `boolean` Is operator
visible in search path?  
`pg_opfamily_is_visible` ( _`opclass`_ `oid` ) → `boolean` Is operator family
visible in search path?  
`pg_statistics_obj_is_visible` ( _`stat`_ `oid` ) → `boolean` Is statistics
object visible in search path?  
`pg_table_is_visible` ( _`table`_ `oid` ) → `boolean` Is table visible in
search path? (This works for all types of relations, including views,
materialized views, indexes, sequences and foreign tables.)  
`pg_ts_config_is_visible` ( _`config`_ `oid` ) → `boolean` Is text search
configuration visible in search path?  
`pg_ts_dict_is_visible` ( _`dict`_ `oid` ) → `boolean` Is text search
dictionary visible in search path?  
`pg_ts_parser_is_visible` ( _`parser`_ `oid` ) → `boolean` Is text search
parser visible in search path?  
`pg_ts_template_is_visible` ( _`template`_ `oid` ) → `boolean` Is text search
template visible in search path?  
`pg_type_is_visible` ( _`type`_ `oid` ) → `boolean` Is type (or domain)
visible in search path?  
  
  

All these functions require object OIDs to identify the object to be checked.
If you want to test an object by name, it is convenient to use the OID alias
types (`regclass`, `regtype`, `regprocedure`, `regoperator`, `regconfig`, or
`regdictionary`), for example:

    
    
    SELECT pg_type_is_visible('myschema.widget'::regtype);
    

Note that it would not make much sense to test a non-schema-qualified type
name in this way — if the name can be recognized at all, it must be visible.

### 9.26.4. System Catalog Information Functions #

[Table 9.72](functions-info.html#FUNCTIONS-INFO-CATALOG-TABLE
"Table 9.72. System Catalog Information Functions") lists functions that
extract information from the system catalogs.

**Table  9.72. System Catalog Information Functions**

Function Description  
---  
`format_type` ( _`type`_ `oid`, _`typemod`_ `integer` ) → `text` Returns the
SQL name for a data type that is identified by its type OID and possibly a
type modifier. Pass NULL for the type modifier if no specific modifier is
known.  
`pg_char_to_encoding` ( _`encoding`_ `name` ) → `integer` Converts the
supplied encoding name into an integer representing the internal identifier
used in some system catalog tables. Returns `-1` if an unknown encoding name
is provided.  
`pg_encoding_to_char` ( _`encoding`_ `integer` ) → `name` Converts the integer
used as the internal identifier of an encoding in some system catalog tables
into a human-readable string. Returns an empty string if an invalid encoding
number is provided.  
`pg_get_catalog_foreign_keys` () → `setof record` ( _`fktable`_ `regclass`,
_`fkcols`_ `text[]`, _`pktable`_ `regclass`, _`pkcols`_ `text[]`, _`is_array`_
`boolean`, _`is_opt`_ `boolean` ) Returns a set of records describing the
foreign key relationships that exist within the PostgreSQL system catalogs.
The _`fktable`_ column contains the name of the referencing catalog, and the
_`fkcols`_ column contains the name(s) of the referencing column(s).
Similarly, the _`pktable`_ column contains the name of the referenced catalog,
and the _`pkcols`_ column contains the name(s) of the referenced column(s). If
_`is_array`_ is true, the last referencing column is an array, each of whose
elements should match some entry in the referenced catalog. If _`is_opt`_ is
true, the referencing column(s) are allowed to contain zeroes instead of a
valid reference.  
`pg_get_constraintdef` ( _`constraint`_ `oid` [, _`pretty`_ `boolean` ] ) →
`text` Reconstructs the creating command for a constraint. (This is a
decompiled reconstruction, not the original text of the command.)  
`pg_get_expr` ( _`expr`_ `pg_node_tree`, _`relation`_ `oid` [, _`pretty`_
`boolean` ] ) → `text` Decompiles the internal form of an expression stored in
the system catalogs, such as the default value for a column. If the expression
might contain Vars, specify the OID of the relation they refer to as the
second parameter; if no Vars are expected, passing zero is sufficient.  
`pg_get_functiondef` ( _`func`_ `oid` ) → `text` Reconstructs the creating
command for a function or procedure. (This is a decompiled reconstruction, not
the original text of the command.) The result is a complete `CREATE OR REPLACE
FUNCTION` or `CREATE OR REPLACE PROCEDURE` statement.  
`pg_get_function_arguments` ( _`func`_ `oid` ) → `text` Reconstructs the
argument list of a function or procedure, in the form it would need to appear
in within `CREATE FUNCTION` (including default values).  
`pg_get_function_identity_arguments` ( _`func`_ `oid` ) → `text` Reconstructs
the argument list necessary to identify a function or procedure, in the form
it would need to appear in within commands such as `ALTER FUNCTION`. This form
omits default values.  
`pg_get_function_result` ( _`func`_ `oid` ) → `text` Reconstructs the
`RETURNS` clause of a function, in the form it would need to appear in within
`CREATE FUNCTION`. Returns `NULL` for a procedure.  
`pg_get_indexdef` ( _`index`_ `oid` [, _`column`_ `integer`, _`pretty`_
`boolean` ] ) → `text` Reconstructs the creating command for an index. (This
is a decompiled reconstruction, not the original text of the command.) If
_`column`_ is supplied and is not zero, only the definition of that column is
reconstructed.  
`pg_get_keywords` () → `setof record` ( _`word`_ `text`, _`catcode`_ `"char"`,
_`barelabel`_ `boolean`, _`catdesc`_ `text`, _`baredesc`_ `text` ) Returns a
set of records describing the SQL keywords recognized by the server. The
_`word`_ column contains the keyword. The _`catcode`_ column contains a
category code: `U` for an unreserved keyword, `C` for a keyword that can be a
column name, `T` for a keyword that can be a type or function name, or `R` for
a fully reserved keyword. The _`barelabel`_ column contains `true` if the
keyword can be used as a “bare” column label in `SELECT` lists, or `false` if
it can only be used after `AS`. The _`catdesc`_ column contains a possibly-
localized string describing the keyword's category. The _`baredesc`_ column
contains a possibly-localized string describing the keyword's column label
status.  
`pg_get_partkeydef` ( _`table`_ `oid` ) → `text` Reconstructs the definition
of a partitioned table's partition key, in the form it would have in the
`PARTITION BY` clause of `CREATE TABLE`. (This is a decompiled reconstruction,
not the original text of the command.)  
`pg_get_ruledef` ( _`rule`_ `oid` [, _`pretty`_ `boolean` ] ) → `text`
Reconstructs the creating command for a rule. (This is a decompiled
reconstruction, not the original text of the command.)  
`pg_get_serial_sequence` ( _`table`_ `text`, _`column`_ `text` ) → `text`
Returns the name of the sequence associated with a column, or NULL if no
sequence is associated with the column. If the column is an identity column,
the associated sequence is the sequence internally created for that column.
For columns created using one of the serial types (`serial`, `smallserial`,
`bigserial`), it is the sequence created for that serial column definition. In
the latter case, the association can be modified or removed with `ALTER
SEQUENCE OWNED BY`. (This function probably should have been called
`pg_get_owned_sequence`; its current name reflects the fact that it has
historically been used with serial-type columns.) The first parameter is a
table name with optional schema, and the second parameter is a column name.
Because the first parameter potentially contains both schema and table names,
it is parsed per usual SQL rules, meaning it is lower-cased by default. The
second parameter, being just a column name, is treated literally and so has
its case preserved. The result is suitably formatted for passing to the
sequence functions (see [Section 9.17](functions-sequence.html "9.17. Sequence
Manipulation Functions")). A typical use is in reading the current value of
the sequence for an identity or serial column, for example:

    
    
    SELECT currval(pg_get_serial_sequence('sometable', 'id'));
      
  
`pg_get_statisticsobjdef` ( _`statobj`_ `oid` ) → `text` Reconstructs the
creating command for an extended statistics object. (This is a decompiled
reconstruction, not the original text of the command.)  
`pg_get_triggerdef` ( _`trigger`_ `oid` [, _`pretty`_ `boolean` ] ) → `text`
Reconstructs the creating command for a trigger. (This is a decompiled
reconstruction, not the original text of the command.)  
`pg_get_userbyid` ( _`role`_ `oid` ) → `name` Returns a role's name given its
OID.  
`pg_get_viewdef` ( _`view`_ `oid` [, _`pretty`_ `boolean` ] ) → `text`
Reconstructs the underlying `SELECT` command for a view or materialized view.
(This is a decompiled reconstruction, not the original text of the command.)  
`pg_get_viewdef` ( _`view`_ `oid`, _`wrap_column`_ `integer` ) → `text`
Reconstructs the underlying `SELECT` command for a view or materialized view.
(This is a decompiled reconstruction, not the original text of the command.)
In this form of the function, pretty-printing is always enabled, and long
lines are wrapped to try to keep them shorter than the specified number of
columns.  
`pg_get_viewdef` ( _`view`_ `text` [, _`pretty`_ `boolean` ] ) → `text`
Reconstructs the underlying `SELECT` command for a view or materialized view,
working from a textual name for the view rather than its OID. (This is
deprecated; use the OID variant instead.)  
`pg_index_column_has_property` ( _`index`_ `regclass`, _`column`_ `integer`,
_`property`_ `text` ) → `boolean` Tests whether an index column has the named
property. Common index column properties are listed in [Table 9.73](functions-
info.html#FUNCTIONS-INFO-INDEX-COLUMN-PROPS "Table 9.73. Index Column
Properties"). (Note that extension access methods can define additional
property names for their indexes.) `NULL` is returned if the property name is
not known or does not apply to the particular object, or if the OID or column
number does not identify a valid object.  
`pg_index_has_property` ( _`index`_ `regclass`, _`property`_ `text` ) →
`boolean` Tests whether an index has the named property. Common index
properties are listed in [Table 9.74](functions-info.html#FUNCTIONS-INFO-
INDEX-PROPS "Table 9.74. Index Properties"). (Note that extension access
methods can define additional property names for their indexes.) `NULL` is
returned if the property name is not known or does not apply to the particular
object, or if the OID does not identify a valid object.  
`pg_indexam_has_property` ( _`am`_ `oid`, _`property`_ `text` ) → `boolean`
Tests whether an index access method has the named property. Access method
properties are listed in [Table 9.75](functions-info.html#FUNCTIONS-INFO-
INDEXAM-PROPS "Table 9.75. Index Access Method Properties"). `NULL` is
returned if the property name is not known or does not apply to the particular
object, or if the OID does not identify a valid object.  
`pg_options_to_table` ( _`options_array`_ `text[]` ) → `setof record` (
_`option_name`_ `text`, _`option_value`_ `text` ) Returns the set of storage
options represented by a value from `pg_class`.`reloptions` or
`pg_attribute`.`attoptions`.  
`pg_settings_get_flags` ( _`guc`_ `text` ) → `text[]` Returns an array of the
flags associated with the given GUC, or `NULL` if it does not exist. The
result is an empty array if the GUC exists but there are no flags to show.
Only the most useful flags listed in [Table 9.76](functions-
info.html#FUNCTIONS-PG-SETTINGS-FLAGS "Table 9.76. GUC Flags") are exposed.  
`pg_tablespace_databases` ( _`tablespace`_ `oid` ) → `setof oid` Returns the
set of OIDs of databases that have objects stored in the specified tablespace.
If this function returns any rows, the tablespace is not empty and cannot be
dropped. To identify the specific objects populating the tablespace, you will
need to connect to the database(s) identified by `pg_tablespace_databases` and
query their `pg_class` catalogs.  
`pg_tablespace_location` ( _`tablespace`_ `oid` ) → `text` Returns the file
system path that this tablespace is located in.  
`pg_typeof` ( `"any"` ) → `regtype` Returns the OID of the data type of the
value that is passed to it. This can be helpful for troubleshooting or
dynamically constructing SQL queries. The function is declared as returning
`regtype`, which is an OID alias type (see [Section 8.19](datatype-oid.html
"8.19. Object Identifier Types")); this means that it is the same as an OID
for comparison purposes but displays as a type name. For example:

    
    
    SELECT pg_typeof(33);
     pg_typeof
    -----------
     integer
    
    SELECT typlen FROM pg_type WHERE oid = pg_typeof(33);
     typlen
    --------
          4
      
  
`COLLATION FOR` ( `"any"` ) → `text` Returns the name of the collation of the
value that is passed to it. The value is quoted and schema-qualified if
necessary. If no collation was derived for the argument expression, then
`NULL` is returned. If the argument is not of a collatable data type, then an
error is raised. For example:

    
    
    SELECT collation for (description) FROM pg_description LIMIT 1;
     pg_collation_for
    ------------------
     "default"
    
    SELECT collation for ('foo' COLLATE "de_DE");
     pg_collation_for
    ------------------
     "de_DE"
      
  
`to_regclass` ( `text` ) → `regclass` Translates a textual relation name to
its OID. A similar result is obtained by casting the string to type `regclass`
(see [Section 8.19](datatype-oid.html "8.19. Object Identifier Types"));
however, this function will return `NULL` rather than throwing an error if the
name is not found.  
`to_regcollation` ( `text` ) → `regcollation` Translates a textual collation
name to its OID. A similar result is obtained by casting the string to type
`regcollation` (see [Section 8.19](datatype-oid.html "8.19. Object Identifier
Types")); however, this function will return `NULL` rather than throwing an
error if the name is not found.  
`to_regnamespace` ( `text` ) → `regnamespace` Translates a textual schema name
to its OID. A similar result is obtained by casting the string to type
`regnamespace` (see [Section 8.19](datatype-oid.html "8.19. Object Identifier
Types")); however, this function will return `NULL` rather than throwing an
error if the name is not found.  
`to_regoper` ( `text` ) → `regoper` Translates a textual operator name to its
OID. A similar result is obtained by casting the string to type `regoper` (see
[Section 8.19](datatype-oid.html "8.19. Object Identifier Types")); however,
this function will return `NULL` rather than throwing an error if the name is
not found or is ambiguous.  
`to_regoperator` ( `text` ) → `regoperator` Translates a textual operator name
(with parameter types) to its OID. A similar result is obtained by casting the
string to type `regoperator` (see [Section 8.19](datatype-oid.html
"8.19. Object Identifier Types")); however, this function will return `NULL`
rather than throwing an error if the name is not found.  
`to_regproc` ( `text` ) → `regproc` Translates a textual function or procedure
name to its OID. A similar result is obtained by casting the string to type
`regproc` (see [Section 8.19](datatype-oid.html "8.19. Object Identifier
Types")); however, this function will return `NULL` rather than throwing an
error if the name is not found or is ambiguous.  
`to_regprocedure` ( `text` ) → `regprocedure` Translates a textual function or
procedure name (with argument types) to its OID. A similar result is obtained
by casting the string to type `regprocedure` (see [Section 8.19](datatype-
oid.html "8.19. Object Identifier Types")); however, this function will return
`NULL` rather than throwing an error if the name is not found.  
`to_regrole` ( `text` ) → `regrole` Translates a textual role name to its OID.
A similar result is obtained by casting the string to type `regrole` (see
[Section 8.19](datatype-oid.html "8.19. Object Identifier Types")); however,
this function will return `NULL` rather than throwing an error if the name is
not found.  
`to_regtype` ( `text` ) → `regtype` Translates a textual type name to its OID.
A similar result is obtained by casting the string to type `regtype` (see
[Section 8.19](datatype-oid.html "8.19. Object Identifier Types")); however,
this function will return `NULL` rather than throwing an error if the name is
not found.  
  
  

Most of the functions that reconstruct (decompile) database objects have an
optional _`pretty`_ flag, which if `true` causes the result to be “pretty-
printed”. Pretty-printing suppresses unnecessary parentheses and adds
whitespace for legibility. The pretty-printed format is more readable, but the
default format is more likely to be interpreted the same way by future
versions of PostgreSQL; so avoid using pretty-printed output for dump
purposes. Passing `false` for the _`pretty`_ parameter yields the same result
as omitting the parameter.

**Table  9.73. Index Column Properties**

Name | Description  
---|---  
`asc` | Does the column sort in ascending order on a forward scan?  
`desc` | Does the column sort in descending order on a forward scan?  
`nulls_first` | Does the column sort with nulls first on a forward scan?  
`nulls_last` | Does the column sort with nulls last on a forward scan?  
`orderable` | Does the column possess any defined sort ordering?  
`distance_orderable` | Can the column be scanned in order by a “distance” operator, for example `ORDER BY col <-> constant` ?  
`returnable` | Can the column value be returned by an index-only scan?  
`search_array` | Does the column natively support `col = ANY(array)` searches?  
`search_nulls` | Does the column support `IS NULL` and `IS NOT NULL` searches?  
  
  

**Table  9.74. Index Properties**

Name | Description  
---|---  
`clusterable` | Can the index be used in a `CLUSTER` command?  
`index_scan` | Does the index support plain (non-bitmap) scans?  
`bitmap_scan` | Does the index support bitmap scans?  
`backward_scan` | Can the scan direction be changed in mid-scan (to support `FETCH BACKWARD` on a cursor without needing materialization)?  
  
  

**Table  9.75. Index Access Method Properties**

Name | Description  
---|---  
`can_order` | Does the access method support `ASC`, `DESC` and related keywords in `CREATE INDEX`?  
`can_unique` | Does the access method support unique indexes?  
`can_multi_col` | Does the access method support indexes with multiple columns?  
`can_exclude` | Does the access method support exclusion constraints?  
`can_include` | Does the access method support the `INCLUDE` clause of `CREATE INDEX`?  
  
  

**Table  9.76. GUC Flags**

Flag | Description  
---|---  
`EXPLAIN` | Parameters with this flag are included in `EXPLAIN (SETTINGS)` commands.  
`NO_SHOW_ALL` | Parameters with this flag are excluded from `SHOW ALL` commands.  
`NO_RESET` | Parameters with this flag do not support `RESET` commands.  
`NO_RESET_ALL` | Parameters with this flag are excluded from `RESET ALL` commands.  
`NOT_IN_SAMPLE` | Parameters with this flag are not included in `postgresql.conf` by default.  
`RUNTIME_COMPUTED` | Parameters with this flag are runtime-computed ones.  
  
  

### 9.26.5. Object Information and Addressing Functions #

[Table 9.77](functions-info.html#FUNCTIONS-INFO-OBJECT-TABLE
"Table 9.77. Object Information and Addressing Functions") lists functions
related to database object identification and addressing.

**Table  9.77. Object Information and Addressing Functions**

Function Description  
---  
`pg_describe_object` ( _`classid`_ `oid`, _`objid`_ `oid`, _`objsubid`_
`integer` ) → `text` Returns a textual description of a database object
identified by catalog OID, object OID, and sub-object ID (such as a column
number within a table; the sub-object ID is zero when referring to a whole
object). This description is intended to be human-readable, and might be
translated, depending on server configuration. This is especially useful to
determine the identity of an object referenced in the `pg_depend` catalog.
This function returns `NULL` values for undefined objects.  
`pg_identify_object` ( _`classid`_ `oid`, _`objid`_ `oid`, _`objsubid`_
`integer` ) → `record` ( _`type`_ `text`, _`schema`_ `text`, _`name`_ `text`,
_`identity`_ `text` ) Returns a row containing enough information to uniquely
identify the database object specified by catalog OID, object OID and sub-
object ID. This information is intended to be machine-readable, and is never
translated. _`type`_ identifies the type of database object; _`schema`_ is the
schema name that the object belongs in, or `NULL` for object types that do not
belong to schemas; _`name`_ is the name of the object, quoted if necessary, if
the name (along with schema name, if pertinent) is sufficient to uniquely
identify the object, otherwise `NULL`; _`identity`_ is the complete object
identity, with the precise format depending on object type, and each name
within the format being schema-qualified and quoted as necessary. Undefined
objects are identified with `NULL` values.  
`pg_identify_object_as_address` ( _`classid`_ `oid`, _`objid`_ `oid`,
_`objsubid`_ `integer` ) → `record` ( _`type`_ `text`, _`object_names`_
`text[]`, _`object_args`_ `text[]` ) Returns a row containing enough
information to uniquely identify the database object specified by catalog OID,
object OID and sub-object ID. The returned information is independent of the
current server, that is, it could be used to identify an identically named
object in another server. _`type`_ identifies the type of database object;
_`object_names`_ and _`object_args`_ are text arrays that together form a
reference to the object. These three values can be passed to
`pg_get_object_address` to obtain the internal address of the object.  
`pg_get_object_address` ( _`type`_ `text`, _`object_names`_ `text[]`,
_`object_args`_ `text[]` ) → `record` ( _`classid`_ `oid`, _`objid`_ `oid`,
_`objsubid`_ `integer` ) Returns a row containing enough information to
uniquely identify the database object specified by a type code and object name
and argument arrays. The returned values are the ones that would be used in
system catalogs such as `pg_depend`; they can be passed to other system
functions such as `pg_describe_object` or `pg_identify_object`. _`classid`_ is
the OID of the system catalog containing the object; _`objid`_ is the OID of
the object itself, and _`objsubid`_ is the sub-object ID, or zero if none.
This function is the inverse of `pg_identify_object_as_address`. Undefined
objects are identified with `NULL` values.  
  
  

### 9.26.6. Comment Information Functions #

The functions shown in [Table 9.78](functions-info.html#FUNCTIONS-INFO-
COMMENT-TABLE "Table 9.78. Comment Information Functions") extract comments
previously stored with the [COMMENT](sql-comment.html "COMMENT") command. A
null value is returned if no comment could be found for the specified
parameters.

**Table  9.78. Comment Information Functions**

Function Description  
---  
`col_description` ( _`table`_ `oid`, _`column`_ `integer` ) → `text` Returns
the comment for a table column, which is specified by the OID of its table and
its column number. (`obj_description` cannot be used for table columns, since
columns do not have OIDs of their own.)  
`obj_description` ( _`object`_ `oid`, _`catalog`_ `name` ) → `text` Returns
the comment for a database object specified by its OID and the name of the
containing system catalog. For example, `obj_description(123456, 'pg_class')`
would retrieve the comment for the table with OID 123456.  
`obj_description` ( _`object`_ `oid` ) → `text` Returns the comment for a
database object specified by its OID alone. This is _deprecated_ since there
is no guarantee that OIDs are unique across different system catalogs;
therefore, the wrong comment might be returned.  
`shobj_description` ( _`object`_ `oid`, _`catalog`_ `name` ) → `text` Returns
the comment for a shared database object specified by its OID and the name of
the containing system catalog. This is just like `obj_description` except that
it is used for retrieving comments on shared objects (that is, databases,
roles, and tablespaces). Some system catalogs are global to all databases
within each cluster, and the descriptions for objects in them are stored
globally as well.  
  
  

### 9.26.7. Data Validity Checking Functions #

The functions shown in [Table 9.79](functions-info.html#FUNCTIONS-INFO-
VALIDITY-TABLE "Table 9.79. Data Validity Checking Functions") can be helpful
for checking validity of proposed input data.

**Table  9.79. Data Validity Checking Functions**

Function Description Example(s)  
---  
`pg_input_is_valid` ( _`string`_ `text`, _`type`_ `text` ) → `boolean` Tests
whether the given _`string`_ is valid input for the specified data type,
returning true or false. This function will only work as desired if the data
type's input function has been updated to report invalid input as a “soft”
error. Otherwise, invalid input will abort the transaction, just as if the
string had been cast to the type directly. `pg_input_is_valid('42',
'integer')` → `t` `pg_input_is_valid('42000000000', 'integer')` → `f`
`pg_input_is_valid('1234.567', 'numeric(7,4)')` → `f`  
`pg_input_error_info` ( _`string`_ `text`, _`type`_ `text` ) → `record` (
_`message`_ `text`, _`detail`_ `text`, _`hint`_ `text`, _`sql_error_code`_
`text` ) Tests whether the given _`string`_ is valid input for the specified
data type; if not, return the details of the error that would have been
thrown. If the input is valid, the results are NULL. The inputs are the same
as for `pg_input_is_valid`. This function will only work as desired if the
data type's input function has been updated to report invalid input as a
“soft” error. Otherwise, invalid input will abort the transaction, just as if
the string had been cast to the type directly. `select * from
pg_input_error_info('42000000000', 'integer')` →

    
    
                           message                        | detail | hint | sql_error_code
    ------------------------------------------------------+--------+------+----------------
     value "42000000000" is out of range for type integer |        |      | 22003
    

`select message, detail from pg_input_error_info('1234.567', 'numeric(7,4)')`
→

    
    
            message         |                                      detail
    ------------------------+----------------------------------​-------------------------------------------------
     numeric field overflow | A field with precision 7, scale 4 must round to an absolute value less than 10^3.
      
  
  

### 9.26.8. Transaction ID and Snapshot Information Functions #

The functions shown in [Table 9.80](functions-info.html#FUNCTIONS-PG-SNAPSHOT
"Table 9.80. Transaction ID and Snapshot Information Functions") provide
server transaction information in an exportable form. The main use of these
functions is to determine which transactions were committed between two
snapshots.

**Table  9.80. Transaction ID and Snapshot Information Functions**

Function Description  
---  
`age` ( `xid` ) → `integer` Returns the number of transactions between the
supplied transaction id and the current transaction counter.  
`mxid_age` ( `xid` ) → `integer` Returns the number of multixacts IDs between
the supplied multixact ID and the current multixacts counter.  
`pg_current_xact_id` () → `xid8` Returns the current transaction's ID. It will
assign a new one if the current transaction does not have one already (because
it has not performed any database updates); see [Section 74.1](transaction-
id.html "74.1. Transactions and Identifiers") for details. If executed in a
subtransaction, this will return the top-level transaction ID; see [Section
74.3](subxacts.html "74.3. Subtransactions") for details.  
`pg_current_xact_id_if_assigned` () → `xid8` Returns the current transaction's
ID, or `NULL` if no ID is assigned yet. (It's best to use this variant if the
transaction might otherwise be read-only, to avoid unnecessary consumption of
an XID.) If executed in a subtransaction, this will return the top-level
transaction ID.  
`pg_xact_status` ( `xid8` ) → `text` Reports the commit status of a recent
transaction. The result is one of `in progress`, `committed`, or `aborted`,
provided that the transaction is recent enough that the system retains the
commit status of that transaction. If it is old enough that no references to
the transaction survive in the system and the commit status information has
been discarded, the result is `NULL`. Applications might use this function,
for example, to determine whether their transaction committed or aborted after
the application and database server become disconnected while a `COMMIT` is in
progress. Note that prepared transactions are reported as `in progress`;
applications must check [`pg_prepared_xacts`](view-pg-prepared-xacts.html
"54.16. pg_prepared_xacts") if they need to determine whether a transaction ID
belongs to a prepared transaction.  
`pg_current_snapshot` () → `pg_snapshot` Returns a current _snapshot_ , a data
structure showing which transaction IDs are now in-progress. Only top-level
transaction IDs are included in the snapshot; subtransaction IDs are not
shown; see [Section 74.3](subxacts.html "74.3. Subtransactions") for details.  
`pg_snapshot_xip` ( `pg_snapshot` ) → `setof xid8` Returns the set of in-
progress transaction IDs contained in a snapshot.  
`pg_snapshot_xmax` ( `pg_snapshot` ) → `xid8` Returns the `xmax` of a
snapshot.  
`pg_snapshot_xmin` ( `pg_snapshot` ) → `xid8` Returns the `xmin` of a
snapshot.  
`pg_visible_in_snapshot` ( `xid8`, `pg_snapshot` ) → `boolean` Is the given
transaction ID _visible_ according to this snapshot (that is, was it completed
before the snapshot was taken)? Note that this function will not give the
correct answer for a subtransaction ID (subxid); see [Section
74.3](subxacts.html "74.3. Subtransactions") for details.  
  
  

The internal transaction ID type `xid` is 32 bits wide and wraps around every
4 billion transactions. However, the functions shown in [Table
9.80](functions-info.html#FUNCTIONS-PG-SNAPSHOT "Table 9.80. Transaction ID
and Snapshot Information Functions"), except `age` and `mxid_age`, use a
64-bit type `xid8` that does not wrap around during the life of an
installation and can be converted to `xid` by casting if required; see
[Section 74.1](transaction-id.html "74.1. Transactions and Identifiers") for
details. The data type `pg_snapshot` stores information about transaction ID
visibility at a particular moment in time. Its components are described in
[Table 9.81](functions-info.html#FUNCTIONS-PG-SNAPSHOT-PARTS
"Table 9.81. Snapshot Components"). `pg_snapshot`'s textual representation is
`_`xmin`_ :_`xmax`_ :_`xip_list`_`. For example `10:20:10,14,15` means
`xmin=10, xmax=20, xip_list=10, 14, 15`.

**Table  9.81. Snapshot Components**

Name | Description  
---|---  
`xmin` | Lowest transaction ID that was still active. All transaction IDs less than `xmin` are either committed and visible, or rolled back and dead.  
`xmax` | One past the highest completed transaction ID. All transaction IDs greater than or equal to `xmax` had not yet completed as of the time of the snapshot, and thus are invisible.  
`xip_list` | Transactions in progress at the time of the snapshot. A transaction ID that is `xmin <= _`X`_ < xmax` and not in this list was already completed at the time of the snapshot, and thus is either visible or dead according to its commit status. This list does not include the transaction IDs of subtransactions (subxids).  
  
  

In releases of PostgreSQL before 13 there was no `xid8` type, so variants of
these functions were provided that used `bigint` to represent a 64-bit XID,
with a correspondingly distinct snapshot data type `txid_snapshot`. These
older functions have `txid` in their names. They are still supported for
backward compatibility, but may be removed from a future release. See [Table
9.82](functions-info.html#FUNCTIONS-TXID-SNAPSHOT "Table 9.82. Deprecated
Transaction ID and Snapshot Information Functions").

**Table  9.82. Deprecated Transaction ID and Snapshot Information Functions**

Function Description  
---  
`txid_current` () → `bigint` See `pg_current_xact_id()`.  
`txid_current_if_assigned` () → `bigint` See
`pg_current_xact_id_if_assigned()`.  
`txid_current_snapshot` () → `txid_snapshot` See `pg_current_snapshot()`.  
`txid_snapshot_xip` ( `txid_snapshot` ) → `setof bigint` See
`pg_snapshot_xip()`.  
`txid_snapshot_xmax` ( `txid_snapshot` ) → `bigint` See `pg_snapshot_xmax()`.  
`txid_snapshot_xmin` ( `txid_snapshot` ) → `bigint` See `pg_snapshot_xmin()`.  
`txid_visible_in_snapshot` ( `bigint`, `txid_snapshot` ) → `boolean` See
`pg_visible_in_snapshot()`.  
`txid_status` ( `bigint` ) → `text` See `pg_xact_status()`.  
  
  

### 9.26.9. Committed Transaction Information Functions #

The functions shown in [Table 9.83](functions-info.html#FUNCTIONS-COMMIT-
TIMESTAMP "Table 9.83. Committed Transaction Information Functions") provide
information about when past transactions were committed. They only provide
useful data when the [track_commit_timestamp](runtime-config-
replication.html#GUC-TRACK-COMMIT-TIMESTAMP) configuration option is enabled,
and only for transactions that were committed after it was enabled. Commit
timestamp information is routinely removed during vacuum.

**Table  9.83. Committed Transaction Information Functions**

Function Description  
---  
`pg_xact_commit_timestamp` ( `xid` ) → `timestamp with time zone` Returns the
commit timestamp of a transaction.  
`pg_xact_commit_timestamp_origin` ( `xid` ) → `record` ( _`timestamp`_
`timestamp with time zone`, _`roident`_ `oid`) Returns the commit timestamp
and replication origin of a transaction.  
`pg_last_committed_xact` () → `record` ( _`xid`_ `xid`, _`timestamp`_
`timestamp with time zone`, _`roident`_ `oid` ) Returns the transaction ID,
commit timestamp and replication origin of the latest committed transaction.  
  
  

### 9.26.10. Control Data Functions #

The functions shown in [Table 9.84](functions-info.html#FUNCTIONS-CONTROLDATA
"Table 9.84. Control Data Functions") print information initialized during
`initdb`, such as the catalog version. They also show information about write-
ahead logging and checkpoint processing. This information is cluster-wide, not
specific to any one database. These functions provide most of the same
information, from the same source, as the [pg_controldata](app-
pgcontroldata.html "pg_controldata") application.

**Table  9.84. Control Data Functions**

Function Description  
---  
`pg_control_checkpoint` () → `record` Returns information about current
checkpoint state, as shown in [Table 9.85](functions-info.html#FUNCTIONS-PG-
CONTROL-CHECKPOINT "Table 9.85. pg_control_checkpoint Output Columns").  
`pg_control_system` () → `record` Returns information about current control
file state, as shown in [Table 9.86](functions-info.html#FUNCTIONS-PG-CONTROL-
SYSTEM "Table 9.86. pg_control_system Output Columns").  
`pg_control_init` () → `record` Returns information about cluster
initialization state, as shown in [Table 9.87](functions-info.html#FUNCTIONS-
PG-CONTROL-INIT "Table 9.87. pg_control_init Output Columns").  
`pg_control_recovery` () → `record` Returns information about recovery state,
as shown in [Table 9.88](functions-info.html#FUNCTIONS-PG-CONTROL-RECOVERY
"Table 9.88. pg_control_recovery Output Columns").  
  
  

**Table  9.85. `pg_control_checkpoint` Output Columns**

Column Name | Data Type  
---|---  
`checkpoint_lsn` | `pg_lsn`  
`redo_lsn` | `pg_lsn`  
`redo_wal_file` | `text`  
`timeline_id` | `integer`  
`prev_timeline_id` | `integer`  
`full_page_writes` | `boolean`  
`next_xid` | `text`  
`next_oid` | `oid`  
`next_multixact_id` | `xid`  
`next_multi_offset` | `xid`  
`oldest_xid` | `xid`  
`oldest_xid_dbid` | `oid`  
`oldest_active_xid` | `xid`  
`oldest_multi_xid` | `xid`  
`oldest_multi_dbid` | `oid`  
`oldest_commit_ts_xid` | `xid`  
`newest_commit_ts_xid` | `xid`  
`checkpoint_time` | `timestamp with time zone`  
  
  

**Table  9.86. `pg_control_system` Output Columns**

Column Name | Data Type  
---|---  
`pg_control_version` | `integer`  
`catalog_version_no` | `integer`  
`system_identifier` | `bigint`  
`pg_control_last_modified` | `timestamp with time zone`  
  
  

**Table  9.87. `pg_control_init` Output Columns**

Column Name | Data Type  
---|---  
`max_data_alignment` | `integer`  
`database_block_size` | `integer`  
`blocks_per_segment` | `integer`  
`wal_block_size` | `integer`  
`bytes_per_wal_segment` | `integer`  
`max_identifier_length` | `integer`  
`max_index_columns` | `integer`  
`max_toast_chunk_size` | `integer`  
`large_object_chunk_size` | `integer`  
`float8_pass_by_value` | `boolean`  
`data_page_checksum_version` | `integer`  
  
  

**Table  9.88. `pg_control_recovery` Output Columns**

Column Name | Data Type  
---|---  
`min_recovery_end_lsn` | `pg_lsn`  
`min_recovery_end_timeline` | `integer`  
`backup_start_lsn` | `pg_lsn`  
`backup_end_lsn` | `pg_lsn`  
`end_of_backup_record_required` | `boolean`  
  
  

* * *

[Prev](functions-srf.html "9.25. Set Returning Functions")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](functions-admin.html "9.27. System Administration Functions")  
---|---|---  
9.25. Set Returning Functions  | [Home](index.html "PostgreSQL 16.9 Documentation") |  9.27. System Administration Functions  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-info.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

