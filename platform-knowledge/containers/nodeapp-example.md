# Containerize a node-express application 🐳

### Dockerfile
> filename to create a container configuration for the app
- a docker image is built using a Dockerfile
- exact file name to be followed with casing and spelling

```Dockerfile
#1 - use a base image
FROM ubuntu:latest

#2 - Install Nodej
RUN apt-get update
RUN apt-get install -y curl
RUN curl -sL <link to download nodejs via curl> | bash -
RUN apt-get upgrade -y
RUN apt-get install nodejs

#3 - set working directory for the app in the container
WORKDIR /home/app

#4 - copy code files in the container destination app folder
# copy one by one
COPY package.json package.json
COPY package-lock.json package-lock.json

# OR 

# copy everything
COPY . .

#5 - Install npm dependencies
RUN npm install

#6 - Run the app
ENTRYPOINT ["node", "main.js"]
```

### Build the image
```bash
docker build -t <image_name>
```

### Run the container using the built image
```Bash
docker run -it <image_name>
```
- add port mappings, env configs in the above command as needed

## Caching Layers & Efficient Caching
> All the commands in the `Dockerfile` are cached as LayersHence...
- a command heirarchy is important while configuring a `Dockerfile`
- the order of the commands in the Dockerfile will impact build pipelines and cost
- maintain and use `.dockerignore` file to ignore files while copying into the container like (Node Modules)
- always copy and run projects from an isolated folder on the container rather than the container root
- set a working directory in the container

### Example Scenario
- Consider the following dockerfile:

```Dockerfile
FROM ubuntu:latest

RUN apt-get update
RUN apt-get install -y curl
RUN curl -sL <link to download nodejs via curl> | bash -
RUN apt-get upgrade -y
RUN apt-get install nodejs

WORKDIR /home/app

COPY . .

RUN npm install


ENTRYPOINT ["node", "main.js"]
```

- any changes to the code file will lead to unecessary npm dependency installations, which will increase the build time for docker image
- an optimised version of this can be like so...

```Dockerfile
FROM ubuntu:latest

RUN apt-get update
RUN apt-get install -y curl
RUN curl -sL <link to download nodejs via curl> | bash -
RUN apt-get upgrade -y
RUN apt-get install nodejs

WORKDIR /home/app

COPY package.json package.json
COPY package-lock.json package-lock.json

RUN npm install

COPY . .

ENTRYPOINT ["node", "main.js"]
```

- only if the changes are found in the `package.json` or `package-lock.json`, then the dependencies are installed
- else the step is cached and skipped to the next sstep in the build process 

## Publishing to the docker hub:
1. create repository on docker hub
2. build image with repository name
    - example:
    ```bash
    docker build -t piyush/yt-node .
    ```
3. push the image
    ```bash
    docker push <image_name>
    ```
    - example
    ```bash
    docker push piyush/yt-node
    ```

- if not logged in locally
```bash
docker login
```
