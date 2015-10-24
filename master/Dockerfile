FROM jenkins:latest

MAINTAINER thshaw

#Prebake our recommended plugins into the latest jenkins image

COPY plugins.txt /usr/share/jenkins/plugins.txt

RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt
