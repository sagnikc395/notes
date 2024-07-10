- How to use Docker and Containerisation.
- not too hard to understand and not too much code to write 
- Why learning it?
	- most os projects use docker containerized way to setup the project locally.
	- biggest hurdle is to install correct depenedencies -> containerization is better and as a developer dont have to worry about things and help us even setup db locally fast.
	- good to know how to deploy using Docker
	- path to container orchestration
	- automatic restarts using pm2 
	- much more lightweight than full virtual machines and much easier to orchestrate -> heavier to install all the dependencies and setup things.
- cal.com uses docker to setup their dev setup.
- traditional route:
	- ssh to machine
	- install the dependenices
	- install the db 
	- install pm2 
	- and start the server  and apply migrations.
	- and ping the site 
- Problems1:
	- The dependencies take space and installed to local system and need to remove if not using it.
	- no auto-destroy
- Docker:
	- starts a container on the machine.
	- self contained VM.
	- small machine with our dependencies installed.
	- they created image ->
		- the image is independent of the base operating system
		- still able to start the same thing if we run the image
		- very big file, contains everything that we require in our Dockerfile
	- very similar to an ISO file, require all that files that are required to run the files locally.
- Container Properties:
	- Involves building self-sufficient software packages that perform consistently ,regardless of the machines they run on.
	- Its basically taking the snapshot of a machine, the filesystem and letting us use and deploy it as a construct.
- Docker:
	- Docker engine is a popular open-source container runtime that allows software developers to build,deploy and test containerized applications on various platforms.
	- Docker containers are self-contained packages of applications and related files that are created with the Docker framework.
- Docker has 3 parts:
	- Docker Engine
	- CLI
	- Docker Hub
- Images are stored in their own registries, however different cloud providers have their own registries -> like AWS.

### Images and Containers:
- Image is like a template from which consistent containers can be created.
- Images define the initial filesystem of new containers.Bundle our application's source code and its dependencies into a self-contained package which is ready to use with a container runtime. Within the image, the filesystem contentn is represented as multiple independent layers.


### Starting a Dockerfile:
- Create a single Dockerfile in the root of your application to setup the Docker instance.
- we start from a base image(ubutnu/alpine/node)
- add all software to install
- copy over the files we want to present in the container.
- build the project(npm install/ npm run dev,npm run build)
- expose the right set of ports
- start your process

### Running the Image:
- Build the image:
	- docker build -t \<image-name>
- Running the image:
	- docker run \<image-name>
