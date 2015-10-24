# Jenkins CI using docker-compose

The goal :

Spin up a CI pipeline including a Jenkins Master, Build agents (centoOS) and with pre-baked plugins.  Then we should be able to take the same file and spin the same CI infrastructure up on Joyent.

The CentOS build agents are containers and will be scaled up and down with the docker-compose scale command.

# Setup 

We want to keep the jenkins data outside the Master container to keep it persistent.

```
  mkdir jenkins_data
  chmod 777 jenkins_data
```

# Make sure we have all the latest versions of the Jenkins Master and Agent images

```
  docker-compose pull
```

Note : If you wish to rebuild the Master or agent images the Dockerfiles are available under master and agents directories.

# Start Jenkins Master and one Build Agent

```
docker-compose up -d
```

# Start more build agents

```
docker-compose scale cento6.6=3
```
Verify this agent is automatically added to the Jenkins CI master

# Upgrade master

Shut down master, delete container, pull new image and start

docker-compose stop
docker-compose rm -f jenkins
docker-compose pull

Start Jenkins Master : 
docker-compose up -d jenkins


