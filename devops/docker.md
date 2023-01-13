# Docker

> ❌ A travailler

> ✔️ Auto validation par l'étudiant

## 🎓 J'ai compris et je peux expliquer

- la création d'une image docker ✔️
- l'éxécution d'un container ✔️
- l'orchestration de containers avec docker-compose ✔️


## 💻 J'utilise

### Un exemple personnel commenté ✔️

## Create an image with Dockerfile
A Dockerfile defines how an image is build. Images are ran in containers 
```bash
# Load executable and environment (partial OS)
FROM node:alpine
# Run mkdir command 
RUN mkdir /app
# Define Working dir : all path are relative to it
WORKDIR /app
# Copy package json files
COPY package*.json .
# Install packages
RUN npm i
# Copy source files
COPY src src
# Start node project on container execution
CMD npm run start
```

Reminder: Docker uses its own cache system. When building the image, Docker will detect if any modifications were made on copied files. For each copy instruction, if copied files are untouched from the previous generated image, Docker will use its cache. If modifications were found, Docker will run every command starting from the command that leads to changes. Source folder tends to be modified a lot while development. Place ``COPY src src`` before RUN npm i`` and a package installation will occur every time the source folder files change.

### Build an image
```bash
docker build -t nameImage .

-t : gives image a name
```

### Push an image
```bash
docker login
docker build -t user/nameImage .
docker push user/nameImage

-t : gives image a name
```

### Get images list
```bash
docker images
docker image ls
```

### Delete an image
```bash
docker rmi imageId
docker image rm imageId
```

## Start a container without docker-compose

### Start a container
```bash
docker run -d -p "5000:5000" --name myContainerName image

-d : detached
-p : ports
--name : containerName if not defined name is generated
```

### Enter into a container
```bash
docker exec -it myContainerNameOrId bash/sh
```
The 'exec' command is used to perform commands inside the container.

### Display container list
```bash
docker ps -a

- a : returns all containers including exited ones.
```
### Inspect container

```bash
docker inspect containerNameOrId
```
Useful to get container's informations : configuration, network settings...

### Stop a container
```bash
docker stop containerNameOrId
```

### Delete a container
```bash
docker rm containerNameOrId
```

## Start containers using docker-compose

Docker-compose is useful to configure and launch several services at once. These services are running inside their own container and all of them are connected to the same network. They can communicate together using either their IP inside the network or their name thanks to the DNS resolver.

### Configure a service with a specific port and image
```bash
services:
  client:
    container_name: wilder_client
    image: wilder_client
    ports:
      - "3000:4000"
      
ports: This property is used to map the machine port to the container port. Services communicate through the port machine and not the container port, in this example port 3000.
image: The image to run into the container. First docker seeks for this image in local, if not found fetch dockerhub
container_name: Gives a name to the container
client: Name of the service. This name can be used to identify the container on the network
```

`Reminder: When this docker compose will be executed, a default network will be created. If not specified, its name will be : foldername_default`

### Configure a service with a build
Instead of specifying a prior build image for a service, we can specify a path to a Dockerfile. On docker-compose command execution, Docker will build the image. If the image is already available locally, it won't build it unless you specify it with ``--build`` option.

```bash
services:
  server:
    depends_on:
      db:
        condition: service_healthy
    container_name: wilder_server
    build: ./server
    volumes:
      - ./server/src:/app/src
    ports:
      - "4000:4000"
```

### Inspect networks
Networks can be inspected to be sure that containers are connected to it.

```bash
docker network ls
docker inspect network networkNameOrID
```

### Binding volumes
By default, the data inside a container is not persistent. When the container is stopped, all the data is lost. To fix this issue, we can bind volumes from the machine to the container, doing so data is loaded when the service is launched and saved when it is stopped. Binded volumes are interesting for development purpose : hot reload for instance.

```bash
services:
  client:
    container_name: wilder_client
    image: wilder_client
    volumes:
      - ./client/src:/app/src
    ports:
      - "3000:4000"
      
volumes: Binds the ./client/src folder to /app/src
```

### Services dependencies

We may want a service to start after being sure that another service was successfully started. Docker compose allows to do this.
```bash
services:
  db:
    container_name: postgres
    image: postgres:15-alpine
    healthcheck:
      test: ["CMD-SHELL", "pg_isready"]
      interval: 10s
      timeout: 30s
      retries: 5
      start_period: 30s
  server:
    depends_on:
      db:
        condition: service_healthy
    container_name: wilder_server
    build: ./server
    volumes:
      - ./server/src:/app/src
    ports:
      - "4000:4000"
      
 healthcheck: Check the service health. In this case, we want to be sure that postgres is successfully started before starting the server service
 depends_on: Wait the service it depends on to be started before being started. Here, server waits for db to be healthy before being started. 
 ```
### Environment variables
Environment variables can be defined for each service 
```bash
services:
  db:
    environment:
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_USER=postgres
```

### Run commands
Commands to run on the service launching can be specified
```bash
services:
  server:
    command: npm run start
```

### Start services with docker-compose
```bash
docker compose [-d] [-f docker.compose.dev.yml] up [servicename] [--build]

-d : detached mode
-f filename: if not specified docker compose will seek for a config file called docker.compose.yml
servicename: if not specified docker compose will start all the services in the configuration file. 
--build : If defined, it will force rebuild all the image (defined with 'build option') in the configuration file. The image is generated with the same behaviour described above ( docker cache ).
```


### Stop services with docker-compose
```bash
docker compose stop
```

### Delete services with docker-compose
```bash
docker compose down
```

### Links



### Utilisation dans un projet ❌

[lien github](...)

Description :

### Utilisation en production si applicable ❌

[lien du projet](...)

Description :

### Utilisation en environement professionnel ✔️

Description :
- At PixPay all databases are dockerized.
- I created a Dockerized localhost HTTPS proxy using NGINX to be able to use SSL on local environment.

## 🌐 J'utilise des ressources

### Titre

- lien
- description

## 🚧 Je franchis les obstacles

### Point de blocage ❌ / ✔️

Description:

Plan d'action : (à valider par le formateur)

- action 1 ❌ / ✔️
- action 2 ❌ / ✔️
- ...

Résolution :

## 📽️ J'en fais la démonstration

- J'ai ecrit un [tutoriel](...) ❌ / ✔️
- J'ai fait une [présentation](...) ❌ / ✔️
