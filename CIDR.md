---
title : CIDR
notetype : feed
date : 07-11-2021
---

CIDR (Classless Inter-Domain Routing) notation can be used to represent a range of IP addresses. It has two parts:
- prefix - Network address (a normal IP address)
- suffix - number of bits of the network address provided in the prefix

An example cidr block looks like this: `192.0.2.0/24`

Since ipv4 network address has 32 bits, specifying an address with the suffix 32 (e.g. `189.120.95.72/32`) will describe that exact ip address - `189.120.95.72`

With prefix 24 (`189.120.95.72/24`), first 24 bits of the address are kept static, while the last 8 bits show the actual range of addresses represented by this CIDR block. In other words, this will represent all the addresses from `189.120.95.0` to `189.120.95.255`.

Similarily with prefix 16 (`189.120.95.72/24`), half of the address is taken as-is, while the other half represents the range (`189.120.0.0` to `189.120.255.255`)

Following the same pattern, suffix `/0` will always mean any ip address regardless of the network address provided, so it's usually written like `0.0.0.0/0`

-----

Status: #🌲 

References:
- 
