---
layout: post
title: Centos7升级OpenSSL&编译Nginx支持TLS v1.3
excerpt: Docker 安装
cover: /assets/img/docker.png
tags: Linux OpenSSL Nginx
---

#### Centos7升级OpenSSL&编译Nginx支持TLS v1.3

#### 升级OpenSSL
```bash
wget https://www.openssl.org/source/openssl-1.1.1o.tar.gz

tar -xzf openssl-1.1.1o.tar.gz

rm -rf /usr/src/openssl
mv openssl-1.1.1o /usr/src/openssl

cd /usr/src/openssl

./config --prefix=/usr/local/openssl
make -j4
make install

mv /usr/bin/openssl /usr/bin/openssl-102k
mv /usr/include/openssl /usr/include/openssl-102k

ln -s /usr/local/openssl/bin/openssl /usr/bin/openssl
ln -s /usr/local/openssl/include/openssl/ /usr/include/openssl

echo "/usr/local/openssl/lib" >> /etc/ld.so.conf
ldconfig -v

```
#### 重新编译Nginx

```bash
wget https://nginx.org/download/nginx-1.22.0.tar.gz

tar -xzf nginx-1.22.0.tar.gz

rm -rf /usr/src/nginx
mv nginx-1.22.0 /usr/src/nginx

cd /usr/src/nginx

./configure \
--prefix=/etc/nginx \
--sbin-path=/usr/sbin/nginx \
--modules-path=/usr/lib64/nginx/modules \
--conf-path=/etc/nginx/nginx.conf \
--error-log-path=/var/log/nginx/error.log \
--http-log-path=/var/log/nginx/access.log \
--pid-path=/var/run/nginx.pid \
--lock-path=/var/run/nginx.lock \
--http-client-body-temp-path=/var/cache/nginx/client_temp \
--http-proxy-temp-path=/var/cache/nginx/proxy_temp \
--http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp \
--http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp \
--http-scgi-temp-path=/var/cache/nginx/scgi_temp \
--user=nginx \
--group=nginx \
--with-compat \
--with-file-aio \
--with-threads \
--with-http_addition_module \
--with-http_auth_request_module \
--with-http_dav_module \
--with-http_flv_module \
--with-http_gunzip_module \
--with-http_gzip_static_module \
--with-http_mp4_module \
--with-http_random_index_module \
--with-http_realip_module \
--with-http_secure_link_module \
--with-http_slice_module \
--with-http_ssl_module \
--with-http_stub_status_module \
--with-http_sub_module \
--with-http_v2_module \
--with-mail \
--with-mail_ssl_module \
--with-stream \
--with-stream_realip_module \
--with-stream_ssl_module \
--with-stream_ssl_preread_module \
--with-openssl=/usr/src/openssl \
--with-cc-opt='-O2 -g -pipe -Wall -Wp,-D_FORTIFY_SOURCE=2 -fexceptions -fstack-protector-strong --param=ssp-buffer-size=4 -grecord-gcc-switches -m64 -mtune=generic -fPIC' \
--with-ld-opt='-Wl,-z,relro -Wl,-z,now -pie'

make -j4
make install 
```
