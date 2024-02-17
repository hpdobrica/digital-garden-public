---
title : Docker Container Network Setup
notetype : feed
date : 03-11-2021
---

Whenever a container is created, [[Docker]] creates a [[01 Inbox/Network Namespaces]] for it. 

You wont be able to see it when running `ip netns` because [Docker doesn't create a symlink for it](https://stackoverflow.com/questions/31265993/docker-networking-namespace-not-visible-in-ip-netns-list). Let's assume you created the symlink as described in the link.

```bash
ip netns
#> somenamespaceid
```

Inspecting the created container will indeed show that it's using namespace defined above:

```bash
docker inspect mycontainer
#> ...
#> "SandboxID": "somenamespaceid123sadbio1n414psnd",
#> "SandboxKey": "/var/run/docker/netns/somenamespaceid",
#> ...
```

So how does the Docker now attach the container (and/or the network namespace it's in) to the bridge network? It creates a virtual cable with two interfaces on each end.

If you run `ip link` on the host, you will see one end of the cable attached to the local bridge `docker0` :

```bash

ip link
#> ...
#> 18: veth70597a7@if17: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500...
#> ...

```

If you run the same command in context of a namespace, you will see the interface on the other end of the cable:

```bash

ip -n somenamespaceid link
#> ...
#> 3: eth0@if18 <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500...
#> ...

```

The two interfaces can be identified as paired by the same virtual cable bacause they have sequential odd-even `if` numbers in their names (`@if17` is pair with `@if18`, `@if1` is pair with `@if2`).

In case you requested a port mapping while running a container, Docker executes some aditional steps to enable this, as described in [[Docker Port Mapping]].

-----

Status: #🌲 

