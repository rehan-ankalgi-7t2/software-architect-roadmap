# Docker 🐳

> ### What is Docker?
> Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly.

> ### Why use Docker?
> Docker streamlines the development lifecycle by allowing developers to work in standardized environments using local containers which provide your applications and services. Containers are great for continuous integration and continuous delivery (CI/CD) workflows.
- Environment differences
- Environemnt replication Problem across developer and other machines

## Docker Architecture
![docker architecture](https://docs.docker.com/get-started/images/docker-architecture.webp)

- uses client-server architecture
- docker client talks to the docker Daemon
- Docker daemon (`dockerd`) is responsible for all the heavy lifting of `building`, `running` and `distributing` the docker container
- docker client and docker daemon can run on the same system or docker client can be connected to a remote docker daemon
- docker client and dockerd communicate via REST API, over UNIX socket or network interface
- another docker client is `docker compose` that lets you work with applications consisting of a set of containers.

## Basics

1. `Image`: An image is a read-only template with instructions for creating a Docker container.

2. `Container`: A container is a runnable instance of an image. 
    ```bash
    docker run -it ubuntu
    ```
    - `-it`:  attaches the terminal to the current container session (command context stays inside the terminal)
    - `ubuntu`:  image name
    - multiple containers can run using a same image but maintain different environments

### Port mappings
> ports actively used by containerized app should be exposed and mapped to a port on the host system
```bash
docker run -it -p 6000:9000 mailhog
```
- `6000`: system port
- `9000`: container app port

### Environment variables
```bash
docker run -it -p 1025:1025 -e key=value -e key=value -e key=value mailhog
```
- `-e` flag indicates env variable