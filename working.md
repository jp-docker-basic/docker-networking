# How Docker Networking Works

Docker uses your host’s network stack to implement its networking system. It works by manipulating `iptables rules` to route traffic to your containers. This also provides isolation between `Docker networks` and your host.

The containers are running in the `background`. Use the docker `attach command` to connect to alpine1.

> `docker attach alpine1`

```bash
/ #
```

The prompt changes to `#` to indicate that you are the root user within the container. Use the `ip addr show` command to show the network interfaces for `alpine1` as they look from within the container:

```bash
# ip addr show

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
27: eth0@if28: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue state UP
    link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.2/16 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:acff:fe11:2/64 scope link
       valid_lft forever preferred_lft forever
```

The first interface is the loopback device. Ignore it for now. Notice that the second interface has the IP address `172.17.0.2`, which is the same address shown for `alpine1` in the previous step.

