---
title : Network Router
notetype : feed
date : 18-05-2022
---

A router helps connect two networks together. It can be thought of as another host with many network ports. Since it connects to two networks, it will be assigned two IPs - one on each network.

In order for a system to reach a system in another network, it will need to go through a router. Since router is just another device in the network, a system will need a way to find it. This is where **Gateway** comes in.

If a network was a room, the Gateway would be a door to the outside world - to the other networks or to the internet. The systems need to know where the door is in order to be able to go through it. To see the existing routing configuration on a system, you can run the [[Linux Networking]] `route` command, which displays kernel's routing table:

```bash
route
#> Kernel IP routing table
#> Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
#> default         172.17.0.1      0.0.0.0         UG    0      0        0 ens3
#> 172.17.0.0      *               255.255.0.0     U     0      0        0 ens3
#> 172.18.0.0      *               255.255.255.0   U     0      0        0 docker0
```

If there is no gateway configured, a system will not be able to reach the systems outside of its network. To configure a gateway on a system you can use the following command:

```bash
ip route add 192.168.2.0/24 via 192.168.1.1
```

This command specifies that you can reach devices in the network `192.168.2.0` via a Router located at `192.168.1.1`. Note that this has to be configured on all the systems in order for communication between them to work as expected.


You can configure the router to forward traffic to IP addresses on the internet. Now we could run the same command as above to tell our computer that some public address can be reached via our router like this `ip route add <SOME-PUBLIC-IP> via 192.168.1.1`, but since there are too many possible addresses you might want to reach, it's not a feasible solution. This is where **Default Gateway** comes to the rescue.

You can configure your host so that requests to any network outside of this one go through this particular router. So in a setup like this, all you would need to do is execute `ip route add default via 192.168.1.1` which will add a default row to the `route` table. 

In the beginning, we said that router can be thought of just as another server in the network. To learn more about this, check out [[How to make a Linux Host act as a Router]].





-----

Status: #📥

References:
- 
