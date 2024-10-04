# Docker Compose 🐙

![](https://media.licdn.com/dms/image/D4D12AQHyejiPAN-Paw/article-cover_image-shrink_600_2000/0/1707453517262?e=2147483647&v=beta&t=QSLpqomh7uKiKOAbzjhvz6bD-6lqk_aOm2et7lwm3x4)

- example: cal.com (opensource)
```mermaid
  graph cal.com;
      Postgres:5432 --> cal.com;
      redis:6372 --> cal.com;
      Mailhog --> cal.com;
```

> docker compose is a tool for defining and running multi-container applications

- docker compose for above example
```yml
version "3.8" #docker-compose version

services:
    postgres:
        image: postgres # from hub.docker.com
        ports:
            - "5432:5432"
        environments:
            POSTGRES_USER: postgres
            POSTGRES_DB: review
            POSTGRES_PASSWORD: password
    
    redis:
        image: redis
        ports:
            - "6379:6379"
```

- to setup and run all containers
```bash
docker compose up
```

- to delete all the containers run by docker compose up command
```bash
docker compose down
```
