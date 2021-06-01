---
layout: default
parent: JENKINS
nav_order: 1
---
# Setup Jenkins

Jenkins can be installed locally. However, quickest method is to use docker image. So, we will follow this approach.

***Pre-requisites:-***

To install a docker image, docker must be installed. Follow [Install docker](../docker/install_docker) link for this.

Jenkins docker image is available on Docker Hub [here](https://hub.docker.com/r/jenkins/jenkins).

To use docker-compose, click [here](https://github.com/kathuriaas/docker-compose-examples)

## Step 1 : Pull Jenkins docker image

```shell
# Pull image from Docker Hub
docker pull jenkins/jenkins

# Verify jenkins image is available locally
docker images
```

## Step 2 : Start container from image that will start Jenkins server

We will start a container using image jenkins/jenkins:latest.  
PORT 8080 of container will be published to port 8080 of host machine (`-p host_port:container_port`). So, jenkins page will be available at `localhost:8080`.  
It will also mount jenkins_home volume in container.

```shell
# Docker Run
docker run -d -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins
```

## Step 3 : Get initial admin password

```shell
# Read initial admin password from container
docker exec -it <container ID> cat /var/jenkins_home/secrets/initialAdminPassword
```

## Step 4 : Login to Jenkins Home

- Open link `localhost:8080` in your browser.
- Enter password retrieved in last step.
- Login to Jenkins admin portal.
- You are now all set to use Jenkins.
