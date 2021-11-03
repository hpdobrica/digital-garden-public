---
title : DNS Server
notetype : feed
date : 02-11-2021
---

DNS Server is a server who's primary purpose is the DNS resolution. It holds a database of IP addresses and Domain Names, and is able to communicate with other DNS Servers to help with the queries it doesn't know about. They use port 53 (thus [[Route53]]) and UDP protocol to communicate.

A machine can be pointed to use DNS Server for name resolution by specifying it's IP address in `/etc/resolv.conf` file like so:

```bash

cat /etc/resolv.conf
#> hostname 192.168.1.100

```

Once this is set up on a machine, every time the host comes across a name it doesn't know about (e.g. it's not specified in `/etc/hosts`), it looks it up from the DNS Server.

> Checking first the `/etc/hosts` file and then the DNS Server is the default order of operations, which can be overridden by file `/etc/nsswitch.conf`

So what happens if you try to ping a server which is neither in the local config nor in the dns server, e.g. _www.youtube.com_?

Since no one knows about it, the request will fail. One way to overcome this is adding another DNS server to your resolv.conf file which knows about it:

```bash

cat /etc/resolv.conf 
#> hostname 192.168.1.100 
#> hostname 8.8.8.8

```

`8.8.8.8` is a public DNS Server hosted by Google. You can have multiple entries in your resolv.conf file to overcome this, but this means that you'd have to edit all the hosts in your network to make youtube work everywhere. If we had a local DNS Server, what we can could do instead is configure it to forward all unknown host names to the public nameserver on the internet.

-----

Status: #🌲 

References:
- 
