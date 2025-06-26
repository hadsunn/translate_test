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

Supported Versions: [Current](/docs/current/datatype-net-types.html
"PostgreSQL 17 - 8.9. Network Address Types") ([17](/docs/17/datatype-net-
types.html "PostgreSQL 17 - 8.9. Network Address Types")) /
[16](/docs/16/datatype-net-types.html "PostgreSQL 16 - 8.9. Network Address
Types") / [15](/docs/15/datatype-net-types.html "PostgreSQL 15 - 8.9. Network
Address Types") / [14](/docs/14/datatype-net-types.html "PostgreSQL 14 -
8.9. Network Address Types") / [13](/docs/13/datatype-net-types.html
"PostgreSQL 13 - 8.9. Network Address Types")

Development Versions: [18](/docs/18/datatype-net-types.html "PostgreSQL 18 -
8.9. Network Address Types") / [devel](/docs/devel/datatype-net-types.html
"PostgreSQL devel - 8.9. Network Address Types")

Unsupported versions: [12](/docs/12/datatype-net-types.html "PostgreSQL 12 -
8.9. Network Address Types") / [11](/docs/11/datatype-net-types.html
"PostgreSQL 11 - 8.9. Network Address Types") / [10](/docs/10/datatype-net-
types.html "PostgreSQL 10 - 8.9. Network Address Types") /
[9.6](/docs/9.6/datatype-net-types.html "PostgreSQL 9.6 - 8.9. Network Address
Types") / [9.5](/docs/9.5/datatype-net-types.html "PostgreSQL 9.5 -
8.9. Network Address Types") / [9.4](/docs/9.4/datatype-net-types.html
"PostgreSQL 9.4 - 8.9. Network Address Types") / [9.3](/docs/9.3/datatype-net-
types.html "PostgreSQL 9.3 - 8.9. Network Address Types") /
[9.2](/docs/9.2/datatype-net-types.html "PostgreSQL 9.2 - 8.9. Network Address
Types") / [9.1](/docs/9.1/datatype-net-types.html "PostgreSQL 9.1 -
8.9. Network Address Types") / [9.0](/docs/9.0/datatype-net-types.html
"PostgreSQL 9.0 - 8.9. Network Address Types") / [8.4](/docs/8.4/datatype-net-
types.html "PostgreSQL 8.4 - 8.9. Network Address Types") /
[8.3](/docs/8.3/datatype-net-types.html "PostgreSQL 8.3 - 8.9. Network Address
Types") / [8.2](/docs/8.2/datatype-net-types.html "PostgreSQL 8.2 -
8.9. Network Address Types") / [8.1](/docs/8.1/datatype-net-types.html
"PostgreSQL 8.1 - 8.9. Network Address Types") / [8.0](/docs/8.0/datatype-net-
types.html "PostgreSQL 8.0 - 8.9. Network Address Types") /
[7.4](/docs/7.4/datatype-net-types.html "PostgreSQL 7.4 - 8.9. Network Address
Types") / [7.3](/docs/7.3/datatype-net-types.html "PostgreSQL 7.3 -
8.9. Network Address Types") / [7.2](/docs/7.2/datatype-net-types.html
"PostgreSQL 7.2 - 8.9. Network Address Types") / [7.1](/docs/7.1/datatype-net-
types.html "PostgreSQL 7.1 - 8.9. Network Address Types")

__

8.9. Network Address Types  
---  
[Prev](datatype-geometric.html "8.8. Geometric Types")  | [Up](datatype.html "Chapter 8. Data Types") | Chapter 8. Data Types | [Home](index.html "PostgreSQL 16.9 Documentation") |  [Next](datatype-bit.html "8.10. Bit String Types")  
  
* * *

## 8.9. Network Address Types #

