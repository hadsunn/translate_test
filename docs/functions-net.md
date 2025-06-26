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

Supported Versions: [Current](/docs/current/functions-net.html "PostgreSQL 17
- 9.12. Network Address Functions and Operators") ([17](/docs/17/functions-
net.html "PostgreSQL 17 - 9.12. Network Address Functions and Operators")) /
[16](/docs/16/functions-net.html "PostgreSQL 16 - 9.12. Network Address
Functions and Operators") / [15](/docs/15/functions-net.html "PostgreSQL 15 -
9.12. Network Address Functions and Operators") / [14](/docs/14/functions-
net.html "PostgreSQL 14 - 9.12. Network Address Functions and Operators") /
[13](/docs/13/functions-net.html "PostgreSQL 13 - 9.12. Network Address
Functions and Operators")

Development Versions: [18](/docs/18/functions-net.html "PostgreSQL 18 -
9.12. Network Address Functions and Operators") /
[devel](/docs/devel/functions-net.html "PostgreSQL devel - 9.12. Network
Address Functions and Operators")

Unsupported versions: [12](/docs/12/functions-net.html "PostgreSQL 12 -
9.12. Network Address Functions and Operators") / [11](/docs/11/functions-
net.html "PostgreSQL 11 - 9.12. Network Address Functions and Operators") /
[10](/docs/10/functions-net.html "PostgreSQL 10 - 9.12. Network Address
Functions and Operators") / [9.6](/docs/9.6/functions-net.html "PostgreSQL 9.6
- 9.12. Network Address Functions and Operators") / [9.5](/docs/9.5/functions-
net.html "PostgreSQL 9.5 - 9.12. Network Address Functions and Operators") /
[9.4](/docs/9.4/functions-net.html "PostgreSQL 9.4 - 9.12. Network Address
Functions and Operators") / [9.3](/docs/9.3/functions-net.html "PostgreSQL 9.3
- 9.12. Network Address Functions and Operators") / [9.2](/docs/9.2/functions-
net.html "PostgreSQL 9.2 - 9.12. Network Address Functions and Operators") /
[9.1](/docs/9.1/functions-net.html "PostgreSQL 9.1 - 9.12. Network Address
Functions and Operators") / [9.0](/docs/9.0/functions-net.html "PostgreSQL 9.0
- 9.12. Network Address Functions and Operators") / [8.4](/docs/8.4/functions-
net.html "PostgreSQL 8.4 - 9.12. Network Address Functions and Operators") /
[8.3](/docs/8.3/functions-net.html "PostgreSQL 8.3 - 9.12. Network Address
Functions and Operators") / [8.2](/docs/8.2/functions-net.html "PostgreSQL 8.2
- 9.12. Network Address Functions and Operators") / [8.1](/docs/8.1/functions-
net.html "PostgreSQL 8.1 - 9.12. Network Address Functions and Operators") /
[8.0](/docs/8.0/functions-net.html "PostgreSQL 8.0 - 9.12. Network Address
Functions and Operators") / [7.4](/docs/7.4/functions-net.html "PostgreSQL 7.4
- 9.12. Network Address Functions and Operators") / [7.3](/docs/7.3/functions-
net.html "PostgreSQL 7.3 - 9.12. Network Address Functions and Operators") /
[7.2](/docs/7.2/functions-net.html "PostgreSQL 7.2 - 9.12. Network Address
Functions and Operators") / [7.1](/docs/7.1/functions-net.html "PostgreSQL 7.1
- 9.12. Network Address Functions and Operators")

__

9.12. Network Address Functions and Operators  
---  
[Prev](functions-geometry.html "9.11. Geometric Functions and Operators")  | [Up](functions.html "Chapter 9. Functions and Operators") | Chapter 9. Functions and Operators | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](functions-textsearch.html "9.13. Text Search Functions and Operators")  
  
* * *

## 9.12. Network Address Functions and Operators #

The IP network address types, `cidr` and `inet`, support the usual comparison
operators shown in [Table 9.1](functions-comparison.html#FUNCTIONS-COMPARISON-
OP-TABLE "Table 9.1. Comparison Operators") as well as the specialized
operators and functions shown in [Table 9.39](functions-net.html#CIDR-INET-
OPERATORS-TABLE "Table 9.39. IP Address Operators") and [Table
9.40](functions-net.html#CIDR-INET-FUNCTIONS-TABLE "Table 9.40. IP Address
Functions").

Any `cidr` value can be cast to `inet` implicitly; therefore, the operators
and functions shown below as operating on `inet` also work on `cidr` values.
(Where there are separate functions for `inet` and `cidr`, it is because the
behavior should be different for the two cases.) Also, it is permitted to cast
an `inet` value to `cidr`. When this is done, any bits to the right of the
netmask are silently zeroed to create a valid `cidr` value.

**Table  9.39. IP Address Operators**

Operator Description Example(s)  
---  
`inet` `<<` `inet` → `boolean` Is subnet strictly contained by subnet? This
operator, and the next four, test for subnet inclusion. They consider only the
network parts of the two addresses (ignoring any bits to the right of the
netmasks) and determine whether one network is identical to or a subnet of the
other. `inet '192.168.1.5' << inet '192.168.1/24'` → `t` `inet '192.168.0.5'
<< inet '192.168.1/24'` → `f` `inet '192.168.1/24' << inet '192.168.1/24'` →
`f`  
`inet` `<<=` `inet` → `boolean` Is subnet contained by or equal to subnet?
`inet '192.168.1/24' <<= inet '192.168.1/24'` → `t`  
`inet` `>>` `inet` → `boolean` Does subnet strictly contain subnet? `inet
'192.168.1/24' >> inet '192.168.1.5'` → `t`  
`inet` `>>=` `inet` → `boolean` Does subnet contain or equal subnet? `inet
'192.168.1/24' >>= inet '192.168.1/24'` → `t`  
`inet` `&&` `inet` → `boolean` Does either subnet contain or equal the other?
`inet '192.168.1/24' && inet '192.168.1.80/28'` → `t` `inet '192.168.1/24' &&
inet '192.168.2.0/28'` → `f`  
`~` `inet` → `inet` Computes bitwise NOT. `~ inet '192.168.1.6'` →
`63.87.254.249`  
`inet` `&` `inet` → `inet` Computes bitwise AND. `inet '192.168.1.6' & inet
'0.0.0.255'` → `0.0.0.6`  
`inet` `|` `inet` → `inet` Computes bitwise OR. `inet '192.168.1.6' | inet '0.0.0.255'` → `192.168.1.255`  
`inet` `+` `bigint` → `inet` Adds an offset to an address. `inet '192.168.1.6'
+ 25` → `192.168.1.31`  
`bigint` `+` `inet` → `inet` Adds an offset to an address. `200 + inet
'::ffff:fff0:1'` → `::ffff:255.240.0.201`  
`inet` `-` `bigint` → `inet` Subtracts an offset from an address. `inet
'192.168.1.43' - 36` → `192.168.1.7`  
`inet` `-` `inet` → `bigint` Computes the difference of two addresses. `inet
'192.168.1.43' - inet '192.168.1.19'` → `24` `inet '::1' - inet '::ffff:1'` →
`-4294901760`  
  
  

**Table  9.40. IP Address Functions**

Function Description Example(s)  
---  
`abbrev` ( `inet` ) → `text` Creates an abbreviated display format as text.
(The result is the same as the `inet` output function produces; it is
“abbreviated” only in comparison to the result of an explicit cast to `text`,
which for historical reasons will never suppress the netmask part.)
`abbrev(inet '10.1.0.0/32')` → `10.1.0.0`  
`abbrev` ( `cidr` ) → `text` Creates an abbreviated display format as text.
(The abbreviation consists of dropping all-zero octets to the right of the
netmask; more examples are in [Table 8.22](datatype-net-types.html#DATATYPE-
NET-CIDR-TABLE "Table 8.22. cidr Type Input Examples").) `abbrev(cidr
'10.1.0.0/16')` → `10.1/16`  
`broadcast` ( `inet` ) → `inet` Computes the broadcast address for the
address's network. `broadcast(inet '192.168.1.5/24')` → `192.168.1.255/24`  
`family` ( `inet` ) → `integer` Returns the address's family: `4` for IPv4,
`6` for IPv6. `family(inet '::1')` → `6`  
`host` ( `inet` ) → `text` Returns the IP address as text, ignoring the
netmask. `host(inet '192.168.1.0/24')` → `192.168.1.0`  
`hostmask` ( `inet` ) → `inet` Computes the host mask for the address's
network. `hostmask(inet '192.168.23.20/30')` → `0.0.0.3`  
`inet_merge` ( `inet`, `inet` ) → `cidr` Computes the smallest network that
includes both of the given networks. `inet_merge(inet '192.168.1.5/24', inet
'192.168.2.5/24')` → `192.168.0.0/22`  
`inet_same_family` ( `inet`, `inet` ) → `boolean` Tests whether the addresses
belong to the same IP family. `inet_same_family(inet '192.168.1.5/24', inet
'::1')` → `f`  
`masklen` ( `inet` ) → `integer` Returns the netmask length in bits.
`masklen(inet '192.168.1.5/24')` → `24`  
`netmask` ( `inet` ) → `inet` Computes the network mask for the address's
network. `netmask(inet '192.168.1.5/24')` → `255.255.255.0`  
`network` ( `inet` ) → `cidr` Returns the network part of the address, zeroing
out whatever is to the right of the netmask. (This is equivalent to casting
the value to `cidr`.) `network(inet '192.168.1.5/24')` → `192.168.1.0/24`  
`set_masklen` ( `inet`, `integer` ) → `inet` Sets the netmask length for an
`inet` value. The address part does not change. `set_masklen(inet
'192.168.1.5/24', 16)` → `192.168.1.5/16`  
`set_masklen` ( `cidr`, `integer` ) → `cidr` Sets the netmask length for a
`cidr` value. Address bits to the right of the new netmask are set to zero.
`set_masklen(cidr '192.168.1.0/24', 16)` → `192.168.0.0/16`  
`text` ( `inet` ) → `text` Returns the unabbreviated IP address and netmask
length as text. (This has the same result as an explicit cast to `text`.)
`text(inet '192.168.1.5')` → `192.168.1.5/32`  
  
  

### Tip

The `abbrev`, `host`, and `text` functions are primarily intended to offer
alternative display formats for IP addresses.

The MAC address types, `macaddr` and `macaddr8`, support the usual comparison
operators shown in [Table 9.1](functions-comparison.html#FUNCTIONS-COMPARISON-
OP-TABLE "Table 9.1. Comparison Operators") as well as the specialized
functions shown in [Table 9.41](functions-net.html#MACADDR-FUNCTIONS-TABLE
"Table 9.41. MAC Address Functions"). In addition, they support the bitwise
logical operators `~`, `&` and `|` (NOT, AND and OR), just as shown above for
IP addresses.

**Table  9.41. MAC Address Functions**

Function Description Example(s)  
---  
`trunc` ( `macaddr` ) → `macaddr` Sets the last 3 bytes of the address to
zero. The remaining prefix can be associated with a particular manufacturer
(using data not included in PostgreSQL). `trunc(macaddr '12:34:56:78:90:ab')`
→ `12:34:56:00:00:00`  
`trunc` ( `macaddr8` ) → `macaddr8` Sets the last 5 bytes of the address to
zero. The remaining prefix can be associated with a particular manufacturer
(using data not included in PostgreSQL). `trunc(macaddr8
'12:34:56:78:90:ab:cd:ef')` → `12:34:56:00:00:00:00:00`  
`macaddr8_set7bit` ( `macaddr8` ) → `macaddr8` Sets the 7th bit of the address
to one, creating what is known as modified EUI-64, for inclusion in an IPv6
address. `macaddr8_set7bit(macaddr8 '00:34:56:ab:cd:ef')` →
`02:34:56:ff:fe:ab:cd:ef`  
  
  

* * *

[Prev](functions-geometry.html "9.11. Geometric Functions and Operators")  | [Up](functions.html "Chapter 9. Functions and Operators") |  [Next](functions-textsearch.html "9.13. Text Search Functions and Operators")  
---|---|---  
9.11. Geometric Functions and Operators  | [Home](index.html "PostgreSQL 16.9 Documentation") |  9.13. Text Search Functions and Operators  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/functions-net.html/) to report
a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

