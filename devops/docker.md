# Docker

* Installation Docker on Centos 7
* Create Account [http://hub.docker.com](http://hub.docker.com)
* Create Docker Registry
* Create Own Image

## Installation Docker on Centos 7

#### 1. Install Needed Package

```
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

#### 2. Add Repository Docker CE

```
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

#### 3. Install Docker CE

```
sudo yum install docker-ce
```

#### 4. Add User to Docker Group

```
sudo usermod -aG docker $(whoami)
```

#### 5. Set Docker at boot time

```
sudo systemctl enable docker.service
```

#### 6. Start Docker Service

```
sudo systemctl start docker.service
```

## Reference

[https://github.com/NaturalHistoryMuseum/scratchpads2/wiki/Install-Docker-and-Docker-Compose-\(Centos-7\)](https://github.com/NaturalHistoryMuseum/scratchpads2/wiki/Install-Docker-and-Docker-Compose-%28Centos-7%29)