[8.9.1. `inet`](datatype-net-types.html#DATATYPE-INET)

[8.9.2. `cidr`](datatype-net-types.html#DATATYPE-CIDR)

[8.9.3. `inet` vs. `cidr`](datatype-net-types.html#DATATYPE-INET-VS-CIDR)

[8.9.4. `macaddr`](datatype-net-types.html#DATATYPE-MACADDR)

[8.9.5. `macaddr8`](datatype-net-types.html#DATATYPE-MACADDR8)

PostgreSQL offers data types to store IPv4, IPv6, and MAC addresses, as shown
in [Table 8.21](datatype-net-types.html#DATATYPE-NET-TYPES-TABLE
"Table 8.21. Network Address Types"). It is better to use these types instead
of plain text types to store network addresses, because these types offer
input error checking and specialized operators and functions (see [Section
9.12](functions-net.html "9.12. Network Address Functions and Operators")).

**Table  8.21. Network Address Types**

Name | Storage Size | Description  
---|---|---  
`cidr` | 7 or 19 bytes | IPv4 and IPv6 networks  
`inet` | 7 or 19 bytes | IPv4 and IPv6 hosts and networks  
`macaddr` | 6 bytes | MAC addresses  
`macaddr8` | 8 bytes | MAC addresses (EUI-64 format)  
  
  

When sorting `inet` or `cidr` data types, IPv4 addresses will always sort
before IPv6 addresses, including IPv4 addresses encapsulated or mapped to IPv6
addresses, such as ::10.2.3.4 or ::ffff:10.4.3.2.

### 8.9.1. `inet` #

The `inet` type holds an IPv4 or IPv6 host address, and optionally its subnet,
all in one field. The subnet is represented by the number of network address
bits present in the host address (the “netmask”). If the netmask is 32 and the
address is IPv4, then the value does not indicate a subnet, only a single
host. In IPv6, the address length is 128 bits, so 128 bits specify a unique
host address. Note that if you want to accept only networks, you should use
the `cidr` type rather than `inet`.

The input format for this type is _`address/y`_ where _`address`_ is an IPv4
or IPv6 address and _`y`_ is the number of bits in the netmask. If the _`/y`_
portion is omitted, the netmask is taken to be 32 for IPv4 or 128 for IPv6, so
the value represents just a single host. On display, the _`/y`_ portion is
suppressed if the netmask specifies a single host.

### 8.9.2. `cidr` #

The `cidr` type holds an IPv4 or IPv6 network specification. Input and output
formats follow Classless Internet Domain Routing conventions. The format for
specifying networks is _`address/y`_ where _`address`_ is the network's lowest
address represented as an IPv4 or IPv6 address, and _`y`_ is the number of
bits in the netmask. If _`y`_ is omitted, it is calculated using assumptions
from the older classful network numbering system, except it will be at least
large enough to include all of the octets written in the input. It is an error
to specify a network address that has bits set to the right of the specified
netmask.

[Table 8.22](datatype-net-types.html#DATATYPE-NET-CIDR-TABLE "Table 8.22. cidr
Type Input Examples") shows some examples.

**Table  8.22. `cidr` Type Input Examples**

`cidr` Input | `cidr` Output | ``abbrev(`cidr`)``  
---|---|---  
192.168.100.128/25 | 192.168.100.128/25 | 192.168.100.128/25  
192.168/24 | 192.168.0.0/24 | 192.168.0/24  
192.168/25 | 192.168.0.0/25 | 192.168.0.0/25  
192.168.1 | 192.168.1.0/24 | 192.168.1/24  
192.168 | 192.168.0.0/24 | 192.168.0/24  
128.1 | 128.1.0.0/16 | 128.1/16  
128 | 128.0.0.0/16 | 128.0/16  
128.1.2 | 128.1.2.0/24 | 128.1.2/24  
10.1.2 | 10.1.2.0/24 | 10.1.2/24  
10.1 | 10.1.0.0/16 | 10.1/16  
10 | 10.0.0.0/8 | 10/8  
10.1.2.3/32 | 10.1.2.3/32 | 10.1.2.3/32  
2001:4f8:3:ba::/64 | 2001:4f8:3:ba::/64 | 2001:4f8:3:ba/64  
2001:4f8:3:ba:​2e0:81ff:fe22:d1f1/128 | 2001:4f8:3:ba:​2e0:81ff:fe22:d1f1/128 | 2001:4f8:3:ba:​2e0:81ff:fe22:d1f1/128  
::ffff:1.2.3.0/120 | ::ffff:1.2.3.0/120 | ::ffff:1.2.3/120  
::ffff:1.2.3.0/128 | ::ffff:1.2.3.0/128 | ::ffff:1.2.3.0/128  
  
  

### 8.9.3. `inet` vs. `cidr` #

The essential difference between `inet` and `cidr` data types is that `inet`
accepts values with nonzero bits to the right of the netmask, whereas `cidr`
does not. For example, `192.168.0.1/24` is valid for `inet` but not for
`cidr`.

### Tip

If you do not like the output format for `inet` or `cidr` values, try the
functions `host`, `text`, and `abbrev`.

### 8.9.4. `macaddr` #

The `macaddr` type stores MAC addresses, known for example from Ethernet card
hardware addresses (although MAC addresses are used for other purposes as
well). Input is accepted in the following formats:

`'08:00:2b:01:02:03'`  
---  
`'08-00-2b-01-02-03'`  
`'08002b:010203'`  
`'08002b-010203'`  
`'0800.2b01.0203'`  
`'0800-2b01-0203'`  
`'08002b010203'`  
  
These examples all specify the same address. Upper and lower case is accepted
for the digits `a` through `f`. Output is always in the first of the forms
shown.

IEEE Standard 802-2001 specifies the second form shown (with hyphens) as the
canonical form for MAC addresses, and specifies the first form (with colons)
as used with bit-reversed, MSB-first notation, so that 08-00-2b-01-02-03 =
10:00:D4:80:40:C0. This convention is widely ignored nowadays, and it is
relevant only for obsolete network protocols (such as Token Ring). PostgreSQL
makes no provisions for bit reversal; all accepted formats use the canonical
LSB order.

The remaining five input formats are not part of any standard.

### 8.9.5. `macaddr8` #

The `macaddr8` type stores MAC addresses in EUI-64 format, known for example
from Ethernet card hardware addresses (although MAC addresses are used for
other purposes as well). This type can accept both 6 and 8 byte length MAC
addresses and stores them in 8 byte length format. MAC addresses given in 6
byte format will be stored in 8 byte length format with the 4th and 5th bytes
set to FF and FE, respectively. Note that IPv6 uses a modified EUI-64 format
where the 7th bit should be set to one after the conversion from EUI-48. The
function `macaddr8_set7bit` is provided to make this change. Generally
speaking, any input which is comprised of pairs of hex digits (on byte
boundaries), optionally separated consistently by one of `':'`, `'-'` or
`'.'`, is accepted. The number of hex digits must be either 16 (8 bytes) or 12
(6 bytes). Leading and trailing whitespace is ignored. The following are
examples of input formats that are accepted:

`'08:00:2b:01:02:03:04:05'`  
---  
`'08-00-2b-01-02-03-04-05'`  
`'08002b:0102030405'`  
`'08002b-0102030405'`  
`'0800.2b01.0203.0405'`  
`'0800-2b01-0203-0405'`  
`'08002b01:02030405'`  
`'08002b0102030405'`  
  
These examples all specify the same address. Upper and lower case is accepted
for the digits `a` through `f`. Output is always in the first of the forms
shown.

The last six input formats shown above are not part of any standard.

To convert a traditional 48 bit MAC address in EUI-48 format to modified
EUI-64 format to be included as the host portion of an IPv6 address, use
`macaddr8_set7bit` as shown:

    
    
    SELECT macaddr8_set7bit('08:00:2b:01:02:03');
    
        macaddr8_set7bit
    -------------------------
     0a:00:2b:ff:fe:01:02:03
    (1 row)
    
    

* * *

[Prev](datatype-geometric.html "8.8. Geometric Types")  | [Up](datatype.html "Chapter 8. Data Types") |  [Next](datatype-bit.html "8.10. Bit String Types")  
---|---|---  
8.8. Geometric Types  | [Home](index.html "PostgreSQL 16.9 Documentation") |  8.10. Bit String Types  
  
## Submit correction

If you see anything in the documentation that is not correct, does not match
your experience with the particular feature or requires further clarification,
please use [this form](/account/comments/new/16/datatype-net-types.html/) to
report a documentation issue.

[Privacy Policy](/about/privacypolicy) | [Code of Conduct](/about/policies/coc/) | [About PostgreSQL](/about/) | [Contact](/about/contact/)  

Copyright (C) 1996-2025 The PostgreSQL Global Development Group

