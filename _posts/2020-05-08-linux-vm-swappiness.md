---
layout: post
title: Linux vm.swappiness参数设置与内存交换
excerpt: 内核参数vm.swappiness控制换出运行时内存的相对权重，参数值可设置范围在0到100之间。参数值大小对如何使用交换空间有很大联系。值越大表示越积极使用交换空间，值越小表示越积极使用物理内存。
cover: /assets/img/linux.png
tags: Linux
---

#### 简介

内核参数vm.swappiness控制换出运行时内存的相对权重，参数值可设置范围在0到100之间。参数值大小对如何使用交换空间有很大联系。值越大表示越积极使用交换空间，值越小表示越积极使用物理内存。

#### 参数值说明

swappiness=0 

最大限度使用物理内存，当剩余空闲内存低于vm.min_free_kbytes limit时，使用交换空间。

对于3.5以后的内核和RedHat 2.6.32之后的内核，设置为0会禁止使用交换空间，从而引发Out of memory，这种情况可以设置为1进行最少量的交换，而不禁用交换。

swappiness=60

默认值，物理内存使用率超过100-60=40%时开始使用交换空间。

swappiness＝100

积极使用交换空间，并把内存上的数据及时搬运到交换空间。

#### 参数调整方法

临时调整：

```shell
sysctl vm.swappiness = 10 
```

永久调整：

```shell
vim /etc/sysctl.conf 

#/etc/sysctl.conf 
vm.swappiness=10

sysctl -p
```





