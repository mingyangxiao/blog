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


其中 $url_encoded_filename 是原始文件名使用UTF-8编码后按照RFC3986标准进行百分号编码所得到