# [Some notes about Docker](https://docs.docker.com)

## Some docker images commands

First, download the **app** from the docker web site: https://github.com/docker/getting-started/tree/master/app

The app folder should have the following files and folders:

	- Dockerfile  
	- package.json  
	- spec  
	- src  
	- yarn.lock
	
Now we can build the (container) image. To do this we access the app folder and run the following code with the option "*-t*", which flags our image with the name "app":

	/app$ docker build -t app .

Now that our image has been built, we can inspect the images that we have running the following code:

	docker images

We should have something like this:

	REPOSITORY             TAG           IMAGE ID       CREATED         SIZE

	app                    latest        bb6d28039b8c   7 months ago    91MB
	node                   12-alpine     bb6d28039b8c   7 months ago    91MB

Now that we have our image, if we want to run this application (*app*), we can run the following code in iteractive mode ("*-it*") and access the bash ("*sh*"): 

	app$ docker run -it app sh
	
	/ # ls
	bin    dev    etc    home   lib    media  mnt    opt    proc   root   run    sbin   srv    sys    tmp    usr    var
	/ # node --version
	v12.22.12
	
To exit the container we simply type "exit":

	/ # exit
	
To list the containers that are running we type the following code:

	docker ps
	
To stop the container:

	docker stop CONTAINER_ID

To add a specific tag we can use "REPO_NAME:TAG", in the example below, we use "app:v1.0.0":

	app$ docker build -t app:v1.0.0 .

To remove:

	docker image remove app:v1.0.0

If we want to push an image to **docker hub** we run "docker push USER_NAME_ON_DOCKERHUB/REPO_NAME:TAG":

	docker push myusername/app:v1
	
To save and load a local docker image we run: 

	docker image save -o appv2.tar app:v1
	
	docker image load -i appv2.tar
	
## Some docker containers commands

To list the containers that are running:
	
	docker ps
	
We we get something like the example below we need to build our docker image

	CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
	

Build the docker image:

	app$ docker build -t app:v2 .
	
If we want to give a name to our container we can run the following code:
	
	app$ docker run -d --name container_name app:v2
	
To see the logs and the available options run
	
	docker logs --help

To see the options to run a container we type
	
	docker run --help

	>>> Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

For example, if we want to run a container in background and print container ID (*-d*) and publish a container's port(s) to the host (*-p*) we type: 

	docker run -d -p 80:3000 --name container_name app:v2
	
Now, if we want to list the files in a docker image we can run the following code:

	docker exec container_name ls
	
	>>> Dockerfile
	>>> appv2.tar
	>>> node_modules
	>>> package.json
	>>> spec
	>>> src
	>>> yarn.lock
	
To stop or start a container we run 

	docker stop container_name

	docker start container_name

To remove one or more containers:

	docker rm
	
Options to remove:
	
	docker rm --help

	>>> Usage:  docker rm [OPTIONS] CONTAINER [CONTAINER...]

We can also create volumes:

	docker volume create app-dados
	
## Some docker compose commands

First, download the "netflix" folder and check if [docker compose](https://docs.docker.com/compose/install/) is installed in your computer

In the netflix folder run the following code to build the image e run the container:

	netflix$ docker compose up
	
To list the container that are running with docker compose type
	
	docker compose ps

Now, if you to see how the network of docker works with multiple containers run the following codes:

	netflix$ docker exec -it -u root e258f97f04c3 sh

	/app # ifconfig
	
To see the logs:
	
	docker compose logs
	
