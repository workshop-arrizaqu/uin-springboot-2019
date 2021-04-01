# Practice With Docker

\#\#PATH 1 - pull image

\* login linux:centos

\* login hub.docker.com

\* pull docker

```
\* docker pull tomcat:8.5-jdk11-openjdk-buster
```

\#\# PATH 2 - create container

\* docker container ls

\* docker container ls --all \(show all container running or not\)

\* docker container create --name tomcat1 tomcat:8.5-jdk11-openjdk-buster \(name container is tomcat1\)

\#\# PATH 3 - RUN Container

\* sudo docker container start tomcat1

\* sudo docker container ls \(to ensure that container of tomcat1 is running\)

\#\# PATH 4 - REMOVE Container

\* docker container stop tomcat1

\* docker container rm tomcat1 tomcat2

\* docker container ls --all

\#\# PATH 5 - EXPOSE PORT for External system

\* sudo docker container create --name tomcat1 -p 8080:8080 tomcat:8.5-jdk11-openjdk-buster

\* sudo docker container start tomcat2

\*  sudo docker container ls

\#\# PATH 6 - REMOVE docker image

\* docker image rm dockername / id \(must stop and remove first from related container\)

\#\# PATH 7 - create DOCKERFILE

\* create dockerfile

\* &lt;docker build -t simpleapp . &gt;

\#\# PATH 8 - Pass Environtment

\* docker container create --name simpleapp -e MYVAR=Docker -p 8080:3030 simpleapp:0.0.1

\* docker container inspect simpleapp

