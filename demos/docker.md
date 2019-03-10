# Docker demo

## Installing Docker
The installation for Docker for different OS/Distros can be found at [docker.com](https://docs.docker.com/v17.09/engine/installation/#server)

#### Direct links to installation
1. [Install on Ubuntu](https://docs.docker.com/v17.09/engine/installation/linux/docker-ce/ubuntu/)
1. [Install on Windows](https://docs.docker.com/v17.09/docker-for-windows/install/)
1. [Install on Mac](https://docs.docker.com/v17.09/docker-for-mac/install/#install-and-run-docker-for-mac)

## Check if Docker is working
```bash
    sudo docker run hello-world
```

## Hello world program
1. Change user to root (admin) user
    ```bash
        sudo su
    ```
1. Let's first pull a docker image from a docker registry
    ```bash
        docker pull busybox
    ```
1. Check if the new image that you pulled was downloaded
    ```bash
        docker images
    ```
1. Use the docker run command to run the container image
    ```bash
        docker run busybox echo "hello from busybox"
    ```
1. To list all dockers that were run
    ```bash
        docker ps -a
    ```
1. List all the processes running on the machine
    ```bash
        ps aux
    ```
1. List all network interfaces on machine
    ```bash
        ip link show
    ```
1. Exec into container
    ```bash
        docker run --name=test -it busybox sh
    ```
1. Try out some commands in the container
    ```bash
        ls
        ps aux
        ip link show
    ```
1. Exit the docker container
    ```bash
        exit
    ```
1. List all docker containers. You will still see the old container in terminated state.
    ```bash
        docker ps -a
    ```
1. Delete the container
    ```bash
        docker rm test
    ```
1. List all stopped containers
    ```bash
        docker ps -a
    ```
1. Delete all stale containers
    ```bash
        docker container prune
    ```

### Running your own PHP app

1. Create a new folder in your home directory and navigate to it
    ```bash
        mkdir ~/demo-app && cd ~/demo-app
    ```
1. (Optional) Install vim editor. Optionally you could use an editor of your choice to edit files below.
    ```bash
        sudo apt-get install vim
    ```
1. vim commands can be found in [this vim cheat sheat](https://devhints.io/vim)
1. Open a new file `index.php`
    ```bash
        vim index.php
    ```
1. Copy the following contents into it
    ```php
        <?php
            echo "<h1> My first php app </h1>";
            echo "You are viewing your application on version: V1";
        ?>
    ```
1. Save and exit `index.php`
1. Now similarily create a file `Dockerfile` and copy the following contents.
    ```bash
        vim Dockerfile
    ```
    ```bash
        FROM php:5-apache
        ADD index.php /var/www/html/index.php
        RUN chmod a+rx index.php
    ```
1. Save and exit `Dockerfile`
1. Now build the Docker image for your demo-app
    ```bash
        docker build -t demo-app:v1 .
    ```
1. Now run your newly created app
    ```bash
        docker run --rm -p 8888:80 demo-app:v1
    ```
1. Open the following link on your browser.
    [localhost:8080](http://localhost:8888/)
1. Come back to your terminal and use `Ctrl+C` to kill the running demo-app.

### Updating your app from v1 to v2
1. Update the `index.php` to the following
    ```php
        <?php
            echo "<h1> My second php app </h1>";
            echo "You are viewing your application on version: V2";
        ?>
    ```
1. Rebuild your container image with a new image-tag
    ```bash
        docker build -t demo-app:v2 .
    ```
1. Now re-run your newly created app
    ```bash
        docker run --rm -p 8888:80 demo-app:v2
    ```
1. Open the following link on your browser.
    [localhost:8080](http://localhost:8888/)
1. Now you see the new message which shows the new version of your app.
1. Come back to your terminal and use `Ctrl+C` to kill the running demo-app.
