# How Docker Networking Works

Docker uses your host’s network stack to implement its networking system. It works by manipulating `iptables rules` to route traffic to your containers. This also provides isolation between `Docker networks` and your host.

The containers are running in the `background`. Use the docker `attach command` to connect to alpine1.


> `docker attach alpine1`

```bash
/ #
```

The prompt changes to `#` to indicate that you are the root user within the container. Use the `ip addr show` command to show the network interfaces for `alpine1` as they look from within the container: