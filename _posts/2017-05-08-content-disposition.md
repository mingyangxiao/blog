---
layout: post
title: 文件下载Content-Disposition设置
excerpt: 文件下载Content-Disposition设置
---


```
Content-Disposition: attachment;
                      filename="$url_encoded_filename";
                      filename*=utf-8''$url_encoded_filename
```