---
layout: post
title: Docker镜像离线迁移
excerpt: Docker镜像离线导出与导入
cover: /assets/img/docker.png
tags: Docker 运维
---

离网机器无法通过在线镜像仓库拉取镜像，可通过从联网机器导出镜像后在离网机器上导入的方式迁移镜像（需保持架构一致）。

在联网机上先清理悬空镜像（重建留下的旧层，迁移用不上）：

```shell
docker rmi $(docker image ls -f dangling=true -q)
```

再把全部镜像导出压缩成一个包：

```shell
docker save $(docker images --format '{{.Repository}}:{{.Tag}}') | gzip > all.tar.gz
```

把all.tar.gz拷到离网机器，导入：

```shell
docker load -i all.tar.gz
docker images
```

docker load自动识别gzip，不用先解压。

## 参考资料

1. [docker save](https://docs.docker.com/reference/cli/docker/image/save/)
2. [docker load](https://docs.docker.com/reference/cli/docker/image/load/)
