FROM centos:centos6.6 

MAINTAINER tommyoshaw 

RUN yum -y install java-1.7.0-openjdk git 

# Cleanup cache
RUN yum clean all

# Set JENKINS_HOME same as master
ENV JENKINS_HOME /var/jenkins_home

RUN mkdir -p $JENKINS_HOME
RUN useradd -d "$JENKINS_HOME/worker" -u 1000 -m -s /bin/bash jenkins

# Add swarm-client
RUN curl -o /bin/swarm-client.jar -k http://maven.jenkins-ci.org/content/repositories/releases/org/jenkins-ci/plugins/swarm-client/1.22/swarm-client-1.22-jar-with-dependencies.jar

# Add start script
ADD start.sh /bin/start-agent.sh
RUN chmod +x /bin/start-agent.sh

# Login as jenkins
ENV HOME $JENKINS_HOME/worker
USER root 

# Start
CMD /bin/start-agent.sh

