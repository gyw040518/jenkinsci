# Jenkins CI using docker-compose

Setup CI infrastructure that includes a Jenkins Master with pre-baked plugins and containerised build agent (CentOS).  This CI infrastructure is opensource, portable, extensible, simple to upgrade and scalable, as all good CI infrastructure should be.  This has been tested locally but can be easily deployed into Joyents Triton.

Note : Triton doesn't support shared volumes from the host, but the Jenkins Master and agent work as expected when the shared volume is commented out in the docker-compose.yml.
```
volumes:
    - ./jenkins_data:/var/jenkins_home
```

The CentOS build agents are containers and will be scaled up and down with the docker-compose scale command. The build agents are not using persistent storage so make sure you copy anything important from them before removing.

Based on work by the European Environment Agency : https://hub.docker.com/u/eeacms/

## Prerequisites

  docker
  
  docker-compose
  
  (Tested using Docker version 1.9.0 and Docker Compose version 1.4.2)
  
## Setup 

We want to keep the jenkins data outside the Master container to keep it persistent.

```
  mkdir jenkins_data
  chmod 777 jenkins_data
```

## Make sure we have all the latest versions of the Jenkins Master and Agent images

```
  docker-compose pull
```
![Example](/gifs/pull.gif)

Note : If you wish to rebuild the Master or agent images the Dockerfiles are available under master and agents directories.

## Start Jenkins Master and one Build Agent

```
docker-compose up -d

```
![Example](/gifs/composeup.gif)

## Start more build agents

```
docker-compose scale cento6.6=3
```
![Example](/gifs/scale.gif)

Verify this agent is automatically added to the Jenkins CI master

## Check logs of a service

```
docker-compose logs centos6.6
```
![Example](/gifs/logs.gif)

## Upgrade master

Shut down master, delete container, pull new image and start

```
docker-compose stop
docker-compose rm -f jenkins
docker-compose pull
docker-compose up -d jenkins
```

![Example](/gifs/upgrade.gif)
