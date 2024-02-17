---
title : Linux Networking
notetype : feed
date : 18-05-2022
---

This note serves as a link to connect Linux Networking related notes.

Get started on the topic by checking one of these out:
- [[Public/How to make a Linux Host act as a Router]]

Some of the useful networking commands:
```bash
# list and modify interfaces on the host
ip link 

# see the ip addresses assigned to interfaces
ip addr

# used to set ip addresses on the interfaces (changes valid until reboot)
ip addr add 192.168.1.0 dev eth0

# see the routing table - these two are aliases
ip route
route

# add entries to the routing table
ip route add 192.168.2.0/24 via 192.168.1.1

# check if interface packet forwarding is enabled on a host
cat /proc/sys/net/ipv4/ip_forward

arp


netstat -tulpn
netstat -tulpna # show all connections - useful to see number



```



-----

Status: #🗺️ 


