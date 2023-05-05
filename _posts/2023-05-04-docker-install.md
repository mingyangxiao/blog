---
layout: post
title: Centos7 Docker 安装
excerpt: Docker 安装
cover: /assets/img/docker.png
tags: Linux Docker
---

#### CentOS 7 Docker安装步骤

# 1.安装yum工具
```bash
sudo yum install -y yum-utils
```

# 2.卸载旧docker
```bash
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

# 3.添加docker官方源
```bash
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

# 4.安装docker engine 及 docker compose
```bash
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

# 5.启动服务&开机自启动
```bash
sudo systemctl enable docker && systemctl start docker
```

