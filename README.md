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
$ docker-compose up -d traefik

# Load Balances
$ docker-compose up -d --scale whoami=2
```
