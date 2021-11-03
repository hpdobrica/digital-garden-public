---
title : DNS
notetype : feed
date : 31-10-2021
---

DNS (Domain Name System) provides us a way to give names to ip addresses. For example, if you have a database running on a host in your local network behind the ip 192.168.1.6 (Host B), you can name it "db" by adding a line in the hosts file on your host (Host A):

```bash
# appends to a file every line you make (icluding \n) until you interrupt
cat >> /etc/hosts
192.168.1.6 db

```

Whatever we put inside `/etc/hosts` file will be taken for granted, and is the source of truth for that host - If we run `hostname` on host B, we will see that the actual name of the host is `host-2`, but host A doesn't care. You can even use this approach to fool system A that system B is Google.

Whenever you try to reach db, the host A will look at its hosts file, find the record that says db points to 192.168.1.6, and reach to that IP address. If it can't find the requested [[Domain Name]], it will ask DNS server for help. This process is known as [[DNS Resolution]].

Within a small network, you can get away with specifying the names and the ip addresses of other hosts in the hosts file. As the system grows, this will grow harder to maintain as the files will grow bigger, and as one of the server IPs changes, you'd have to update all of the hosts. The solution to this is to centrally manage DNS entries in a [[DNS Server]].

-----

Status: #🌲 
References:
-
