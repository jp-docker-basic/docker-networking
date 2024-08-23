# Docker Network Commands

The docker network command is used for managing Docker networks. It provides functionality to create, inspect, list, connect, disconnect, and remove networks within Docker. Here are some commonly used subcommands and examples of how to utilize the docker network command:

![docker networking commands](image.png)

Here’s an example of creating a Docker network with custom options:

```Dockerfile
docker network create \
  --driver bridge \
  --subnet 172.18.0.0/16 \
  --gateway 172.18.0.1 \
  --ip-range 172.18.0.0/24 \
  my-custom-network
```
In this example:

- `--driver bridge`: Specifies the network driver as bridge. You can use other drivers like overlay, macvlan, etc., based on your requirements.
- `--subnet 172.18.0.0/16`: Defines the subnet for the network.
- `--gateway 172.18.0.1`: Specifies the gateway IP address for the network.
- `--ip-range 172.18.0.0/24`: Defines the range of IP addresses that can be assigned to containers on this network.
- `my-custom-network`: The name given to the network.

## Connect a Container to a Network:
To connect a Docker container to a network, you can use the docker network connect command followed by the network name and the container name or ID.

> docker network connect my-network my-container

In this example:

- `my-network` is the name of the network to which you want to connect the container.
- `my-container` is the name or ID of the container you want to connect to the network.


### Docker network prune:

The docker network prune command is used to remove all unused Docker networks from your system.

> docker network prune

If you want to skip the confirmation prompt, you can use the -f or --force option:

> docker network prune -f
