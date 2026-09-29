---
layout: post
title: 离线更新Windows系统证书库
excerpt: 离线机器通过SST与STL文件全量更新根证书库
cover: /assets/img/kb-big.jpg
tags: Windows 证书 运维
---

Windows系统默认内置的根证书是确保网络安全和身份验证的重要组成部分。根证书由可信的证书颁发机构（CA）签发，用于验证其他证书（如网站SSL证书、软件签名证书）的合法性，当用户访问HTTPS网站或运行签名软件时，Windows会通过根证书构建信任链，确认终端证书的有效性。

根证书库的更新依赖Windows Update，离线机器无法自动更新。当某个根CA过期或被替换后，离线机器访问依赖该CA的HTTPS站点就会校验失败：浏览器报证书错误，Java报PKIX path building failed。

如需在离线机器上更新证书，可在正常联网的Windows电脑上生成相关文件后导入，主要涉及以下文件：

```shell
authroot.sst：受信任根证书本体
authroot.stl：受信任根证书哈希清单
disallowedcert.sst：不信任证书本体
disallowedcert.stl：不信任证书哈希清单
```

在联网机器上（管理员命令行）生成authroot.sst：

```shell
certutil -generateSSTFromWU D:\cert\authroot.sst
```

下载另外3个文件到D:\cert：

```shell
http://ctldl.windowsupdate.com/msdownload/update/v3/static/trustedr/en/authrootstl.cab
http://ctldl.windowsupdate.com/msdownload/update/v3/static/trustedr/en/disallowedcertstl.cab
http://ctldl.windowsupdate.com/msdownload/update/v3/static/trustedr/en/disallowedcert.sst
```

解压两个cab，得到authroot.stl和disallowedcert.stl。将4个文件拷贝到离线机器，管理员执行：

```shell
certutil -addstore -f Root D:\cert\authroot.sst
certutil -addstore -f Root D:\cert\authroot.stl
certutil -addstore -f Disallowed D:\cert\disallowedcert.sst
certutil -addstore -f Disallowed D:\cert\disallowedcert.stl
```

也可以mmc里加证书管理单元，在"受信任的根证书颁发机构"和"不受信任的证书"里分别走导入向导。

装完验证：

```shell
certutil -verifystore Root
```

或者certmgr.msc里看"受信任的根证书颁发机构"的数量对不对。

只缺单个根证书的话不用全量同步，从CA官网下载DER格式的.cer，`certutil -addstore Root xxx.cer` 直接加。

## 参考资料

1. [获取及安装最新微软更新提供Windows系统根证书](https://www.cnblogs.com/namelost/p/18852679)
2. [How to Update Trusted Root Certificates in Windows](https://woshub.com/updating-trusted-root-certificates-in-windows-10/)
3. [Configure trusted roots and disallowed certificates in Windows](https://learn.microsoft.com/en-us/windows-server/identity/ad-cs/configure-trusted-roots-disallowed-certificates)
