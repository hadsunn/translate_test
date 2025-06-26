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

Supported Versions: [Current](/docs/current/jit-reason.html "PostgreSQL 17 -
32.1. What Is JIT compilation?") ([17](/docs/17/jit-reason.html "PostgreSQL 17
- 32.1. What Is JIT compilation?")) / [16](/docs/16/jit-reason.html
"PostgreSQL 16 - 32.1. What Is JIT compilation?") / [15](/docs/15/jit-
reason.html "PostgreSQL 15 - 32.1. What Is JIT compilation?") /
[14](/docs/14/jit-reason.html "PostgreSQL 14 - 32.1. What Is JIT
compilation?") / [13](/docs/13/jit-reason.html "PostgreSQL 13 - 32.1. What Is
JIT compilation?")

Development Versions: [18](/docs/18/jit-reason.html "PostgreSQL 18 -
32.1. What Is JIT compilation?") / [devel](/docs/devel/jit-reason.html
"PostgreSQL devel - 32.1. What Is JIT compilation?")

Unsupported versions: [12](/docs/12/jit-reason.html "PostgreSQL 12 -
32.1. What Is JIT compilation?") / [11](/docs/11/jit-reason.html "PostgreSQL
11 - 32.1. What Is JIT compilation?")

__

32.1. What Is JIT compilation?  
---  
[Prev](jit.html "Chapter 32. Just-in-Time Compilation \(JIT\)")  | [Up](jit.html "Chapter 32. Just-in-Time Compilation \(JIT\)") | Chapter 32. Just-in-Time Compilation (JIT) | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](jit-decision.html "32.2. When to JIT?")  
  
* * *

## 32.1. What Is JIT compilation? #

[32.1.1. JIT Accelerated Operations](jit-reason.html#JIT-ACCELERATED-
OPERATIONS)

[32.1.2. Inlining](jit-reason.html#JIT-INLINING)

[32.1.3. Optimization](jit-reason.html#JIT-OPTIMIZATION)

Just-in-Time (JIT) compilation is the process of turning some form of
interpreted program evaluation into a native program, and doing so at run
time. For example, instead of using general-purpose code that can evaluate
arbitrary SQL expressions to evaluate a particular SQL predicate like `WHERE
a.col = 3`, it is possible to generate a function that is specific to that
expression and can be natively executed by the CPU, yielding a speedup.

PostgreSQL has builtin support to perform JIT compilation using
[LLVM](https://llvm.org/) when PostgreSQL is built with [`--with-
llvm`](install-make.html#CONFIGURE-WITH-LLVM).

See `src/backend/jit/README` for further details.

### 32.1.1. JIT Accelerated Operations #

Currently PostgreSQL's JIT implementation has support for accelerating
expression evaluation and tuple deforming. Several other operations could be
accelerated in the future.

Expression evaluation is used to evaluate `WHERE` clauses, target lists,
aggregates and projections. It can be accelerated by generating code specific
to each case.

Tuple deforming is the process of transforming an on-disk tuple (see [Section
73.6.1](storage-page-layout.html#STORAGE-TUPLE-LAYOUT "73.6.1. Table Row
Layout")) into its in-memory representation. It can be accelerated by creating
a function specific to the table layout and the number of columns to be
extracted.

### 32.1.2. Inlining #

PostgreSQL is very extensible and allows new data types, functions, operators
and other database objects to be defined; see [Chapter 38](extend.html
"Chapter 38. Extending SQL"). In fact the built-in objects are implemented
using nearly the same mechanisms. This extensibility implies some overhead,
for example due to function calls (see [Section 38.3](xfunc.html "38.3. User-
Defined Functions")). To reduce that overhead, JIT compilation can inline the
bodies of small functions into the expressions using them. That allows a
significant percentage of the overhead to be optimized away.

### 32.1.3. Optimization #

LLVM has support for optimizing generated code. Some of the optimizations are
cheap enough to be performed whenever JIT is used, while others are only
beneficial for longer-running queries. See
<https://llvm.org/docs/Passes.html#transform-passes> for more details about
optimizations.

* * *

[Prev](jit.html "Chapter 32. Just-in-Time Compilation \(JIT\)")  | [Up](jit.html "Chapter 32. Just-in-Time Compilation \(JIT\)") |  [Next](jit-decision.html "32.2. When to JIT?")  
---|---|---  
Chapter 32. Just-in-Time Compilation (JIT)  | [Home](index.html "PostgreSQL 16.9 Documentation") |  32.2. When to JIT?  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/jit-reason.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

