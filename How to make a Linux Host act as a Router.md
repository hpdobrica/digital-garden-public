---
title : How to make a Linux Host act as a Router
notetype : feed
date : 18-05-2022
---

Let's say we have 3 hosts (`A`, `B` and `C`), and two networks (`192.168.1.0` and `192.168.2.0`):
- Host `A` is connected to network `192.168.1.0` via interface `eth0` and has IP `192.168.1.5`
- Host `C` is connected network `192.168.2.0` via interface `eth0` and has IP `192.168.2.5`
- Host `B` is connected to both networks via interfaces `eth0` and `eth1` and has one ip for each network - `192.168.1.6` and `192.168.2.6` 

Now let's say that we want to enable host `A` to talk to host `C`. This is by default not possible as they are not members of the same network. If we try to ping `C` from `A`, we would get a `Network is unreachable` error.

Luckily, we have host `B` which is connected to both networks, and we can configure `A` and `C` to use `B` as a gateway:

```bash
# host A
ip route add 192.168.2.0/24 via 192.168.1.6 

# host C
ip route add 192.168.1.0/24 via 192.168.2.6

```

Doing this is just half of the solution though. The problem now is that even though two networks are connected via host `B`, host `B` won't forward packets between it's `eth0` and `eth1` by default. is a security consideration in [[Linux Networking]], because allowing packet forwarding from one interface to another can accidentally expose your private network to the public.

In order to allow packet forwarding like this, you need to manually enable it. Whether a host can forward packets between interfaces is governed by the file `/proc/sys/net/ipv4/ip_forward`:

```bash
cat /proc/sys/net/ipv4/ip_forward
#> 0
```

Having `0` in there means forwarding is not enabled. you can enable it by simply doing `echo 1 > /proc/sys/net/ipv4/ip_forward`. From this point on, host `A` will be able to ping host `C` by using host `B` as a router.

Last thing to note is that the change above won't persist across restarts. In order to persist it, you need to set the value `net.ipv4.ip_forward` in `/etc/sysctl.conf` to `1`.

-----

Status: #💡 

References:
- 
