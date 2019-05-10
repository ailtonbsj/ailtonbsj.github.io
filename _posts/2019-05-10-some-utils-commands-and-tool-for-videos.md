---
layout: post
title:  "Some utils commands and tools for Videos"
date:   2019-05-10 14:01:00 -0300
categories: tutorial linux video
---
This is a list of some utils command for linux tool for video:
```bash
# Slice part of video in mp4
# Where: --s start de time, -t is the duration of video
ffmpeg -i source.mp4 -ss 00:00:10 -t 00:00:30 -vcodec copy -acodec copy output.mp4
```
