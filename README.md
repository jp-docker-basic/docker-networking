# What Is a Docker Network?

Networking is about communication among processes, and Docker’s networking is no different.

Docker networking is primarily used to establish communication between Docker containers and the outside world via the host machine where the Docker daemon is running.

Docker allows you to create three different types of network drivers out-of-the-box: `bridge`, `host`, and `none`. However, they may not fit every use case, so we’ll also explore user-defined networks such as `overlay` and `macvlan`. Let’s take a closer look at each one.

> Docker uses `iptables` on the host machine to prevent access outside of the bridge.

Let’s look at some examples of how a `bridge network` driver works.

- Check the available network by running the `docker network ls` command
- Start two `busybox` containers named `busybox1` and `busybox2` in detached mode by passing the `-dit` flag.

```Dockerfile
$ docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
5077a7b25ae6   bridge    bridge    local
7e25f334b07f   host      host      local
475e50be0fe0   none      null      local
```

```dockerfile
docker run -dit --name busybox1 busybox /bin/sh
docker run -dit --name busybox2 busybox /bin/sh
```

- Run the `docker ps` command to verify that containers are up and running.

```Dockerfile
$ docker ps
CONTAINER ID   IMAGE     COMMAND     CREATED          STATUS          PORTS     NAMES
9e6464e82c4c   busybox   "/bin/sh"   5 seconds ago    Up 5 seconds              busybox2
7fea14032748   busybox   "/bin/sh"   26 seconds ago   Up 26 seconds             busybox1
```

- Verify that the containers are attached to the bridge network.

```Dockerfile
$ docker network inspect bridge
```

### User-defined Bridge Networks

Using the `Docker CLI`, it is possible to create other networks. You can create a second bridge network using:

> docker network create my_bridge --driver bridge

Now, attach “busybox1” and “busybox2” to the same network:

> docker network connect my_bridge busybox1
> docker network connect my_bridge busybox2

We can conclude that only user-defined bridge networks support `automatic service discovery`. If you need to use service discovery with containers, don’t use the `default bridge`, create a new one.

**Note: important command**

#### - For Root user
> whoami 

#### - Host ip address
> hostname -i 