# NGINX
![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTaHKUNmd0azmVRTJ4IkwUl2ZfgzE6jJdYdqQ&s)

> Powerful web server
- uses non-threaded, event driven architecture

## understanding `forward` and `reverse` proxy
![](https://i.ytimg.com/vi/4NB0NDtOwIQ/maxresdefault.jpg)

### Forward proxy
- forword proxy / proxy is a web server that sits between the client and the requested server
- forward proxy shields the client
- it protects user identity and avoids browsing restrictions
- blocks access to a certain content
- **example:** VPN
- simply put, server is not aware of requesting client

### Reverse proxy
- Reverse proxy / proxy is a web server that sits between the client and the requested server
- forward proxy shields the Web servers
- protects from DDos attacks
- blocks access to a certain content
- **example:** VPN
- simply put, client is not aware of which server is reponding

> `NGINX` is a popular choice for reverse proxy

## Real Architecture
![](https://cdn-media-1.freecodecamp.org/images/RooSvbKlAWsOjkz8JPactXH-GPf4Pe6DC3Ue)

## Advantages of `NGINX`
- can handle 10,000 concurrent requests
- Http Caching
- can act as `reverse proxy`
- can act as `Load Balancer` 
- can act as `API Gateway`
- serve and cache static file (images, media, videos)
- Handle SSL Certificates

## Prerequisite for learning NGINX
- Docker Containerisation 🐳
- Linux 🐧
- AWS