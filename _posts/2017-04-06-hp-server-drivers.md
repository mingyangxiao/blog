---
layout: post
title: 惠普服务器没有使用SmartStart引导，安装Windows驱动的方法
excerpt: 惠普服务器没有使用SmartStart引导，安装Windows驱动的方法
---

1. 打开SmartStart光盘的这个目录：\compaq\csp\nt 。

2. 复制cpfiles.exe到硬盘，双击后进行解压，解压好后会生成一个叫cpfiles的文件夹。

3. 打开cpfiles这个文件夹，在最前面会有两个记事本文件，文件中会有一行“ProLiant Support Pack for Microsoft Windows Server xxxx” 字样，如果与当前系统符合，记下该文件名。

4. 找到和刚才的文件名同名的cmd文件, 双击运行，这样会把服务器上没有打上的HP设备驱动全部自动安装上。