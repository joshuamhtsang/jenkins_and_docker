# jenkins_and_docker
A Jenkins instance which can run docker commands.

# How to use

## Running the Jenkins container.

Build the Docker image using the Dockerfile in this repo.

$ docker build -t myjenkins .

Run a container:

$ docker run -d -u root -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):/usr/bin/docker -v <DIR_OUTSIDE_CONTAINER>:/var/jenkins_home -p 8080:8080 myjenkins

Note that the volume bindings for 'docker.sock' allow docker commands run inside the Jenkins container to spawn containers in the Jenkin container's host.

Once the Jenkins container is running, you can access the Jenkins UI:  < IP address or web domain address >:8080

## Auxiliaries.

Common things you need to do are:

1. Add Github credentials (usename and password).
2. Install Plugins with 'Plugin Manager': 
     'Docker plugin', 'Docker Compose Build Step plugin'
3. Install docker-compose in Jenkins container (see below).

## Installing docker-compose in Jenkins container.

The image automatically does this already, but manual steps are never-the-less given here.  You need to get a bash shell up in the Jenkins container.  First, find the container name/id of the Jenkins container:

$ docker ps

Then:

$ docker exec -it <container_name/id> bash

Once inside, follow the instructions:

https://docs.docker.com/compose/install/

## Setting up SSH keypair in Jenkins container.

This is needed in order for Jenkins to clone code from your Github.  Like above, get a bash shell up in the Jenkins container.  Then, do:

$ ssh-keygen

Once the key is made, add the public key to your Github account 'Settings' -> SSH and GPG keys.
