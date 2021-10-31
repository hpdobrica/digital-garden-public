---
title : DNS
notetype : feed
date : 31-10-2021
---

DNS ([[Domain Name]] System) provides us a way to give names to ip addresses. For example, if you have a database running on a host in your local network behind the ip 192.168.1.6 (Host B), you can name it "db" by adding a line in the hosts file on your host (Host A):

```bash
# appends to a file every line you make (icluding \n) until you interrupt
cat >> /etc/hosts
192.168.1.6 db

```

Whatever we put inside `/etc/hosts` file will be taken for granted, and is the source of truth for that host - If we run `hostname` on host B, we will see that the actual name of the host is `host-2`, but host A doesn't care. You can even use this approach to fool system A that system B is Google.

Whenever you try to reach db, the host A will look at its hosts file, find the record that says db points to 192.168.1.6, and reach to that IP address. This process is called **Name Resolution**.

Within a small network, you can get away with specifying the names and the ip addresses of other hosts in the hosts file - in fact this is how it was done in the past, until the environments grew and these files became too big to maintain. If one of the server's IP changes, you'd have to modify its IP on all other hosts. The solution to this was to move all of these entries to a separate server that will manage them centrally - this is called a **DNS Server**.

After we moved all of our entries to the DNS Server, we need a way to point all of our towards it for name resolution. We can do this by specifying the IP of the DNS Server inside of `/etc/resolv.conf` file.

```bash

cat /etc/resolv.conf
#> hostname 192.168.1.100

```

Once this is set up on all of your hosts, every time the host comes across a name it doesn't know about (not in `/etc/hosts`), it looks it up from the DNS Server.

> Checking first the `/etc/hosts` file and then the DNS Server is the default order of operations, which can be overridden by file `/etc/nsswitch.conf`

What happens if you try to ping a server which is neither in the local config nor in the dns server, e.g. _www.youtube.com_?

Since no one knows about it, the request will fail. You can overcome this by adding another DNS server to your resolv.conf file that knows about it:

```bash

cat /etc/resolv.conf 
#> hostname 192.168.1.100 
#> hostname 8.8.8.8

```

`8.8.8.8` is a public DNS Server hosted by Google. You can have multiple entries in your resolv.conf file to overcome this, but this means that you'd have to edit all the hosts in your network to make youtube work everywhere. If we had a local DNS Server, what we can could do instead is configure it to forward all unknown host names to the public nameserver on the internet.
