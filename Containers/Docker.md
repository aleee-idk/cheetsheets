
# Table of Contents

1.  [Terminology:](#orgb3c6bfd)
    1.  [Image: Template for an enviroment.](#orgedd5fca)
    2.  [Container: Running instance of an Image.](#org916ca53)
    3.  [Volumes: Allows sharing of data (Files and folders) between host and containers.](#orgfe9e992)
    4.  [Tags: Allows control image version.](#orgc8b8a83)
2.  [Docker:](#orgfdeff6f)
    1.  [Commands:](#orgc3a17f7)
        1.  [Image managment:](#org0e17187)
        2.  [Conainers:](#orge943377)
        3.  [Volumes:](#orgef73642)
        4.  [Commands:](#org703d12a)
        5.  [Manage containers:](#orgefecd03)
    2.  [Dockerfile:](#orgb4c6263)
        1.  [Base image:](#org2961fc7)
        2.  [Add files or directories:](#org973a0e9)
        3.  [Set work directory](#orgc73c8df)
        4.  [Execute commands when the container build:](#org30d7e62)
        5.  [Run command when the conteiner start:](#orga58e829)
    3.  [.dockerignore](#orgc6ee16b)
    4.  [Docker Registries:](#orgc97b998)
        1.  [Login to docker hub:](#org36efe61)
        2.  [Upload image:](#org1fcce71)
        3.  [Download image:](#org65ade5a)
3.  [Docker Compose:](#org9f74206)
    1.  [Commands:](#org525c760)
        1.  [Spin up all of the services:](#org7ad6c1c)
        2.  [tear it all down:](#orge356c57)
        3.  [viw all logs:](#orgcba6b34)
    2.  [docker-compose file:](#org5ff52fc)
        1.  [version:](#org55c7e47)
        2.  [Services:](#org1491e18)
        3.  [Exanple:](#orga39965b)
4.  [Tips and Tricks:](#orgf68cf4e)
    1.  [Enter the container: *exect -it container<sub>id</sub><sub>or</sub><sub>name</sub> \\/bin\\/container<sub>shell</sub>*](#orga8b785b)
    2.  [Add files that not change very often so when build an image use cache.](#orgb0b7c64)
    3.  [To reduce resource usage, use alpine as base image.](#orgc498a4e)



<a id="orgb3c6bfd"></a>

# Terminology:


<a id="orgedd5fca"></a>

## Image: Template for an enviroment.

An image needs to have enerything the aplication need to run.
An image is also an Snapshot


<a id="org916ca53"></a>

## Container: Running instance of an Image.


<a id="orgfe9e992"></a>

## Volumes: Allows sharing of data (Files and folders) between host and containers.


<a id="orgc8b8a83"></a>

## Tags: Allows control image version.


<a id="orgfdeff6f"></a>

# Docker:


<a id="orgc3a17f7"></a>

## Commands:

All commands are run with *&ldquo;docker &#x2026;&rdquo;*
Example: &ldquo;docker run *some image:version*&rdquo;
All the flag listed below can be used together.


<a id="org0e17187"></a>

### Image managment:

1.  Downlad an image:

    pull *image*

2.  List Images:

    images


<a id="orge943377"></a>

### Conainers:

1.  List containers:

    -   All running containers:
        ps (running containers)
    -   Format output:
        ps &#x2013;format=&ldquo;ID\t{{.ID}}\nNAME\t{{.Names}}\nImage\t{{.Image}}\nPORTS\t{{.Ports}}\nCOMMAND\t{{.Command}}\nCREATED\t{{.CreatedAt}}\nSTATUS\t{{.Status}}\n&rdquo;
    -   All conteiners:
        ps -a (all containers)
    -   Another method:
        container ls

2.  Run a container (for the first time):

    run *image*:/version/

3.  Run a container in detached mode (in the background):

    run -d *image*:/version/

4.  Build an image from a Dockerfile:

    build -t *name*:/tag name/ *where the Dockerfile is*

5.  Tag an image:

    tag *image*:/original-tag/ *image*:/new-tag/

6.  Name a container:

    run &#x2013;name *name* *image*:/version/

7.  Expose ports:

    run -p *host port*:/container port/ *image*:/version/
    Multiple host port can be mapped to the same container port, just add another -p flag

8.  Start a container:

    start *container id or name*

9.  Stop conteiner:

    stop *container id or name*

10. Delete containers:

    rm *container id or name*

11. Delete all conteiners:

    rm -f $(docker ps -aq)
    -f Force delete, inclusive running containers


<a id="orgef73642"></a>

### Volumes:

1.  Attach a folder from the host to the container:

    run -v *host folder*:/container destination/ *image*:/version/
    After the destination directory you can add *&ldquo;:ro&rdquo;* to make it read only

2.  Share volumes between containers:

    run &#x2013;volumes-from *container id or name* *image*:/version/


<a id="org703d12a"></a>

### Commands:

1.  Run command inside container:

    exec -it *container id or name* *command*


<a id="orgefecd03"></a>

### Manage containers:

1.  Get information:

    inspect *id or name of container*

2.  See logs:

    logs *id or name of container*

3.  See live logs:

    logs -f *id or name of container*


<a id="orgb4c6263"></a>

## Dockerfile:


<a id="org2961fc7"></a>

### Base image:

FROM *image*:/version/


<a id="org973a0e9"></a>

### Add files or directories:

ADD *files or directory* *destination*
wildcards works


<a id="orgc73c8df"></a>

### Set work directory

WORKDIR *directory*
If the directory doesn&rsquo; exist it will create it


<a id="org30d7e62"></a>

### Execute commands when the container build:

RUN *Command*


<a id="orga58e829"></a>

### Run command when the conteiner start:

CMD *Command*


<a id="orgc6ee16b"></a>

## .dockerignore

Works similar to .gitignore, just add every file and directory that don&rsquo;t needs to be in the container. Common stuff:

-   node<sub>modules</sub>
-   Dockerfile
-   .git


<a id="orgc97b998"></a>

## Docker Registries:

This will refere to upload to docker hub.


<a id="org36efe61"></a>

### Login to docker hub:

login


<a id="org1fcce71"></a>

### Upload image:

push *user repo*\\//image/:/tag/


<a id="org65ade5a"></a>

### Download image:

pull *user repo*\\//image/:/tag/


<a id="org9f74206"></a>

# Docker Compose:


<a id="org525c760"></a>

## Commands:


<a id="org7ad6c1c"></a>

### Spin up all of the services:

up
add the &#x2013;build flag to rebuild the images every time needed, oterwise it just gonna use the same.


<a id="orge356c57"></a>

### tear it all down:

down


<a id="orgcba6b34"></a>

### viw all logs:

logs


<a id="org5ff52fc"></a>

## docker-compose file:


<a id="org55c7e47"></a>

### version:

start with version, just use the lastest one


<a id="org1491e18"></a>

### Services:

the conteiners to run. The images come from the dockerfile in the current directory.

1.  Undet this you can add the flags for the conteiner like port


<a id="orga39965b"></a>

### Exanple:

[<https://github.com/mikesir87/dockercon-2020-compose-talk>]

    version: "3.8"
    services:
      proxy:
        image: traefik:2.2
        command: --providers.docker
        ports:
          - 80:80
        volumes:
          - /var/run/docker.sock:/var/run/docker.sock
    
      app:
        build:
          context: .
          target: backend-dev
        volumes:
          - nodemodules:/app/node_modules
          - ./backend:/app
          - ./config:/config
        environment:
          MYSQL_HOST: mysql
          MYSQL_USER_FILE: /config/MYSQL_USER
          MYSQL_PASSWORD_FILE: /config/MYSQL_PASSWORD
          MYSQL_DB_FILE: /config/MYSQL_DB
        labels:
          traefik.http.routers.backend.rule: Host(`localhost`) && PathPrefix(`/items`)
          traefik.http.services.backend.loadbalancer.server.port: 3000
    
      frontend:
        build:
          context: .
          target: frontend-base
        stdin_open: true
        volumes:
          - nodemodules-frontend:/app/node_modules
          - ./frontend:/app
        labels:
          traefik.http.routers.frontend.rule: Host(`localhost`)
          traefik.http.services.frontend.loadbalancer.server.port: 3000
    
    
      mysql:
        image: mysql:5.7
        volumes:
          - ./config:/config
          - mysql-data:/var/lib/mysql
        environment:
          MYSQL_USER_FILE: /config/MYSQL_USER
          MYSQL_PASSWORD_FILE: /config/MYSQL_PASSWORD
          MYSQL_DATABASE_FILE: /config/MYSQL_DB
          MYSQL_RANDOM_ROOT_PASSWORD: "true"
    
    volumes:
      nodemodules:
      nodemodules-frontend:
      mysql-data:


<a id="orgf68cf4e"></a>

# Tips and Tricks:


<a id="orga8b785b"></a>

## Enter the container: *exect -it container<sub>id</sub><sub>or</sub><sub>name</sub> \\/bin\\/container<sub>shell</sub>*

Use inspect to check the container shell


<a id="orgb0b7c64"></a>

## Add files that not change very often so when build an image use cache.


<a id="orgc498a4e"></a>

## To reduce resource usage, use alpine as base image.

some image have alpine as supported tag.

