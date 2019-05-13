# jenkins_and_docker
A Jenkins instance which can run docker commands.






docker run -d -u root -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):/usr/bin/docker -v jenkins_home:/var/jenkins_home -p 8080:8080 myjenkins
