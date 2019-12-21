# Docker Image

* Check Docker Version
* Check List Docker Images
* Create Docker Image
  * Create Docker file
  * Build Image
  * Build Image by Name

## Check Docker version

```
[root@localhost myimage]# sudo docker version
Client: Docker Engine - Community
 Version:           19.03.5
 API version:       1.40
 Go version:        go1.12.12
 Git commit:        633a0ea
 Built:             Wed Nov 13 07:25:41 2019
 OS/Arch:           linux/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          19.03.5
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.12.12
  Git commit:       633a0ea
  Built:            Wed Nov 13 07:24:18 2019
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.2.10
  GitCommit:        b34a5c8af56e510852c35414db4c1f4fa6172339
 runc:
  Version:          1.0.0-rc8+dev
  GitCommit:        3e425f80a8c931f88e6d94a8c831b9d5aa481657
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683
```

## Check List Docker Images

```
docker images
```

## Create Docker Images

### Create Docker File

```
[root@localhost arrizaqu]# mkdir docker-images
[root@localhost arrizaqu]# cd docker-images
[root@localhost docker-images]# ls
[root@localhost docker-images]# touch DockerFile
[root@localhost docker-images]# vi DockerFile
```

#### Edit Dockerfile :

```
FROM alpine

CMD ["echo","hello docker image"]
```

### Build Image

> docker build .

```
[root@localhost docker-images]# docker build .
Sending build context to Docker daemon  2.048kB
Step 1/2 : FROM alpine
 ---> c85b8f829d1f
Step 2/2 : CMD ["echo","hello docker image"]
 ---> Running in 1b0d3a569eba
Removing intermediate container 1b0d3a569eba
 ---> 0ce1bec6b524
Successfully built 0ce1bec6b524[root@localhost docker-images]# docker build .
Sending build context to Docker daemon  2.048kB
Step 1/2 : FROM alpine
 ---> c85b8f829d1f
Step 2/2 : CMD ["echo","hello docker image"]
 ---> Running in 1b0d3a569eba
Removing intermediate container 1b0d3a569eba
 ---> 0ce1bec6b524
Successfully built 0ce1bec6b524
```

Build Image by Name

> docker build -t helloworld .

```
[root@localhost docker-images]# docker build -t helloworld .
Sending build context to Docker daemon  2.048kB
Step 1/2 : FROM alpine
 ---> c85b8f829d1f
Step 2/2 : CMD ["echo","hello docker image"]
 ---> Using cache
 ---> 5c12e43154a9
Successfully built 5c12e43154a9
Successfully tagged helloworld:latest
```



