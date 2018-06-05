---
layout: post
title: SSH使用公钥验证并禁用密码验证
tags: Linux SSH
---

创建密钥对

##### Windows

Xshell , putty 等工具均可生成密钥对

##### Linux / Mac

```shell
ssh-keygen -t rsa
```

根据提示操作，最后会显示密钥对存放路径

```she
Your identification has been saved in/root/.ssh/id_rsa.
Yourpublic key has been saved in/root/.ssh/id_rsa.pub.
```

创建.ssh文件夹及authorized_keys文件，注意权限

```shell
mkdir .ssh
chmod 700 .ssh
touch ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

导入公钥数据(pubkey即id_rsa.pub中内容)

```shell
echo 'pubkey' >> ~/.ssh/authorized_keys
```

编辑sshd_config文件

```shell
vi /etc/ssh/sshd_config
```

修改以下配置

```shell
#禁用密码验证
PasswordAuthentication no

#启用密钥验证
RSAAuthentication yes
PubkeyAuthentication yes
```

重启SSH服务

```shell
#RHEL/CentOS系统：
service sshd restart

#Debian/Ubuntu系统：
service ssh restart
```

