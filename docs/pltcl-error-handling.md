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

Supported Versions: [Current](/docs/current/pltcl-error-handling.html
"PostgreSQL 17 - 44.8. Error Handling in PL/Tcl") ([17](/docs/17/pltcl-error-
handling.html "PostgreSQL 17 - 44.8. Error Handling in PL/Tcl")) /
[16](/docs/16/pltcl-error-handling.html "PostgreSQL 16 - 44.8. Error Handling
in PL/Tcl") / [15](/docs/15/pltcl-error-handling.html "PostgreSQL 15 -
44.8. Error Handling in PL/Tcl") / [14](/docs/14/pltcl-error-handling.html
"PostgreSQL 14 - 44.8. Error Handling in PL/Tcl") / [13](/docs/13/pltcl-error-
handling.html "PostgreSQL 13 - 44.8. Error Handling in PL/Tcl")

Development Versions: [18](/docs/18/pltcl-error-handling.html "PostgreSQL 18 -
44.8. Error Handling in PL/Tcl") / [devel](/docs/devel/pltcl-error-
handling.html "PostgreSQL devel - 44.8. Error Handling in PL/Tcl")

Unsupported versions: [12](/docs/12/pltcl-error-handling.html "PostgreSQL 12 -
44.8. Error Handling in PL/Tcl") / [11](/docs/11/pltcl-error-handling.html
"PostgreSQL 11 - 44.8. Error Handling in PL/Tcl") / [10](/docs/10/pltcl-error-
handling.html "PostgreSQL 10 - 44.8. Error Handling in PL/Tcl") /
[9.6](/docs/9.6/pltcl-error-handling.html "PostgreSQL 9.6 - 44.8. Error
Handling in PL/Tcl")

__

44.8. Error Handling in PL/Tcl  
---  
[Prev](pltcl-event-trigger.html "44.7. Event Trigger Functions in PL/Tcl")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") | Chapter 44. PL/Tcl — Tcl Procedural Language | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](pltcl-subtransactions.html "44.9. Explicit Subtransactions in PL/Tcl")  
  
* * *

## 44.8. Error Handling in PL/Tcl #

Tcl code within or called from a PL/Tcl function can raise an error, either by
executing some invalid operation or by generating an error using the Tcl
`error` command or PL/Tcl's `elog` command. Such errors can be caught within
Tcl using the Tcl `catch` command. If an error is not caught but is allowed to
propagate out to the top level of execution of the PL/Tcl function, it is
reported as an SQL error in the function's calling query.

Conversely, SQL errors that occur within PL/Tcl's `spi_exec`, `spi_prepare`,
and `spi_execp` commands are reported as Tcl errors, so they are catchable by
Tcl's `catch` command. (Each of these PL/Tcl commands runs its SQL operation
in a subtransaction, which is rolled back on error, so that any partially-
completed operation is automatically cleaned up.) Again, if an error
propagates out to the top level without being caught, it turns back into an
SQL error.

Tcl provides an `errorCode` variable that can represent additional information
about an error in a form that is easy for Tcl programs to interpret. The
contents are in Tcl list format, and the first word identifies the subsystem
or library reporting the error; beyond that the contents are left to the
individual subsystem or library. For database errors reported by PL/Tcl
commands, the first word is `POSTGRES`, the second word is the PostgreSQL
version number, and additional words are field name/value pairs providing
detailed information about the error. Fields `SQLSTATE`, `condition`, and
`message` are always supplied (the first two represent the error code and
condition name as shown in [Appendix A](errcodes-appendix.html
"Appendix A. PostgreSQL Error Codes")). Fields that may be present include
`detail`, `hint`, `context`, `schema`, `table`, `column`, `datatype`,
`constraint`, `statement`, `cursor_position`, `filename`, `lineno`, and
`funcname`.

A convenient way to work with PL/Tcl's `errorCode` information is to load it
into an array, so that the field names become array subscripts. Code for doing
that might look like

    
    
    if {[catch { spi_exec $sql_command }]} {
        if {[lindex $::errorCode 0] == "POSTGRES"} {
            array set errorArray $::errorCode
            if {$errorArray(condition) == "undefined_table"} {
                # deal with missing table
            } else {
                # deal with some other type of SQL error
            }
        }
    }
    

(The double colons explicitly specify that `errorCode` is a global variable.)

* * *

[Prev](pltcl-event-trigger.html "44.7. Event Trigger Functions in PL/Tcl")  | [Up](pltcl.html "Chapter 44. PL/Tcl — Tcl Procedural Language") |  [Next](pltcl-subtransactions.html "44.9. Explicit Subtransactions in PL/Tcl")  
---|---|---  
44.7. Event Trigger Functions in PL/Tcl  | [Home](index.html "PostgreSQL 16.9 Documentation") |  44.9. Explicit Subtransactions in PL/Tcl  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/pltcl-error-handling.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

