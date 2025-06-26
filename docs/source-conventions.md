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

Supported Versions: [Current](/docs/current/source-conventions.html
"PostgreSQL 17 - 56.4. Miscellaneous Coding Conventions")
([17](/docs/17/source-conventions.html "PostgreSQL 17 - 56.4. Miscellaneous
Coding Conventions")) / [16](/docs/16/source-conventions.html "PostgreSQL 16 -
56.4. Miscellaneous Coding Conventions") / [15](/docs/15/source-
conventions.html "PostgreSQL 15 - 56.4. Miscellaneous Coding Conventions") /
[14](/docs/14/source-conventions.html "PostgreSQL 14 - 56.4. Miscellaneous
Coding Conventions") / [13](/docs/13/source-conventions.html "PostgreSQL 13 -
56.4. Miscellaneous Coding Conventions")

Development Versions: [18](/docs/18/source-conventions.html "PostgreSQL 18 -
56.4. Miscellaneous Coding Conventions") / [devel](/docs/devel/source-
conventions.html "PostgreSQL devel - 56.4. Miscellaneous Coding Conventions")

Unsupported versions: [12](/docs/12/source-conventions.html "PostgreSQL 12 -
56.4. Miscellaneous Coding Conventions") / [11](/docs/11/source-
conventions.html "PostgreSQL 11 - 56.4. Miscellaneous Coding Conventions") /
[10](/docs/10/source-conventions.html "PostgreSQL 10 - 56.4. Miscellaneous
Coding Conventions") / [9.6](/docs/9.6/source-conventions.html "PostgreSQL 9.6
- 56.4. Miscellaneous Coding Conventions")

__

56.4. Miscellaneous Coding Conventions  
---  
[Prev](error-style-guide.html "56.3. Error Message Style Guide")  | [Up](source.html "Chapter 56. PostgreSQL Coding Conventions") | Chapter 56. PostgreSQL Coding Conventions | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](nls.html "Chapter 57. Native Language Support")  
  
* * *

## 56.4. Miscellaneous Coding Conventions #

### C Standard #

Code in PostgreSQL should only rely on language features available in the C99
standard. That means a conforming C99 compiler has to be able to compile
postgres, at least aside from a few platform dependent pieces.

A few features included in the C99 standard are, at this time, not permitted
to be used in core PostgreSQL code. This currently includes variable length
arrays, intermingled declarations and code, `//` comments, universal character
names. Reasons for that include portability and historical practices.

Features from later revisions of the C standard or compiler specific features
can be used, if a fallback is provided.

For example `_Static_assert()` and `__builtin_constant_p` are currently used,
even though they are from newer revisions of the C standard and a GCC
extension respectively. If not available we respectively fall back to using a
C99 compatible replacement that performs the same checks, but emits rather
cryptic messages and do not use `__builtin_constant_p`.

### Function-Like Macros and Inline Functions #

Both macros with arguments and `static inline` functions may be used. The
latter are preferable if there are multiple-evaluation hazards when written as
a macro, as e.g., the case with

    
    
    #define Max(x, y)       ((x) > (y) ? (x) : (y))
    

or when the macro would be very long. In other cases it's only possible to use
macros, or at least easier. For example because expressions of various types
need to be passed to the macro.

When the definition of an inline function references symbols (i.e., variables,
functions) that are only available as part of the backend, the function may
not be visible when included from frontend code.

    
    
    #ifndef FRONTEND
    static inline MemoryContext
    MemoryContextSwitchTo(MemoryContext context)
    {
        MemoryContext old = CurrentMemoryContext;
    
        CurrentMemoryContext = context;
        return old;
    }
    #endif   /* FRONTEND */
    

In this example `CurrentMemoryContext`, which is only available in the
backend, is referenced and the function thus hidden with a `#ifndef FRONTEND`.
This rule exists because some compilers emit references to symbols contained
in inline functions even if the function is not used.

### Writing Signal Handlers #

To be suitable to run inside a signal handler code has to be written very
carefully. The fundamental problem is that, unless blocked, a signal handler
can interrupt code at any time. If code inside the signal handler uses the
same state as code outside chaos may ensue. As an example consider what
happens if a signal handler tries to acquire a lock that's already held in the
interrupted code.

Barring special arrangements code in signal handlers may only call async-
signal safe functions (as defined in POSIX) and access variables of type
`volatile sig_atomic_t`. A few functions in `postgres` are also deemed signal
safe, importantly `SetLatch()`.

In most cases signal handlers should do nothing more than note that a signal
has arrived, and wake up code running outside of the handler using a latch. An
example of such a handler is the following:

    
    
    static void
    handle_sighup(SIGNAL_ARGS)
    {
        int         save_errno = errno;
    
        got_SIGHUP = true;
        SetLatch(MyLatch);
    
        errno = save_errno;
    }
    

`errno` is saved and restored because `SetLatch()` might change it. If that
were not done interrupted code that's currently inspecting `errno` might see
the wrong value.

### Calling Function Pointers #

For clarity, it is preferred to explicitly dereference a function pointer when
calling the pointed-to function if the pointer is a simple variable, for
example:

    
    
    (*emit_log_hook) (edata);
    

(even though `emit_log_hook(edata)` would also work). When the function
pointer is part of a structure, then the extra punctuation can and usually
should be omitted, for example:

    
    
    paramInfo->paramFetch(paramInfo, paramId);
    

* * *

[Prev](error-style-guide.html "56.3. Error Message Style Guide")  | [Up](source.html "Chapter 56. PostgreSQL Coding Conventions") |  [Next](nls.html "Chapter 57. Native Language Support")  
---|---|---  
56.3. Error Message Style Guide  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 57. Native Language Support  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/source-conventions.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

