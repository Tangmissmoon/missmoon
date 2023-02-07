---
title: 记一次解决bug/优化命令的过程
categories:
 - 记录
tags: 
 - Bugs
 - k8s
 - docker
 - yml
---

今天遇到两个需要查询的问题：
1. **构建镜像失败**：使用`docker build`命令构建镜像的时候反复出现`Failed to build yarl···`提示，没有头绪；
2. **在副本名称匹配结果下过滤状态**：线上服务提示异常，需要去pod里查看具体日志，来排查引起报错的问题，pod的副本集比较多，除了使用`grep`筛选名称以外，希望过滤掉非`running`状态的pod；

先简单再过下，什么是`docker`，我们为什么会用到它？

**docker**，多平台适用，常用来开发、交付和运行应用程序，打包应用，形成更小的单元，这些单元具有应用运行所需的功能，也包括库、系统工具和其他必需组建，这些特质能保证软件开发者，专注于应用的开发，在交付/发布过程，避免出现被环境配置搞得头大的情况，因此，也让服务供应商节省服务迁移产生的损耗。[AWS，关于docker的介绍](https://aws.amazon.com/cn/docker/)，顺便说，`docker`是容器的操作系统，容器是用于虚拟化服务器的操作系统，虚拟机则是虚拟化服务器的硬件。

简单来说，就是每次打包部署，先构建一个`image`（镜像），之后基于这个镜像，再生成 `container`（容器），再运行容器，相当于启动应用程序。分为三步，使用命令完成：

1. `docker build [OPTIONS] PATH | URL | -` `build`命令有多种，从文件 `Dockerfile`的使用， 从链接`docker build -t hello-world https://github.com/docker-library/hello-world.git#master:amd64/hello-world` ,还有解压文件，具体可以翻翻文档；[docker docs](https://docs.docker.com/engine/reference/commandline/build/)，这一步完成镜像的构建；
2. `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]` ，通过第一步构建得到的镜像，替换掉下面示例`ubuntu`的位置，生成容器：
  e.g.:`docker run -it ubuntu /bin/bash`
3. `docker exec`，执行容器

步骤清晰了，我们就来找问题出现的原因，检索“docker build”+错误提示“Failed to build yarl”，替换基础镜像。

第二个问题，比较棘手，

今天学习的是《effective python》的第15条，不要过分依赖给字典添加条目时所用的顺序，`3.5`之前的版本，顺序不定，这跟字典类型以前跟哈希表实现有关，内置的`hash`函数和随机种子数来确定，因此`dict`相关的方法都不能保证固定的顺序，而`3.6`开始，字典会保留添加时所使用的顺序。

>内置的`Collections`模块提供的OrderedDict，行为和3.7版本后的标准dict很像，但性能有较到区别。实现LRU缓存，（least-recently-used缓存）OrderedDict比dict类型更合适。





