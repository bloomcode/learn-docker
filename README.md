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