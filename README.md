<p align="center">
  <img src="./img/docker-logo.png"/>
</p>

# Docker - Tips and Tricks

## Listing Containers

* Lists all active containers at moment:
    
    ```
    docker ps
    ```

* Lists all active and inactive containers:
    
    ```
    docker ps -a
    ```


## Initializing Containers

* Initializes a container with the image "image_name":
    
    ```
    docker run image_name
    ```

    * Examples of images (link: https://hub.docker.com/search?type=image):
        * nginx;
        * ubuntu;
        * node;
        * mysql;


* Executing the command "bash" after download the image and start the container:

    ```
    docker run ubuntu bash
    ```


* Initializing the iteractive mode on terminal. Here it's possible interact with terminal:

    ```
    docker run -it ubuntu
    ```

* Initializing with iteractive mode on terminal and removing container after it was stopped:

    ```
    docker run -it --rm ubuntu
    ```

* Initializing and defining a name to container:

    ```
    docker run --name "container_name" ubuntu
    ```

* Starting an existent container:

    ```
    docker start "container_name"
    ```

* Stopping a container that was running:

    ```
    docker stop "container_name"
    ```

# Publishing Ports With Nginx

* Redirecting port from docker host (8080) to container (80):

    ```
    docker run -p 8080:80 nginx
    ```

* Detaching terminal from nginx's process:

    ```
    docker run -d -p 8080:80 nginx
    ```

# Removing Containers

* Removing an existent container by id:

    ```
    docker rm "container_id"
    ```
* Removing an existent container by name:

    ```
    docker rm "container_name"
    ```

* Removing a container in execution using -f to "force" the process to be executed:

    ```
    docker rm "container_name/container_id" -f
    ```

* Removing all the containers filtering by each "container_id" and using -f to "force" the process to be executed:

    ```
    docker rm $(docker ps -a -q) -f
    ```

# Accessing and Changing a Container's Files

* Executing a command into the container:

    ```
    docker exec "container_name" "command_name"
    ```

    * Examples of commands:
        * bash;
        * ls;
        * cd.

* Executing a command into the container with interactive mode:

    ```
    docker exec -it "container_name" "command_name"
    ```

# Starting With Bind Mounts

* Creating a volume (is a path that exists into the docker host) into the container:

    ```
    docker run -d --name "container_name" -p 8080:80 -v "local_path"
    ```

    * Examples of "local_path":
        * ~/Projects/user/test123
        * /home/etc/user/projects


* Creating a volume with bind mounts(most recent command):

    ```
    docker run -d --name "container_name" -p 8080:80 --mount type=bind,source="local_path",target="target_path"
    ```
    * Obs: It's possible to get the local path using the command "$(pwd)", exemple:
    
        ```
        docker run -d --name nginx -p 8080:80 --mount type=bind,source="$(pwd)"/html,target=/usr/share/nginx/html
        ```

# Working With Volumes

* Listing all volumes:

    ```
    docker volume ls
    ```

* Creating a volume:

    ```
    docker volume create "volume_name"
    ```

* Inspecting a volume: 

    ```
    docker volume inspect "volume_name"
    ```

* Starting a container with volume:

    ```
    docker run -d --name "container_name" -p 8080:80 --mount type=volume,source="volume_name",target="target_path"
    ```

* Deleting all volumes and all directories and files in each one:

    ```
    docker volume prune
    ```
    
# Understanding Images and DockerHub

* Listing all images:

    ```
    docker images
    ```

* Removing a specific image:

    ```
    docker rmi "image_name:image_version"
    ```

# Creating The First Image With DockerFile

* Sample example of dockerfile:

    [nginx with vim](./dockerfile/Dockerfile)

* After to create the dockerfile with the specifics instructions, you must run this command at the terminal to execute and build the file:

    ```
    docker build -t "name of image"
    ```