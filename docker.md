# Docker

| Task                                                         | Description                                  |
| ------------------------------------------------------------ | -------------------------------------------- |
| Find an image                                                | docker search <image-name>                   |
| Launch a redis container (with latest version) in background | docker run -d redis                          |
| Launch a 3.2 version of a reds container in background       | docker run -d redis:3.2                      |
| List all running containers                                  | docker ps                                    |
| Details of a running container                               | docker inspect <friendly-name\|container-id> |
| Logs of a running container                                  | docker logs <friendly-name\|container-id>    |
| Launch a container in foreground                             | docker run -it ubuntu bash                   |
|                                                              |                                              |
|                                                              |                                              |

### Find running containers

1. 'docker ps' command lists all running containers

2. To know more details about a running container: 

   ```
   docker inspect <friendly-name|container-id>
   ```

3. To display the messages a container has written to standard error or standard out, use: 

   ```
   docker logs <friendly-name|container-id>
   ```

4. To execute the container in foreground, use the option ```-it```. For example, ```docker run -it ubuntu bash``` allows to get access to a bash shell inside of a container

### Accessing the containers

1. For a service running in a container to be accessible by process outside the container, a port needs to be exposed on the host. Ports are bound when containers are started using the 
   ```-p <host-port>:<container-port>``` option
2. A name can be defined for a running container using the option ```--name <container-name>```
3. To expose the application on a randomly available port, just use the ```-p <container-port>``` option. To know the port that has been assigned, use:

```
docker port <friendly-name|container-id> <container-port>
```

**Note:** By default, the port on the host is mapped to 0.0.0.0, which means all IP addresses. You can specify a particular IP address when you define the port mapping, for example, ```-p 127.0.0.1:6379:6379```

### Persisting data

Data stored in containers gets removed when a container is deleted and re-created. For the data to be persited and made available post recreate, we need to use volumes. Binding volumes to a container is done using the option ```-v <host-dir>:<container-dir>```

For example, the official Redis image stores logs and data into a ```/data``` directory. Any data which needs to be saved on the Docker Host, and not inside containers, should be stored in ```/opt/docker/data/redis```. The command to be used is: 

```
docker run -d --name redisMapped -v /opt/docker/data/redis:/data redis
```

## Deploy Static HTML Website as a container

- Docker Images are built based on the contents of a Dockerfile. The Dockerfile is a list of instructions describing how to deploy your application.

  ```
  FROM nginx:alpine
  COPY . /usr/share/nginx/html
  ```

  The first line defines our base image. The second line copies the content of the current directory into a particular location inside the container.

- Build the static HTML image using the below command: 

  ```
  docker build -t webserver-image:v1 .
  ```

- You can view a list of all the images on the host using ```docker images```

- Launch the newly built image providing the friendly name and tag. As it's a web server, bind port 80 to our host using the -p parameter.

  ```
  docker run -d -p 80:80 webserver-image:v1
  ```