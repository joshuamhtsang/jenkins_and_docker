# jenkins_and_docker
A Jenkins instance which can run docker commands.

# How to use

Build the Docker image.

$ docker build -t myjenkins .

Run a container:

$ docker run -d -u root -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):/usr/bin/docker -v jenkins_home:/var/jenkins_home -p 8080:8080 myjenkins


