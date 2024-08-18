# What Is a Docker Network?

Networking is about communication among processes, and Docker’s networking is no different. 

Docker networking is primarily used to establish communication between Docker containers and the outside world via the host machine where the Docker daemon is running.

Docker allows you to create three different types of network drivers out-of-the-box: `bridge`, `host`, and `none`. However, they may not fit every use case, so we’ll also explore user-defined networks such as `overlay` and `macvlan`. Let’s take a closer look at each one.

> Docker uses `iptables` on the host machine to prevent access outside of the bridge.

Let’s look at some examples of how a `bridge network` driver works.

- Check the available network by running the `docker network ls` command
- Start two `busybox` containers named `busybox1` and `busybox2` in detached mode by passing the `-dit` flag.