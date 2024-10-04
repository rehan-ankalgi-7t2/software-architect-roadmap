# Docker Networking

```bash
# show all network drivers available
docker network ls

docker network create -d <mode> <network name>
# example: docker network create -d bridge youtube

docker run -it --network=<network driver mode> <image name>

# show network details with containers using it
docker network <network name> inspect
```


## Network Drivers
![](https://miro.medium.com/v2/resize:fit:1372/0*X34tDynHLvheJOKN)

### 1. Bridge Driver
- In terms of networking, a bridge network is a Link Layer device which forwards traffic between network segments.
- A bridge can be a hardware device or a software device running within a host machine's kernel.

> In terms of Docker, a bridge network uses a software bridge which lets containers connected to the same bridge network communicate, while providing isolation from containers that aren't connected to that bridge network.

- default network driver
> **container networking**: the ability of containers to connect to and communicate with each other or to non docker workloads

### 2. Host driver
> enables the container to directly connect to the network available on the host machine without any bridge mechanism
- container network stack isn't isolated from docker host
- Host mode networking can be useful for the following use cases:
    - To optimize performance
    - In situations where a container needs to handle a large range of ports
    - no need for explicitly exposing and mapping of ports

### 3. None driver
- disables network access for the container

### 4. Custom network mode / driver
```bash
docker network create -d <mode> <network name>
# example: docker network create -d bridge youtube

docker run -it --network=youtube --name tony-stark ubuntu
```