---
layout: post
title: acme.sh 自动化申请证书
excerpt: acme.sh 自动化申请证书
cover: /assets/img/letsencrypt.png
tags: HTTPS
---

#### acme.sh 自动化申请证书

#### 1. 安装acme.sh
```bash
curl https://get.acme.sh | sh -s email=example@email.com
```

#### 2. 申请ECC证书

```bash
acme.sh --issue \
--keylength ec-256 \
--dns dns_dp \
-d xiaomingyang.com \
-d *.xiaomingyang.com
```

#### 3. 安装证书
```bash
acme.sh --installcert \
--ecc \
-d xiaomingyang.com \
--key-file /etc/nginx/certs/xiaomingyang.com.key \
--fullchain-file /etc/nginx/certs/xiaomingyang.com.crt \
--reloadcmd "systemctl restart nginx"
```
