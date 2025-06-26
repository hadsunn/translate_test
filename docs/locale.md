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

Supported Versions: [Current](/docs/current/locale.html "PostgreSQL 17 -
24.1. Locale Support") ([17](/docs/17/locale.html "PostgreSQL 17 -
24.1. Locale Support")) / [16](/docs/16/locale.html "PostgreSQL 16 -
24.1. Locale Support") / [15](/docs/15/locale.html "PostgreSQL 15 -
24.1. Locale Support") / [14](/docs/14/locale.html "PostgreSQL 14 -
24.1. Locale Support") / [13](/docs/13/locale.html "PostgreSQL 13 -
24.1. Locale Support")

Development Versions: [18](/docs/18/locale.html "PostgreSQL 18 - 24.1. Locale
Support") / [devel](/docs/devel/locale.html "PostgreSQL devel - 24.1. Locale
Support")

Unsupported versions: [12](/docs/12/locale.html "PostgreSQL 12 - 24.1. Locale
Support") / [11](/docs/11/locale.html "PostgreSQL 11 - 24.1. Locale Support")
/ [10](/docs/10/locale.html "PostgreSQL 10 - 24.1. Locale Support") /
[9.6](/docs/9.6/locale.html "PostgreSQL 9.6 - 24.1. Locale Support") /
[9.5](/docs/9.5/locale.html "PostgreSQL 9.5 - 24.1. Locale Support") /
[9.4](/docs/9.4/locale.html "PostgreSQL 9.4 - 24.1. Locale Support") /
[9.3](/docs/9.3/locale.html "PostgreSQL 9.3 - 24.1. Locale Support") /
[9.2](/docs/9.2/locale.html "PostgreSQL 9.2 - 24.1. Locale Support") /
[9.1](/docs/9.1/locale.html "PostgreSQL 9.1 - 24.1. Locale Support") /
[9.0](/docs/9.0/locale.html "PostgreSQL 9.0 - 24.1. Locale Support") /
[8.4](/docs/8.4/locale.html "PostgreSQL 8.4 - 24.1. Locale Support") /
[8.3](/docs/8.3/locale.html "PostgreSQL 8.3 - 24.1. Locale Support") /
[8.2](/docs/8.2/locale.html "PostgreSQL 8.2 - 24.1. Locale Support")

__

24.1. Locale Support  
---  
[Prev](charset.html "Chapter 24. Localization")  | [Up](charset.html "Chapter 24. Localization") | Chapter 24. Localization | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](collation.html "24.2. Collation Support")  
  
* * *

## 24.1. Locale Support #

[24.1.1. Overview](locale.html#LOCALE-OVERVIEW)

[24.1.2. Behavior](locale.html#LOCALE-BEHAVIOR)

[24.1.3. Selecting Locales](locale.html#LOCALE-SELECTING-LOCALES)

[24.1.4. Locale Providers](locale.html#LOCALE-PROVIDERS)

[24.1.5. ICU Locales](locale.html#ICU-LOCALES)

[24.1.6. Problems](locale.html#LOCALE-PROBLEMS)

_Locale_ support refers to an application respecting cultural preferences
regarding alphabets, sorting, number formatting, etc. PostgreSQL uses the
standard ISO C and POSIX locale facilities provided by the server operating
system. For additional information refer to the documentation of your system.

### 24.1.1. Overview #

Locale support is automatically initialized when a database cluster is created
using `initdb`. `initdb` will initialize the database cluster with the locale
setting of its execution environment by default, so if your system is already
set to use the locale that you want in your database cluster then there is
nothing else you need to do. If you want to use a different locale (or you are
not sure which locale your system is set to), you can instruct `initdb`
exactly which locale to use by specifying the `--locale` option. For example:

    
    
    initdb --locale=sv_SE
    

This example for Unix systems sets the locale to Swedish (`sv`) as spoken in
Sweden (`SE`). Other possibilities might include `en_US` (U.S. English) and
`fr_CA` (French Canadian). If more than one character set can be used for a
locale then the specifications can take the form
_`language_territory.codeset`_. For example, `fr_BE.UTF-8` represents the
French language (fr) as spoken in Belgium (BE), with a UTF-8 character set
encoding.

What locales are available on your system under what names depends on what was
provided by the operating system vendor and what was installed. On most Unix
systems, the command `locale -a` will provide a list of available locales.
Windows uses more verbose locale names, such as `German_Germany` or
`Swedish_Sweden.1252`, but the principles are the same.

Occasionally it is useful to mix rules from several locales, e.g., use English
collation rules but Spanish messages. To support that, a set of locale
subcategories exist that control only certain aspects of the localization
rules:

`LC_COLLATE` | String sort order  
---|---  
`LC_CTYPE` | Character classification (What is a letter? Its upper-case equivalent?)  
`LC_MESSAGES` | Language of messages  
`LC_MONETARY` | Formatting of currency amounts  
`LC_NUMERIC` | Formatting of numbers  
`LC_TIME` | Formatting of dates and times  
  
The category names translate into names of `initdb` options to override the
locale choice for a specific category. For instance, to set the locale to
French Canadian, but use U.S. rules for formatting currency, use `initdb
--locale=fr_CA --lc-monetary=en_US`.

If you want the system to behave as if it had no locale support, use the
special locale name `C`, or equivalently `POSIX`.

Some locale categories must have their values fixed when the database is
created. You can use different settings for different databases, but once a
database is created, you cannot change them for that database anymore.
`LC_COLLATE` and `LC_CTYPE` are these categories. They affect the sort order
of indexes, so they must be kept fixed, or indexes on text columns would
become corrupt. (But you can alleviate this restriction using collations, as
discussed in [Section 24.2](collation.html "24.2. Collation Support").) The
default values for these categories are determined when `initdb` is run, and
those values are used when new databases are created, unless specified
otherwise in the `CREATE DATABASE` command.

The other locale categories can be changed whenever desired by setting the
server configuration parameters that have the same name as the locale
categories (see [Section 20.11.2](runtime-config-client.html#RUNTIME-CONFIG-
CLIENT-FORMAT "20.11.2. Locale and Formatting") for details). The values that
are chosen by `initdb` are actually only written into the configuration file
`postgresql.conf` to serve as defaults when the server is started. If you
remove these assignments from `postgresql.conf` then the server will inherit
the settings from its execution environment.

Note that the locale behavior of the server is determined by the environment
variables seen by the server, not by the environment of any client. Therefore,
be careful to configure the correct locale settings before starting the
server. A consequence of this is that if client and server are set up in
different locales, messages might appear in different languages depending on
where they originated.

### Note

When we speak of inheriting the locale from the execution environment, this
means the following on most operating systems: For a given locale category,
say the collation, the following environment variables are consulted in this
order until one is found to be set: `LC_ALL`, `LC_COLLATE` (or the variable
corresponding to the respective category), `LANG`. If none of these
environment variables are set then the locale defaults to `C`.

Some message localization libraries also look at the environment variable
`LANGUAGE` which overrides all other locale settings for the purpose of
setting the language of messages. If in doubt, please refer to the
documentation of your operating system, in particular the documentation about
gettext.

To enable messages to be translated to the user's preferred language, NLS must
have been selected at build time (`configure --enable-nls`). All other locale
support is built in automatically.

### 24.1.2. Behavior #

The locale settings influence the following SQL features:

  * Sort order in queries using `ORDER BY` or the standard comparison operators on textual data 

  * The `upper`, `lower`, and `initcap` functions 

  * Pattern matching operators (`LIKE`, `SIMILAR TO`, and POSIX-style regular expressions); locales affect both case insensitive matching and the classification of characters by character-class regular expressions 

  * The `to_char` family of functions 

  * The ability to use indexes with `LIKE` clauses

The drawback of using locales other than `C` or `POSIX` in PostgreSQL is its
performance impact. It slows character handling and prevents ordinary indexes
from being used by `LIKE`. For this reason use locales only if you actually
need them.

As a workaround to allow PostgreSQL to use indexes with `LIKE` clauses under a
non-C locale, several custom operator classes exist. These allow the creation
of an index that performs a strict character-by-character comparison, ignoring
locale comparison rules. Refer to [Section 11.10](indexes-opclass.html
"11.10. Operator Classes and Operator Families") for more information. Another
approach is to create indexes using the `C` collation, as discussed in
[Section 24.2](collation.html "24.2. Collation Support").

### 24.1.3. Selecting Locales #

Locales can be selected in different scopes depending on requirements. The
above overview showed how locales are specified using `initdb` to set the
defaults for the entire cluster. The following list shows where locales can be
selected. Each item provides the defaults for the subsequent items, and each
lower item allows overriding the defaults on a finer granularity.

  1. As explained above, the environment of the operating system provides the defaults for the locales of a newly initialized database cluster. In many cases, this is enough: If the operating system is configured for the desired language/territory, then PostgreSQL will by default also behave according to that locale.

  2. As shown above, command-line options for `initdb` specify the locale settings for a newly initialized database cluster. Use this if the operating system does not have the locale configuration you want for your database system.

  3. A locale can be selected separately for each database. The SQL command `CREATE DATABASE` and its command-line equivalent `createdb` have options for that. Use this for example if a database cluster houses databases for multiple tenants with different requirements.

  4. Locale settings can be made for individual table columns. This uses an SQL object called _collation_ and is explained in [Section 24.2](collation.html "24.2. Collation Support"). Use this for example to sort data in different languages or customize the sort order of a particular table.

  5. Finally, locales can be selected for an individual query. Again, this uses SQL collation objects. This could be used to change the sort order based on run-time choices or for ad-hoc experimentation.

### 24.1.4. Locale Providers #

PostgreSQL supports multiple _locale providers_. This specifies which library
supplies the locale data. One standard provider name is `libc`, which uses the
locales provided by the operating system C library. These are the locales used
by most tools provided by the operating system. Another provider is `icu`,
which uses the external ICU library. ICU locales can only be used if support
for ICU was configured when PostgreSQL was built.

The commands and tools that select the locale settings, as described above,
each have an option to select the locale provider. The examples shown earlier
all use the `libc` provider, which is the default. Here is an example to
initialize a database cluster using the ICU provider:

    
    
    initdb --locale-provider=icu --icu-locale=en
    

See the description of the respective commands and programs for details. Note
that you can mix locale providers at different granularities, for example use
`libc` by default for the cluster but have one database that uses the `icu`
provider, and then have collation objects using either provider within those
databases.

Which locale provider to use depends on individual requirements. For most
basic uses, either provider will give adequate results. For the libc provider,
it depends on what the operating system offers; some operating systems are
better than others. For advanced uses, ICU offers more locale variants and
customization options.

### 24.1.5. ICU Locales #

#### 24.1.5.1. ICU Locale Names #

The ICU format for the locale name is a [Language Tag](locale.html#ICU-
LANGUAGE-TAG "24.1.5.3. Language Tag").

    
    
    CREATE COLLATION mycollation1 (provider = icu, locale = 'ja-JP');
    CREATE COLLATION mycollation2 (provider = icu, locale = 'fr');
    

#### 24.1.5.2. Locale Canonicalization and Validation #

When defining a new ICU collation object or database with ICU as the provider,
the given locale name is transformed ("canonicalized") into a language tag if
not already in that form. For instance,

    
    
    CREATE COLLATION mycollation3 (provider = icu, locale = 'en-US-u-kn-true');
    NOTICE:  using standard form "en-US-u-kn" for locale "en-US-u-kn-true"
    CREATE COLLATION mycollation4 (provider = icu, locale = 'de_DE.utf8');
    NOTICE:  using standard form "de-DE" for locale "de_DE.utf8"
    

If you see this notice, ensure that the `provider` and `locale` are the
expected result. For consistent results when using the ICU provider, specify
the canonical [language tag](locale.html#ICU-LANGUAGE-TAG "24.1.5.3. Language
Tag") instead of relying on the transformation.

A locale with no language name, or the special language name `root`, is
transformed to have the language `und` ("undefined").

ICU can transform most libc locale names, as well as some other formats, into
language tags for easier transition to ICU. If a libc locale name is used in
ICU, it may not have precisely the same behavior as in libc.

If there is a problem interpreting the locale name, or if the locale name
represents a language or region that ICU does not recognize, you will see the
following warning:

    
    
    CREATE COLLATION nonsense (provider = icu, locale = 'nonsense');
    WARNING:  ICU locale "nonsense" has unknown language "nonsense"
    HINT:  To disable ICU locale validation, set parameter icu_validation_level to DISABLED.
    CREATE COLLATION
    

[icu_validation_level](runtime-config-client.html#GUC-ICU-VALIDATION-LEVEL)
controls how the message is reported. Unless set to `ERROR`, the collation
will still be created, but the behavior may not be what the user intended.

#### 24.1.5.3. Language Tag #

A language tag, defined in BCP 47, is a standardized identifier used to
identify languages, regions, and other information about a locale.

Basic language tags are simply _`language`_`-`_`region`_ ; or even just
_`language`_. The _`language`_ is a language code (e.g. `fr` for French), and
_`region`_ is a region code (e.g. `CA` for Canada). Examples: `ja-JP`, `de`,
or `fr-CA`.

Collation settings may be included in the language tag to customize collation
behavior. ICU allows extensive customization, such as sensitivity (or
insensitivity) to accents, case, and punctuation; treatment of digits within
text; and many other options to satisfy a variety of uses.

To include this additional collation information in a language tag, append
`-u`, which indicates there are additional collation settings, followed by one
or more `-`_`key`_`-`_`value`_ pairs. The _`key`_ is the key for a [collation
setting](collation.html#ICU-COLLATION-SETTINGS "24.2.3.2. Collation Settings
for an ICU Locale") and _`value`_ is a valid value for that setting. For
boolean settings, the `-`_`key`_ may be specified without a corresponding
`-`_`value`_ , which implies a value of `true`.

For example, the language tag `en-US-u-kn-ks-level2` means the locale with the
English language in the US region, with collation settings `kn` set to `true`
and `ks` set to `level2`. Those settings mean the collation will be case-
insensitive and treat a sequence of digits as a single number:

    
    
    CREATE COLLATION mycollation5 (provider = icu, deterministic = false, locale = 'en-US-u-kn-ks-level2');
    SELECT 'aB' = 'Ab' COLLATE mycollation5 as result;
     result
    --------
     t
    (1 row)
    
    SELECT 'N-45' < 'N-123' COLLATE mycollation5 as result;
     result
    --------
     t
    (1 row)
    

See [Section 24.2.3](collation.html#ICU-CUSTOM-COLLATIONS "24.2.3. ICU Custom
Collations") for details and additional examples of using language tags with
custom collation information for the locale.

### 24.1.6. Problems #

If locale support doesn't work according to the explanation above, check that
the locale support in your operating system is correctly configured. To check
what locales are installed on your system, you can use the command `locale -a`
if your operating system provides it.

Check that PostgreSQL is actually using the locale that you think it is. The
`LC_COLLATE` and `LC_CTYPE` settings are determined when a database is
created, and cannot be changed except by creating a new database. Other locale
settings including `LC_MESSAGES` and `LC_MONETARY` are initially determined by
the environment the server is started in, but can be changed on-the-fly. You
can check the active locale settings using the `SHOW` command.

The directory `src/test/locale` in the source distribution contains a test
suite for PostgreSQL's locale support.

Client applications that handle server-side errors by parsing the text of the
error message will obviously have problems when the server's messages are in a
different language. Authors of such applications are advised to make use of
the error code scheme instead.

Maintaining catalogs of message translations requires the on-going efforts of
many volunteers that want to see PostgreSQL speak their preferred language
well. If messages in your language are currently not available or not fully
translated, your assistance would be appreciated. If you want to help, refer
to [Chapter 57](nls.html "Chapter 57. Native Language Support") or write to
the developers' mailing list.

* * *

[Prev](charset.html "Chapter 24. Localization")  | [Up](charset.html "Chapter 24. Localization") |  [Next](collation.html "24.2. Collation Support")  
---|---|---  
Chapter 24. Localization  | [Home](index.html "PostgreSQL 16.9 Documentation") |  24.2. Collation Support  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/locale.html/) to report a
documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

