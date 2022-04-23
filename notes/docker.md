Docker Compose
* Allows to start multiple containers at once.

Dockerfile
* To build our own docker image.

Volumes
* To persist data in docker.

Containers
* A way to package application with all the necessary dependencies & configuration.
* Portable => can be easily shared and moved around within teams.
* Make development, deployment, testing more efficient.

Where do containers live? 
* Container repository
    * Private repositories
    * Public repository for Docker => Dockerhub

How do containers improve the development process?
Before Containers
    * Installation process different on each environment.
    * Installation steps are very long(inefficient) and prone to human errors.

After Containers
    * None of the dependency is installed directly on our OS. Container uses its own isolated environment(linux based).
    * One command to install the app and remains the same irrespective of the OS.
    * Possible to run 2 diff version of app on the same local env.

How do containers improve the deployment process?
Before Containers
    * Developers will share a list of artifacts & installation steps for the application as well as all the involved services. Everything needs to be installed on the OS.
    * Lot of possibilities of misunderstandings.

After Containers
    * Developers and operations work together to package the application in a container.
    * No environmental configuration needed on server - except Docker runtime.


What is a container technically?
* A container is a layer of images stacked on top each other.
* Most have linux as base image because of small size. eg alpine based.
* docker run
    * it will first see if it can find the image locally. If not, it will pull the image from docker hub.
    * on running, you will see all the layers of images on which it is dependent along with their hashes which are getting downloaded.
    * the advanatage of the layer based approach is that if a different version of postgres image needs to be installed, only those images would need to be downloaded which are new or different or updated.

Different between docker image and docker container
* Docker image => It's the actual package that can be moved around.
* Container is the running environment for image.
* docker ps --> to get the container id

What is the difference between docker and VM?
* There are two main layers in the operating system: the OS Kernel layer which interacts with the hardware and the application layer which interacts with the OS kernel.
* All linux distributions, even though have the same OS kernel, their applications layer varies.
* Docker virtualizes the application layer. It uses the kernel of the host because it doesn't have its own kernel.
* VM has it's own application layer and kernel.
* Size: The size of docker images is much smaller because they have to implement just one layer. Docker images => MBs, Virtual Machines => GBs.
* Speed: Docker containers start and run much faster.
* Compatibility: VM of any OS can run on any OS host. Same is not true with docker.
    * A linux based docker image might not be compatible with a windows based docker kernel. This is true for older windows versions.
    * Workaround: docker toolbox. ==> abstracts the os kernel to make it possible to run different docker images.

Components of a container
* Application image: postgres, redis, mongo, ...
* Environment configs
* It also has a port binded to it to talk to the application running inside of container.
* The file system in a container is virtual. It has its own abstraction of the OS.

Docker Commands:
* docker images => list images, ps => list all running containers
* docker run -d redis => detached mode. => pull the image and start the container.
* docker stop container_id
* docker start container_id => start the stopped container.
* docker ps -a => list running and stopped containers.
* If we are running two different redis versions via docker, how do we ensure that there are no conflicts?

Container Post vs Host Port
* How does docker port binding work?
    https://betterprogramming.pub/how-does-docker-port-binding-work-b089f23ca4c8
    * Docker containers can connect to the outside world without any configuration.
    * But the outside world cannot connect to the docker container by default. 
* While running the docker ps command, we see the container port and not the host port. The host port has to be different else it would lead to a conflict.
* We can do the port binding via the -p flag in the docker run command.
    docker run -p hostPort:containerPort.
* After this, you'll be able to see the bindings when running docker ps.