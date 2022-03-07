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
    docker run -it ubuntu bash
    ```

* Starting an existent containter:

    ```
    docker start "container_name"
    ```

* Stopping a containter that was running:

    ```
    docker stop "container_name"
    ```