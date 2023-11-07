---
title: Install Homeland with Docker - Homeland
---

## Homeland Docker

[Homeland](http://gethomeland.com) builit on Docker for automated deploy.

## System requirements

- Linux Server [4 Core CPU, 4G Memory, 50G Disk, 64 bit] - _Better use Rocky Linux 9.2_
- [Docker](https://www.docker.com/), [Docker Compose](https://docs.docker.com/compose/)

## Usage

### Install Docker:

This script was made for Rocky Linux 9.2, If you use other system version, please read [Docker Installaction](https://docker.github.io/engine/installation/linux/), the script original from [DO](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-rocky-linux-9#step-1-installing-docker)

```bash
sudo dnf check-update
sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo dnf install docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
sudo systemctl status docker
sudo systemctl enable docker
```

### Test Docker

```bash
docker info # 24.0.7
docker compose version # version v2.21.0
````

### Get oauth2id docker

```bash
yum install git
git clone https://github.com/thape-cn/oauth2id-docker
cd oauth2id-docker/
```

## Application configuration

Homeland use `app.local.env` file to config, there have an example in `app.default.env`. You must read the [Configuration](/docs/configuration/config-file/) and customize the config variables with your application.

**Required settings**

Please edit `app.local.env` file:

```conf
# For auto SSL get cert
domain=your-host.com
# default: admin@admin.com, when you use this email register a user, you will get the admin role.
# Or you can change it as your email.
admin_emails=admin@admin.com
```

## Install

```bash
make install
```

## Startup

```bash
make start
```

Now, you can visit https://your-host.com

## Commands

| Command       | Desc                                                   |
| ------------- | ------------------------------------------------------ |
| make install  | For first install, create database                     |
| make update   | Update docker image and restart application for update |
| make start    | Startup application                                    |
| make stop     | Stop application containers (except Database, Redis)   |
| make restart  | Restart application                                    |
| make status   | Show container status                                  |
| make console  | Enter the Rails console                                |
| make stop-all | Stop all services (including Databse, Redis)           |
| make reindex  | Rebuild Search indexes                                 |
