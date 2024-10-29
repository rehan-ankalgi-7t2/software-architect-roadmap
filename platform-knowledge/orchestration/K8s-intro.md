# Kubernetes
![logo](https://upload.wikimedia.org/wikipedia/commons/6/67/Kubernetes_logo.svg)

> `Kubernetes` is a portable, extensible, open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation.

## Cluster Architecture
_The architectural concepts behind Kubernetes._

A Kubernetes cluster consists of a `control plane` plus a set of worker machines, called `nodes`, that run containerized applications. 
- Every cluster needs at least one worker node in order to run Pods.
- The worker node(s) host the `Pods` that are the components of the application workload. 
- The control plane manages the worker nodes and the Pods in the cluster. 
- In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault-tolerance and high availability.

![Kubernetes Architecture](https://kubernetes.io/images/docs/kubernetes-cluster-architecture.svg)

## Deployment through the history
A brief history of application deployment throughout history

### 1. Traditional deployment (late 1990s to early 2000s)
- **Method**: manual `File Transfer Protocol (FTP)` uploads to servers. Webmasters would develop the application locally and then transfer it manually to a production server.
- **Tools**: standard FTP clients like `FileZilla` or `WS_FTP`, among others.

### 2. Containerization and microservices (mid 2010s)
- **Method**: applications began to be developed as collections of loosely coupled microservices. Containers encapsulated these services, ensuring they had all the dependencies they needed to run.
- **Tools**: `Docker`, `Kubernetes`, `Docker Swarm`, and `Platform.sh`.

Continuing on the PaaS theme, two of the things the early PaaS system did not resolve were running software locally and running microservices. Not running micro-services locally as this was basically impossible at the time.

The early PaaS systems were about simplification, and as we said they centered around the specific use case of the single monolith with the single managed database. 

## container orchestration
![alt text](https://media1.tenor.com/m/GIukGbIHmBkAAAAd/tom-and-jerry-orchestra.gif)
### Problem

- the docker containers have operations that needed to be managed, like...
1. start container
2. stop container
3. destroy containers
4. restart container in case of failure
5. deployment
6. scaling
7. securing

- these operations are collectively known as `container orchestration`

> `Container orchestration` automatically provisions, deploys, scales, and manages containerized applications without worrying about the underlying infrastructure.

- google built an in-house solution to automate container orchestration, known as <a href="https://research.google/pubs/large-scale-cluster-management-at-google-with-borg">Google Borg</a>.
- Borg is used for large scale cluster management
- same team at google built an opensource tool for same use case, inspired from 'borg', it is known as `Kubernetes` today
- google donated this open source tool to <a href="https://www.cncf.io/">CNCF (Cloud Native Computing Foundation)</a> in 2014

### Vendor Lock in
![alt text](https://media1.tenor.com/m/dPAud0MREJsAAAAd/cat-stuck.gif)
- `AWS ECS` is a container orchestration service, but it quickly escalates to `vendor lock in`
- AWS can anytime increase the billing amount for this service
- Vendor Lock in leads to `cloud migration` problem
- K8s is `cloud agnostic` and generic to cloud platforms
- hence K8s architecture is a little complicated in nature