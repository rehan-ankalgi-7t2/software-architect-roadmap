# Multi-stage builds

With multi-stage builds, 
- you use multiple `FROM` statements in your Dockerfile. 
- Each `FROM` instruction can use a different `base`, and each of them begins a new stage of the build. 
- You can selectively copy artifacts from one stage to another, leaving behind everything you don't want in the final image.

consider below `Dockerfile`

**Example: Compiling the typescript code in the build stage and running the compiled code in the runner stage**
```Dockerfile
FROM ubuntu

RUN apt-get update
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_18.x | bash -
RUN apt-get upgrade -y
RUN apt-get install -y nodejs
RUN apt-get install typescript # assume 2.5 GB

WORKDIR /app

COPY package.json package.json
COPY package-lock.json package-lock.json

RUN npm install

ENTRYPOINT [ "node", "main.js" ]
```
- this above Dockerfile is a single-stage build
- the typescript installation is not a necessity in the runner stage, it should be considered only in the build stage.
- in a production app the compiled javascript code is used instead of the typescript code
- hence below stage changes


```Dockerfile
FROM ubuntu AS build # build stage

RUN apt-get update
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_18.x | bash -
RUN apt-get upgrade -y
RUN apt-get install -y nodejs
RUN apt-get install typescript

WORKDIR /app

COPY package.json package.json
COPY package-lock.json package-lock.json

RUN npm install
RUN tsc -p . # build complete

FROM node AS runner # runner stage
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT [ "node", "main.js" ] # runner
```

- final image is built on the basis of final stage build (nothing but runner stage in this example)