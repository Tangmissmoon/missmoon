---
title: 如何使用mac，处理压测的问题
categories:
 - 工作笔记
tags: 
 - mac
 - 随笔
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=450 src="//music.163.com/outchain/player?type=0&id=596729952&auto=1&height=430"></iframe>

# Mac上可以处理的工作
 
今天做了三件事情，修bug，开发新功能，培训。
如果需要简单的压测，使用mac默认的ab工具即可。

```bash
ab -n 500 -c 10 https://asdqwe-copy1-27595-80.baidu.com/ > test.html
```