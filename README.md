# One Piece

## Install Docker Engine on CentOS

```bash
# Install the yum-utils package (which provides the yum-config-manager utility) and set up the repository.
$ sudo yum install -y yum-utils
$ sudo yum-config-manager  --add-repo  https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/centos/docker-ce.repo

# Install the latest version of Docker Engine, containerd, and Docker Compose
$ sudo yum install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

# Configure Docker to start on boot
$ systemctl enable docker

# Start Docker
$ sudo systemctl start docker

# Verify that Docker Engine is installed correctly by running the hello-world image
$ sudo docker run hello-world
$ curl -H Host:whoami.docker.localhost http://127.0.0.1
```

## Traefik Edge Router

```bash
$ docker network create traefik

$ docker-compose up -d traefik

# Load Balances
$ docker-compose -f whoami/docker-compose.yml up -d --scale whoami=2

$ curl -H Host:whoami.docker.localhost http://127.0.0.1
Hostname: 7b645fb009a6
IP: 127.0.0.1
IP: 192.168.80.4
RemoteAddr: 192.168.80.2:55256
GET / HTTP/1.1
Host: whoami.docker.localhost
User-Agent: curl/7.79.1
Accept: */*
Accept-Encoding: gzip
X-Forwarded-For: 192.168.80.1
X-Forwarded-Host: whoami.docker.localhost
X-Forwarded-Port: 80
X-Forwarded-Proto: http
X-Forwarded-Server: 8c53eb9d9163
X-Real-Ip: 192.168.80.1

$ curl -H Host:whoami.docker.localhost http://127.0.0.1
Hostname: f7b70204ca25
IP: 127.0.0.1
IP: 192.168.80.5
RemoteAddr: 192.168.80.2:43302
GET / HTTP/1.1
Host: whoami.docker.localhost
User-Agent: curl/7.79.1
Accept: */*
Accept-Encoding: gzip
X-Forwarded-For: 192.168.80.1
X-Forwarded-Host: whoami.docker.localhost
X-Forwarded-Port: 80
X-Forwarded-Proto: http
X-Forwarded-Server: 8c53eb9d9163
X-Real-Ip: 192.168.80.1
```

## Infrastructure

### Private NPM Registry

```bash
$ docker-compose -f verdaccio/docker-compose.yml up -d

$ curl -H Host:verdaccio.docker.localhost http://127.0.0.1/-/verdaccio/data/packages
[]
```

### Jenkins CI

```bash
$ docker-compose -f jenkins/docker-compose.yml up -d
```
