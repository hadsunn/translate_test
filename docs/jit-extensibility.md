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

Supported Versions: [Current](/docs/current/jit-extensibility.html "PostgreSQL
17 - 32.4. Extensibility") ([17](/docs/17/jit-extensibility.html "PostgreSQL
17 - 32.4. Extensibility")) / [16](/docs/16/jit-extensibility.html "PostgreSQL
16 - 32.4. Extensibility") / [15](/docs/15/jit-extensibility.html "PostgreSQL
15 - 32.4. Extensibility") / [14](/docs/14/jit-extensibility.html "PostgreSQL
14 - 32.4. Extensibility") / [13](/docs/13/jit-extensibility.html "PostgreSQL
13 - 32.4. Extensibility")

Development Versions: [18](/docs/18/jit-extensibility.html "PostgreSQL 18 -
32.4. Extensibility") / [devel](/docs/devel/jit-extensibility.html "PostgreSQL
devel - 32.4. Extensibility")

Unsupported versions: [12](/docs/12/jit-extensibility.html "PostgreSQL 12 -
32.4. Extensibility") / [11](/docs/11/jit-extensibility.html "PostgreSQL 11 -
32.4. Extensibility")

__

32.4. Extensibility  
---  
[Prev](jit-configuration.html "32.3. Configuration")  | [Up](jit.html "Chapter 32. Just-in-Time Compilation \(JIT\)") | Chapter 32. Just-in-Time Compilation (JIT) | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](regress.html "Chapter 33. Regression Tests")  
  
* * *

## 32.4. Extensibility #

[32.4.1. Inlining Support for Extensions](jit-extensibility.html#JIT-
EXTENSIBILITY-BITCODE)

[32.4.2. Pluggable JIT Providers](jit-extensibility.html#JIT-PLUGGABLE)

### 32.4.1. Inlining Support for Extensions #

PostgreSQL's JIT implementation can inline the bodies of functions of types
`C` and `internal`, as well as operators based on such functions. To do so for
functions in extensions, the definitions of those functions need to be made
available. When using [PGXS](extend-pgxs.html "38.18. Extension Building
Infrastructure") to build an extension against a server that has been compiled
with LLVM JIT support, the relevant files will be built and installed
automatically.

The relevant files have to be installed into `$pkglibdir/bitcode/$extension/`
and a summary of them into `$pkglibdir/bitcode/$extension.index.bc`, where
`$pkglibdir` is the directory returned by `pg_config --pkglibdir` and
`$extension` is the base name of the extension's shared library.

### Note

For functions built into PostgreSQL itself, the bitcode is installed into
`$pkglibdir/bitcode/postgres`.

### 32.4.2. Pluggable JIT Providers #

PostgreSQL provides a JIT implementation based on LLVM. The interface to the
JIT provider is pluggable and the provider can be changed without recompiling
(although currently, the build process only provides inlining support data for
LLVM). The active provider is chosen via the setting [jit_provider](runtime-
config-client.html#GUC-JIT-PROVIDER).

#### 32.4.2.1. JIT Provider Interface #

A JIT provider is loaded by dynamically loading the named shared library. The
normal library search path is used to locate the library. To provide the
required JIT provider callbacks and to indicate that the library is actually a
JIT provider, it needs to provide a C function named `_PG_jit_provider_init`.
This function is passed a struct that needs to be filled with the callback
function pointers for individual actions:

    
    
    struct JitProviderCallbacks
    {
        JitProviderResetAfterErrorCB reset_after_error;
        JitProviderReleaseContextCB release_context;
        JitProviderCompileExprCB compile_expr;
    };
    
    extern void _PG_jit_provider_init(JitProviderCallbacks *cb);
    

* * *

[Prev](jit-configuration.html "32.3. Configuration")  | [Up](jit.html "Chapter 32. Just-in-Time Compilation \(JIT\)") |  [Next](regress.html "Chapter 33. Regression Tests")  
---|---|---  
32.3. Configuration  | [Home](index.html "PostgreSQL 16.9 Documentation") |  Chapter 33. Regression Tests  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/jit-extensibility.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

