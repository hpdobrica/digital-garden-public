---
title : Docker Bridge Network
notetype : feed
date : 03-11-2021
---

When [[Docker]] is installed, it creates an internal private network which is by default called `bridge` . You can see this network like this:

```bash
docker network ls
#> NETWORK ID     NAME      DRIVER    SCOPE
#> 71f0f1f94055   bridge    bridge    local
```

While docker refers to this network as `bridge`, to the host this network is visible as `docker0`:

```bash
ip link
#> ...
#> 4: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN mode DEFAULT group default
```

Docker accomplishes this by creating a [[Linux Bridge]] like so:

```bash
ip link add docker0 type bridge
```

Linux Bridge, while acting like a [[Network Switch]] to the [[01 Inbox/Network Namespaces]], it acts as an interface to the host. Therefore the interface `docker0` on the host is assigned an IP address.

```bash
ip addr
#> ...
#> 4: docker0: ...172.17.0.1 ...
#> ...
```

Once this is set up, every time container is created with `--network bridge`, Docker attaches it to this bridge. See [[Docker Container Network Setup]] for more details.




-----

Status: #💡 

