# Docker On Centos 7

* Installation Docker on Centos 7
* Installation Docker Compose
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

## Installation Docker Compose

#### 1. Install Extra Packages for Enterprise Linux

```
sudo yum install epel-release
```

#### 2. Install python-pip

```
sudo yum install -y python-pip
```

#### 3. Install Docker Compose

```
sudo pip install docker-compose
```

#### 4. Upgrade Python packages on CentOS 7

```
sudo yum upgrade python*
```

#### 5. To verify a successful Docker Compose installation

```
docker-compose version
```

## ================= OTHER INSTALL DOCKER COMPOSE ========

### Add Docker Compose Repository 

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

### Grant to execute service

```
sudo chmod +x /usr/local/bin/docker-compose
```

### Check version

> docker-compose --version



### Example 

```
[root@localhost arrizaqu]# sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compoose
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   617    0   617    0     0    669      0 --:--:-- --:--:-- --:--:--   669
100 11.2M  100 11.2M    0     0   466k      0  0:00:24  0:00:24 --:--:--  721k
[root@localhost arrizaqu]# sudo chmod +x /usr/local/bin/docker-compose
[root@localhost arrizaqu]# docker-compose --version
docker-compose version 1.23.2, build 1110ad01
```

## Reference

[https://github.com/NaturalHistoryMuseum/scratchpads2/wiki/Install-Docker-and-Docker-Compose-\(Centos-7\)](https://github.com/NaturalHistoryMuseum/scratchpads2/wiki/Install-Docker-and-Docker-Compose-%28Centos-7%29)

[https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-centos-7](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-centos-7)

