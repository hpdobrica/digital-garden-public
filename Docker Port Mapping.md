---
title : Docker Port Mapping
notetype : feed
date : 07-11-2021
---

[[Docker]] provides us a way to map ports of a container to ports of the host (`docker run -p 9000:80 nginx`) . This will make sure that any traffic that reaches host on the port 8080, will be forwarded to our container on port 80.

Docker accomplishes this with iptables, by setting a rule like this:

```bash

iptables -t nat -A DOCKER -j DNAT --dport 9000 --to-destination 172.17.0.3:80


```


To see the rule docker creates, you can list the rules in the iptables like so:

```bash

iptables -nvL -t nat

```


-----

Status: #🌲 

References:
- 
