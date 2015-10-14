---
layout: post
title: ffmpeg截图
---

    ffmpeg -ss 1 -i test1.flv -vframes 1 -f image2  -y test1.jpg

>-ss 可以使用00:00:01时间轴格式，也可以直接指定秒数。