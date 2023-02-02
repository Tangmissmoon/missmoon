---
title: 解决docker login出错过程
categories:
 - 记录
tags: 
 - 解决问题
 - docker
---

# 前因

在一次`docker login`登陆过程中遇到这类报错：
```bash
Error while pushing images to registry: dial tcp: lookup registry on 192.168.65.1:53: no such host
```
检索得知，没有映射上对应的IP地址，可以通过配置host解决。mac系统编辑hosts文件
```vim
vim /etc/hosts
```
增加私服地址，和对应的IP，再输入login命令又获得：

```sh
docker login certificate relies on legacy Common Name field, use SANs or temporarily enable Common Name matching with GODEBUG=x509ignoreCN=0
```

## 后果

在网上找解决办法，发现除了配置host，还需要加`insecure-registries`，也有处理`registry-mirrors`的。

[docker-registry-fails-x509](https://www.ibm.com/docs/en/cloud-paks/cp-management/2.2.x?topic=tcnm-logging-into-your-docker-registry-fails-x509-certificate-signed-by-unknown-authority-error)

[docker for mac](https://github.com/docker/for-mac/issues/1733) 
 
## 具体操作

找到`daemon.json`文件，在大括号里添加

```json
"registry-mirrors": [
"https://registry.docker-cn.com"
],
```
因为我用的是colima，替代docker，所以主机上这个文件在colima下有一份，在`vim ~/.colima-docker/docker/daemon.json`，设置后没有解决问题，再次尝试后解决`vim ~/.colima/docker/daemon.json`，两个位置都试试。

[docker-cmd](https://docs.docker.com/engine/reference/commandline/dockerd/)
 
{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}

{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}

