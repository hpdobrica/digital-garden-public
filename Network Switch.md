---
title : Network Switch
notetype : feed
date : 18-05-2022
---

In [[Public/Linux Networking]], the most basic form of a network is two PCs connected with a switch.

In order for machines to connect to a switch, we need an interface on each host (these can be physical or virtual). To see the interfaces on the host, we can run the following:

```bash
ip link
#> 1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1
#>    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
#> 2: ens3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP mode DEFAULT group default qlen 1000
#>    link/ether 02:42:ac:11:00:0a brd ff:ff:ff:ff:ff:ff
#> 3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN mode DEFAULT group default 
#>    link/ether 02:42:aa:c0:e3:ed brd ff:ff:ff:ff:ff:ff
#> 4: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state DOWN mode DEFAULT group default 
#>    link/ether 02:42:aa:c0:e3:ed brd ff:ff:ff:ff:ff:ff
```

If the switch creates a network with [[Public/CIDR]] 192.168.1.0/24, we can use the interface to assign the addresses to the machines on this network:

```bash
ip addr add 192.168.1.10/24 dev eth0
```

This command will assign ip adress `192.168.1.10` and subnet mask `255.255.255.0` to the interface `eth0`. However, **this change will be lost with restart**. To persist it, you need to make a change in `/etc/network/interfaces` file.

The switch can only send/receive packets from/to the systems within its network. If we have another network, in order for host from network 1 to reach the host on network 2, we will need a [[Public/Network Router]].




-----

Status: #💡 

References:
- 
