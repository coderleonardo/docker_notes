# Some notes about Docker

## Some commands about docker images

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
	
