---
layout: post
title: Centos7 Docker 安装
excerpt: Docker 安装
cover: /assets/img/docker.png
tags: Linux Docker
---

#### CentOS 7 Docker安装步骤

```bash
#安装yum工具
sudo yum install -y yum-utils
```

```bash
#卸载旧docker
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

```bash
#添加docker官方源
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

```bash
#安装docker engine 及 docker compose
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

```bash
#启动服务
sudo systemctl enable docker && systemctl start docker
```

