# How Docker Networking Works

Docker uses your host’s network stack to implement its networking system. It works by manipulating `iptables rules` to route traffic to your containers. This also provides isolation between `Docker networks` and your host.