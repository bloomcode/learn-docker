# Overview

An open platform for developers and sysadmins to build, ship and run distributed applications.

Docker allows you to run containers. A container is a sandboxed process running an application and its dependencies on the host operating system. The application inside the container considers itself to be the only process running on the machine while the machine can run multiple containers independently.

## Deploying your first Docker container

### Running a container

1. Existing images can be found at registry.hub.docker.com/ or by using the command: 
   ```
   docker search <image name>
   ```
2. To start a container based on a Docker image, use the command: 
    ```
    docker run <options> <image-name>
    ```
    - To launch a redis container in the background (-d option), use: 
      ```
      docker run -d redis
      ```
      This will launch the container with the latest image of redis available in the registry. To launch redis container with a particular version such as 3.2, specify the tag as:
      ```
      docker run -d redis:3.2
      ```

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
