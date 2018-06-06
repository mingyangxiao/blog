---
layout: post
titile: Linux 编译安装 Git
tags: Linux Git
---

从 https://mirrors.edge.kernel.org/pub/software/scm/git/ 下载git源码

```shell
wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.17.1.tar.gz
```

解压

```shell
tar -zxf git-2.17.1.tar.gz
```

安装编译所需依赖

```shell
#RHEL/CentOS
yum install curl-devel expat-devel gettext-devel openssl-devel perl-devel zlib-devel \
            asciidoc xmlto docbook2X

#Debian/Ubuntu
apt-get install libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev \
                asciidoc xmlto docbook2x install-info 
```

RHEL/CentOS 还需进行以下操作

```shell
ln -s /usr/bin/db2x_docbook2texi /usr/bin/docbook2x-texi
```

编译安装

```shell
cd git-2.17.1

make prefix=/usr/local all doc info
make prefix=/usr install install-doc install-html install-info
```

查看git版本

```shell
git --version
#2.17.1
```



